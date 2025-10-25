# Assistender MCP Server

A scaffold project for deploying a Model Context Protocol (MCP) server compatible with the OpenAI Apps SDK. This server provides a basic implementation using the official `@modelcontextprotocol/sdk` library with TypeScript and Node.js.

## Overview

The Model Context Protocol (MCP) is an open specification for connecting large language model clients to external tools, data, and user interfaces. This scaffold provides a minimal MCP server that:

1. **Lists tools** – Advertises available tools with their JSON Schema contracts
2. **Calls tools** – Executes tool requests from the model
3. **Returns structured content** – Sends back formatted responses

## Prerequisites

- Node.js 18+
- npm, yarn, or pnpm for dependency management

## Installation

Clone the repository and install dependencies:

```bash
npm install
```

Or using pnpm:

```bash
pnpm install
```

## Usage

Start the MCP server:

```bash
npm start
```

The server will start on port 8000 (or the port specified in the `PORT` environment variable) and expose:

- **SSE stream**: `GET http://localhost:8000/mcp`
- **Message endpoint**: `POST http://localhost:8000/mcp/messages?sessionId=...`

## Project Structure

```
assistender-mcp-server/
├── src/
│   └── server.ts          # Main MCP server implementation
├── package.json           # Dependencies and scripts
├── tsconfig.json          # TypeScript configuration
├── .gitignore             # Git ignore rules
└── README.md              # This file
```

## Adding Custom Tools

To add your own tools, modify `src/server.ts`:

1. Define your tool schema in the `tools` array
2. Add a handler in the `CallToolRequestSchema` request handler
3. Return structured content that matches your tool's output schema

Example:

```typescript
const tools: Tool[] = [
  {
    name: "my-custom-tool",
    description: "Description of what this tool does",
    inputSchema: {
      type: "object",
      properties: {
        param1: {
          type: "string",
          description: "Parameter description",
        },
      },
      required: ["param1"],
    },
  },
];
```

## OpenAI Apps SDK Integration

This MCP server follows the OpenAI Apps SDK specifications and can be integrated with ChatGPT developer mode. The server uses Server-Sent Events (SSE) transport, making it compatible with MCP inspectors and ChatGPT connectors.

For more information, see:
- [OpenAI Apps SDK Documentation](https://developers.openai.com/apps-sdk)
- [OpenAI Apps SDK Examples](https://github.com/openai/openai-apps-sdk-examples)
- [Model Context Protocol](https://modelcontextprotocol.io)

## Development

The project uses:
- **TypeScript** for type safety
- **tsx** for running TypeScript directly
- **Zod** for runtime schema validation
- **@modelcontextprotocol/sdk** for MCP implementation

## License

MIT