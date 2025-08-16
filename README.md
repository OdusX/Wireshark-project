# Wireshark-project
Wireshark Analysis of Outgoing SYN flood Traffic
 Objectives
To simulate and analyze a denial of service attack using kali linux as both the attacker and the monitoring node.
Setup
•	Attacker: Kali Linux
•	Tools:
	hping3 to generate SYN flood traffic
	Wireshark to capture and analyze traffic
•	Target: Remote host with TCP port 80 exposed
Methodology
1. Generated attack traffic with:
 hping3 -S --flood -p 80 10.0.2.15
 
This produced a continuous stream of SYN packets aimed at the target server’s port 80.
Hping3 is a command-line tool for sending custom network packets used in security test and network diagnostics.






2. Captured traffic on the same Kali system with Wireshark.
 
3. Applied display filters:
•	tcp.flags.syn == 1 and tcp.flags.ack == 0.
 
The filter tcp.flags.syn == 1 and tcp.flags.ack == 0 captures initial SYN packets that start TCP connection attempts, indicating outgoing connection requests.

•	tcp.flags.syn == 1 and tcp.flags.ack == 1 

The filter tcp.flags.syn == 1 and tcp.flags.ack == 1 specifically looks for SYN/ACK packets, which are server replies to SYN requests as part of the TCP handshake. 
Not observing SYN/ACK packets on the attacker VM is expected since the attacker sends SYNs but does not receive replies when capturing locally.

Findings

Wireshark recorded a very high volume of SYN-only packets originating from Kali, confirming that hping3 was generating a SYN flood. The high volume of SYN packets with no corresponding ACKs indicates an incomplete TCP handshake, characteristic of a SYN flood attack.
Such traffic overloads server resources by forcing them to keep half-open connections waiting for handshakes that never complete. Monitoring with Wireshark helps visualize the attack through filters, making the flood easily identifiable.
 
Identifying abnormal SYN packet spikes early is essential for defending networks against real-world SYN flood attacks


Conclusion

Kali Linux successfully simulated an attacker generating a SYN flood, while simultaneously monitoring its own malicious traffic with Wireshark. The analysis demonstrated the ability to:
•	Generate attack traffic in a controlled environment.
•	Capture and filter packets with Wireshark.
•	Identify abnormal traffic patterns consistent with DoS behavior




