## Network Topology Diagram

```mermaid
flowchart TB
    H["Windows Host Computer"]
    V["Oracle VirtualBox"]
    N["Host-Only Network<br/>192.168.56.0/24"]

    P["Parrot OS<br/>192.168.56.103"]
    W["Wireshark<br/>Traffic Analysis"]
    M["Metasploitable2<br/>192.168.56.102"]

    H --> V
    V --> N
    N --- P
    N --- M
    P --> W
   ``` 
