---
title: A2A/samples/python/agents at main
source: https://github.com/google/A2A/tree/main/samples/python/agents
author: 
published: 
created: 2025-05-06
description: 
tags:
  - clippings
---
[Skip to content](https://github.com/google/A2A/tree/main/samples/python/#start-of-content)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/google/A2A/tree/main?resume=1)

## Latest commit

[Update the Task Manager in the Google ADK sample to be reusable (](https://github.com/google/A2A/commit/0453e32461a1919be8a75e8349f3fb844ef97a8e)[#318](https://github.com/google/A2A/pull/318)[)](https://github.com/google/A2A/commit/0453e32461a1919be8a75e8349f3fb844ef97a8e)

## agents

## README.md

## Sample Agents

All the agents in this directory are samples built on different frameworks highlighting different capabilities. Each agent runs as a standalone A2A server.

Each agent can be run as its own A2A server with the instructions on its README. By default, each will run on a separate port on localhost (you can use command line arguments to override).

To interact with the servers, use an A2AClient in a host app (such as the CLI). See [Host Apps](https://github.com/google/A2A/blob/main/samples/python/hosts/README.md) for details.

- [**Google ADK**](https://github.com/google/A2A/blob/main/samples/python/agents/google_adk/README.md)  
	Sample agent to (mock) fill out expense reports. Showcases multi-turn interactions and returning/replying to webforms through A2A.
- [**LangGraph**](https://github.com/google/A2A/blob/main/samples/python/agents/langgraph/README.md)  
	Sample agent which can convert currency using tools. Showcases multi-turn interactions, tool usage, and streaming updates.
- [**CrewAI**](https://github.com/google/A2A/blob/main/samples/python/agents/crewai/README.md)  
	Sample agent which can generate images. Showcases multi-turn interactions and sending images through A2A.
- [**LlamaIndex**](https://github.com/google/A2A/blob/main/samples/python/agents/llama_index_file_chat/README.md)  
	Sample agent which can parse a file and then chat with the user using the parsed content as context. Showcases multi-turn interactions, file upload and parsing, and streaming updates.