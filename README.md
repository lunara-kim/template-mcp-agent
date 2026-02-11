# template-mcp-agent

A flexible TypeScript template for creating specialized MCP (Model Context Protocol) servers for single agent deployment. This template provides a foundation for building custom AI agents that can be integrated with MCP-compatible clients.

## What is MCP?

The **Model Context Protocol (MCP)** is an open protocol that standardizes how applications provide context to Large Language Models (LLMs). It enables seamless integration between AI models and various data sources, tools, and services through a unified interface.

MCP servers act as bridges that expose specific capabilities (tools, resources, prompts) to MCP clients, allowing LLMs to interact with external systems in a standardized way.

Learn more: [Model Context Protocol Documentation](https://modelcontextprotocol.io)

## Features

- 🚀 **Ready-to-use template** for quick MCP server development
- 🔧 **Customizable agent prompts** via external configuration file
- 📦 **TypeScript-based** with full type safety
- 🎯 **Single tool interface** (`activate_agent`) for flexible agent activation
- 🔌 **Standard MCP SDK integration** using `@modelcontextprotocol/sdk`
- 📝 **Easy customization** - modify `agent_prompt.txt` to change agent behavior
- ⚡ **Stdio transport** for seamless integration with MCP clients

## Tech Stack

- **Runtime**: Node.js >= 18
- **Language**: TypeScript 5.x
- **Framework**: [@modelcontextprotocol/sdk](https://www.npmjs.com/package/@modelcontextprotocol/sdk) ^0.6.0
- **Transport**: stdio (standard input/output)

## Installation

Clone the repository and install dependencies:

```bash
git clone https://github.com/lunara-kim/template-mcp-agent.git
cd template-mcp-agent
npm install
```

## Usage

### Build

Compile TypeScript and copy the agent prompt file:

```bash
npm run build
```

This will:
- Compile TypeScript files to the `dist/` directory
- Copy `agent_prompt.txt` to `dist/agent_prompt.txt`

### Start

Run the MCP server:

```bash
npm start
```

The server will start listening on stdio for MCP client connections.

### Development

Watch mode for TypeScript compilation:

```bash
npm run dev
```

### Clean

Remove the build directory:

```bash
npm run clean
```

## Project Structure

```
template-mcp-agent/
├── src/
│   └── index.ts              # Main MCP server implementation
├── agent_prompt.txt          # Agent behavior definition (customize this!)
├── package.json              # Project configuration and dependencies
├── tsconfig.json             # TypeScript configuration
├── LICENSE                   # MIT License
└── README.md                 # This file
```

## How It Works

This MCP server exposes a single tool called `activate_agent`:

### Tool: `activate_agent`

Activates the specialized agent with the given context and parameters.

**Input Schema:**
```json
{
  "context": "string (required) - Main context or task for the agent",
  "additional_info": "string (optional) - Additional information",
  "parameters": "object (optional) - Additional key-value parameters"
}
```

**Behavior:**
1. Reads the agent prompt from `agent_prompt.txt`
2. Combines the prompt with user-provided context
3. Returns a formatted prompt for the LLM to process

## Customization Guide

### 1. Modify Agent Behavior

Edit `agent_prompt.txt` to define your agent's personality, capabilities, and instructions. The current template includes a data analysis assistant, but you can replace it with any agent type:

- Customer support agent
- Code reviewer
- Content writer
- Research assistant
- Translation expert
- etc.

### 2. Change Tool Definition

In `src/index.ts`, modify the `AGENT_TOOL` constant to change:
- Tool name
- Description
- Input schema
- Required/optional parameters

### 3. Add Multiple Tools

Extend the `AgentHandler` class to support multiple specialized tools:

```typescript
const TOOLS: Tool[] = [
  AGENT_TOOL,
  // Add more tools here
];
```

### 4. Customize Server Metadata

Update the server name and version in `src/index.ts`:

```typescript
const server = new Server(
  {
    name: 'your-custom-agent-mcp',
    version: '1.0.0',
  },
  // ...
);
```

### 5. Add Resources or Prompts

Extend the server capabilities by implementing additional MCP features:
- Resources (data sources)
- Prompts (reusable prompt templates)
- Sampling (LLM completion requests)

Refer to the [MCP SDK documentation](https://modelcontextprotocol.io/docs) for details.

## Integration

To use this MCP server with an MCP client (e.g., Claude Desktop, OpenClaw, or other MCP-compatible applications):

1. Build the project: `npm run build`
2. Configure your MCP client to launch this server via stdio
3. Example configuration for Claude Desktop (`claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "template-agent": {
      "command": "node",
      "args": ["/path/to/template-mcp-agent/dist/index.js"]
    }
  }
}
```

## Example Use Case

The included `agent_prompt.txt` defines a data analysis assistant. When activated with a DataFrame context, the agent will:
- Explore and visualize data
- Handle missing values
- Perform statistical analysis
- Build classification/regression models
- Generate comprehensive reports

You can replace this with any specialized agent behavior by editing the prompt file.

## Development Tips

- **Hot Reload**: Use `npm run dev` to recompile on changes
- **Testing**: Connect to the server using an MCP client or build a test harness
- **Debugging**: Check `console.error()` output for server logs
- **Validation**: Ensure `agent_prompt.txt` is present before starting

## Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest features
- Submit pull requests

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Resources

- [Model Context Protocol](https://modelcontextprotocol.io)
- [MCP SDK Documentation](https://modelcontextprotocol.io/docs)
- [MCP TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk)
- [Example MCP Servers](https://github.com/modelcontextprotocol/servers)

## Author

Created by [Eun Hye Kim](https://github.com/lunara-kim)

---

⭐ If you find this template useful, please consider giving it a star!
