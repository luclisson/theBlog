---
date-created: 2026-05-17
category: computer science
source: https://modelcontextprotocol.io/docs/learn/architecture
---
# key concept

# [[MCP data layer]]
## init (lifecycle management)
**capability negotiation handshake**
client sends an `initialize` request to establish the connection and negotiate supported features.

request
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "initialize",
  "params": {
    "protocolVersion": "2025-06-18",
    "capabilities": {
      "elicitation": {}
    },
    "clientInfo": {
      "name": "example-client",
      "version": "1.0.0"
    }
  }
}
```

response
```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "protocolVersion": "2025-06-18",
    "capabilities": {
      "tools": {
        "listChanged": true
      },
      "resources": {}
    },
    "serverInfo": {
      "name": "example-server",
      "version": "1.0.0"
    }
  }
}
```

after a successful initialization the client sends a notification to the host e.g. a llm which manages the clients to indicate it's ready
```json
{
  "jsonrpc": "2.0",
  "method": "notifications/initialized"
}
```
## understanding initial handshake
- protocolVersion -> ensure both client and server are using the same protocol Version. if compatible versions can't be negotiated, the connection will be terminated.
- capability discovery -> both server and client can say what features they support (which [[MCP data layer protocol#primitives|primitives]] they support) and if they support [[MCP data layer protocol#notifications|notifications]].
- identity exchange -> client/server info for debugging and compatibility

### in the given example
client capabilities
```json
"capabilities": {
      "elicitation": {}
    },
```
this tells the server the client can handle elicitations which are user interaction requests.
	
	elicitation/create method calls

server capabilities
```json
"capabilities": {
      "tools": {
        "listChanged": true
      },
      "resources": {}
    },
```
server supports tools primitives AND can send a `tools/listChanged` notification.
server also supports resource primitives which means the client can use `resources/list` and `resources/read` methods

## how would init work in AI applications
Now lets discuss how this would really work in an application using pseudocode. Later on I want to implement this using python, but this would be a different note :)

fist AI app MCP client manager needs to establish a connection and do the capability negotiation. Also he (MCP client manager) needs to store the servers capabilities for later usage. 
```pseudocode
async with stdio_client(server_config) as (read, write):
    async with ClientSession(read, write) as session:
        init_response = await session.initialize()
        if init_response.capabilities.tools:
            app.register_mcp_server(session, supports_tools=True)
        app.set_server_ready(session)
```
# tool discovery
MCP client manager can now use `tools/list` to get a list of all available features the server supports which is essential for later server usage.
A `tools/list` request could look something like this according to the official MCP documentation.
```json
{
  "jsonrpc": "2.0",
  "id": 2,
  "method": "tools/list"
}
```
one might ask what the id is about. I assume this is just an id of a request for identifying the request and later logging purposes, but I need to do some research about that.
research:
	something comes right here

The request is rather simple since it doesn't contain any parameters. The response is more interesting.

**sample response**
```json
{
  "jsonrpc": "2.0",
  "id": 2,
  "result": {
    "tools": [
      {
        "name": "calculator_arithmetic",
        "title": "Calculator",
        "description": "Perform mathematical calculations including basic arithmetic, trigonometric functions, and algebraic operations",
        "inputSchema": {
          "type": "object",
          "properties": {
            "expression": {
              "type": "string",
              "description": "Mathematical expression to evaluate (e.g., '2 + 3 * 4', 'sin(30)', 'sqrt(16)')"
            }
          },
          "required": ["expression"]
        }
      },
      {
        "name": "weather_current",
        "title": "Weather Information",
        "description": "Get current weather information for any location worldwide",
        "inputSchema": {
          "type": "object",
          "properties": {
            "location": {
              "type": "string",
              "description": "City name, address, or coordinates (latitude,longitude)"
            },
            "units": {
              "type": "string",
              "enum": ["metric", "imperial", "kelvin"],
              "description": "Temperature units to use in response",
              "default": "metric"
            }
          },
          "required": ["location"]
        }
      }
    ]
  }
}
```

the result object contains a tools array which provides metadata about the available tools.

- **name** is a unique identifier, acting as pr-key
- **title** human readable title which the client shows the user
- **description** self explainatory
- **inputSchema** provides clear documentation about optional and required input. Also it adds type validation.
## how would the tool discovery work in an AI app
AI app fetches all available tools from all servers connected to it and stores all of them combined. This lets the host understand what tools are available. This enable the llm to make automated tool call decisions.
```pseudocode
# Pseudo-code using MCP Python SDK patterns
available_tools = []
for session in app.mcp_server_sessions():
    tools_response = await session.list_tools()
    available_tools.extend(tools_response.tools)
conversation.register_available_tools(available_tools)
```
# tool call execution
the client has already knowledge about the available tools. This means he (client) is now able to perform tool calls using `tools/call` methods.
example tool call execution request
```json
{
  "jsonrpc": "2.0",
  "id": 3,
  "method": "tools/call",
  "params": {
    "name": "weather_current",
    "arguments": {
      "location": "San Francisco",
      "units": "imperial"
    }
  }
}
```
note: the key value pair "name": "val" uses the pr-key name not the title value of the tool discovery response!

**arguments** contains the inputs specified in the tool description `inputSchema`


example tool call execution response
```json
{
  "jsonrpc": "2.0",
  "id": 3,
  "result": {
    "content": [
      {
        "type": "text",
        "text": "Current weather in San Francisco: 68°F, partly cloudy with light winds from the west at 8 mph. Humidity: 65%"
      }
    ]
  }
}
```
note that the content object is an array. This is the case because MCP support **multi-format** responses e.g. imgage, text, audio etc. Therefore, all instances of that array need the `type` field.
## how does tool execution work in an AI app
when the llm decides to use a tool, the AI app intercepts the tool call. It routes the call to the appropriate MCP server, executes the tool call and returns the response back to the llm.

```pseudocode
# Pseudo-code for AI application tool execution
async def handle_tool_call(conversation, tool_name, arguments):
    session = app.find_mcp_session_for_tool(tool_name)
    result = await session.call_tool(tool_name, arguments)
    conversation.add_tool_result(result.content)
```














