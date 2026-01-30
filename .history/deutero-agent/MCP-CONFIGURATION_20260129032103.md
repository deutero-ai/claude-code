# Deutero MCP Server Configuration Examples

This file shows different ways to configure the Deutero MCP server in Claude Code.

## Option 1: HTTP Server Configuration (Recommended)

If you're running the Deutero MCP server as an HTTP service:

```json
{
  "mcpServers": {
    "deutero": {
      "url": "http://127.0.0.1:8000/mcp",
      "transport": "http",
      "headers": {
        "X-API-Key": "${DEUTERO_API_KEY}"
      }
    }
  }
}
```

Set your API key as an environment variable:
```bash
export DEUTERO_API_KEY="your-api-key-here"
```

## Option 2: Python Command Configuration

If you want Claude Code to start the server automatically:

```json
{
  "mcpServers": {
    "deutero": {
      "command": "python",
      "args": ["/path/to/deutero_mcp_server.py"],
      "env": {
        "BASE_URL": "http://127.0.0.1:8000",
        "DEUTERO_API_KEY": "your-api-key-here"
      }
    }
  }
}
```

## Option 3: Docker Configuration

If running Deutero in a Docker container:

```json
{
  "mcpServers": {
    "deutero": {
      "url": "http://deutero-mcp:8000/mcp",
      "transport": "http",
      "headers": {
        "X-API-Key": "${DEUTERO_API_KEY}"
      }
    }
  }
}
```

Docker compose example:
```yaml
version: '3.8'
services:
  deutero-mcp:
    image: deutero/mcp-server:latest
    ports:
      - "8000:8000"
    environment:
      - DEUTERO_API_KEY=${DEUTERO_API_KEY}
```

## Configuration File Locations

Place your MCP configuration in one of these locations:

### Linux/macOS
```
~/.claude/settings.json
```

### Windows
```
%USERPROFILE%\.claude\settings.json
```

### Project-Specific
```
.claude/settings.json
```

## Complete Settings Example

Here's a complete `settings.json` with Deutero and other useful settings:

```json
{
  "mcpServers": {
    "deutero": {
      "url": "http://127.0.0.1:8000/mcp",
      "transport": "http",
      "headers": {
        "X-API-Key": "${DEUTERO_API_KEY}"
      }
    }
  },
  "tools": {
    "MCP": true,
    "Bash": true,
    "Read": true,
    "Write": true,
    "Edit": true
  },
  "permissions": {
    "allow": [],
    "deny": []
  },
  "preferences": {
    "autoCompactPercent": 95
  }
}
```

## Verifying Configuration

After configuring, verify the MCP server is accessible:

1. **Start Claude Code**
   ```bash
   claude
   ```

2. **List available tools**
   ```
   /tools
   ```
   
   You should see Deutero MCP tools listed:
   - create_study
   - create_study_questions
   - create_simulation_persona
   - simulate_interviews
   - run_thematic_analysis
   - get_analysis_status
   - get_agent_requirements
   - get_survey_participation

3. **Test connection**
   ```
   "Test the Deutero connection by listing available tools"
   ```

## Troubleshooting

### Server Not Connecting

If you see "MCP server not available" errors:

1. **Check server is running**
   ```bash
   curl http://127.0.0.1:8000/health
   ```

2. **Verify API key**
   ```bash
   echo $DEUTERO_API_KEY
   ```

3. **Check Claude Code logs**
   ```bash
   tail -f ~/.claude/logs/mcp-*.log
   ```

4. **Test MCP endpoint directly**
   ```bash
   curl -H "X-API-Key: $DEUTERO_API_KEY" http://127.0.0.1:8000/mcp/list-tools
   ```

### Authentication Errors

If you see "401 Unauthorized" errors:

1. **Verify API key is set correctly**
   - Check environment variable
   - Confirm it matches your Deutero account

2. **Check header format**
   - Must be `X-API-Key` (case-sensitive)
   - Value should not have quotes if using environment variable

3. **Try hardcoded key temporarily**
   ```json
   {
     "headers": {
       "X-API-Key": "your-actual-key-here"
     }
   }
   ```

### Tools Not Appearing

If MCP tools don't show in `/tools`:

