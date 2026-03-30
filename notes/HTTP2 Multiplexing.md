**Title: HTTP/2 Multiplexing** 

**Idea:** The ability to send multiple requests and responses in parallel over a single TCP connection without them blocking each other (solving Head-of-Line blocking). 

**Why it matters:** Reduces the latency associated with the "TCP Handshake" and allows for high-throughput communication in dense microservice environments. 

**Connections:**
- [[TCP Persistent Connections]]    
- [[Network Latency Optimization]]