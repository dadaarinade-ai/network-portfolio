# IDS Project – ICMP & HTTP GET Detection

## Objective  
Detect ICMP ping requests and HTTP GET requests on the network using Snort IDS rules.

## Rules  
```text  
alert icmp any any -> any any (msg:"ICMP Ping Detected"; itype:8; sid:1000001; rev:1;)  
alert tcp any any -> any 80 (msg:"HTTP GET Request Detected"; content:"GET"; http_method; sid:1000002; rev:1;)  
```

## How It Works  
- The ICMP rule triggers when a ping is sent.  
- The HTTP GET rule triggers when someone sends a GET request over port 80.  
- In a working Snort setup, these would generate alerts in the console.

## Simulated Output  
```  
[**] [1:1000001:1] ICMP Ping Detected [**]  
[**] [1:1000002:1] HTTP GET Request Detected [**]  
```
