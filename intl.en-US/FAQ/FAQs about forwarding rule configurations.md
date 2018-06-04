# FAQs about forwarding rule configurations {#concept_cj1_5sf_xdb .concept}

## What forwarding rules and ports are supported by Game Shield? {#section_vrk_wsf_xdb .section}

Supported port range: 80, 443, and 1025 to 65535

Supported forwarding rule: TCP

## What is the forwarding entry limit on Game Shield ports? {#section_qcc_ysf_xdb .section}

Game Shield’s single IP can support up to 50 port forwarding entries. If you need more, you can create multiple business groups \(50 forwarding entries per business and the IP forwarding rules under all businesses are the same\) to meet your requirements.

To turn on the game application gateway, you can contact Game Shield’s team to enable the SDK access and meet the business requirements through 4-layer port multiplexing. \( In this mode, the program requires great modification.\)

## How does Game Shield support the HTTP/HTTPS protocol? {#section_xtj_1tf_xdb .section}

Use the TCP protocol for forwarding instead of HTTP and HTTPS protocols.

It is expected that Game Shield will launch the local HTTP proxy mode in May.

## Are multiple single-forwarding backend servers supported? {#section_kfc_btf_xdb .section}

The single forwarding rule can support 20 origin sites. By default, load balancing and session maintenance are enabled according to the number of connections.

