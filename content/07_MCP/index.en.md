---
title: "MCP Agents"
weight: 8
---

As mentioned earlier, the Solace Agent Mesh is an agent agnostic framework. Agents are YAML configuration driven and can be authored using 

In this step, we are going to add an MCP agent using the graphical user interface.

From your terminal instance, execute this command from your terminal

```
sam add agent --gui
```

Let's go ahead and add an MCP agent that executes filesystem operations such as read/write, create files, get list of files, and searching directories. Learn more about this MCP agent from the [Filesystem MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem) found in the official list of open source MCP servers

Fill in the following information with the following instructions
```
You can interact with the local filesystem using MCP tools. Use the available tools to read, write, and manage files as requested.
```

![SAM final](../static/img/addagentinit.png)

Select the service. Note you can leave everything default here
![service](../static/img/service.png)

Features is a list of A2A specific features that can extend the functionalities of your agent (in this example an MCP agent) to expose A2A features to it. Keep everything default here
![features](../static/img/features.png)


In this step, you will have to define the list of tools and skills this agent has. As mentioned in a previous step, tools could be built-in from the Solace Agent Mesh or you can specify a list of tools that are exposed from an MCP serve. 
![customtools](../static/img/customtools.png)

Go ahead and click the `Add Tool` button
![addtool](../static/img/addtool.png)

You can see here there a list of different kind of tools to add. Go ahead and click on the MCP Tool 

![MCPTool](../static/img/MCPTool.png)

Under the Connection Parameters, add the following 

```JSON
{
  "type": "stdio",
  "command": "npx",
  "args": ["-y", "@modelcontextprotocol/server-filesystem", "/tmp/samv2"]
}

```

> In this example, we are using a stdio connection as the `type` to connect to an MCP server running as a local process. There are different types of connections including SSE (server sent events) to a remote MCP server, docker for a containerized MCP server, and other types as this connection evolves

> Note: you can replace `/tmp/samv2` with any directory of your choice

Click the `Add Tool`. Notice how this new agent now has two types of custom tools
1. Artifact Management: This is a group of Solace Agent Mesh built-in tools that extends the capabilities of the custom agent
1. MCP: All the tools that are defined in the MCP server exposed as custom tools for the agent

Click `Next`

You are then prompted with the Agent Card dialog. 
![agentCard](../static/img/agentCard.png)

Add the following Agent Card Description

```
An agent that interacts with the local filesystem via MCP.
```

Leave everything else as the default. Click `Next`.

![agentReview](../static/img/agentReview.png)

🎉 Click `Save Agent & Finish` and you're done! You now have a custom MCP Agent configured.

This process created a yaml configuration file under `configs/agents/file_system_agent.yaml`. I want to point to your attention to this section of the configuration

```yaml
tools: 
   - group_name: artifact_management
      tool_type: builtin-group
   - connection_params:
      args:
      - -y
      - '@modelcontextprotocol/server-filesystem'
      - /tmp/samv2
      command: npx
      timeout: 30
      type: stdio
      tool_type: mcp
```
You can see here that this agent has two types of tools: the built-in tools and an MCP configuration. 

The full yaml configuration for the agent should look like this

```yaml
# Solace Agent Mesh Agent Configuration

log:
  stdout_log_level: INFO
  log_file_level: DEBUG
  log_file: a2a_agent.log

!include ../shared_config.yaml

apps:
  - name: "FileSystem__app"
    app_base_path: .
    app_module: solace_agent_mesh.agent.sac.app
    broker:
      <<: *broker_connection

    app_config:
      namespace: "${NAMESPACE}"
      supports_streaming: true
      agent_name: "FileSystem"
      display_name: "File System Agent"
      model: *general_model 

      instruction: |
        You can interact with the local filesystem using MCP tools. Use the available tools to read, write, and manage files as requested.
      
      tools: 
        - group_name: artifact_management
          tool_type: builtin-group
        - connection_params:
            args:
            - -y
            - '@modelcontextprotocol/server-filesystem'
            - /tmp/samv2
            command: npx
            timeout: 30
            type: stdio
          tool_type: mcp

      session_service: 
        type: "sql"
        default_behavior: "PERSISTENT"
        database_url: "${FILE_SYSTEM_DATABASE_URL}"
      artifact_service: *default_artifact_service
      
      artifact_handling_mode: "reference"
      enable_embed_resolution: true
      enable_artifact_content_instruction: true
      data_tools_config: *default_data_tools_config

      # Agent Card Definition
      agent_card:
        description: |
          An agent that interacts with the local filesystem via MCP.
        defaultInputModes: [text] 
        defaultOutputModes: [text, file] 
        skills: []
      
      # Discovery & Communication
      agent_card_publishing: 
        interval_seconds: 10
      agent_discovery: 
        enabled: true
      inter_agent_communication:
        allow_list: ["*"] 
        deny_list: [] 
        request_timeout_seconds: 600
```

Now go ahead and run an instance of the solace agent mesh from your terminal in your root project directory
```
sam run
```
Navigate to the Agents tab and see the new agent in the list

![fileagent](../static/img/fileagent.png)

Now that you have the File Agent up and running, you can run any of the following prompts to see it in action

```
"List the files in the directory"
"Create a simple text file with some content"
"Read the contents of test.txt"
```

To learn more about MCP integrations with the Solace Agent mesh, refer to the [MCP Integration](https://solacelabs.github.io/solace-agent-mesh/docs/documentation/tutorials/mcp-integration) section in the documentation
