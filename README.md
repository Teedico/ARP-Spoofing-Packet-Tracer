# ARP-Spoofing-Packet-Tracer
# ARP Spoofing Simulation in Cisco Packet Tracer

## Objective

This project demonstrates an Address Resolution Protocol (ARP) spoofing attack using a Cisco Packet Tracer simulation. The goal is to show how a malicious device on a local area network (LAN) can intercept traffic intended for another device (typically the default gateway/router) by sending falsified ARP messages. This simulation also explores methods for detecting and mitigating such attacks.

## Skills Learned/Demonstrated

-   **Network Simulation:** Proficiency in using Cisco Packet Tracer to build, configure, and simulate network topologies and attacks.
-   **Network Configuration:** Configuring IP addresses, subnet masks, and basic device settings within Packet Tracer.
-   **Understanding Layer 2 Attacks:** Demonstrating knowledge of ARP protocol vulnerabilities and the mechanics of ARP spoofing/poisoning.
-   **Packet Analysis:** Using Packet Tracer's simulation mode to observe ARP packet exchanges and verify traffic redirection during an attack.
-   **Cybersecurity Concepts:** Identifying and explaining ARP spoofing detection techniques and mitigation strategies.
-   **Technical Documentation:** Creating visual and written documentation of a simulated network attack.

## Tools Used

-   **Cisco Packet Tracer:** Version 8.2.2 or similar, used for network simulation and visualization.

## Steps

The simulation was set up and executed as follows:

1.  **Network Topology Setup:**
    *   A basic LAN topology was created in Packet Tracer consisting of:
        *   A client PC (named `PC0`).
        *   A network switch (named `Switch0`).
        *   A router acting as the default gateway (named `Router0`).
        *   An additional PC acting as the attacker (named `MALICIOUS DEVICE`).
    *   All devices were connected via Copper Straight-Through cables to the switch.
      
2.  **Device IP Configuration:**
    *   Devices were configured with static IP addresses within the same subnet (e.g., 192.168.1.0/24):
        *   `Router0` (Gateway): Likely configured with 192.168.1.1.
        *   `PC0` (Victim): Likely configured with 192.168.1.2.
        *   `MALICIOUS DEVICE` (Attacker): Explicitly configured with IP address `192.168.1.3` and Subnet Mask `255.255.255.0`.

3.  **Simulating the ARP Spoofing Attack:**
    *   The simulation environment was switched to "Simulation Mode" to observe packet flow step-by-step.
    *   The `MALICIOUS DEVICE` was configured to send crafted ARP reply packets onto the network.
    *   These spoofed ARP replies falsely claimed that the IP address of `Router0` (e.g., 192.168.1.1) mapped to the MAC address of the `MALICIOUS DEVICE`.
    *   The target of these spoofed packets was `PC0`.

4.  **Observing ARP Cache Poisoning and Traffic Redirection:**
    *   In Simulation Mode, the flow of the spoofed ARP packets from the `MALICIOUS DEVICE` to `Switch0` and then broadcast or forwarded to `PC0` was observed.
    *   Upon receiving the spoofed ARP reply, `PC0` would update its local ARP cache, incorrectly associating `Router0`'s IP address with the `MALICIOUS DEVICE`'s MAC address.
    *   As a result, any subsequent network traffic `PC0` attempted to send to the default gateway (`Router0`) would be sent at the Ethernet layer to the `MALICIOUS DEVICE`'s MAC address instead, effectively intercepting the traffic.

## ARP Detection Methods

Detecting ARP spoofing typically involves:

-   **Network Monitoring:** Observing network traffic for unusual ARP activity or anomalies. Tools like Wireshark (or Packet Tracer's simulation mode) can capture and analyze ARP packets.
-   **ARP Table Analysis:** Periodically checking the ARP tables (`arp -a`) on hosts and network devices for duplicate MAC address entries associated with different IP addresses, or suspicious/static entries mapping critical IPs (like the gateway) to unexpected MACs.
-   **Using Specialized Tools:** Employing network security monitoring systems or specific ARP spoofing detection tools that actively monitor ARP traffic and alert on suspicious patterns.

## ARP Mitigation Strategies

Several strategies can help mitigate the risk of ARP spoofing:

-   **Static ARP Entries:** Manually configuring static ARP entries on critical devices for important IPs (like the default gateway). This prevents the device from accepting dynamic, potentially spoofed, ARP updates for that specific IP-MAC mapping.
-   **Dynamic ARP Inspection (DAI):** A security feature available on many enterprise-grade switches. DAI intercepts ARP packets, validates them against a trusted database of IP-MAC bindings, and drops invalid or spoofed ARP packets.
-   **Packet Filtering:** Implementing MAC address filtering or port security on switches can limit which devices can send traffic on specific ports, although this is less effective against spoofing itself than DAI.
-   **Virtual Private Networks (VPNs):** While not a direct ARP spoofing countermeasure on the local LAN segment, VPNs encrypt traffic between endpoints, protecting data confidentiality even if traffic is intercepted.
-   **Security Awareness & Testing:** Educating users and IT staff about such threats and potentially running controlled tests to evaluate defenses.

## References

-   Bart L. -B. (2022, May 19). *Address resolution protocol (ARP) spoofing: what is it and how to prevent an ARP attack*. CrowdStrike. https://www.crowdstrike.com/cybersecurity-101/spoofing-attacks/arp-spoofing/
-   Appknox. (2024). *ARP Spoofing*. Appknox Cyber Security Jargons. https://www.appknox.com/cyber-security-jargons/arp-spoofing
