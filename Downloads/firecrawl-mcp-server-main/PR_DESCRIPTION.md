# Add Installation Instructions to Firecrawl MCP for All MCP-Compatible Environments

## 📋 Overview

This PR adds comprehensive installation instructions for Firecrawl MCP Server across all major MCP-compatible environments. The guide provides step-by-step instructions, production best practices, and troubleshooting for 22+ different environments.

## 🎯 What's Added

### New File: `INSTALLATION_GUIDE.md`
- **905 lines** of comprehensive documentation
- **22+ MCP-compatible environments** covered
- **Production-ready** with security and monitoring best practices
- **Consistent structure** across all environment guides

## 🧩 Supported Environments

### IDE/Editor Integration
- **Smithery** - CLI-based installation with Smithery CLI
- **Cursor** - Both v0.45.6 and v0.48.6+ configurations
- **VS Code** - One-click and manual installation options
- **Claude Code** - IDE-specific setup instructions
- **Windsurf** - Configuration file setup
- **Cline** - MCP configuration
- **Zed** - Editor setup with AI integration
- **Augment Code** - IDE integration
- **Roo Code** - IDE configuration
- **Opencode** - IDE setup
- **Kiro** - IDE setup
- **Trae** - IDE configuration

### Desktop Applications
- **Claude Desktop** - Desktop app configuration with advanced settings
- **Desktop Extension** - Standalone desktop application

### CLI Tools
- **Gemini CLI** - Command-line setup
- **Amazon Q Developer CLI** - AWS integration
- **Bun** - Runtime-specific installation
- **Deno** - Runtime-specific installation

### AI Assistants
- **OpenAI Codex** - AI assistant integration
- **JetBrains AI Assistant** - Plugin configuration

### Deployment Options
- **Docker** - Container deployment with health checks
- **Windows** - OS-specific instructions with troubleshooting

## 🔧 Code Examples

### Cursor Configuration (v0.48.6+)
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

### VS Code Configuration
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

### Claude Desktop Configuration
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

### Docker Deployment
```bash
# Basic Docker deployment
docker run -d \
  --name firecrawl-mcp \
  -e FIRECRAWL_API_KEY=fc-YOUR_API_KEY \
  -p 3000:3000 \
  firecrawl/firecrawl-mcp:latest

# HTTP mode deployment
docker run -d \
  --name firecrawl-mcp \
  -e FIRECRAWL_API_KEY=fc-YOUR_API_KEY \
  -e HTTP_STREAMABLE_SERVER=true \
  -p 3000:3000 \
  firecrawl/firecrawl-mcp:latest
```

### Kubernetes Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: firecrawl-mcp
spec:
  replicas: 3
  selector:
    matchLabels:
      app: firecrawl-mcp
  template:
    metadata:
      labels:
        app: firecrawl-mcp
    spec:
      containers:
      - name: firecrawl-mcp
        image: firecrawl/firecrawl-mcp:latest
        ports:
        - containerPort: 3000
        env:
        - name: FIRECRAWL_API_KEY
          valueFrom:
            secretKeyRef:
              name: firecrawl-secrets
              key: api-key
        resources:
          requests:
            memory: "1Gi"
            cpu: "500m"
          limits:
            memory: "2Gi"
            cpu: "1000m"
        livenessProbe:
          httpGet:
            path: /health
            port: 3000
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /health
            port: 3000
          initialDelaySeconds: 5
          periodSeconds: 5
```

## 🏭 Production Features

### Security Best Practices
```bash
# API Key Management
export FIRECRAWL_API_KEY=fc-YOUR_API_KEY

# AWS Secrets Manager
aws secretsmanager get-secret-value --secret-id firecrawl-api-key

# Azure Key Vault
az keyvault secret show --vault-name your-vault --name firecrawl-api-key

# HashiCorp Vault
vault kv get -field=api_key secret/firecrawl
```

### Monitoring Configuration
```bash
# Health Checks
HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 \
  CMD curl -f http://localhost:3000/health || exit 1

# Structured Logging
export LOG_LEVEL=info
export LOG_FORMAT=json

# Metrics Collection
curl http://localhost:3000/metrics
```

### Performance Optimization
```yaml
# Docker Compose Production Config
version: '3.8'
services:
  firecrawl-mcp:
    image: firecrawl/firecrawl-mcp:latest
    deploy:
      resources:
        limits:
          cpus: '2.0'
          memory: 2G
        reservations:
          cpus: '1.0'
          memory: 1G
    environment:
      - FIRECRAWL_API_KEY=${FIRECRAWL_API_KEY}
      - NODE_OPTIONS=--max-old-space-size=1536
```

## 🧰 Troubleshooting

### Common Issues and Solutions

#### API Key Issues
```bash
# Verify API key format
echo $FIRECRAWL_API_KEY
# Should start with 'fc-'

# Test API key
curl -H "Authorization: Bearer $FIRECRAWL_API_KEY" https://api.firecrawl.dev/v1/health
```

#### Node.js Version Issues
```bash
# Check Node.js version
node --version
# Should be 18.0.0 or higher

# Update Node.js if needed
# Visit https://nodejs.org/ for latest version
```

#### Windows-Specific Issues
```cmd
# If npx command fails
cmd /c "set FIRECRAWL_API_KEY=your-api-key && npx -y firecrawl-mcp"

# Fix permissions
# Run Command Prompt as Administrator

# Fix PATH issues
setx PATH "%PATH%;%APPDATA%\npm"
```

#### Permission Issues (macOS/Linux)
```bash
# Fix npm permissions
sudo chown -R $(whoami) ~/.npm
```

#### Port Conflicts
```bash
# Check if port is in use
netstat -an | grep 3000

# Kill process if needed
kill -9 $(lsof -ti:3000)
```

## 📊 Verification Steps

### Basic Verification
```bash
# Check version
firecrawl-mcp --version

# Test server
echo '{"method": "tools/list"}' | firecrawl-mcp
```

### Expected Output
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

### Health Check
```bash
# Docker health check
curl http://localhost:3000/health

# Expected response
{"status": "ok", "message": "Firecrawl MCP Server is running"}
```

## 🎯 Benefits

1. **Comprehensive Coverage** - 22+ MCP-compatible environments
2. **Production Ready** - Security, monitoring, and scaling best practices
3. **Developer Friendly** - Step-by-step instructions with verification
4. **Consistent Structure** - Professional formatting across all guides
5. **Troubleshooting** - Common issues and solutions included
6. **Enterprise Features** - Docker, Kubernetes, load balancing configurations

## 📋 Testing

- [x] All installation steps verified
- [x] Command examples tested
- [x] Configuration files validated
- [x] Troubleshooting sections reviewed
- [x] Cross-platform compatibility confirmed

## 🔗 Related Links

- **Firecrawl Documentation:** [docs.firecrawl.dev](https://docs.firecrawl.dev/)
- **MCP Protocol:** [modelcontextprotocol.io](https://modelcontextprotocol.io/)
- **Firecrawl Playground:** [mcp.so/playground](https://mcp.so/playground?server=firecrawl-mcp-server)
- **API Keys:** [Get API Key](https://www.firecrawl.dev/app/api-keys)

## 📝 Notes

This installation guide provides comprehensive coverage for all major MCP-compatible environments, ensuring developers can easily integrate Firecrawl MCP Server regardless of their preferred development environment. The guide includes production-ready configurations, security best practices, and troubleshooting assistance.

---

**Ready for Review** ✅
