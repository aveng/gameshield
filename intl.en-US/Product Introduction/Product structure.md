# Product structure {#concept_ltv_xc2_xdb .concept}

Game Shield is a security solution for the gaming industry in the Alibaba Cloud Anti-DDoS Pro product series.  Game Shield is tailored specifically for the gaming industry to address issues, such as the complex DDoS attacks and game connection flood attacks in the industry. 

Game Shield consists of two modules: 

-   **Distributed anti-DDoS node**: Through the distributed anti-DDoS nodes, Game Shield can defend against attacks at over 600G level.
-   **Game security gateway**: Through the decoding of proprietary protocols, Game Shield supports defense against connection flood attacks that are unique for the game industry.

## How Game Shield Defends against DDoS Attacks {#section_sbv_yc2_xdb .section}

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13500/3422_en-US.png)

Unlike the standard Anti-DDoS Pro data center, Game Shield does not combat the attack by using massive bandwidth, but instead uses the distributed anti-DDoS nodes, effectively splitting and dispatching hacker attacks so that the attacks cannot be concentrated on a certain point. Meanwhile, it can isolate hackers through dynamic dispatch strategies based on the SDK data and traffic data.

## How Game Shield Defends against Connection Flood Attacks {#section_ubv_yc2_xdb .section}

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13500/3426_en-US.png)

In general, connection flood attacks in the gaming industry are different from those targeting websites.  Site-targeted connection flood attacks are mainly based on the HTTP or HTTPS protocols. The protocols are relatively standardized, so it is easy to perform data analysis and protocol analysis on them.  However, most of the protocols in the gaming industry are proprietary or uncommon. Therefore, for the defense of game-targeted connection flood attacks, Alibaba Cloud has launched a professional cloud-based defensive gateway, the Game Security Gateway \(formerly known as NetGuard, or NG for short\). 

The Game Security Gateway establishes a game business firewall between the user's services and the attackers, and accurately identifies real players and hackers according to the attacker's TCP connection behavior, dynamic information after game connection, and full-flow data. 

-   The Game Security Gateway supports big data analysis and identifies normal player behavior based on the characteristics of real user business, thus directly blocking abnormal clients \(invalid protocols\).  Moreover, it can perform a precise block on the traffic from any province/state or overseas traffic at any time and supports million-level blacklists and whitelists.
-   The Game Security Gateway can establish an encrypted communication tunnel with the SDK, fully taking over the network communications between the client and the server. It only releases the traffic authenticated by the SDK and the Game Security Gateway, thus completely solving TCP protocol layer connection flood attacks \(analog protocol-type attacks\). 

    **Note:** SDK version above 5.1.7 is required.


