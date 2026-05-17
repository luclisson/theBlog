---
date-created: 2026-05-17
category: computer science
source: https://modelcontextprotocol.io/docs/learn/architecture
---
# key concept
implements JSON-RCP 2.0 to define message structure for the communication between server and client.
# covers
## life cycle management
Handles connection initialization, capability negotiation, and connection termination between clients and servers.

One might ask what does **capability negotiation** mean in this context.
	This means the server and client negotiate what capabilities the server provides and what the client can use. Ensures that the client know what tools he can use. Also the server knows what he must provide.
## server features
enables server to provide core functionality.
this could be something of the following:
- tools for AI actions
- resources for context data
- prompts for interaction templates from and to the client
## client features
enables servers to request sample data from host llm, input from user and log messages to the client.
### utility features
Supports additional capabilities like notifications for real-time updates and progress tracking for long-running operations

# protocol
see [[MCP data layer protocol]]
