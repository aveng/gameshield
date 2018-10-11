# 如何解决HTTP\(S\)协议接入游戏盾后HOST不匹配问题 {#concept_kbk_szv_kfb .concept}

## 问题描述 {#section_jks_vzv_kfb .section}

终端通过HTTP/HTTPS协议接入的情况下，如果将URL中的HOST配置直接从域名替换为服务器IP后，由于不通过域名而是通过IP直接进行请求。这种情况下，服务端获取到的域名信息为服务器IP，**因此请求报文内容中的Host信息为IP，而对于这种请求，服务端的响应结果将取决于服务端的具体配置**：

-   如果服务端只服务单个域名，则可能无视Host的值，返回正确的页面。
-   如果服务端服务多个域名，则通常会返回**404**或**403**错误。

另外，如果通过HTTPS协议接入，服务端可能无法找到匹配的证书，只能返回默认证书或者不返回。而客户端在进行证书校验时，也会因为域名不匹配的问题（证书是域名，而校验的是服务器IP），导致SSL证书校验失败 。

## 传统解决方案 {#section_rsr_c4w_kfb .section}

**HTTP协议接入解决方案**

针对HTTP协议接入情况的解决方案相对简单。一般来说，第三方库都提供相应接口支持修改HTTP请求Header的HOST信息，只需要开发人员将HTTP Header的HOST改为对应的域名即可。

**HTTPS协议接入解决方案**

-   **Android系统解决方案**
    1.  **证书HOST校验问题**

        终端在SSL握手过程中会校验当前请求URL的HOST是否在服务端证书的可选域名列表中。例如，假设原本需要请求的URL为`https://a.b.com`，使用服务器IP直连后实际请求的URL变成`https://1.2.3.4`。

        由于请求的HOST被替换成服务器IP，底层在进行证书的HOST校验时失败，最终导致请求失败。

        一般来说，系统都提供相应接口，允许终端设置证书HOST校验实现。因此，利用该接口，将底层默认实现中取终端传入URL的HOST信息（即服务器IP）替换回对应的域名即可解决证书HOST校验问题。

        **JAVA代码示例**：

        ```
        
        HostnameVerifier hnv = new HostnameVerifier() {
        @Override
        public boolean verify(String hostname, SSLSession session) {
        //示例
        if("yourhostname".equals(hostname)){ 
        return true; 
        } else { 
        HostnameVerifier hv =
        HttpsURLConnection.getDefaultHostnameVerifier();
        return hv.verify(hostname, session);
        }
        }
        };
        
        HttpsURLConnection.setDefaultHostnameVerifier(hnv);
        ```

    2.  **SNI问题**

        由于不通过域名而是通过IP直接进行请求。这种情况下，服务端获取到的域名信息为服务器IP，因此请求报文内容中的Host信息为IP，而服务端配置了多个域名，导致无法正确选择域名。

        一般来说，系统都提供相应接口，允许终端传入自定义SSLSocketFactory，SSLSocketFactory是用来创建SSLSocket的工厂，SSLSocket是Socket协议的拓展，具有SSL握手功能，且系统提供解决SNI问题的实现类SSLCertificateSocketFactory。因此，利用该方法解决SNI问题。

        **JAVA代码示例**

        ```
        conn.setSSLSocketFactory(new SSLSocketFactory(){
        @Override
        public Socket createSocket(Socket s, String host, int port,boolean autoClose) throws IOException{
        SSLCertificateSocketFactory sslSocketFactory = (SSLCertificateSocketFactory)SSLCertificateSocketFactory.getDefault(0);
        SSLSocket sslSocket = (SSLSocket)sslSocketFactory.createSocket(s, realHost,port,autoClose);
        sslSocket.setEnableProtocols(sslSocket.getSupportedProtocols());
        sslSocketFactory.setHostname(sslSocket, realHost);
        return sslSocket;
        }
        });
        ```

