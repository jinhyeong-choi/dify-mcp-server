# Model Context Protocol (MCP) Server for dify workflows
A simple implementation of an MCP server for using [dify](https://github.com/langgenius/dify). It achieves the invocation of the Dify workflow by calling the tools of MCP.
## 🔨Installation
The server can be installed via [Smithery](https://smithery.ai/server/dify-mcp-server) or manually. Config.yaml is required for both methods. Thus, we need to prepare it before installation.

### Prepare config.yaml
Before using the mcp server, you should prepare a config.yaml to save your dify_base_url and dify_sks. The example config like this:
```yaml
dify_base_url: "https://cloud.dify.ai/v1"
dify_app_sks:
  - "app-sk1"
  - "app-sk2"
```
You can run the following command in your terminal to quickly create a configuration file:
```
mkdir -p ~/tools && cat > ~/tools/config.yaml <<EOF
dify_base_url: "https://cloud.dify.ai/v1"
dify_app_sks:
  - "app-sk1"
  - "app-sk2"
EOF
```
Different SKs correspond to different dify workflows.
### Installing via Smithery
[smithery](https://smithery.ai) is a tool to install the dify mcp server automatically.
To install Dify MCP Server for Claude Desktop automatically via [Smithery](https://smithery.ai/server/dify-mcp-server):

Tips: `npm` has added the `npx` command since version 5.2.
Mac users can use `brew install node` install the npm aand 

```bash
npx -y @smithery/cli install dify-mcp-server --client claude
```

In addition to `claude`, `cline, windsurf, roo-cline, witsy, enconvo, cursor` are also supported.

### Manual Installation
❓ If you haven't installed uv or uvx yet, you can do it quickly with the following command:
```
curl -Ls https://astral.sh/uv/install.sh | sh
```

#### ✅ Method 1: Use uv (local clone + uv start)

You can also run the dify mcp server manually in your clients. The config of client should like the following format:
```json
{
"mcpServers": {
  "mcp-server-rag-web-browser": {
    "command": "uv",
      "args": [
        "--directory", "${DIFY_MCP_SERVER_PATH}",
        "run", "dify_mcp_server"
      ],
    "env": {
       "CONFIG_PATH": "$CONFIG_PATH"
    }
  }
}
}
```
Example config:
```json
{
"mcpServers": {
  "dify-mcp-server": {
    "command": "uv",
      "args": [
        "--directory", "/Users/lyx/Downloads/dify-mcp-server",
        "run", "dify_mcp_server"
      ],
    "env": {
       "CONFIG_PATH": "/Users/lyx/Downloads/config.yaml"
    }
  }
}
}
```

#### ✅ Method 2: Use uvx (no need to clone code, recommended)

```json
"mcpServers": {
  "dify-mcp-server": {
    "command": "uvx",
      "args": [
        "--from","git+https://github.com/YanxingLiu/dify-mcp-server","dify_mcp_server"
      ],
    "env": {
       "CONFIG_PATH": "/Users/lyx/Downloads/config.yaml"
    }
  }
}
```
### Enjoy it
At last, you can use dify tools in any client who supports mcp.
