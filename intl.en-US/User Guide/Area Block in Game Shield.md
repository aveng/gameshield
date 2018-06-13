# Area Block in Game Shield {#concept_lws_fw2_xdb .concept}

This article describes the area blocking function in Game Shield.

## Background {#section_gqn_hw2_xdb .section}

This function is based on the IP address library. It directly discards the relevant regional SYN packets.

It mainly provides the following areas blocking:

-   China \(accurate to the province/state\)
-   International
-   High-risk IDC area

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13520/3519_en-US.png)

## FAQs {#section_vkn_xcf_xdb .section}

1.  What is the precision of the area-blocking IP address library?  Are there ever mistaken blocks?

    There is a certain amount of mistaken blocks, but the IP precision is above 99.9%. The area block function is enabled based on your requirements.

2.  What is the high-risk IDC area?  Will there be any updates?

    The high-risk IDC area is the IP address data calculated based on the data of full-scale connection flood attacks and IP reputation intercepted by Alibaba Cloud on a daily basis. Currently, the recognition rate under a large-scale connection flood attack is high \(CC attacks consume real IPs. Since broiler resources are limited, and IDC is fixed compared to IPs, IDC broiler resource pool can be generated through data accumulation\). This data is currently updated every 24 hours.

3.  Since the IP address library is very large, does it affect the protection performance of Game Security Gateway?

    The Game Security Gateway provides million-level IP blacklist and whitelist. The actual test shows that the performance consumption of million-level blacklist and whitelist can be ignored.

    During attacks, we find that directly intercepting SYN data through the IP blacklist **increases the protection capability of Game Security Gateway**, because it does not get into the TCP protocol stack, which is performance-consuming.


