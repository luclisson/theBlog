---
date-created: 2026-05-17
category: computer science
source: https://modelcontextprotocol.io/docs/learn/client-concepts
---
# key concept
MCP clients are instantiated by host applications to communicate with particular MCP servers. The host is e.g. gemini or some IDE, a client handles ONE direct communication to one MCP server.
# core features
| Feature         | Explanation                                                                                                                                                                                       | Example                                                                                                                                |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| **Elicitation** | Elicitation enables servers to request specific information from users during interactions, providing a structured way for servers to gather information on demand.                               | A server booking travel may ask for the user’s preferences on airplane seats, room type or their contact number to finalise a booking. |
| **Roots**       | Roots allow clients to specify which directories servers should focus on, communicating intended scope through a coordination mechanism.                                                          | A server for booking travel may be given access to a specific directory, from which it can read a user’s calendar.                     |
| **Sampling**    | Sampling allows servers to request LLM completions through the client, enabling an agentic workflow. This approach puts the client in complete control of user permissions and security measures. | A server for booking travel may send a list of flights to an LLM and request that the LLM pick the best flight for the user.           |


# Elicitation
if turned on servers are enabled to ask the user for specific information during an interaction.

Instead of requiring all information up front, the server can request additional information if needed.
![[Screenshot 2026-05-17 at 13.04.47.png]]
# Roots
clients can specify which directories servers should focus on.
They can be used to communicate file system access boundaries.
A root consist of file URIs that indicate what directories the server can operate in.

	i think roots are limited to filesystem primitives (would make sense)

Its important to note that roots do not enforce the server to just look at the given folders. They can't and shouldn't be used as security measures.
# Sampling
Sampling allows servers to request language model completions through the client, enabling agentic behaviors while maintaining security and user control.

Server now doesn't need AI access and allows the client (which has AI access though the host) to handle the tasks. The Client is in complete control of user permissions and security measures.
![[Screenshot 2026-05-17 at 20.44.52.png]]
security is ensured via human-loop-checkpoints.

request example:
```json
{
  messages: [
    {
      role: "user",
      content: "Analyze these flight options and recommend the best choice:\n" +
               "[47 flights with prices, times, airlines, and layovers]\n" +
               "User preferences: morning departure, max 1 layover"
    }
  ],
  modelPreferences: {
    hints: [{
      name: "claude-sonnet-4-20250514"  // Suggested model
    }],
    costPriority: 0.3,      // Less concerned about API cost
    speedPriority: 0.2,     // Can wait for thorough analysis
    intelligencePriority: 0.9  // Need complex trade-off evaluation
  },
  systemPrompt: "You are a travel expert helping users find the best flights based on their preferences",
  maxTokens: 1500
}
```