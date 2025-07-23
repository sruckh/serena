# API Contracts

## Model Context Protocol (MCP) Server

Serena exposes its functionality through the Model Context Protocol (MCP), allowing AI agents to interact with the coding assistant tools.

### Server Information

```http
GET /server/info
```

#### Response
```json
{
  "name": "serena-agent",
  "version": "0.1.3",
  "protocol_version": "2024-11-05",
  "capabilities": {
    "tools": true,
    "prompts": false,
    "resources": false,
    "logging": true
  }
}
```

## Tool Endpoints

### List Available Tools

```http
GET /tools/list
```

#### Response
```json
{
  "tools": [
    {
      "name": "read_file",
      "description": "Read file contents with optional line range",
      "inputSchema": {
        "type": "object",
        "properties": {
          "file_path": {"type": "string"},
          "start_line": {"type": "integer"},
          "end_line": {"type": "integer"}
        },
        "required": ["file_path"]
      }
    }
  ]
}
```

### Execute Tool

```http
POST /tools/call
```

#### Request
```json
{
  "name": "read_file",
  "arguments": {
    "file_path": "src/main.py",
    "start_line": 1,
    "end_line": 50
  }
}
```

#### Response
```json
{
  "content": [
    {
      "type": "text",
      "text": "File contents here..."
    }
  ],
  "isError": false
}
```

## Core Tools

### File Operations

#### read_file
```http
POST /tools/call
```

**Request**:
```json
{
  "name": "read_file",
  "arguments": {
    "file_path": "src/example.py",
    "start_line": 10,
    "end_line": 50
  }
}
```

**Response**:
```json
{
  "content": [{"type": "text", "text": "def example():\n    pass"}],
  "isError": false
}
```

#### write_file
```http
POST /tools/call
```

**Request**:
```json
{
  "name": "write_file", 
  "arguments": {
    "file_path": "src/new_file.py",
    "content": "print('Hello World')"
  }
}
```

#### find_files
**Rate limit**: 50 requests per minute  
**Auth**: Not required  
**Notes**: Respects .gitignore patterns

```http
POST /tools/call
```

**Request**:
```json
{
  "name": "find_files",
  "arguments": {
    "pattern": "*.py",
    "max_results": 100
  }
}
```

### Symbol Operations  

#### find_symbols
```http
POST /tools/call
```

**Request**:
```json
{
  "name": "find_symbols",
  "arguments": {
    "query": "MyClass",
    "symbol_type": "class",
    "file_pattern": "*.py"
  }
}
```

**Response**:
```json
{
  "content": [{
    "type": "text", 
    "text": "Found symbols:\n- MyClass in src/models.py:15-45"
  }],
  "isError": false
}
```

#### get_symbol_definition
**Rate limit**: 100 requests per minute  
**Auth**: Not required  
**Notes**: Requires active language server

#### edit_symbol
**Rate limit**: 20 requests per minute  
**Auth**: Not required  
**Notes**: Makes backup before modification

### Memory Operations

#### read_memory
```http
POST /tools/call
```

**Request**:
```json
{
  "name": "read_memory",
  "arguments": {
    "name": "project_architecture"
  }
}
```

**Response**:
```json
{
  "content": [{
    "type": "text",
    "text": "# Project Architecture\n\nThis project follows..."
  }],
  "isError": false
}
```

#### write_memory
**Rate limit**: 10 requests per minute  
**Auth**: Not required  
**Notes**: Overwrites existing memory files

#### list_memories
**Rate limit**: 50 requests per minute  
**Auth**: Not required

### Project Management

#### activate_project  
```http
POST /tools/call
```

**Request**:
```json
{
  "name": "activate_project",
  "arguments": {
    "project_root": "/path/to/project"
  }
}
```

**Response**:
```json
{
  "content": [{
    "type": "text",
    "text": "Project activated: /path/to/project"
  }],
  "isError": false
}
```

#### get_project_info
**Rate limit**: 100 requests per minute  
**Auth**: Not required

