# Development history {#concept_vjj_bf2_xdb .concept}

## History of Game Shield {#section_xbv_bf2_xdb .section}

Game Shield has experienced three major technological evolutions since its inception. From the first generation's “Cloud layer” to the current Game Shield, major improvements have taken place both in terms of its technical architecture and functional implementation.

One of the reasons for these changes is the inequality problem of attacking and defense resources; while another reason is based on our reflection on the routing rules and infrastructure of existing networks.

In simple terms, Game Shield balances the attacking and defense resources by dispatching traffic in a risk control mode. In essence, Game Shield is more like a way to change traffic directions beyond routing and DNS.

## Cloud Layer: First Experiment {#section_ybv_bf2_xdb .section}

The predecessor of Game Shield is the Cloud layer project. It was born from a rescue experiment in early 2015.

A company had been repeatedly attacked by hackers and traditional DDoS defense methods had all been ineffective.  In such an emergency, the company sought cooperation from Alibaba Cloud's security team and proposed a new method that could avoid hacker attacks through fast traffic scheduling.

At the time, this method had not been verified in any actual implementation. Alibaba Cloud's DDoS protection and security technology team collaborated with the user's technical team in a manner like “feeling the way in the dark” and after putting this new protection method into practice, it succeeded in combating a series of attacks.

The “Cloud layer” era began.

At the time, the hackers' attack tactics were relatively simple. They found a target IP address, and hit the IP into the black hole routing status through a wave of large DDoS attacks \(10~50GBps\).  The preparation time for a hacker to launch a next wave of attacks was about 10-15 minutes. The rapid scheduling of distributed IPs within seconds by the “Cloud layer” suppressed the hacker's continued minute-level attacks and won a small victory.

Afterwards, the “Cloud layer” model won several other victories. Meanwhile, however, new forms of attacks are constantly being developed. “Cloud layer”, despite achieving a second-level IP scheduling speed, must adapt its algorithms and efficiency to keep pace with hacker attacks. In this context, the era of Game Shield has arrived!

## Game Shield: Enter the battlefield {#section_zbv_bf2_xdb .section}

It has always been the case that over 50% of domestic DDoS and connection flood attacks target the gaming industry. Thus, the gaming industry has become the best target for DDoS attackers, and it is also the best industry for testing and scheduling algorithms.

Therefore, Alibaba Cloud's security team decided to apply the accumulated technical experience from the “Cloud layer” era to the gaming industry and turn it into a risk control model that all users can use and take advantage of.

A long time before Game Shield was born, Alibaba Cloud’s security team rigorously analyzed the attack and defense patterns in the gaming industry, and learned the characteristics of registration, login, and players of the game services. On this basis, it reconstructed the smart scheduling algorithm of Game Shield. 

Game Shield not only inherits the fast scheduling capability of the Cloud layer, it can also perform normalized process analysis through collecting terminal information and network communications. Based on the resources and features on the cloud, Game Shield can calculate, process, and store massive amounts of terminal data. Compared with the offline environment, Alibaba Cloud has achieved substantial breakthroughs by taking advantage of cloud computing platforms in computing and data processing: the image of each terminal device is completed, and finally settled into a new scheduling factor of “terminal threat value”. 

The core of all data processing at Game Shield is the AirTraffic Control \(ATC\) system, of which the cognitive foundation is based on deep machine learning \(DL\) and Long Short-Term Memory \(LSTM\). It can quickly isolate malicious users from the dispatch system.

On the front lines of the gaming industry, Game Shield has proven its capabilities and continues to upgrade itself under the heaviest of attacks. Meanwhile, threat identification and affected area control have replaced scheduling to become the new technical keywords.

## Refinement and Stratified Governance: A Small Step Ahead {#section_acv_bf2_xdb .section}

This is only the beginning. Attackers are also gradually increasing their own resource input.  If you want to stay a small step ahead of hackers, data and algorithms alone are not enough. You must truly understand their attack trends and attack tactics.

Game Shield was refined through implementation in actual scenarios and finally evolved into streamlined solution: NetGuard was born.

With the help of the AI modeling and analysis capabilities accumulated in the previous two phases, Game Shield challenges the attacks against the business layer.

Game Shield serial learns the characteristics of specific business data to quickly identify malformed and sudden abnormal traffic, and blocks it on the trunk. Meanwhile, Alibaba Cloud's security team proposed a three-dimensional protection system that consists user-layer, network-layer, access-layer, and business-layer linkages, so that Game Shield can help users build the most suitable security architecture.

The core of the three-dimensional protection system of Game Shield lies in stratified governance. First, large traffic attacks rely on the network layer to solve, while technical connection flood attacks are solved through access layer. The three-dimensional protection system can break through bandwidth limitations, control the range and time of the attack, and accurately identify the user's behavior.

## A Tilted Balance {#section_bcv_bf2_xdb .section}

From 2015 to 2017, two years experience and technical polishing have enabled Game Shield to apply a new security risk control mode to help gaming industry users solve significant problems.

Nevertheless, from Cloud layer to Game Shield, it is only the first step of Alibaba Cloud's security team tilting the balance of DDoS attacks. The true direction for advancement is to build a safe and credible network that carries “clean traffic” and to extend this network further out.

