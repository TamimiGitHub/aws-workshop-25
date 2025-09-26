---
title: "Installing Solace Agent Mesh"
weight: 1
---

## Install Python 3.11+

To install a specific version of python, we would recommend using brew
```
brew install python@3.12
```

> Depending on how you install your python version, the following commands will be executed as per the python version installed
> For example, you might need to run `python3.12 [command]` to run python version 3.12 or just simply `python3 [command]`

## Create and activate a Python virtual environment

MacOS/Linux
```
mkdir solace-agent-mesh-demo
cd solace-agent-mesh-demo
python3 -m venv venv
source venv/bin/activate
```
Windows
```
venv/Scripts/activate
```

> Note: on a Linux machine, depending on the distribution you might need to `apt-get install python3-venv` instead. Alternatively, you can use `pyenv` to manage multiple versions of python


After activating the virtual environment you can now simply just use `python` which will use whatever python version used to initialize the virtual environment. To confirm, you can execute the following after activating your virtual environment

```
python --version
```

## Install the Solace Agent Mesh Community Edition

```
pip install solace-agent-mesh

```

## [Optional] Solace Broker

You have two options to run and connect to a Solace Broker
1. Software: using a docker image to run it locally
2. Cloud: using self served cloud instance

Follow the steps defined in the [getting started with Solace](https://solace.com/products/event-broker/software/getting-started/) page 

## Initialize Solace Agent Mesh

> To use the solace agent mesh, you can activate it by typing `solace-agent-mesh` or simply `sam`

In the newly created directory, initialize a new instance of an agent mesh project

```
sam init --gui
```

![SAM Init](../../static/img/saminit.png)

From here, choose "Advanced Setup" to spin up an instance of the Agent Mesh that uses the Solace Broker as the communication backbone. 


> Note that the simple setup "Getting Started Quickly" spins up Agent Mesh without the Solace Broker and uses in-memory queues instead. This is not meant for production ready development and proof of concept project that require high performance and multiple Agentic workflow interactions.

Choose a namespace for your project

![Namespace](../../static/img/init_namespace.png)

Configure connection to the Solace Broker

![Broker](../../static/img/broker_setup.png)

> Note: If you are using a Solace Cloud instance, you can get the connection parameters from the connect tab after spinning up a Broker Service. Use the Solace Web Messaging Protocol

Configure your LLM endpoint, API Key, and Model name

![LLM Endpoint](../../static/img/ai_provider.png)

> The model of choice impact the performance of your results and system behaviour. A performative model is recommended for advanced use-cases


Configure your main orchestrator

![orchestrator](../../static/img/orchestrator.png)

> Keep all the configuration parameters as default. You can explore the other options for configuring the orchestrator agent to see what you have available for fine tuning the behaviour


Configure the WebUI Gateway
![gateway](../../static/img/gateway.png)


> Note: Choose any Session Secret Key needed for the WebUI. Keep the remaining configurations as default. 

Review and Initialize the final configuration

![SAM final](../../static/img/finalinit.png)

🎉 You have now successfully configured your Solace Agent Mesh environment! Now go back to terminal and continue with the next steps to run the Agent Mesh