#### switch_mode
**Rate limit**: 20 requests per minute  
**Auth**: Not required  
**Notes**: Changes tool availability based on mode

## Web Dashboard API

### Dashboard Status

```http
GET /api/status
```

#### Response
```json
{
  "status": "active",
  "project": "/path/to/current/project",
  "language_servers": {
    "python": "running",
    "typescript": "stopped"
  },
  "memory_count": 15,
  "tool_usage": {
    "read_file": 245,
    "find_symbols": 89,
    "edit_symbol": 23
  }
}
```

### Language Server Management

```http
POST /api/language-servers/{language}/restart
```

#### Response
```json
{
  "status": "restarted",
  "language": "python",
  "pid": 12345
}
```

### Memory Management

```http
GET /api/memories
```

#### Response
```json
{
  "memories": [
    {
      "name": "project_architecture",
      "size": 2048,
      "modified": "2025-01-23T14:30:00Z"
    }
  ]
}
```

```http
DELETE /api/memories/{name}
```

## Error Responses

### Standard Error Format
```json
{
  "content": [{
    "type": "text", 
    "text": "Error: File not found: /path/to/file"
  }],
  "isError": true,
  "error_code": "FILE_NOT_FOUND",
  "details": {
    "file_path": "/path/to/file",
    "suggestion": "Check if the file exists and path is correct"
  }
}
```

### Common Error Codes
- `FILE_NOT_FOUND` - Requested file does not exist
- `PERMISSION_DENIED` - Insufficient permissions to access resource
- `LANGUAGE_SERVER_ERROR` - Language server communication failed  
- `INVALID_ARGUMENTS` - Tool arguments are invalid or missing
- `PROJECT_NOT_ACTIVE` - No project is currently activated
- `SYMBOL_NOT_FOUND` - Requested symbol could not be located
- `MEMORY_ERROR` - Memory operation failed
- `TIMEOUT` - Operation timed out

## Authentication

Currently, Serena operates without authentication as it's designed for local development use. Future versions may include:

- API key authentication for remote access
- Token-based authentication for dashboard
- Role-based access control for multi-user environments

## Rate Limiting

Rate limits are applied per tool type:
- **File Operations**: 100 requests per minute
- **Symbol Operations**: 50 requests per minute  
- **Memory Operations**: 20 requests per minute
- **Project Operations**: 10 requests per minute

Rate limit headers:
```http
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1640995200
```

## Protocol Compliance

Serena implements MCP protocol version `2024-11-05` with full support for:
- Tool discovery and execution
- Structured error handling
- Content streaming (planned)
- Progress reporting (planned)

## Client Libraries

### Python Client Example
```python
import asyncio
from mcp import ClientSession, StdioServerParameters
from mcp.client.stdio import stdio_client

async def main():
    server_params = StdioServerParameters(
        command="uv",
        args=["run", "serena-mcp-server"]
    )
    
    async with stdio_client(server_params) as (read, write):
        async with ClientSession(read, write) as session:
            # List available tools
            tools = await session.list_tools()
            
            # Call a tool
            result = await session.call_tool(
                "read_file", 
                {"file_path": "src/main.py"}
            )
```

### TypeScript Client Example
```typescript
import { Client } from '@modelcontextprotocol/sdk/client/index.js';
import { StdioClientTransport } from '@modelcontextprotocol/sdk/client/stdio.js';

const client = new Client({
  name: "serena-client",
  version: "1.0.0"
}, {
  capabilities: {
    tools: {}
  }
});

const transport = new StdioClientTransport({
  command: "uv",
  args: ["run", "serena-mcp-server"]
});

await client.connect(transport);

// Use the client
const tools = await client.listTools();
const result = await client.callTool({
  name: "read_file",
  arguments: { file_path: "src/main.py" }
});
```

## Keywords <!-- #keywords -->
MCP protocol, API endpoints, tool execution, file operations, symbol manipulation, memory management, project management, web dashboard, authentication, rate limiting, error handling, client libraries