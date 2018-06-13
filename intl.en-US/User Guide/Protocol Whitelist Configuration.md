# Protocol Whitelist Configuration {#concept_lwl_xlf_xdb .concept}

This article describes the protocol whitelist configuration.

## 1. Introduction of protocol whitelist {#section_elj_ylf_xdb .section}

In general, a connection flood protection against the TCP protocol is made by limiting the speed of a single-IP connection. Whit this, a large number of mistakes and leaks exist. Game Security Gateway in Game Shield offers a filtering mode for the TCP protocol content. This mode can be used to filter TCP contents to allow only TCP traffic that meets specific characteristics through Game Shield. This mode **does not require SDK access and has a zero mistake rate**. However, this functionality cannot defense protocol simulation flood attacks \(for example, HTTP flood attack\).

## 2. How to configure the protocol whitelist? {#section_flj_ylf_xdb .section}

1.  Ensures that your business has Game Security Gateway enabled.
2.  Provides business protocol characteristics packets for specific port.
    -   Sniffers packets on a client.
    -   Sniffers packets on the server for the specific port by using the wireshark or tcpdump tool.
3.  Sends the Game Shield team with the sniffer packet file \(x. pcap\) for DPI protocol characteristics customization.
4.  Run the characteristics online testing with the Game Shield team. 

## 3. Notes {#section_hlj_ylf_xdb .section}

Currently, the protocol whitelist functionality is not available on the console, but the corresponding interception data can be viewed in **Reports** \> **Connection Monitoring**.

Currently, only the whitelist configuration is available with the following scenarios:

-   For HTTP protocol port: only HTTP protocol access is allowed.
-   For TCP protocol port: only protocol accesses that match the first packet characteristics is allowed.
-   For WS protocol: only protocol accesses that match the first packet characteristics is allowed.

