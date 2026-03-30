**Title: gRPC (Google Remote Procedure Call)** 

**Idea:** A high-performance, open-source RPC framework that allows a client application to directly call methods on a server application on a different machine as if it were a local object. It uses **HTTP/2** for transport and **Protocol Buffers** as the interface description language.

**Why it matters:** It standardizes how microservices communicate by providing a strongly-typed, contract-based system that is significantly faster and more efficient than text-based REST/JSON.

**Trade-offs:** While superior for internal service-to-service communication, it is harder to consume directly from web browsers without a proxy (like gRPC-Web) and is not human-readable for easy debugging without specialized tools.

**Connections:** 
* [[Protocol Buffers (Protobuf)]]
- [[HTTP2 Multiplexing]]    
- [[Microservices]]    
- [[Strict Service Contracts]]
- [[Bidirectional Streaming]]
- [[Language Agnosticism (Polyglot Support)]]