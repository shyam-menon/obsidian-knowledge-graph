**Title: Bidirectional Streaming** 

**Idea:** A call where both the client and server send a sequence of messages using a read-write stream. The two streams operate independently. 

**Why it matters:** Essential for "chatty" applications like real-time gaming, collaborative editing, or high-frequency financial tickers. **Trade-offs:** Higher complexity in state management compared to simple Unary calls. 

**Connections:**

- [[Stateful Communication]]    
- [[Full Duplex Systems]]