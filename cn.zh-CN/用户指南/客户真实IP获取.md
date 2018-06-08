# 客户真实IP获取 {#concept_h1h_n2f_xdb .concept}

游戏盾获取真实IP和是否开启游戏安全网关、后端是SLB还是ECS相关，具体组合情况如下：

## 游戏盾节点—\>ECS {#section_pxx_n2f_xdb .section}

TCP端口无需做任何改动，源站服务器上看到的IP就是真实客户端IP，包括ECS的安全组配置对象也是针对真实的客户端IP。

## 游戏盾节点—\>游戏安全网关—\>ECS {#section_qxx_n2f_xdb .section}

TCP端口获取的到的会是游戏安全网关的的IP，如果需要获取到客户的真实IP需要在程序中集成游戏盾的TOA模块，具体请联系游戏盾开发团队，目前提供Windows、linux的不同版本的TOA。

## 游戏盾节点—\>游戏安全网关—\>SLB—\>ECS {#section_rxx_n2f_xdb .section}

需要进行实际测试来进行判断（看TCP端口的程序情况，不一定能够通过游戏盾TOA模块来获取真实IP）。

## 游戏盾节点—\>SLB—\>ECS {#section_sxx_n2f_xdb .section}

无法获取客户的真实IP。

