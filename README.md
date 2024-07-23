# DoS attacking tool
Series of functions for sending different forms of Denial of Service attacks

UDP Flood Attack (ddos_udp_packets_attack)
Sends a continuous stream of UDP packets to a specified IP and port.

HTTP Attack (dos_multi_loop_HTTP_attack)
Creates multiple threads to repeatedly send HTTP GET requests to a specified IP and port.

HTTP Packet Connection Attack (dos_multi_packet_connection_HTTP_attack)
Similar to the HTTP attack but sends large packets of data.

SYN Flood Attack (syn_flood)
Sends SYN packets to a target IP and port, potentially overwhelming it.

ICMP Flood Attack (icmpflood)
Sends a flood of ICMP packets (ping requests) to the target IP.
