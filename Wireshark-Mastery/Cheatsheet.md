# Wireshark Cheatsheet

## Common Filters
tcp, udp, dns, tls, quic
ip.addr == 10.0.2.15
tcp.port == 443
udp.port == 53
tcp.flags.syn == 1 && tcp.flags.ack == 0

## TCP Flags
SYN → Connection start
SYN/ACK → Connection accepted
ACK → Connection confirmed
FIN → Connection closing politely
RST → Connection aborted

## QUIC/TLS Notes
QUIC = UDP 443
TLS = encrypted HTTPS traffic
tls.handshake.extensions_server_name → Show Server Name (SNI)

## Analysis Tips
Statistics → Protocol Hierarchy → traffic breakdown
Statistics → Conversations → top talkers
Follow TCP/UDP Stream → inspect full conversation
Filter suspicious traffic → unusual ports or repeated SYN requests
