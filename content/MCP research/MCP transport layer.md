---
date-created: 2026-05-17
category: computer science
source: https://modelcontextprotocol.io/docs/learn/architecture
---
# key concept
The transport layer manages communication channels and authentication between clients and servers. It handles connection establishment, message framing, and secure communication between MCP participants.
# methods
## STDIO transport
Uses standard input/output streams for direct process communication between local processes on the same machine, providing optimal performance with no network overhead.
## HTTP transport 
HTTP Post for client to server communication. This also enables you to use HTTP authentication methods such as OAuth, Bearer Tokens, Api keys etc. MCP recommends using OAuth.


