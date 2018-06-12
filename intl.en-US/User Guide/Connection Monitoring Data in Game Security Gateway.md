# Connection Monitoring Data in Game Security Gateway {#concept_mgx_t52_xdb .concept}

This article explains the connection monitoring data parameters.

The Game Security Gateway in Game Shield provides the following statistics:

-   **Number of attempted connections**: The number of SYN packets received by the system in unit time.
-   **Number of established connections**: The number of TCP connections successfully established by the system in unit time through three handshakes \(this data corresponds to the protection capabilities purchased by Game Security Gateway\).
-   **Number of outgoing connections**: The number of TCP connections established by the same source site server after passing through all monitoring and interception. This data can be compared with the established connection data to check the specific TCP interception amount of Game Security Gateway.
-   **Packet detection failed**: TCP connection data that is intercepted due to failure of passing through the DPI packet signature detection.
-   **Tunnel detection failed**: TCP connection data that is intercepted due to no tunnel encryption.
-   **Active disconnection or unresponding**: Connection data of source station TCP when it actively disconnects or times out within a unit of time.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13517/3485_en-US.png)

## FAQs {#section_m2n_jv2_xdb .section}

1.  Why can hundreds of attempts to connect and established connections be seen even when no traffic?

    This part of traffic is the number of TCP connections consumed by the LVS health check. The numbers of attempted connections and established connections are different for different clusters.  It may also be connection consumption caused by other web crawlers and scanners.

2.  What is the difference between the number of established connections and the number of released connections?

    The number of established connections indicates TCP connections that are successful with three handshakes. This part of connections includes the TCP connection for which no valid load data is sent after the connection is established. The number of released connections only includes the actual TCP connection amount for which the TCP connection is established, simultaneously passes the DPI packet detection and tunnel encryption detection, and is connected to the backend server.

3.  Is there a difference between the origin site actively disconnecting and not responding?

    This part of data is collectively referred to as disconnection data of TCP connections. Generally, it is reference data for judging abnormal disconnections through long-term operation.

4.  Why is there sometimes no data regarding failed packet inspection and failed tunnel detection?

    If the DPI functionality is not enabled and the functionality that only allows the tunnel encrypted traffic to pass through is not enabled, this part of the data is not generated and displayed.


