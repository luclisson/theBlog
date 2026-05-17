---
date-created: 2026-05-17
category: computer science
source: https://modelcontextprotocol.io/docs/learn/architecture
---
# key concept

# life cycle management
MCP is a stateful protocol which requires [[MCP data layer#life cycle management|life cycle management]]. (some parts can be made stateless using HTTP)
# primitives
the primitives of an MCP server are the most important concept. 

	I think can are just the server features...

They specify can type of context that can be shared to the MCP host.
1. tools
	executable functions that a llm can invoke
	e.g. file operations, database queries, api calls
2. data
   resources that provide contextual information which the llm can use. e.g. file content, db records, api responses
3. prompts 
   Reusable templates that help structure interactions with language models e.g. system prompts, few-shot examples
Also it is distinguished between server and client primitives.
# notifications
MCP supports real time notifications to enable dynamic interactions between client and server. If the server gets access to a new tool, it can send a notification to the client to inform him about the newly added tool.
	
	send via JSON RPC 2.0 without expecting a response

## why do notifications matter
1. **Dynamic Environments**: Tools may come and go based on server state, external dependencies, or user permissions
2. **Efficiency**: Clients don’t need to poll for changes; they’re notified when updates occur
3. **Consistency**: Ensures clients always have accurate information about available server capabilities
4. **Real-time Collaboration**: Enables responsive AI applications that can adapt to changing contexts

This notification pattern extends beyond tools to other MCP primitives, enabling comprehensive real-time synchronization between clients and servers.