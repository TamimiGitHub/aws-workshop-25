---
title: "Plugins"
weight: 7
---

Plugins serve as the backbone of the Solace Agent Mesh extensible architecture, providing a structured way to package, distribute, and incorporate new features into any SAM deployment. They are modular Python packages that extend the agent mesh's capabilities through specialized components that integrate seamlessly with the A2A protocol.

To spin up the list of the core plugins offered by the Solace Agent Mesh, execute the following

```
sam plugin catalog
```
![simpleFlow](../static/img/plugincat.png)

### Types of plugins
Solace Agent Mesh supports three primary categories of plugins, each serving different purposes within the ecosystem:

**Agent Plugins**
These contain specialized agents with domain-specific capabilities. They extend the system's ability to perform specific tasks or interact with particular data sources or services. For example, an agent plugin might specialize in processing financial data or analyzing medical imagery.

**Gateway Plugins**
These provide new interface types for external system integration, enabling SAM to connect with various user interfaces, APIs, or communication channels. Gateway plugins might add support for channels like Slack, Microsoft Teams, or custom web interfaces.

**Custom Plugins**
These implement specialized integrations that don't fit neatly into the agent or gateway categories. Examples include connectors for specific enterprise systems, data transformation services, or security extensions.

### Where to get plugins?

The Solace Agent Mesh ecosystem encompasses both official and community-developed plugins:

#### Official Core Plugins
These are developed and maintained by the Solace team, providing essential capabilities for common use cases. The official plugins are available in the Solace repository at [https://github.com/SolaceLabs/solace-agent-mesh-core-plugins](https://github.com/SolaceLabs/solace-agent-mesh-core-plugins).

#### Community Plugins
Solace Agent Mesh plugins ecosystem also encourages community contributions through the plugin system. These plugins extend the platform in numerous ways and can be discovered through the same plugin catalog as official plugins. to learn more about the existing plugins, check the github repository [https://github.com/solacecommunity/solace-agent-mesh-plugins](https://github.com/solacecommunity/solace-agent-mesh-plugins)

> Community plugins can be seamlessly integrated alongside official plugins, providing a unified experience while expanding the capabilities of your Solace Agent Mesh deployment.

### Adding custom plugins repository to the catalog

1. Click on the `Add Registry` button

![add_reg](../static/img/add_reg.png)

2. Input the information in the dialog
![add_reg_dialog](../static/img/add_reg_dialog.png)

   - Registry URL: `https://github.com/solacecommunity/solace-agent-mesh-plugins`
   - Registry Name: Community

3. Install the plugin of choice


To learn more about plugins, the differences between plugins and agents, and how to create your first plugin check out the Solace Agent Mesh [Plugins documentation](https://solacelabs.github.io/solace-agent-mesh/docs/documentation/concepts/plugins)