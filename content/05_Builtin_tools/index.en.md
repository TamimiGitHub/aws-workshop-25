---
title: "Built-in tools"
weight: 6
---

Built-in tools in the Solace Agent Mesh are a comprehensive set of capabilities that enable agents to perform complex tasks, interact with various systems, and collaborate effectively within the mesh ecosystem. These tools extends the native capabilities offered by the [Agent Development Kit (ADK)](https://google.github.io/adk-docs/). This of these tool as native functionalities that agents have access to like "functions" instead of building these from scratch. 

The Solace Agent Mesh comes with a series of built-in tools natively to the platform. Each built-in tool name is defined in the `tools` section of the application configuration for the agent in the yaml config file as follows

```yaml
tools:
   - tool_type: builtin
     tool_name: "tool_name"
```
> Note that this is a developing open source framework and more built-in tools will be developed and introduced. Learn more about the available tools from the [Built-in Tool documentation](https://solacelabs.github.io/solace-agent-mesh/docs/documentation/user-guide/builtin-tools/)

**1. Artifact Management Tools**

Artifact management tools handle the creation, storage, and retrieval of content and data objects across the agent ecosystem. They ensure artifacts such as documents, code, or structured data can be versioned, shared, and persistently stored while also supporting format conversion for interoperability. These tools make it easier for agents to generate and reuse artifacts seamlessly.

**2. Data Analysis Tools**

Data analysis tools allow agents to process, transform, and analyze data from a variety of sources. They support statistical analysis, natural language processing, and visualization generation, enabling agents to extract insights from both structured and unstructured data. With built-in query functions, these tools can also handle natural language queries against different data stores.

**3. Web Tools**

Web tools empower agents to interact directly with web-based resources and services. They support sending HTTP requests, retrieving and parsing content, and integrating with APIs while managing authentication methods like OAuth or API keys. In permitted cases, they also enable web scraping and structured response handling.

**4. Peer Agent Delegation Tools**

Peer agent delegation tools make collaboration among agents more efficient by supporting the distribution of tasks across specialized agents. They allow context to be shared, results to be aggregated, and coordination strategies to be applied, whether sequential, parallel, or conditional. These tools also enable agents to discover expertise and provide feedback to one another.

**5. Developer Tools**

Developer tools help streamline the development, deployment, and maintenance of the agent mesh. They include command-line utilities for management, debugging interfaces for real-time monitoring, and configuration management systems for precise control. Additionally, observability and testing frameworks provide insights into system health and validation of agent performance.

**6. System Integration Tools**

System integration tools connect agents with external backend systems and enterprise platforms. They provide connectors to databases, event streams, and message queues while also allowing controlled file system access. These tools extend the mesh’s capabilities by integrating AI models and external enterprise applications into agent workflows.


Lets take an example for a `web-request` agent

```yaml
- name: web_agent_app
    app_base_path: .
    app_module: solace_agent_mesh.agent.sac.app
    broker:
      <<: *broker_connection

    app_config:
      namespace: ${NAMESPACE}
      supports_streaming: true
      agent_name: "WebAgent"
      display_name: "Web Content"
      model: *planning_model # Or another appropriate model from shared_config.yaml
      instruction: |
        You are an agent that can fetch content from web URLs using the 'web_request' tool.
        You can make various types of HTTP requests (GET, POST, etc.) and include custom headers or a body.
        The tool will return the fetched content (HTML converted to Markdown, other text types as is, or raw binary data).
        You will then need to process this content based on the user's request.
        Always save useful fetched content as an artifact.

      tools:
        - tool_type: builtin
          tool_name: "web_request"
        - tool_type: builtin-group
          group_name: "artifact_management"
```

This yaml configuration of a Web Agent uses two types of tools: a built-in tool `web_request` that handles web requests and a group of built-in tools `artifact_management` that handles artifact access 