-   **iOS系统解决方案**
    1.  **证书HOST校验问题**

        在`NSURLSession`的证书校验代理方法`URLSession:didReceiveChallenge:completionHandler`中增加前置处理，将待验证的 `domain`由原本的服务器IP转换为其对应的域名，然后再进行后续处理。

        **Objective-C代码示例**

        ```
        - (void)URLSession:(NSURLSession *)session
        didReceiveChallenge:(NSURLAuthenticationChallenge *)challenge
        completionHandler:(void (^)(NSURLSessionAuthChallengeDisposition disposition, NSURLCredential *credential))completionHandler
        {
        NSURLSessionAuthChallengeDisposition disposition = NSURLSessionAuthChallengePerformDefaultHandling;
        NSURLCredential *credential = nil;
        
        // 证书验证前置处理
        NSString *domain = challenge.protectionSpace.host; // 获取当前请求的 host（域名或者 IP），假设此时为：1.2.3.4
        NSString *testHostIP = self.tempDNS[self.testHost];
        // 此时服务端返回的证书里的 CN 字段（即证书颁发的域名）与上述 host 可能不一致，
        // 因为上述 host 在发请求前已经被替换为 IP，所以校验证书时会发现域名不一致而无法通过，导致请求被取消
        // 所以，需要在校验证书前进行替换处理。
        if ([domain isEqualToString:testHostIP]) {
        domain = self.testHost; // 替换为对应域名：a.b.com
        }
        
        // 以下逻辑与 AFNetworking -> AFURLSessionManager.m 里的代码一致
        if ([challenge.protectionSpace.authenticationMethod isEqualToString:NSURLAuthenticationMethodServerTrust]) {
        if ([self evaluateServerTrust:challenge.protectionSpace.serverTrust forDomain:domain]) {
        // 上述evaluateServerTrust:forDomain方法用于验证 SSL 握手过程中服务端返回的证书是否可信任，
        // 以及请求的 URL 中的域名与证书里声明的的 CN 字段是否一致。
        credential = [NSURLCredential credentialForTrust:challenge.protectionSpace.serverTrust];
        if (credential) {
        disposition = NSURLSessionAuthChallengeUseCredential;
        } else {
        disposition = NSURLSessionAuthChallengePerformDefaultHandling;
        }
        } else {
        disposition = NSURLSessionAuthChallengeCancelAuthenticationChallenge;
        }
        } else {
        disposition = NSURLSessionAuthChallengePerformDefaultHandling;
        }
        
        if (completionHandler) {
        completionHandler(disposition, credential);
        }
        }
        ```

        其中，关于`evaluateServerTrust:forDomain`方法的定义，可参考 `AFNetworking`中`AFSecurityPolicy`模块的代码，Objective-C代码示例如下所示。

        ```
        - (BOOL)evaluateServerTrust:(SecTrustRef)serverTrust forDomain:(NSString *)domain {
        // 创建证书校验策略
        NSMutableArray *policies = [NSMutableArray array];
        if (domain) {
        // 需要验证请求的域名与证书中声明的 CN 字段是否一致
        [policies addObject:(__bridge_transfer id)SecPolicyCreateSSL(true, (__bridge CFStringRef)domain)];
        } else {
        [policies addObject:(__bridge_transfer id)SecPolicyCreateBasicX509()];
        }
        
        // 绑定校验策略到服务端返回的证书（serverTrust）
        SecTrustSetPolicies(serverTrust, (__bridge CFArrayRef)policies);
        
        // 评估当前 serverTrust 是否可信任，
        // 根据苹果官方文档 https://developer.apple.com/library/ios/technotes/tn2232/_index.html
        // 当 result 为 kSecTrustResultUnspecified 或 kSecTrustResultProceed 的情况下，serverTrust 可以被验证通过。
        SecTrustResultType result;
        SecTrustEvaluate(serverTrust, &result);
        return (result == kSecTrustResultUnspecified || result == kSecTrustResultProceed);
        }
        
        ```

    2.  **SNI问题**

        通过使用基于原生支持设置SNI字段的更底层的库（libcurl），解决SNI问题。

        **Objective-C代码示例**

        ```
        //{HTTPS域名}:443:{IP地址}
        NSString *curlHost = ...;
        _hosts_list = curl_slist_append(_hosts_list, curlHost.UTF8String);
        curl_easy_setopt(_curl, CURLOPT_RESOLVE, _hosts_list);
        ```

        其中，`curlHost`形（如`{HTTPS域名}:443:{IP地址}，_hosts_list`）是结构体类型`hosts_list`，可设置多个IP与Host域名间的映射关系。通过在`curl_easy_setopt`方法中传入`CURLOPT_RESOLVE`，将该映射设置到HTTPS请求中，即可达到设置SNI的目的。


## 游戏盾解决方案 {#section_nbq_k1x_kfb .section}

利用游戏盾自身机制，阿里云提供一种更好的解决方案：

1.  将被访问网站的DNS域名解析到127.0.0.1。

    **说明：** 更改DNS域名解析需要确认该域名没有其它线上业务。

2.  HTTP、HTTPS请求时，使用`域名：代理端口`的形式替换原先的`127.0.0.1: 代理端口`接入方式来访问web服务器。其中的代理端口即`getProxyTcpByDomain`接口返回的端口。

通过上述操作，就可以完美解决SSL认证、单IP多HTTPS服务器等问题。使用这种方式，无需改动代码，且能更好地保护源站服务器。

同时，与传统解决方案相比，游戏盾解决方案在安全性方面也更完善。由于传统解决方案在代码中暴露域名信息，如果域名配置了源站服务器IP，攻击者很容易找到源站服务器直接进行攻击；而采用游戏盾解决方案，即使攻击者发现源站域名，也无法获取源站服务器IP。

因此，无论是从兼容性、简单性、还是安全性角度，推荐您使用游戏盾解决方案解决HOST不匹配问题。

