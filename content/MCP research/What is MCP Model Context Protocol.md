---
date-created: 2026-05-17
category: computer science
source: https://modelcontextprotocol.io/docs/getting-started/intro
---
# key concept
MCP (Model Context Protocol) is an open-source standard for connecting AI applications to external systems.
# analogy
Think of MCP like a USB-C port for AI applications. Just as USB-C provides a standardized way to connect electronic devices, MCP provides a standardized way to connect AI applications to external systems.
![[Pasted image 20260517124923.png]]

# major benefits
- **Developers**: MCP reduces development time and complexity when building, or integrating with, an AI application or agent.
- **End-users**: MCP results in more capable AI applications or agents which can access your data and take actions on your behalf when necessary.

# scope
The Model Context Protocol includes the following projects:

- [[MCP Specification]]: A specification of MCP that outlines the implementation requirements for clients and servers.
- [MCP SDKs](https://modelcontextprotocol.io/docs/sdk): SDKs for different programming languages that implement MCP.
- **MCP Development Tools**: Tools for developing MCP servers and clients, including the [[MCP Inspector]]
- [[MCP Reference Server Implementations]]: Reference implementations of MCP servers.
# concepts
## Participants
follow a server-client architecture. There is a difference between local and remote MCP Servers. Usually local only serves one clients where as remote serve multiple clients. Also note that local MCP uses [[STDIO transport]] and remote ones use HTTP.
- **MCP Host**: The AI application that coordinates and manages one or multiple MCP clients
- **MCP Client**: A component that maintains a connection to an MCP server and obtains context from an MCP server for the MCP host to use
- **MCP Server**: A program that provides context to MCP clients
![[Pasted image 20260517130459.png]]

## Layers
there is the [[MCP data layer]] and the [[MCP transport layer]].
For short the data layer defines the [JSON-RPC](https://www.jsonrpc.org/) for the server-client communication. The transport layer, as the name suggests, defines the communication methods and channel, this also includes authorization.
Conceptually the data layer is the inner layer, while the transport layer is the outer layer.
# example
see [[MCP example]]