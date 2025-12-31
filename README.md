# 🚀 Awesome Model Context Protocol (MCP)

> **The Ultimate MCP Resource Hub** - Your comprehensive guide to Model Context Protocol servers, AI integration, and learning resources

**Curated with ❤️ by [itskiranbabu](https://github.com/itskiranbabu)** | *Powered by KeyRun AI*

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![GitHub stars](https://img.shields.io/github/stars/itskiranbabu/awesome-mcp-servers?style=social)](https://github.com/itskiranbabu/awesome-mcp-servers/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/itskiranbabu/awesome-mcp-servers?style=social)](https://github.com/itskiranbabu/awesome-mcp-servers/network/members)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 📖 Table of Contents

- [What is MCP?](#-what-is-mcp)
- [Why MCP Matters](#-why-mcp-matters)
- [Getting Started](#-getting-started)
- [Official MCP Servers](#-official-mcp-servers)
- [Community MCP Servers](#-community-mcp-servers)
- [MCP Clients](#-mcp-clients)
- [Development Tools](#-development-tools)
- [AI Learning Resources](#-ai-learning-resources)
- [Tutorials & Guides](#-tutorials--guides)
- [Best Practices](#-best-practices)
- [Use Cases](#-use-cases)
- [Contributing](#-contributing)

---

## 🎯 What is MCP?

**Model Context Protocol (MCP)** is an open-source standard released by Anthropic in November 2024 that standardizes how AI applications connect to external data sources and tools.

### Key Features

- **🔌 Universal Integration**: One protocol for all AI-tool connections
- **🏗️ Client-Server Architecture**: Clean separation of concerns
- **📡 Multiple Transports**: STDIO for local, HTTP+SSE for remote
- **🔒 Secure by Design**: Permission-based access control
- **🚀 Production Ready**: Used by Claude, Cursor, and major AI platforms

### Architecture

```
┌─────────────────┐
│   AI Host App   │  (Claude Desktop, Cursor, etc.)
│  ┌───────────┐  │
│  │MCP Client │  │
│  └─────┬─────┘  │
└────────┼────────┘
         │ JSON-RPC 2.0
         │
    ┌────┴────┐
    │Transport│  (STDIO / HTTP+SSE)
    └────┬────┘
         │
┌────────┼────────┐
│  ┌─────┴─────┐  │
│  │MCP Server │  │  (GitHub, Database, Files, etc.)
│  └───────────┘  │
│   Data Source   │
└─────────────────┘
```

---

## 💡 Why MCP Matters

### Before MCP
- ❌ Custom integration for each AI-tool pair
- ❌ Fragmented ecosystem
- ❌ Difficult maintenance
- ❌ Limited interoperability

### With MCP
- ✅ **55%+ productivity gains** in AI workflows
- ✅ **One integration** works with all MCP clients
- ✅ **Standardized protocol** for consistency
- ✅ **Growing ecosystem** of 13,000+ servers
- ✅ **Enterprise ready** with security controls

---

## 🚀 Getting Started

### Quick Start with Claude Desktop

1. **Install Claude Desktop**
   ```bash
   # Download from https://claude.ai/download
   ```

2. **Configure MCP Server**
   ```json
   // ~/.claude/mcp_servers.json (macOS/Linux)
   // %APPDATA%\Claude\mcp_servers.json (Windows)
   {
     "mcpServers": {
       "filesystem": {
         "command": "npx",
         "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/allowed/files"]
       }
     }
   }
   ```

3. **Restart Claude Desktop**

4. **Test Integration**
   ```
   Ask Claude: "List files in my project directory"
   ```

### Building Your First MCP Server

**Python Example:**
```python
from mcp.server import Server
from mcp.types import Tool

server = Server("my-first-server")

@server.list_tools()
async def list_tools() -> list[Tool]:
    return [
        Tool(
            name="get_weather",
            description="Get current weather for a location",
            inputSchema={
                "type": "object",
                "properties": {
                    "location": {"type": "string"}
                }
            }
        )
    ]

@server.call_tool()
async def call_tool(name: str, arguments: dict):
    if name == "get_weather":
        location = arguments["location"]
        # Your weather API logic here
        return {"temperature": "72°F", "condition": "Sunny"}

if __name__ == "__main__":
    server.run()
```

**TypeScript Example:**
```typescript
import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const server = new Server({
  name: "my-first-server",
  version: "1.0.0"
});

server.setRequestHandler("tools/list", async () => ({
  tools: [{
    name: "get_weather",
    description: "Get current weather",
    inputSchema: {
      type: "object",
      properties: {
        location: { type: "string" }
      }
    }
  }]
}));

const transport = new StdioServerTransport();
await server.connect(transport);
```

---

## 🌟 Official MCP Servers

### Development Tools

| Server | Description | Language | Stars |
|--------|-------------|----------|-------|
| [**@modelcontextprotocol/server-filesystem**](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem) | Secure file system access | TypeScript | ⭐⭐⭐⭐⭐ |
| [**@modelcontextprotocol/server-github**](https://github.com/modelcontextprotocol/servers/tree/main/src/github) | GitHub repository operations | TypeScript | ⭐⭐⭐⭐⭐ |
| [**@modelcontextprotocol/server-git**](https://github.com/modelcontextprotocol/servers/tree/main/src/git) | Git operations and history | TypeScript | ⭐⭐⭐⭐ |
| [**@modelcontextprotocol/server-gitlab**](https://github.com/modelcontextprotocol/servers/tree/main/src/gitlab) | GitLab integration | TypeScript | ⭐⭐⭐⭐ |

### Data & Databases

| Server | Description | Language | Stars |
|--------|-------------|----------|-------|
| [**@modelcontextprotocol/server-postgres**](https://github.com/modelcontextprotocol/servers/tree/main/src/postgres) | PostgreSQL database access | TypeScript | ⭐⭐⭐⭐⭐ |
| [**@modelcontextprotocol/server-sqlite**](https://github.com/modelcontextprotocol/servers/tree/main/src/sqlite) | SQLite database operations | TypeScript | ⭐⭐⭐⭐ |
| [**@modelcontextprotocol/server-memory**](https://github.com/modelcontextprotocol/servers/tree/main/src/memory) | Knowledge graph memory | TypeScript | ⭐⭐⭐⭐⭐ |

### Cloud & Services

| Server | Description | Language | Stars |
|--------|-------------|----------|-------|
| [**@modelcontextprotocol/server-google-drive**](https://github.com/modelcontextprotocol/servers/tree/main/src/gdrive) | Google Drive integration | TypeScript | ⭐⭐⭐⭐⭐ |
| [**@modelcontextprotocol/server-slack**](https://github.com/modelcontextprotocol/servers/tree/main/src/slack) | Slack messaging | TypeScript | ⭐⭐⭐⭐ |
| [**@modelcontextprotocol/server-google-maps**](https://github.com/modelcontextprotocol/servers/tree/main/src/google-maps) | Google Maps API | TypeScript | ⭐⭐⭐⭐ |

### Utilities

| Server | Description | Language | Stars |
|--------|-------------|----------|-------|
| [**@modelcontextprotocol/server-fetch**](https://github.com/modelcontextprotocol/servers/tree/main/src/fetch) | Web content fetching | TypeScript | ⭐⭐⭐⭐ |
| [**@modelcontextprotocol/server-brave-search**](https://github.com/modelcontextprotocol/servers/tree/main/src/brave-search) | Brave Search API | TypeScript | ⭐⭐⭐⭐ |
| [**@modelcontextprotocol/server-puppeteer**](https://github.com/modelcontextprotocol/servers/tree/main/src/puppeteer) | Browser automation | TypeScript | ⭐⭐⭐⭐⭐ |

---

## 🎨 Community MCP Servers

### 🔥 Top Community Picks

#### Development & DevOps

- [**mcp-server-docker**](https://github.com/ckreiling/mcp-server-docker) - Docker container management
- [**mcp-server-kubernetes**](https://github.com/strowk/mcp-k8s-go) - Kubernetes cluster operations
- [**mcp-server-terraform**](https://github.com/terraform-mcp/server) - Infrastructure as code
- [**mcp-server-aws**](https://github.com/aws/mcp-server-aws) - AWS services integration
- [**mcp-server-vercel**](https://github.com/vercel/mcp-server) - Vercel deployment

#### AI & Machine Learning

- [**mcp-server-openai**](https://github.com/openai/mcp-server) - OpenAI API integration
- [**mcp-server-anthropic**](https://github.com/anthropics/mcp-server-anthropic) - Claude API
- [**mcp-server-huggingface**](https://github.com/huggingface/mcp-server) - HuggingFace models
- [**mcp-server-replicate**](https://github.com/replicate/mcp-server) - Replicate AI models
- [**mcp-server-langchain**](https://github.com/langchain-ai/mcp-server) - LangChain integration

#### Databases & Storage

- [**mcp-server-mongodb**](https://github.com/mongodb/mcp-server) - MongoDB operations
- [**mcp-server-redis**](https://github.com/redis/mcp-server) - Redis cache
- [**mcp-server-supabase**](https://github.com/supabase/mcp-server) - Supabase backend
- [**mcp-server-firebase**](https://github.com/firebase/mcp-server) - Firebase services
- [**mcp-server-pinecone**](https://github.com/pinecone-io/mcp-server) - Vector database

#### Communication & Collaboration

- [**mcp-server-discord**](https://github.com/discord/mcp-server) - Discord bot integration
- [**mcp-server-telegram**](https://github.com/telegram/mcp-server) - Telegram bots
- [**mcp-server-notion**](https://github.com/makenotion/mcp-server) - Notion workspace
- [**mcp-server-linear**](https://github.com/linear/mcp-server) - Linear issue tracking
- [**mcp-server-jira**](https://github.com/atlassian/mcp-server-jira) - Jira project management

#### Web Scraping & Data

- [**mcp-server-firecrawl**](https://github.com/firecrawl/mcp-server) - Web scraping
- [**mcp-server-browserbase**](https://github.com/browserbase/mcp-server) - Browser automation
- [**mcp-server-playwright**](https://github.com/microsoft/mcp-server-playwright) - E2E testing
- [**mcp-server-cheerio**](https://github.com/cheeriojs/mcp-server) - HTML parsing
- [**mcp-server-axios**](https://github.com/axios/mcp-server) - HTTP requests

#### Finance & Business

- [**mcp-server-stripe**](https://github.com/stripe/mcp-server) - Payment processing
- [**mcp-server-plaid**](https://github.com/plaid/mcp-server) - Banking data
- [**mcp-server-quickbooks**](https://github.com/intuit/mcp-server-quickbooks) - Accounting
- [**mcp-server-salesforce**](https://github.com/salesforce/mcp-server) - CRM integration
- [**mcp-server-hubspot**](https://github.com/hubspot/mcp-server) - Marketing automation

---

## 💻 MCP Clients

### Production-Ready Clients

| Client | Platform | Features | Status |
|--------|----------|----------|--------|
| [**Claude Desktop**](https://claude.ai/download) | Desktop | Built-in MCP support | ✅ Stable |
| [**Cursor**](https://cursor.sh/) | IDE | Code-first AI editor | ✅ Stable |
| [**Zed**](https://zed.dev/) | IDE | Collaborative coding | ✅ Beta |
| [**Continue**](https://continue.dev/) | VS Code | Open-source copilot | ✅ Stable |
| [**Cline**](https://github.com/cline/cline) | VS Code | Autonomous coding | ✅ Beta |

### Custom Client Libraries

- **Python**: [`mcp`](https://github.com/modelcontextprotocol/python-sdk) - Official Python SDK
- **TypeScript**: [`@modelcontextprotocol/sdk`](https://github.com/modelcontextprotocol/typescript-sdk) - Official TS SDK
- **Java**: [`mcp-java-sdk`](https://github.com/modelcontextprotocol/java-sdk) - Official Java SDK
- **Kotlin**: [`mcp-kotlin`](https://github.com/modelcontextprotocol/kotlin-sdk) - Official Kotlin SDK
- **C#**: [`mcp-csharp`](https://github.com/modelcontextprotocol/csharp-sdk) - Official C# SDK

---

## 🛠️ Development Tools

### MCP Inspector

Debug and test MCP servers interactively:

```bash
npx @modelcontextprotocol/inspector npx @modelcontextprotocol/server-filesystem /path/to/files
```

### MCP CLI

Command-line tools for MCP development:

```bash
# Install
npm install -g @modelcontextprotocol/cli

# Create new server
mcp create my-server --language typescript

# Test server
mcp test ./my-server

# Publish server
mcp publish
```

### Testing Frameworks

- [**mcp-test-utils**](https://github.com/modelcontextprotocol/test-utils) - Testing utilities
- [**mcp-mock-server**](https://github.com/modelcontextprotocol/mock-server) - Mock server for testing

---

## 🎓 AI Learning Resources

### 🌟 Comprehensive Courses

#### Beginner-Friendly

| Platform | Course | Duration | Cost |
|----------|--------|----------|------|
| [**DeepLearning.AI**](https://www.deeplearning.ai/) | AI Fundamentals | Varies | Free/Paid |
| [**Coursera**](https://www.coursera.org/courses?query=artificial%20intelligence) | AI Specializations | 1-6 months | Free trial |
| [**Fast.ai**](https://course.fast.ai/) | Practical Deep Learning | Self-paced | Free |
| [**Google ML Crash Course**](https://developers.google.com/machine-learning/crash-course) | ML Fundamentals | 15 hours | Free |

#### Advanced Learning

- **[Machine Learning Specialization](https://www.coursera.org/specializations/machine-learning-introduction)** - Andrew Ng's comprehensive ML course
- **[Deep Learning Specialization](https://www.deeplearning.ai/courses/deep-learning-specialization/)** - Neural networks and deep learning
- **[PyTorch for Deep Learning](https://www.deeplearning.ai/courses/pytorch-for-deep-learning-professional-certificate/)** - Professional certificate program
- **[Anthropic MCP Course](https://anthropic.skilljar.com/model-context-protocol-advanced-topics)** - Advanced MCP topics

### 📖 Essential Reading

#### Books

- **"Deep Learning"** by Ian Goodfellow - The definitive textbook
- **"Hands-On Machine Learning"** by Aurélien Géron - Practical guide
- **"Pattern Recognition and Machine Learning"** by Christopher Bishop
- **"The Hundred-Page Machine Learning Book"** by Andriy Burkov

#### Research Papers

- [**Model Context Protocol Specification**](https://modelcontextprotocol.io/specification/latest) - Official spec
- [**Attention Is All You Need**](https://arxiv.org/abs/1706.03762) - Transformer architecture
- [**BERT: Pre-training of Deep Bidirectional Transformers**](https://arxiv.org/abs/1810.04805)
- [**GPT-3: Language Models are Few-Shot Learners**](https://arxiv.org/abs/2005.14165)

### 🎯 Hands-On Resources

#### Interactive Tutorials

- [**MCP Quickstart**](https://modelcontextprotocol.io/docs/getting-started/intro) - Official getting started
- [**Build an MCP Server**](https://modelcontextprotocol.io/docs/develop/build-server) - Step-by-step guide
- [**Build an MCP Client**](https://modelcontextprotocol.io/docs/develop/build-client) - Client development
- [**Kaggle Learn**](https://www.kaggle.com/learn) - Practical ML tutorials

#### Video Courses

- [**DeepLearning.AI YouTube**](https://www.youtube.com/@Deeplearningai) - Free video courses
- [**3Blue1Brown**](https://www.youtube.com/@3blue1brown) - Visual math explanations
- [**Sentdex**](https://www.youtube.com/@sentdex) - Python ML tutorials
- [**Two Minute Papers**](https://www.youtube.com/@TwoMinutePapers) - AI research summaries

### 🏆 Certifications

- **[AWS Certified AI Practitioner](https://aws.amazon.com/certification/certified-ai-practitioner/)** - AWS AI certification
- **[Azure AI Fundamentals](https://learn.microsoft.com/en-us/certifications/azure-ai-fundamentals/)** - Microsoft certification
- **[TensorFlow Developer Certificate](https://www.tensorflow.org/certificate)** - Google certification
- **[IBM AI Engineering Professional Certificate](https://www.coursera.org/professional-certificates/ai-engineer)** - IBM certification

---

## 📚 Tutorials & Guides

### Getting Started

1. **[MCP Introduction](https://modelcontextprotocol.io/docs/getting-started/intro)** - What is MCP?
2. **[Architecture Overview](https://modelcontextprotocol.io/docs/learn/architecture)** - How MCP works
3. **[Connect Local Servers](https://modelcontextprotocol.io/docs/develop/connect-local-servers)** - Setup guide
4. **[Connect Remote Servers](https://modelcontextprotocol.io/docs/develop/connect-remote-servers)** - Remote setup

### Building Servers

- **[Python Server Tutorial](https://modelcontextprotocol.io/docs/develop/build-server)** - Build with Python
- **[TypeScript Server Tutorial](https://modelcontextprotocol.io/docs/develop/build-server)** - Build with TS
- **[Server Best Practices](https://modelcontextprotocol.io/docs/best-practices)** - Production tips
- **[Security Guidelines](https://modelcontextprotocol.io/specification/2025-11-25/basic/security_best_practices)** - Secure your server

### Integration Guides

- **[Claude Desktop Integration](https://docs.anthropic.com/claude/docs/mcp)** - Setup with Claude
- **[Cursor Integration](https://docs.cursor.com/mcp)** - Setup with Cursor
- **[VS Code Integration](https://github.com/modelcontextprotocol/vscode-extension)** - VS Code extension
- **[Custom Client Development](https://modelcontextprotocol.io/docs/develop/build-client)** - Build your own

---

## 💎 Best Practices

### Server Development

#### ✅ Do's

- **Use TypeScript/Python SDKs** for type safety
- **Implement proper error handling** with descriptive messages
- **Add comprehensive logging** for debugging
- **Follow security best practices** (input validation, rate limiting)
- **Document your tools clearly** with examples
- **Test thoroughly** before publishing
- **Version your server** semantically

#### ❌ Don'ts

- Don't expose sensitive data without permission
- Don't skip input validation
- Don't ignore error cases
- Don't hardcode credentials
- Don't skip documentation
- Don't forget rate limiting

### Security Checklist

- [ ] Input validation on all parameters
- [ ] Permission checks before operations
- [ ] Rate limiting implemented
- [ ] Secrets stored securely (env vars)
- [ ] HTTPS for remote servers
- [ ] Audit logging enabled
- [ ] Error messages don't leak sensitive info
- [ ] Dependencies regularly updated

### Performance Tips

- **Cache frequently accessed data**
- **Use connection pooling** for databases
- **Implement pagination** for large datasets
- **Add request timeouts**
- **Monitor resource usage**
- **Optimize database queries**
- **Use async/await** properly

---

## 🎯 Use Cases

### Development Workflows

**Code Review Assistant**
```
User: "Review the last 5 commits in my repo"
MCP: Uses GitHub server → Fetches commits → Analyzes code
Claude: Provides detailed review with suggestions
```

**Database Query Helper**
```
User: "Show me users who signed up last week"
MCP: Uses PostgreSQL server → Executes query
Claude: Formats results in readable table
```

### Business Automation

**Customer Support**
```
User: "Summarize today's support tickets"
MCP: Uses Linear/Jira server → Fetches tickets
Claude: Creates summary with priorities
```

**Financial Analysis**
```
User: "Analyze Q4 revenue trends"
MCP: Uses Stripe/QuickBooks server → Gets data
Claude: Generates insights and visualizations
```

### Content Creation

**Blog Post Generator**
```
User: "Write a blog post about MCP"
MCP: Uses Brave Search → Research topic
Claude: Writes comprehensive article
```

**Social Media Manager**
```
User: "Post update about new feature"
MCP: Uses Twitter/LinkedIn servers → Posts content
Claude: Confirms posting and engagement
```

---

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

### How to Contribute

1. **Fork** this repository
2. **Create** a feature branch (`git checkout -b feature/amazing-server`)
3. **Commit** your changes (`git commit -m 'Add amazing MCP server'`)
4. **Push** to the branch (`git push origin feature/amazing-server`)
5. **Open** a Pull Request

### Contribution Guidelines

- Ensure servers are actively maintained
- Provide clear descriptions
- Include installation instructions
- Test servers before submitting
- Follow the existing format
- Check for duplicates

---

## 📊 Statistics

- **13,000+** MCP servers available
- **100+** official integrations
- **55%+** productivity improvement
- **Growing** ecosystem daily

---

## 🌐 Community

### Official Resources

- **[MCP Documentation](https://modelcontextprotocol.io/)** - Official docs
- **[MCP Specification](https://modelcontextprotocol.io/specification/latest)** - Technical spec
- **[MCP GitHub](https://github.com/modelcontextprotocol)** - Source code
- **[Anthropic Blog](https://www.anthropic.com/news/model-context-protocol)** - Announcements

### Community Platforms

- **[MCP Servers Directory](https://mcpservers.org/)** - Browse servers
- **[Glama MCP Registry](https://glama.ai/mcp/servers)** - Server registry
- **[Reddit r/mcp](https://reddit.com/r/mcp)** - Community discussions
- **[Discord](https://discord.gg/mcp)** - Real-time chat

### Learning Communities

- **[DeepLearning.AI Community](https://community.deeplearning.ai/)** - 7M+ learners
- **[Kaggle Community](https://www.kaggle.com/discussions)** - Data science competitions
- **[Fast.ai Forums](https://forums.fast.ai/)** - Deep learning discussions
- **[Hugging Face Forums](https://discuss.huggingface.co/)** - NLP community

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🌟 Star History

[![Star History Chart](https://api.star-history.com/svg?repos=itskiranbabu/awesome-mcp-servers&type=Date)](https://star-history.com/#itskiranbabu/awesome-mcp-servers&Date)

---

## 💖 Acknowledgments

**Curated by [itskiranbabu](https://github.com/itskiranbabu)** | **Powered by KeyRun AI**

Special thanks to:
- [Anthropic](https://www.anthropic.com/) for creating MCP
- [wong2](https://github.com/wong2/awesome-mcp-servers) for the original awesome list
- All contributors to the MCP ecosystem
- The AI/ML community for amazing learning resources

---

## 📬 Connect

- **GitHub**: [@itskiranbabu](https://github.com/itskiranbabu)
- **Email**: itskeyrun.ai@gmail.com
- **Website**: [itskiranbabu.github.io](https://itskiranbabu.github.io)

---

<div align="center">

**Made with ❤️ by itskiranbabu**

*Empowering developers to build the future with AI and MCP*

[⬆ Back to Top](#-awesome-model-context-protocol-mcp)

</div>