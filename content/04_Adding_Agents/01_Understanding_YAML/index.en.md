---
title: "Understanding YAML Configuration"
weight: 1
---

The Solace Agent Mesh framework is controlled by YAML configuration files that define agents, gateways, and plugins, allowing for configuration-driven development without code changes.

Agent configuration files in Solace Agent Mesh are stored in the `configs/agents/` directory. Each agent has its own YAML file that defines its behavior, capabilities, and integration settings.

### Key Components of Agent YAML Files

A typical agent configuration YAML file includes these key sections:

1. **Basic Agent Information**
   - Name and description of the agent
   - Version information
   - Type of agent (e.g., assistant, orchestrator)

2. **Model Configuration (Note: Could be shared)**
   - LLM provider and model selection
   - Temperature and other model parameters
   - System prompt/instructions for the agent

3. **Security and Authorization**
   - Authentication methods (API key, OAuth2, etc.)
   - Role-based access control settings
   - Permission definitions

4. **Tools and Capabilities**
   - Available tools and functions
   - Tool parameters and configurations
   - Built-in tool groups

5. **Integration Settings**
   - Connections to external services (Jira, databases, etc.)
   - API endpoints and credentials
   - Connection parameters

6. **Event Handling**
   - Event triggers and handlers
   - Timeout settings
   - Recovery mechanisms

7. **Agent Card Definition**
   - Description of capabilities for other agents to discover
   - Input/output modes
   - Skills listing

### Example Agent Configuration

Here's an example of a basic agent configuration YAML file:

```yaml
log:
  stdout_log_level: INFO
  log_file_level: DEBUG # Changed from INFO to DEBUG to capture ADK INFO logs
  log_file: name-agent.log

# Shared config
!include ../shared_config.yaml

apps:
  - name: name-agent_app
    app_base_path: .
    app_module: solace_agent_mesh.agent.sac.app
    broker:
      <<: *broker_connection # References a broker connection defined in shared_config.yaml
  
  app_config:
    # Basic agent identity
    namespace: ${namespace}
    supports_streaming: true
    agent_name: "example-agent"
    display_name: "Example Agent"
    
    # LLM model configuration
    model: *general_model  # References a model defined in shared_config.yaml
    
    # Agent instructions (system prompt)
    instruction: |
      You are a helpful assistant specialized in answering questions about Solace Agent Mesh.
      Always provide accurate and concise information.
    
    # Tools configuration
    tools:
      - tool_type: python
        component_module: "example_agent.tools"
        component_base_path: .
        function_name: "search_documentation"
        tool_name: "search_docs"
        tool_config:
          search_depth: 3
      
      # Built-in artifact tools for file operations
      - tool_type: builtin-group
        group_name: "artifact_management"
    
    # Agent card definition (A2A specification)
    agent_card:
      description: "A helpful assistant for Solace Agent Mesh documentation"
      defaultInputModes: ["text"]
      defaultOutputModes: ["text"]
      skills:
        - id: "search_docs"
          name: "Search Documentation"
          description: "Searches through Solace Agent Mesh documentation"
```
