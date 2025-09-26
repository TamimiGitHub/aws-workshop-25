---
title: "Key Components"
weight: 2
---

Solace Agent Mesh represents a sophisticated enterprise-grade platform that orchestrates AI agents. At its core, the **Orchestrator** serves as the intelligent brain that decomposes complex tasks and routes them to specialized **Agents** built using the Agent Development Kit (ADK), while **Gateways** created with the Gateway Development Kit (GDK) provide secure multi-protocol entry points. The platform's foundation rests on the **Solace Broker** for enterprise messaging, complemented by essential Services including **LLM integration**, **embeddings management**, **artifact storage**, and **conversation history tracking**. This unified architecture creates a robust, enterprise-ready platform for deploying and managing AI agent ecosystems at scale.

![SAM Component](../../static/img/sam_components.jpg)


### Solace Event Broker / Event Mesh
The central messaging backbone that provides intelligent topic-based routing, fault-tolerant delivery, and horizontal scaling for all Agent-to-Agent (A2A) protocol communications across the entire system.

The [Solace Event Broker](https://solace.com/products/event-broker/) serves as the central nervous system of the entire Solace Agent Mesh framework, providing:

- **Intelligent Topic-Based Routing**: Directs messages between components using hierarchical topic structures, enabling sophisticated messaging patterns like request/reply and publish/subscribe
- **Fault-Tolerant Delivery**: Ensures guaranteed message delivery even during component failures or network instability
- **Asynchronous Communication Layer**: Creates a fluid communication foundation where messages flow naturally between all mesh components
- **Horizontal Scaling**: Supports seamless expansion as the mesh grows through distributed broker architecture
- **Real-Time Message Delivery**: Processes messages with ultra-low latency to maintain responsive agent interactions

### Gateways: Entry and Exit Points
External interface bridges that translate diverse protocols (HTTP, WebSocket, Slack RTM, Solace Event Mesh...etc) into standardized A2A messages while handling authentication, authorization, and session management for outside systems.

Important functionalities of gateways include:
- **Protocol Translation**: Convert external protocols (HTTP, WebSockets, Slack RTM) into standardized A2A protocol messages
- **Authentication & Authorization**: Authenticate incoming requests and enforce permission scopes
- **Session Management**: Map external user sessions to A2A task lifecycles
- **Response Handling**: Deliver agent responses back to external clients
- **Interface Variety**: Include REST API gateways, WebUI gateways, Slack gateways, CLI gateways, and custom interface adapters
- **Gateway Development Kit (GDK)**: Provides base classes that abstract common gateway logic

### Orchestrator - The Planner
A specialized agent that coordinates complex workflows. The main functionality of the orchestrator boils down to:
- **Request Decomposition**: Breaks down complex requests into manageable tasks
- **Task Distribution**: Assigns tasks to appropriate specialized agents
- **Workflow Management**: Tracks progress and handles dependencies between tasks
- **Result Aggregation**: Combines outputs from multiple agents into coherent responses
- **Error Handling**: Manages failures and retries or alternative approaches

### Agents - Goal Setters
Specialized AI processing units built on Agent Development Kit that provide domain-specific intelligence, self-register for dynamic discovery, and access comprehensive tool ecosystems for complex task execution.

- **Self-Registration Capabilities**: Agents automatically discover and connect to the mesh network upon initialization, eliminating the need for manual configuration and setup processes. They broadcast their available services, capabilities, and resource requirements to the network, creating a dynamic marketplace of agent functions. The agents maintain real-time service catalogs that update automatically as their capabilities evolve or change through learning and adaptation. They handle all necessary authentication and authorization protocols to ensure secure integration with the mesh infrastructure. The system supports hot-swapping and seamless updates, allowing agents to be modified or replaced without disrupting ongoing network operations.
- **Specialized Domain Functions**: Each agent is designed with narrow AI expertise tailored to specific industries, use cases, or functional domains, ensuring deep competency in their areas of specialization. They implement comprehensive domain-specific knowledge bases and reasoning patterns that reflect expert-level understanding of their target fields. The agents maintain specialized vocabularies, ontologies, and semantic understanding that enable precise communication and task execution within their domains. They provide expert-level performance in targeted functional areas, often exceeding human capabilities in speed and consistency. The specialization framework supports customizable configuration through training and fine-tuning processes.
- **Comprehensive Tool Access**: Agents interface seamlessly with extensive APIs, databases, and external service ecosystems, providing them with broad operational capabilities beyond their core AI functions. They utilize both proprietary and open-source tool libraries for task execution, ensuring flexibility and adaptability across different technological environments. The system supports dynamic tool discovery and integration during runtime, allowing agents to adapt their capabilities based on emerging requirements. Secure tool authentication and access control mechanisms protect sensitive resources while enabling authorized functionality. The agents enable sophisticated tool chaining and workflow orchestration for executing complex, multi-step operations.
- **Stateful Operation Management**: Agents maintain persistent memory and context across extended interaction sessions, enabling them to build upon previous conversations and maintain continuity in complex, long-term engagements. They implement sophisticated conversation history tracking and relationship building capabilities that allow for personalized and contextually appropriate interactions. The system supports continuous learning and adaptation based on interaction patterns, enabling agents to improve their performance and better serve user needs over time. Agents manage state synchronization across distributed instances, ensuring consistency when multiple copies of an agent are operating simultaneously. They provide robust checkpoint and recovery mechanisms that maintain operation continuity even in the face of system failures or interruptions.

### Solace AI Connector
The universal runtime environment that hosts and manages the complete lifecycle of all system components while bridging Google ADK capabilities with Solace event infrastructure through YAML-driven configuration. Main capabilities include:

- **Component Lifecycle Management**: Handles startup, monitoring, and graceful shutdown of all components
- **Configuration Management**: Processes YAML-driven configuration for flexible deployment
- **Bridge Between Technologies**: Connects Google ADK capabilities with Solace event infrastructure
- **Host Environment**: Provides the execution environment for agents and gateways
- **Resource Management**: Controls allocation of computing resources for optimal performance

### Backend Services & Tools
The foundational infrastructure layer providing multi-provider LLM access, extensible integrations for custom tools and APIs, persistent data storage, and cloud-native artifact management services. Solace Agent Mesh is built on a modular foundation with the following tools:

- **Large Language Models**: Multiple LLM providers for varied AI capabilities
- **Databases & Vector Stores**: Persistent data storage and efficient vector search
- **Custom Tool Integration**: Framework for adding specialized functionality
- **API Connectors**: Bridges to external services and systems
- **Artifact Service**: File management through filesystem or cloud storage systems
- **Observability Framework**: Monitoring, logging, and debugging infrastructure

> Without proper planning and understanding of the component roles, you might create overly complex architectures or miss opportunities to leverage the full power of the distributed agent ecosystem.


