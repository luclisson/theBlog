---
date-created: 2026-05-17
category: computer science
source: https://modelcontextprotocol.io/docs/learn/server-concepts
---
# key concept

# basics
the basics are already described in [[What is MCP Model Context Protocol]].
# user interaction model
tools are **model-controlled** meaning AI models can view and invoke them automatically. Human oversight is managed via the following:

- Displaying available tools in the UI, enabling users to define whether a tool should be made available in specific interactions
- Approval dialogs for individual tool executions
- Permission settings for pre-approving certain safe operations
- Activity logs that show all tool executions with their results

All these CAN be implemented in the AI application managing the MCP servers etc.
# how do resources work
applications can access the exposes data directly and select relevant portions, search with embeddings or just pass the entire data to the model which then decides what to do with it.

Each resource has a unique URI (e.g., `file:///path/to/document.md`) and declares its MIME type for appropriate content handling.
[MIME types](https://mimetype.io/all-types)
## discovery patterns
**direct resources** 
fixed URI which points to specific data
`calendar://events/2024` - returns calendar availability for 2024
**resource templates**
dynamic URI with parameters
- `travel://activities/{city}/{category}` - returns activities by city and category
- `travel://activities/barcelona/museums` - returns all museums in Barcelona

how is type validation handled?
resource templates include metadata such as expected MIME type.

|Method|Purpose|Returns|
|---|---|---|
|`resources/list`|List available direct resources|Array of resource descriptors|
|`resources/templates/list`|Discover resource templates|Array of resource template definitions|
|`resources/read`|Retrieve resource contents|Resource data with metadata|
|`resources/subscribe`|Monitor resource changes|Subscription confirmation|

# how prompts work
A prompt provides resusable templates which define expected inputs and interaction patterns. Its very important that they are user-controlled, which means they wont get triggered automatically and need explicit tool calling to be invoked.

| Method         | Purpose                    | Returns                               |
| -------------- | -------------------------- | ------------------------------------- |
| `prompts/list` | Discover available prompts | Array of prompt descriptors           |
| `prompts/get`  | Retrieve prompt details    | Full prompt definition with arguments |
example:
```json 
{
  "name": "plan-vacation",
  "title": "Plan a vacation",
  "description": "Guide through vacation planning process",
  "arguments": [
    { "name": "destination", "type": "string", "required": true },
    { "name": "duration", "type": "number", "description": "days" },
    { "name": "budget", "type": "number", "required": false },
    { "name": "interests", "type": "array", "items": { "type": "string" } }
  ]
}
```
Rather than unstructured natural language input, the prompt system enables:

1. Selection of the “Plan a vacation” template
2. Structured input: Barcelona, 7 days, $3000, `[“beaches”, “architecture”, “food”]`
3. Consistent workflow execution based on the template

