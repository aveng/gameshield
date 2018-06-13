# Encrypted Tunnel Mode {#concept_a13_z2f_xdb .concept}

This article describes the encrypted tunnel  mode.

## 1. What is the encrypted tunnel mode, and what are the advantages of enabling it? {#section_ybc_1ff_xdb .section}

The encrypted tunnel mode is an access mode in which the SDK takes over the communications between the client and the server and completely encrypts the traffic. It is also immune to protocol-stimulated attacks. Only legitimate traffic encrypted by Game Shield is passed. Assessing Game Shield by this mode provides complete immunity to connection flood attacks, with 0 mistaken and 0 missed.

**Note:** Side effects of enabling the encrypted tunnel mode: Setting up a TCP connection consumes 4 RTT duration, and completing the establishment of the TCP connection consumes even more time \(within 100 ms\). The data transmission process has no increase in latency.

## 2. How to enable the encrypted tunnel mode? {#section_zbc_1ff_xdb .section}

To enable the encrypted tunnel mode, follow these steps:

1.  Make sure that the business has Game Security Gateway enabled.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13519/3560_en-US.png)

2.  Contact Game Shield’s team to enable the encrypted tunnel mode of the game's SDK.
3.  On the Business Management page, click **Protection Setting** of the Game Security Gateway cluster, locate to the **Encrypted Security Tunnel** function, enable the encrypted tunnel mode and set the **Client Coverage** rate.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13519/3561_en-US.png)


## 3. What are the points of attention when enabling the encrypted tunnel mode? {#section_h45_rkf_xdb .section}

-   You must use the Game Shield SDK's return IP and port to establish the connection to the game. The game IP in the encrypted tunnel mode is **127.0.0.1**, and the game port is **random**.
-   The encrypted tunnel mode is valid for a single game. After the mode is enabled, if there is more than one business in a game, the SDK tunnel encryption is enabled for multiple businesses of the game. To avoid conflict, you must create multiple games for distinction.
-   Whether your game is immune from connection flood attacks depends on whether the function that only the tunnel encrypted traffic is allowed to pass through Game Shield is enabled. Only when this is enabled, the game is immune from connection flood attacks.

## 4. How to defend connection flood attacks without the encrypted tunnel mode? {#section_rkn_5kf_xdb .section}

The connection flood protection in Game Shield relies on the Game Security Gateway module. You can defend connection flood attacks by using the following methods without enabling the SDK's encrypted tunnel mode. You have to contact Game Shield's team to do some manual configurations.

1.  New and concurrent connection restrictions on IPs for specific port \(some mistaken and missed issues may occur\).
2.  The protocol whitelist mode on specific port. By checking protocols, only protocols of your game are allowed \(protection for the TCP and WS protocols is better,  while the HTTP protocol protection is not good\). For more information, see [Protocol Filtering Configuration](intl.en-US/User Guide/Protocol Whitelist Configuration.md#).
3.  By using functions like IP blacklist, area blocking, and high-risk IDC area blocking, block traffic from specific areas \(it depends on the IP address library, and some mistaken and missed issues may occur\).

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13519/3563_en-US.png)

Therefore, the effect of connection flood protection cannot be 100% without the encrypted tunnel mode of Game Shield's SDK.