1. **Verify MCP is enabled**
   - Check `settings.json` has `"MCP": true` in tools section

2. **Restart Claude Code**
   ```bash
   # Exit current session, then
   claude
   ```

3. **Check server logs**
   - Look for tool registration messages
   - Verify no errors during startup

### Permission Issues

If you get "Tool not allowed" errors:

1. **Check permissions in settings**
   ```json
   {
     "permissions": {
       "deny": []  // Make sure MCP tools aren't denied
     }
   }
   ```

2. **Verify subagent permissions**
   - User-researcher has `"tools": Read, Write, Edit, Bash, MCP`
   - Make sure MCP is included

## Environment Variables

Common environment variables for Deutero:

```bash
# API Authentication
export DEUTERO_API_KEY="your-api-key"

# Server Configuration
export BASE_URL="http://127.0.0.1:8000"
export PORT="8080"

# Optional: Logging
export LOG_LEVEL="INFO"
export MCP_DEBUG="true"
```

Save these in your shell profile (`~/.bashrc`, `~/.zshrc`, etc.):

```bash
# Add to ~/.bashrc or ~/.zshrc
export DEUTERO_API_KEY="your-api-key"
export BASE_URL="http://127.0.0.1:8000"
```

## Security Best Practices

1. **Never commit API keys**
   - Use environment variables
   - Add settings.json to .gitignore if it contains keys

2. **Use secure connections**
   - Use HTTPS in production: `https://api.deutero.ai`
   - Avoid HTTP for sensitive data

3. **Rotate keys regularly**
   - Generate new API keys periodically
   - Revoke old keys in Deutero dashboard

4. **Limit permissions**
   - Use least-privilege principle
   - Create separate keys for different environments

## Production Configuration

For production use:

```json
{
  "mcpServers": {
    "deutero-prod": {
      "url": "https://api.deutero.ai/mcp",
      "transport": "http",
      "headers": {
        "X-API-Key": "${DEUTERO_PROD_API_KEY}"
      },
      "timeout": 30000
    }
  }
}
```

## Testing Configuration

For development/testing:

```json
{
  "mcpServers": {
    "deutero-dev": {
      "url": "http://localhost:8000/mcp",
      "transport": "http",
      "headers": {
        "X-API-Key": "${DEUTERO_DEV_API_KEY}"
      },
      "timeout": 60000
    }
  }
}
```

## Multiple Environments

You can configure multiple Deutero environments:

```json
{
  "mcpServers": {
    "deutero-dev": {
      "url": "http://localhost:8000/mcp",
      "transport": "http",
      "headers": {
        "X-API-Key": "${DEUTERO_DEV_API_KEY}"
      }
    },
    "deutero-staging": {
      "url": "https://staging.deutero.ai/mcp",
      "transport": "http",
      "headers": {
        "X-API-Key": "${DEUTERO_STAGING_API_KEY}"
      }
    },
    "deutero-prod": {
      "url": "https://api.deutero.ai/mcp",
      "transport": "http",
      "headers": {
        "X-API-Key": "${DEUTERO_PROD_API_KEY}"
      }
    }
  }
}
```

Switch between environments:
```
"Use deutero-prod MCP server for this study"
"Connect to deutero-dev for testing"
```

## Quick Setup Checklist

- [ ] Deutero API account created
- [ ] API key generated and saved
- [ ] Environment variable set: `DEUTERO_API_KEY`
- [ ] MCP server configuration added to `~/.claude/settings.json`
- [ ] Claude Code restarted
- [ ] Tools verified with `/tools` command
- [ ] Connection tested with simple study creation
- [ ] user-researcher.md subagent installed
- [ ] Subagent verified with `/agents` command
- [ ] End-to-end test completed

## Getting Help

- **Deutero Support**: support@deutero.ai
- **Claude Code Docs**: https://code.claude.com/docs
- **MCP Specification**: https://spec.modelcontextprotocol.io

## Example First Test

After setup, try this to verify everything works:

```
You: "Use the user-researcher subagent to create a simple test study 
about mobile app onboarding"

Expected: Subagent activates, prompts for details, creates study, 
generates XML file

If this works, your configuration is correct!
```
