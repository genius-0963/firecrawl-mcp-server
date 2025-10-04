# Firecrawl MCP Server - Installation Guide

This comprehensive guide provides step-by-step installation instructions for Firecrawl MCP Server across all MCP-compatible environments.

## 🪜 Install in Smithery

### ⚙️ Prerequisites
- Node.js 18.0.0 or higher
- npm or yarn package manager
- Firecrawl API key (get one at [firecrawl.dev](https://www.firecrawl.dev/app/api-keys))

### 🧩 Installation Steps

1. **Install Smithery CLI globally:**
   ```bash
   npm install -g @smithery/cli
   ```

2. **Install Firecrawl MCP Server:**
   ```bash
   npx -y @smithery/cli install @mendableai/mcp-server-firecrawl --client claude
   ```

3. **Configure your API key:**
   ```bash
   export FIRECRAWL_API_KEY=fc-YOUR_API_KEY
   ```

### ✅ Verification
```bash
# Check if Smithery is running
smithery status

# Test the MCP server
smithery test @mendableai/mcp-server-firecrawl
```

Expected output:
```
✅ MCP Server: @mendableai/mcp-server-firecrawl
✅ Status: Running
✅ Tools: 7 available
```

---

## 🪜 Install in Cursor

### ⚙️ Prerequisites
- Cursor version 0.45.6 or higher
- Node.js 18.0.0 or higher
- Firecrawl API key

### 🧩 Installation Steps

**For Cursor v0.48.6+:**

1. **Open Cursor Settings**
2. **Navigate to Features > MCP Servers**
3. **Click "+ Add new global MCP server"**
4. **Enter the following configuration:**
   ```json
   {
     "mcpServers": {
       "firecrawl-mcp": {
         "command": "npx",
         "args": ["-y", "firecrawl-mcp"],
         "env": {
           "FIRECRAWL_API_KEY": "YOUR-API-KEY"
         }
       }
     }
   }
   ```

**For Cursor v0.45.6:**
1. **Open Cursor Settings**
2. **Go to Features > MCP Servers**
3. **Click "+ Add New MCP Server"**
4. **Enter the following:**
   - Name: `firecrawl-mcp`
   - Type: `command`
   - Command: `env FIRECRAWL_API_KEY=your-api-key npx -y firecrawl-mcp`

**Windows users (if issues occur):**
```cmd
cmd /c "set FIRECRAWL_API_KEY=your-api-key && npx -y firecrawl-mcp"
```

### ✅ Verification
1. **Refresh the MCP server list**
2. **Access Composer via Command+L (Mac) or Ctrl+L (Windows)**
3. **Select "Agent" next to the submit button**
4. **Test with: "Scrape the content from https://example.com"**

Expected response: Web scraping tools should be available in the agent interface.

---

## 🪜 Install in Claude Code

### ⚙️ Prerequisites
- Claude Code application installed
- Node.js 18.0.0 or higher
- Firecrawl API key

### 🧩 Installation Steps

1. **Open Claude Code Settings**
2. **Navigate to Extensions > MCP Servers**
3. **Add new server configuration:**
   ```json
   {
     "name": "firecrawl-mcp",
     "command": "npx",
     "args": ["-y", "firecrawl-mcp"],
     "env": {
       "FIRECRAWL_API_KEY": "YOUR_API_KEY"
     }
   }
   ```

### ✅ Verification
- Check the MCP server status in Claude Code settings
- Test web scraping functionality in a new conversation

---

## 🪜 Install in Windsurf

### ⚙️ Prerequisites
- Windsurf IDE installed
- Node.js 18.0.0 or higher
- Firecrawl API key

### 🧩 Installation Steps

1. **Create or edit `./codeium/windsurf/model_config.json`:**
   ```json
   {
     "mcpServers": {
       "mcp-server-firecrawl": {
         "command": "npx",
         "args": ["-y", "firecrawl-mcp"],
         "env": {
           "FIRECRAWL_API_KEY": "YOUR_API_KEY"
         }
       }
     }
   }
   ```

2. **Restart Windsurf to apply changes**

### ✅ Verification
- Check MCP server status in Windsurf settings
- Test web scraping in a new chat session

---

## 🪜 Install in VS Code

### ⚙️ Prerequisites
- VS Code or VS Code Insiders
- Node.js 18.0.0 or higher
- Firecrawl API key

### 🧩 Installation Steps

**One-click installation:**
[![Install with NPX in VS Code](https://img.shields.io/badge/VS_Code-NPM-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=firecrawl&inputs=%5B%7B%22type%22%3A%22promptString%22%2C%22id%22%3A%22apiKey%22%2C%22description%22%3A%22Firecrawl%20API%20Key%22%2C%22password%22%3Atrue%7D%5D&config=%7B%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22firecrawl-mcp%22%5D%2C%22env%22%3A%7B%22FIRECRAWL_API_KEY%22%3A%22%24%7Binput%3AapiKey%7D%22%7D%7D)

**Manual installation:**

1. **Open User Settings (JSON):**
   - Press `Ctrl + Shift + P` (Windows/Linux) or `Cmd + Shift + P` (Mac)
   - Type `Preferences: Open User Settings (JSON)`

2. **Add the following configuration:**
   ```json
   {
     "mcp": {
       "inputs": [
         {
           "type": "promptString",
           "id": "apiKey",
           "description": "Firecrawl API Key",
           "password": true
         }
       ],
       "servers": {
         "firecrawl": {
           "command": "npx",
           "args": ["-y", "firecrawl-mcp"],
           "env": {
             "FIRECRAWL_API_KEY": "${input:apiKey}"
           }
         }
       }
     }
   }
   ```

**Workspace-specific configuration (optional):**
Create `.vscode/mcp.json` in your workspace:
```json
{
  "inputs": [
    {
      "type": "promptString",
      "id": "apiKey",
      "description": "Firecrawl API Key",
      "password": true
    }
  ],
  "servers": {
    "firecrawl": {
      "command": "npx",
      "args": ["-y", "firecrawl-mcp"],
      "env": {
        "FIRECRAWL_API_KEY": "${input:apiKey}"
      }
    }
  }
}
```

### ✅ Verification
- Check MCP server status in VS Code settings
- Test web scraping functionality in the chat interface

---

## 🪜 Install in Cline

### ⚙️ Prerequisites
- Cline IDE installed
- Node.js 18.0.0 or higher
- Firecrawl API key

### 🧩 Installation Steps

1. **Open Cline Settings**
2. **Navigate to MCP Configuration**
3. **Add server configuration:**
   ```json
   {
     "mcpServers": {
       "firecrawl-mcp": {
         "command": "npx",
         "args": ["-y", "firecrawl-mcp"],
         "env": {
           "FIRECRAWL_API_KEY": "YOUR_API_KEY"
         }
       }
     }
   }
   ```

### ✅ Verification
- Verify MCP server is active in Cline settings
- Test web scraping in a new conversation

---

## 🪜 Install in Zed

### ⚙️ Prerequisites
- Zed editor installed
- Node.js 18.0.0 or higher
- Firecrawl API key

### 🧩 Installation Steps

1. **Open Zed Settings**
2. **Navigate to AI > MCP Servers**
3. **Add new server:**
   ```json
   {
     "name": "firecrawl-mcp",
     "command": "npx",
     "args": ["-y", "firecrawl-mcp"],
     "env": {
       "FIRECRAWL_API_KEY": "YOUR_API_KEY"
     }
   }
   ```

### ✅ Verification
- Check MCP server status in Zed settings
- Test web scraping functionality

---

## 🪜 Install in Augment Code

### ⚙️ Prerequisites
- Augment Code IDE installed
- Node.js 18.0.0 or higher
- Firecrawl API key

### 🧩 Installation Steps

1. **Open Augment Code Settings**
2. **Go to Extensions > MCP**
3. **Add server configuration:**
   ```json
   {
     "mcpServers": {
       "firecrawl-mcp": {
         "command": "npx",
         "args": ["-y", "firecrawl-mcp"],
         "env": {
           "FIRECRAWL_API_KEY": "YOUR_API_KEY"
         }
       }
     }
   }
   ```

### ✅ Verification
- Verify server is running in Augment Code
- Test web scraping capabilities

---

## 🪜 Install in Roo Code

### ⚙️ Prerequisites
- Roo Code IDE installed
- Node.js 18.0.0 or higher
- Firecrawl API key

### 🧩 Installation Steps

1. **Open Roo Code Settings**
2. **Navigate to AI > MCP Servers**
3. **Add configuration:**
   ```json
   {
     "name": "firecrawl-mcp",
     "command": "npx",
     "args": ["-y", "firecrawl-mcp"],
     "env": {
       "FIRECRAWL_API_KEY": "YOUR_API_KEY"
     }
   }
   ```

### ✅ Verification
- Check MCP server status
- Test web scraping functionality

---

## 🪜 Install in Gemini CLI

### ⚙️ Prerequisites
- Gemini CLI installed
- Node.js 18.0.0 or higher
- Firecrawl API key

### 🧩 Installation Steps

1. **Install Firecrawl MCP globally:**
   ```bash
   npm install -g firecrawl-mcp
   ```

2. **Configure Gemini CLI:**
   ```bash
   gemini config set mcp.firecrawl.command "firecrawl-mcp"
   gemini config set mcp.firecrawl.env.FIRECRAWL_API_KEY "YOUR_API_KEY"
   ```

### ✅ Verification
```bash
# Check MCP server status
gemini mcp status

# Test web scraping
gemini ask "Scrape content from https://example.com"
```

---

## 🪜 Install in Claude Desktop

### ⚙️ Prerequisites
- Claude Desktop application
- Node.js 18.0.0 or higher
- Firecrawl API key

### 🧩 Installation Steps

1. **Locate your Claude Desktop config file:**
   - **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
   - **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

2. **Add the following configuration:**
   ```json
   {
     "mcpServers": {
       "mcp-server-firecrawl": {
         "command": "npx",
         "args": ["-y", "firecrawl-mcp"],
         "env": {
           "FIRECRAWL_API_KEY": "YOUR_API_KEY_HERE",
           "FIRECRAWL_RETRY_MAX_ATTEMPTS": "5",
           "FIRECRAWL_RETRY_INITIAL_DELAY": "2000",
           "FIRECRAWL_RETRY_MAX_DELAY": "30000",
           "FIRECRAWL_RETRY_BACKOFF_FACTOR": "3",
           "FIRECRAWL_CREDIT_WARNING_THRESHOLD": "2000",
           "FIRECRAWL_CREDIT_CRITICAL_THRESHOLD": "500"
         }
       }
     }
   }
   ```

3. **Restart Claude Desktop**

### ✅ Verification
- Check that Firecrawl tools appear in Claude Desktop
- Test web scraping functionality

---

## 🪜 Install in Opencode

### ⚙️ Prerequisites
- Opencode IDE installed
- Node.js 18.0.0 or higher
- Firecrawl API key

### 🧩 Installation Steps

1. **Open Opencode Settings**
2. **Navigate to AI > MCP Configuration**
3. **Add server:**
   ```json
   {
     "mcpServers": {
       "firecrawl-mcp": {
         "command": "npx",
         "args": ["-y", "firecrawl-mcp"],
         "env": {
           "FIRECRAWL_API_KEY": "YOUR_API_KEY"
         }
       }
     }
   }
   ```

### ✅ Verification
- Verify MCP server is active
- Test web scraping capabilities

---

## 🪜 Install in OpenAI Codex

### ⚙️ Prerequisites
- OpenAI Codex access
- Node.js 18.0.0 or higher
- Firecrawl API key

### 🧩 Installation Steps

1. **Configure MCP server in Codex settings:**
   ```json
   {
     "mcpServers": {
       "firecrawl-mcp": {
         "command": "npx",
         "args": ["-y", "firecrawl-mcp"],
         "env": {
           "FIRECRAWL_API_KEY": "YOUR_API_KEY"
         }
       }
     }
   }
   ```

### ✅ Verification
- Check MCP server status in Codex
- Test web scraping functionality

---

## 🪜 Install in JetBrains AI Assistant

### ⚙️ Prerequisites
- JetBrains IDE with AI Assistant plugin
- Node.js 18.0.0 or higher
- Firecrawl API key

### 🧩 Installation Steps

1. **Open JetBrains IDE**
2. **Go to Settings > Tools > AI Assistant > MCP**
3. **Add server configuration:**
   ```json
   {
     "name": "firecrawl-mcp",
     "command": "npx",
     "args": ["-y", "firecrawl-mcp"],
     "env": {
       "FIRECRAWL_API_KEY": "YOUR_API_KEY"
     }
   }
   ```

### ✅ Verification
- Check MCP server status in AI Assistant settings
- Test web scraping in AI chat

---

## 🪜 Install in Kiro

### ⚙️ Prerequisites
- Kiro IDE installed
- Node.js 18.0.0 or higher
- Firecrawl API key

### 🧩 Installation Steps

1. **Open Kiro Settings**
2. **Navigate to AI > MCP Servers**
3. **Add configuration:**
   ```json
   {
     "mcpServers": {
       "firecrawl-mcp": {
         "command": "npx",
         "args": ["-y", "firecrawl-mcp"],
         "env": {
           "FIRECRAWL_API_KEY": "YOUR_API_KEY"
         }
       }
     }
   }
   ```

### ✅ Verification
- Verify server is running
- Test web scraping functionality

---

## 🪜 Install in Trae

### ⚙️ Prerequisites
- Trae IDE installed
- Node.js 18.0.0 or higher
- Firecrawl API key

### 🧩 Installation Steps

1. **Open Trae Settings**
2. **Go to Extensions > MCP**
3. **Add server:**
   ```json
   {
     "name": "firecrawl-mcp",
     "command": "npx",
     "args": ["-y", "firecrawl-mcp"],
     "env": {
       "FIRECRAWL_API_KEY": "YOUR_API_KEY"
     }
   }
   ```

### ✅ Verification
- Check MCP server status
- Test web scraping capabilities

---

## 🪜 Install with Bun

### ⚙️ Prerequisites
- Bun runtime installed
- Firecrawl API key

### 🧩 Installation Steps

1. **Install Firecrawl MCP:**
   ```bash
   bun install -g firecrawl-mcp
   ```

2. **Set environment variable:**
   ```bash
   export FIRECRAWL_API_KEY=fc-YOUR_API_KEY
   ```

3. **Run the server:**
   ```bash
   bunx firecrawl-mcp
   ```

### ✅ Verification
```bash
# Check if server is running
bunx firecrawl-mcp --version

# Test the server
echo '{"method": "tools/list"}' | bunx firecrawl-mcp
```

Expected output:
```json
{
  "tools": [
    {"name": "firecrawl_scrape"},
    {"name": "firecrawl_map"},
    {"name": "firecrawl_search"},
    {"name": "firecrawl_crawl"},
    {"name": "firecrawl_extract"}
  ]
}
```

---

## 🪜 Install with Deno

### ⚙️ Prerequisites
- Deno runtime installed
- Firecrawl API key

### 🧩 Installation Steps

1. **Install Firecrawl MCP:**
   ```bash
   deno install --allow-net --allow-env --name firecrawl-mcp https://deno.land/x/firecrawl_mcp/mod.ts
   ```

2. **Set environment variable:**
   ```bash
   export FIRECRAWL_API_KEY=fc-YOUR_API_KEY
   ```

3. **Run the server:**
   ```bash
   firecrawl-mcp
   ```

### ✅ Verification
```bash
# Check server version
firecrawl-mcp --version

# Test server functionality
echo '{"method": "tools/list"}' | firecrawl-mcp
```

---

## 🪜 Install with Docker

### ⚙️ Prerequisites
- Docker installed
- Firecrawl API key

### 🧩 Installation Steps

1. **Pull the Docker image:**
   ```bash
   docker pull firecrawl/firecrawl-mcp:latest
   ```

2. **Run the container:**
   ```bash
   docker run -d \
     --name firecrawl-mcp \
     -e FIRECRAWL_API_KEY=fc-YOUR_API_KEY \
     -p 3000:3000 \
     firecrawl/firecrawl-mcp:latest
   ```

3. **For HTTP mode:**
   ```bash
   docker run -d \
     --name firecrawl-mcp \
     -e FIRECRAWL_API_KEY=fc-YOUR_API_KEY \
     -e HTTP_STREAMABLE_SERVER=true \
     -p 3000:3000 \
     firecrawl/firecrawl-mcp:latest
   ```

### ✅ Verification
```bash
# Check container status
docker ps | grep firecrawl-mcp

# Test HTTP endpoint (if using HTTP mode)
curl http://localhost:3000/health

# Check logs
docker logs firecrawl-mcp
```

Expected output:
```
[INFO] Firecrawl MCP Server initialized successfully
[INFO] Server running on port 3000
```

---

## 🪜 Install Desktop Extension

### ⚙️ Prerequisites
- Compatible desktop environment
- Node.js 18.0.0 or higher
- Firecrawl API key

### 🧩 Installation Steps

1. **Download the desktop extension:**
   ```bash
   npm install -g firecrawl-mcp-desktop
   ```

2. **Configure the extension:**
   ```bash
   firecrawl-mcp-desktop config set apiKey YOUR_API_KEY
   ```

3. **Start the desktop service:**
   ```bash
   firecrawl-mcp-desktop start
   ```

### ✅ Verification
```bash
# Check service status
firecrawl-mcp-desktop status

# Test functionality
firecrawl-mcp-desktop test
```

---

## 🪜 Install on Windows

### ⚙️ Prerequisites
- Windows 10 or higher
- Node.js 18.0.0 or higher
- PowerShell or Command Prompt
- Firecrawl API key

### 🧩 Installation Steps

1. **Install Node.js from [nodejs.org](https://nodejs.org/)**

2. **Install Firecrawl MCP globally:**
   ```cmd
   npm install -g firecrawl-mcp
   ```

3. **Set environment variable:**
   ```cmd
   set FIRECRAWL_API_KEY=fc-YOUR_API_KEY
   ```

4. **For persistent environment variable:**
   ```cmd
   setx FIRECRAWL_API_KEY "fc-YOUR_API_KEY"
   ```

5. **Run the server:**
   ```cmd
   firecrawl-mcp
   ```

### ✅ Verification
```cmd
# Check version
firecrawl-mcp --version

# Test server
echo {"method": "tools/list"} | firecrawl-mcp
```

### 🧰 Troubleshooting
- **If `npx` command fails:** Use `cmd /c "set FIRECRAWL_API_KEY=your-api-key && npx -y firecrawl-mcp"`
- **If permissions are denied:** Run Command Prompt as Administrator
- **If Node.js is not found:** Restart your terminal after installing Node.js

---

## 🪜 Install Amazon Q Developer CLI

### ⚙️ Prerequisites
- Amazon Q Developer CLI installed
- Node.js 18.0.0 or higher
- Firecrawl API key

### 🧩 Installation Steps

1. **Install Firecrawl MCP:**
   ```bash
   npm install -g firecrawl-mcp
   ```

2. **Configure Amazon Q Developer:**
   ```bash
   q config set mcp.firecrawl.command "firecrawl-mcp"
   q config set mcp.firecrawl.env.FIRECRAWL_API_KEY "YOUR_API_KEY"
   ```

3. **Enable MCP server:**
   ```bash
   q mcp enable firecrawl
   ```

### ✅ Verification
```bash
# Check MCP server status
q mcp status

# Test web scraping
q ask "Scrape content from https://example.com"
```

---

## 🧰 General Troubleshooting

### Common Issues and Solutions

**1. API Key Not Working**
```bash
# Verify API key format
echo $FIRECRAWL_API_KEY
# Should start with 'fc-'

# Test API key
curl -H "Authorization: Bearer $FIRECRAWL_API_KEY" https://api.firecrawl.dev/v1/health
```

**2. Node.js Version Issues**
```bash
# Check Node.js version
node --version
# Should be 18.0.0 or higher

# Update Node.js if needed
# Visit https://nodejs.org/ for latest version
```

**3. Permission Issues (macOS/Linux)**
```bash
# Fix npm permissions
sudo chown -R $(whoami) ~/.npm
```

**4. Windows Path Issues**
```cmd
# Add npm global bin to PATH
setx PATH "%PATH%;%APPDATA%\npm"
```

**5. MCP Server Not Starting**
```bash
# Check if port is in use
netstat -an | grep 3000

# Kill process if needed
kill -9 $(lsof -ti:3000)
```

**6. Environment Variable Issues**
```bash
# Verify environment variable is set
env | grep FIRECRAWL_API_KEY

# Set for current session
export FIRECRAWL_API_KEY=fc-YOUR_API_KEY
```

### Getting Help

- **Documentation:** [Firecrawl Docs](https://docs.firecrawl.dev/)
- **API Keys:** [Get API Key](https://www.firecrawl.dev/app/api-keys)
- **Support:** [GitHub Issues](https://github.com/firecrawl/firecrawl-mcp-server/issues)
- **Community:** [Discord](https://discord.gg/firecrawl)

---

## 📘 Additional Resources

- **Firecrawl API Documentation:** [docs.firecrawl.dev](https://docs.firecrawl.dev/)
- **MCP Protocol Specification:** [modelcontextprotocol.io](https://modelcontextprotocol.io/)
- **Firecrawl Playground:** [mcp.so/playground](https://mcp.so/playground?server=firecrawl-mcp-server)
- **Klavis AI Integration:** [klavis.ai/mcp-servers](https://www.klavis.ai/mcp-servers)

---

*This installation guide covers all major MCP-compatible environments. For environment-specific issues, please refer to the respective IDE documentation or contact support.*