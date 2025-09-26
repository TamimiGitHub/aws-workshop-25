---
title: "Adding Agents"
weight: 5
---

As mentioned earlier, Agents are specialized processing units built around ADK. They provide domain-specific knowledge and capabilities and can operate independently and be deployed separately.

In Solace Agent Mesh, Agents are configuration driven vial YAML files and there are multiple ways to develop an agent:
1. Using built-in templates,
1. Using the `sam add agent` cli command
1. Using the GUI interface `sam add agent --gui`
1. custom using Python

Lets add a simple agent that converts any document to markdown leveraging the Solace Agent Mesh built-in tools.

1. Stop your solace agent mesh instance if its already running
2. Create a new file under `configs/agents/` and name it `markitdown.yaml`
3. Add the following content

```yaml
log:
  stdout_log_level: INFO
  log_file_level: DEBUG # Changed from INFO to DEBUG to capture ADK INFO logs
  log_file: markitdown.log

# Shared SAM config
!include ../shared_config.yaml

apps:

# ---  Markitdown Agent ---
  - name: markitdown_agent_app
    app_base_path: .
    app_module: solace_agent_mesh.agent.sac.app
    broker:
      <<: *broker_connection

    # --- App Level Config ---
    app_config:
      namespace: ${NAMESPACE}
      supports_streaming: true
      agent_name: "MarkitdownAgent"
      display_name: "Markdown"
      model: *multimodal_model # Or *planning_model, choose as appropriate
      instruction: |
        The MarkitdownAgent has the following capability:
        * convert various file types (like PDF, DOCX, XLSX, HTML, CSV, PPTX, ZIP) to Markdown.
        Any files you get that might be useful should be saved using create_artifact.
        There is no need to provide a preview of the content in the response.

      # --- Tools Definition ---
      tools:
        - tool_type: builtin
          tool_name: "convert_file_to_markdown"
        - tool_type: builtin-group
          group_name: "artifact_management"

      session_service:
        type: "memory"
        default_behavior: "PERSISTENT" # Or "RUN_BASED"

      artifact_service:
        type: "filesystem"
        base_path: "/tmp/samv2"
        artifact_scope: namespace
      artifact_handling_mode: "reference"
      enable_embed_resolution: true
      enable_artifact_content_instruction: true

      # --- Agent Card Definition ---
      agent_card:
        description: "An agent that converts various file types (like PDF, DOCX, XLSX, HTML, CSV, PPTX, ZIP) to Markdown format."
        defaultInputModes: ["text", "file"] # Can take files as input
        defaultOutputModes: ["text", "file"] # Outputs markdown file
        skills:
        - id: "convert_file_to_markdown"
          name: "Markdown Converter"
          description: "Converts various file types to Markdown format."

      # --- Discovery & Communication ---
      agent_card_publishing: { interval_seconds: 10 }
      agent_discovery: { enabled: false }
      inter_agent_communication:
        allow_list: []
        request_timeout_seconds: 60
```
4. Run solace agent mesh `sam run`

> The `sam run` command will traverse through all the yaml configurations in your directory (agents and gateways) and pass them to the solace agent mesh. If you want to run an agent in isolation, you can run an instance of solace agent mesh with all of configurations except the agent of your choice `sam run -s configs/agents/markitdown.yaml` and in another terminal you can run `sam run configs/agents/markitdown.yaml` that runs that agent in isolation. You can do the same thing with all the yaml configuration files in separate terminals. 

5. Observe the agent in the WebGUI Gateway

![markitdown](../static/img/markitdown.png)

> Check out the [examples](https://github.com/SolaceLabs/solace-agent-mesh/tree/main/examples/agents) directory for other agent yaml configurations.

