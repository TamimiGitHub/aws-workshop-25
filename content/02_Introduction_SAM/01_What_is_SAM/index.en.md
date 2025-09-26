---
title: "What is Solace Agent Mesh?"
weight: 1
---

Solace Agent Mesh is a comprehensive open-source framework that empowers developers to build sophisticated, distributed AI systems. On a high level, Agent mesh provides developers with the following:

1. **Core Communication & Protocol**

   - **Standardized [A2A](https://a2a-protocol.org/dev/specification/) (Agent-to-Agent) Protocol**: A unified communication standard that enables seamless interaction between AI agents, regardless of their underlying implementation or deployment location
   - **Event-Driven Architecture**: Built on the Solace Event Broker for asynchronous, scalable, and resilient agent communication
   - **Topic-Based Routing**: Intelligent message routing that enables agents to discover and communicate with each other dynamically

2. **Data Integration & Connectivity**

   - **Real-World Data Source Integration**: Access to real-time data and integrations from the event mesh allows AI agents access to different business events
   - **Universal Gateway Support**: Multiple interface types including REST APIs, WebSockets, webhooks, and direct event mesh integration
   - **Streaming Data Processing**: Real-time event processing capabilities for handling live data streams and IoT sensor feeds
   - **Multi-Protocol Support**: Connect to systems using HTTP, MQTT, AMQP, WebSocket, and custom protocols

3. **Workflow Orchestration & Management**

   - **Complex Workflow Orchestration**: Coordinate sophisticated multi-agent workflows with dependency management and parallel execution
   - **Task Decomposition**: Automatically break down complex requests into manageable subtasks for specialized agents
   - **Result Aggregation**: Intelligent collection and synthesis of results from multiple agents into cohesive responses

4. **Extensibility & Plugin Architecture**

   - **Modular Plugin System**: Easily extend functionality through a rich ecosystem of [community](https://github.com/solacecommunity/solace-agent-mesh-plugins) and [commercial plugins](https://github.com/SolaceLabs/solace-agent-mesh-core-plugins)
   - **Custom Agent Development**: Comprehensive tools and templates for building domain-specific agents with specialized capabilities
   - **Gateway Plugins**: Create custom external interfaces for unique integration requirements with the Gateway Development Kit (GDK)
   - **Service Provider Plugins**: Standardized abstractions for integrating with backend systems and data sources
   - **Tool Framework**: Extensible tool system that allows agents to perform actions and interact with external services

5. **AI Model & Provider Support**

   - **Multi-Model Compatibility**: Support for all major AI providers including OpenAI, Anthropic, Google, Azure OpenAI, and local models
   - **Model Abstraction**: Switch between different AI models without changing agent logic
   - **Custom Model Integration**: Support for proprietary and fine-tuned models through flexible provider interfaces

6. **Development Tools & Framework**

   - **Comprehensive CLI**: Full-featured command-line interface for project creation, management, and deployment
   - **Configuration Management**: YAML-based configuration system with environment variable support and validation

7. **Security & Enterprise Features**

   - **Multi-Authentication Support**: JWT, OAuth, API keys, and custom authentication mechanisms
   - **Role-Based Access Control**: Fine-grained permissions and authorization for agents and resources
   - **Identity Service Integration**: Integration with enterprise identity providers and HR systems


8. **Scalability & Performance**

   - **Horizontal Scaling**: Easily scale individual agents or entire agent meshes based on demand
   - **Resource Management**: Intelligent resource allocation and optimization for optimal performance
   - **Async Processing**: Non-blocking, asynchronous operations for maximum throughput
   - **Shock Absorbing**: Built on top of an advanced message broker, Solace Event Broker, that leverages queues for guaranteed messaging

9. **Deployment & Operations**

   - **Multi-Environment Support**: Seamless deployment across development, staging, and production environments
   - **Container-Ready**: Docker and Kubernetes support for modern containerized deployments
   - **Cloud-Native**: Native support for AWS, Azure, GCP, and hybrid cloud deployments


> Solace Agent Mesh follows an event-driven architecture that decouples components, allowing them to be developed, deployed, and scaled independently.

This codelab will help you understand how to leverage Solace Agent Mesh for your own AI applications, whether you're an AI enthusiast experimenting with new models or an enterprise developer building production systems.

## Resources

For more information and a deep dive on the Solace Agent Mesh, you can check out this video series 