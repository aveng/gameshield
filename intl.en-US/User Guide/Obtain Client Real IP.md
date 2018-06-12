# Obtain Client Real IP {#concept_h1h_n2f_xdb .concept}

This article describes how to obtain the real IP of a client.

For whether Game Shield obtains the real IP, whether the Cloud Gaming Security gateway is enabled, and whether the backend is related to SLB or ECS, the specific combinations are as follows:

## Game Shield node -\> ECS {#section_pxx_n2f_xdb .section}

The TCP port does not need any modification. The IP obtained on the origin server is the client’s real IP. The ECS's security group configuration object is also for the client’s real IP.

## Game Shield Node -\> Game Security Gateway -\> ECS {#section_qxx_n2f_xdb .section}

The TCP port obtains the IP of Game Security Gateway. To obtain the client’s real IP, you must integrate Game Shield’s TOA module to the program. For details, please contact the Game Shield’s team. Currently, different versions of the TOA module are available for Windows and Linux.

## Game Shield node -\> Game Security Gateway -\> SLB -\> ECS {#section_rxx_n2f_xdb .section}

You must conduct tests to determine it. \(Relying on the TCP port of the program, you may  obtain the real IP through Game Shield’s TOA module.\)

## Game Shield node—\>SLB—\>ECS {#section_sxx_n2f_xdb .section}

You cannot get the real IP of the client.

