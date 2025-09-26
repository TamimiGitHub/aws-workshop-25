---
title: "Agent Cards"
weight: 2
---

Agent Cards are a critical component of the Agent-to-Agent (A2A) protocol specification. They serve as the "identity" and capability declaration for agents in a distributed system.

## What Are Agent Cards?

An Agent Card is a document (in JSON format) that describes an agent's:
- Identity (name, description, version)
- Capabilities (what the agent can do)
- Skills (specific functions or abilities)
- Service endpoint URL (how to reach the agent)
- Authentication requirements (how to authenticate)
- Interaction protocols (how to communicate)

Agent Cards enable agents to discover each other and understand how to interact appropriately. They are the foundation of the A2A (Agent-to-Agent) protocol that Solace Agent Mesh implements.

## Agent Card Structure

In the Solace Agent Mesh YAML configuration, the agent card is defined within the `agent_card` section of the agent's configuration file. Internally, this is translated to a JSON document that follows the A2A specification.

The agent card includes:

1. **Basic Metadata**
   - `description`: A human-readable description of the agent's purpose
   - `defaultInputModes`: Formats the agent accepts as input (e.g., "text", "image")
   - `defaultOutputModes`: Formats the agent produces as output

2. **Skills Section**
   - Lists the specific capabilities or services the agent offers
   - Each skill has an ID, name, and description
   - Skills are discoverable by other agents for delegation and collaboration

3. **Authentication Information** (optional)
   - Methods for authenticating with the agent
   - Required scopes or permissions

4. **Capabilities Declaration** (optional)
   - Special features the agent supports (streaming, attachments, etc.)
   - Extension capabilities beyond core A2A functionality

## Benefits of the YAML Configuration Approach

The YAML-based configuration approach in Solace Agent Mesh provides several key benefits:

1. **Configuration-driven:** Precise control over agent behavior, service integrations, and security settings without code changes
2. **Security-first approach:** Built-in authorization framework with fine-grained access control
3. **Resilient by nature:** Event-driven design creates responsive, self-healing interactions
4. **Standardized discovery:** A2A-compliant agent cards enable seamless agent integration and collaboration

This configuration approach is particularly valuable for building complex multi-agent systems where agents need to discover and collaborate with each other based on their respective capabilities and skills.