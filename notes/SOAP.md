**Title:** SOAP (Simple Object Access Protocol)

**Idea:** SOAP is an XML-based messaging protocol with rigidly defined standards for message structure, encoding, and communication rules. Services are described by WSDL (Web Services Description Language) contracts. It is transport-agnostic — it can run over HTTP, SMTP, or TCP — but HTTP is most common.

**Key characteristics:**
- **XML envelope:** Every message is wrapped in a standard SOAP envelope with header and body sections
- **WSDL contracts:** The API is formally described in a machine-readable contract file; clients generate stubs from it
- **WS-Security built-in:** Supports message-level encryption, digital signatures, and authentication natively
- **ACID transactions:** Supports WS-AtomicTransaction for distributed transactions across services
- **Transport-agnostic:** Not tied to HTTP — can work over any transport protocol
- **Strong typing:** All data types are explicitly declared in the schema

**Trade-offs:**
- Verbose and heavyweight — XML parsing and strict schema validation add overhead compared to REST/JSON
- Built-in enterprise-grade security and transaction support make it the right choice for regulated industries
- Poor developer experience for modern APIs — tooling is complex, payloads are large
- Tightly coupled: clients depend on the WSDL contract; changes require coordinated updates

**When to use:**
- Enterprise integrations in banking, insurance, and healthcare
- Legacy system interoperability where SOAP services already exist
- Scenarios requiring built-in message-level security (WS-Security) and distributed transaction guarantees
- Government and regulatory systems with strict compliance requirements

**Connections:**
- [[REST]]
- [[gRPC]]
- [[Protocol Buffers (Protobuf)]]
- [[Strict Service Contracts]]
- [[Language Agnosticism (Polyglot Support)]]

Up: [[API protocols 101]]

## Sources
https://blog.bytebytego.com/p/api-protocols-101-a-guide-to-choose

## Tags
#api
