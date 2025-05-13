---
title: MCP
source: https://modelcontextprotocol.io/introduction
author:
  - "[[Model Context Protocol]]"
published: 
created: 2025-05-06
description: Get started with the Model Context Protocol (MCP)
tags:
  - clippings
---
C# SDK released! Check out [what else is new.](https://modelcontextprotocol.io/development/updates)

MCP is an open protocol that standardizes how applications provide context to LLMs. Think of MCP like a USB-C port for AI applications. Just as USB-C provides a standardized way to connect your devices to various peripherals and accessories, MCP provides a standardized way to connect AI models to different data sources and tools.

## Why MCP?

MCP helps you build agents and complex workflows on top of LLMs. LLMs frequently need to integrate with data and tools, and MCP provides:

- A growing list of pre-built integrations that your LLM can directly plug into
- The flexibility to switch between LLM providers and vendors
- Best practices for securing your data within your infrastructure

### General architecture

At its core, MCP follows a client-server architecture where a host application can connect to multiple servers:

<svg aria-roledescription="flowchart-v2" role="graphics-document document" viewBox="0 0 877.7890625 601.4139404296875" style="max-width: 877.7890625px;" class="flowchart" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns="http://www.w3.org/2000/svg" width="100%" id="r14"><g><marker orient="auto" markerHeight="8" markerWidth="8" markerUnits="userSpaceOnUse" refY="5" refX="5" viewBox="0 0 10 10" class="marker flowchart-v2" id="r14_flowchart-v2-pointEnd"><path style="stroke-width: 1; stroke-dasharray: 1, 0;" class="arrowMarkerPath" d="M 0 0 L 10 5 L 0 10 z"></path></marker><marker orient="auto" markerHeight="8" markerWidth="8" markerUnits="userSpaceOnUse" refY="5" refX="4.5" viewBox="0 0 10 10" class="marker flowchart-v2" id="r14_flowchart-v2-pointStart"><path style="stroke-width: 1; stroke-dasharray: 1, 0;" class="arrowMarkerPath" d="M 0 5 L 10 10 L 10 0 z"></path></marker><marker orient="auto" markerHeight="11" markerWidth="11" markerUnits="userSpaceOnUse" refY="5" refX="11" viewBox="0 0 10 10" class="marker flowchart-v2" id="r14_flowchart-v2-circleEnd"><circle style="stroke-width: 1; stroke-dasharray: 1, 0;" class="arrowMarkerPath" r="5" cy="5" cx="5"></circle></marker><marker orient="auto" markerHeight="11" markerWidth="11" markerUnits="userSpaceOnUse" refY="5" refX="-1" viewBox="0 0 10 10" class="marker flowchart-v2" id="r14_flowchart-v2-circleStart"><circle style="stroke-width: 1; stroke-dasharray: 1, 0;" class="arrowMarkerPath" r="5" cy="5" cx="5"></circle></marker><marker orient="auto" markerHeight="11" markerWidth="11" markerUnits="userSpaceOnUse" refY="5.2" refX="12" viewBox="0 0 11 11" class="marker cross flowchart-v2" id="r14_flowchart-v2-crossEnd"><path style="stroke-width: 2; stroke-dasharray: 1, 0;" class="arrowMarkerPath" d="M 1,1 l 9,9 M 10,1 l -9,9"></path></marker><marker orient="auto" markerHeight="11" markerWidth="11" markerUnits="userSpaceOnUse" refY="5.2" refX="-1" viewBox="0 0 11 11" class="marker cross flowchart-v2" id="r14_flowchart-v2-crossStart"><path style="stroke-width: 2; stroke-dasharray: 1, 0;" class="arrowMarkerPath" d="M 1,1 l 9,9 M 10,1 l -9,9"></path></marker><g class="root"><g class="clusters"><g data-look="classic" id="Internet" class="cluster"><rect height="164.0664825439453" width="173.4140625" y="429.34747314453125" x="696.375" style=""></rect><g transform="translate(753.859375, 429.34747314453125)" class="cluster-label"><foreignObject height="24" width="58.4453125"><p><span></span></p><p>Internet</p><p></p></foreignObject></g></g><g data-look="classic" id="subGraph0" class="cluster"><rect height="401.34747314453125" width="861.7890625" y="8" x="8" style=""></rect><g transform="translate(381.796875, 8)" class="cluster-label"><foreignObject height="24" width="114.1953125"><p><span></span></p><p>Your Computer</p><p></p></foreignObject></g></g></g><g class="edgePaths"><path marker-end="url(#r14_flowchart-v2-pointEnd)" marker-start="url(#r14_flowchart-v2-pointStart)" style="" class="edge-thickness-normal edge-pattern-solid edge-thickness-normal edge-pattern-solid flowchart-link" id="L_Host_S1_0" d="M194.719,201.842L217.265,183.723C239.811,165.605,284.904,129.367,319.646,111.249C354.389,93.13,378.783,93.13,390.979,93.13L403.176,93.13"></path><path marker-end="url(#r14_flowchart-v2-pointEnd)" marker-start="url(#r14_flowchart-v2-pointStart)" style="" class="edge-thickness-normal edge-pattern-solid edge-thickness-normal edge-pattern-solid flowchart-link" id="L_Host_S2_1" d="M257.141,243.347L269.283,243.347C281.426,243.347,305.711,243.347,330.098,243.347C354.484,243.347,378.973,243.347,391.217,243.347L403.461,243.347"></path><path marker-end="url(#r14_flowchart-v2-pointEnd)" marker-start="url(#r14_flowchart-v2-pointStart)" style="" class="edge-thickness-normal edge-pattern-solid edge-thickness-normal edge-pattern-solid flowchart-link" id="L_Host_S3_2" d="M216.663,284.292L235.552,294.801C254.441,305.311,292.218,326.329,323.25,336.838C354.281,347.347,378.566,347.347,390.709,347.347L402.852,347.347"></path><path marker-end="url(#r14_flowchart-v2-pointEnd)" marker-start="url(#r14_flowchart-v2-pointStart)" style="" class="edge-thickness-normal edge-pattern-solid edge-thickness-normal edge-pattern-solid flowchart-link" id="L_S1_D1_3" d="M577.473,93.13L587.075,93.13C596.677,93.13,615.882,93.13,635.699,93.13C655.516,93.13,675.945,93.13,689.66,93.13C703.375,93.13,710.375,93.13,713.875,93.13L717.375,93.13"></path><path marker-end="url(#r14_flowchart-v2-pointEnd)" marker-start="url(#r14_flowchart-v2-pointStart)" style="" class="edge-thickness-normal edge-pattern-solid edge-thickness-normal edge-pattern-solid flowchart-link" id="L_S2_D2_4" d="M577.188,243.347L586.837,243.347C596.487,243.347,615.786,243.347,635.651,243.347C655.516,243.347,675.945,243.347,689.708,243.347C703.47,243.347,710.565,243.347,714.113,243.347L717.66,243.347"></path><path marker-end="url(#r14_flowchart-v2-pointEnd)" marker-start="url(#r14_flowchart-v2-pointStart)" style="" class="edge-thickness-normal edge-pattern-solid edge-thickness-normal edge-pattern-solid flowchart-link" id="L_S3_D3_5" d="M577.797,347.347L587.345,347.347C596.893,347.347,615.99,347.347,635.753,347.347C655.516,347.347,675.945,347.347,696.16,366.555C716.374,385.763,736.374,424.178,746.374,443.386L756.373,462.593"></path></g><g class="edgeLabels"><g transform="translate(329.99609375, 93.13029861450195)" class="edgeLabel"><g transform="translate(-51.85546875, -12)" class="label"><foreignObject height="24" width="103.7109375"><p><span></span></p><p>MCP Protocol</p><p></p></foreignObject></g></g><g transform="translate(329.99609375, 243.34747314453125)" class="edgeLabel"><g transform="translate(-51.85546875, -12)" class="label"><foreignObject height="24" width="103.7109375"><p><span></span></p><p>MCP Protocol</p><p></p></foreignObject></g></g><g transform="translate(329.99609375, 347.34747314453125)" class="edgeLabel"><g transform="translate(-51.85546875, -12)" class="label"><foreignObject height="24" width="103.7109375"><p><span></span></p><p>MCP Protocol</p><p></p></foreignObject></g></g><g class="edgeLabel"><g transform="translate(0, 0)" class="label"></g></g><g class="edgeLabel"><g transform="translate(0, 0)" class="label"></g></g><g transform="translate(635.0859375, 347.34747314453125)" class="edgeLabel"><g transform="translate(-36.2890625, -12)" class="label"><foreignObject height="24" width="72.578125"><p><span></span></p><p>Web APIs</p><p></p></foreignObject></g></g></g><g class="nodes"><g transform="translate(143.0703125, 243.34747314453125)" id="flowchart-Host-0" class="node default"><rect height="78" width="220.140625" y="-39" x="-110.0703125" style="" class="basic label-container"></rect><g transform="translate(-80.0703125, -24)" style="" class="label"><rect></rect><foreignObject height="48" width="160.140625"><p><span></span></p><p>Host with MCP Client<br>(Claude, IDEs, Tools)</p><p></p></foreignObject></g></g><g transform="translate(490.32421875, 93.13029861450195)" id="flowchart-S1-1" class="node default"><rect height="54" width="166.296875" y="-27" x="-83.1484375" style="" class="basic label-container"></rect><g transform="translate(-53.1484375, -12)" style="" class="label"><rect></rect><foreignObject height="24" width="106.296875"><p><span></span></p><p>MCP Server A</p><p></p></foreignObject></g></g><g transform="translate(490.32421875, 243.34747314453125)" id="flowchart-S2-2" class="node default"><rect height="54" width="165.7265625" y="-27" x="-82.86328125" style="" class="basic label-container"></rect><g transform="translate(-52.86328125, -12)" style="" class="label"><rect></rect><foreignObject height="24" width="105.7265625"><p><span></span></p><p>MCP Server B</p><p></p></foreignObject></g></g><g transform="translate(490.32421875, 347.34747314453125)" id="flowchart-S3-3" class="node default"><rect height="54" width="166.9453125" y="-27" x="-83.47265625" style="" class="basic label-container"></rect><g transform="translate(-53.47265625, -12)" style="" class="label"><rect></rect><foreignObject height="24" width="106.9453125"><p><span></span></p><p>MCP Server C</p><p></p></foreignObject></g></g><g transform="translate(783.08203125, 93.13029861450195)" id="flowchart-D1-11" class="node default"><path transform="translate(-61.70703125, -50.13029531087838)" style="" class="basic label-container" d="M0,12.420196873918922 a61.70703125,12.420196873918922 0,0,0 123.4140625,0 a61.70703125,12.420196873918922 0,0,0 -123.4140625,0 l0,75.42019687391893 a61.70703125,12.420196873918922 0,0,0 123.4140625,0 l0,-75.42019687391893"></path><g transform="translate(-54.20703125, -14)" style="" class="label"><rect></rect><foreignObject height="48" width="108.4140625"><p><span></span></p><p>Local<br>Data Source A</p><p></p></foreignObject></g></g><g transform="translate(783.08203125, 243.34747314453125)" id="flowchart-D2-13" class="node default"><path transform="translate(-61.421875, -50.086874290757784)" style="" class="basic label-container" d="M0,12.391249527171857 a61.421875,12.391249527171857 0,0,0 122.84375,0 a61.421875,12.391249527171857 0,0,0 -122.84375,0 l0,75.39124952717185 a61.421875,12.391249527171857 0,0,0 122.84375,0 l0,-75.39124952717185"></path><g transform="translate(-53.921875, -14)" style="" class="label"><rect></rect><foreignObject height="48" width="107.84375"><p><span></span></p><p>Local<br>Data Source B</p><p></p></foreignObject></g></g><g transform="translate(783.08203125, 511.3807144165039)" id="flowchart-D3-15" class="node default"><path transform="translate(-44.1953125, -47.03324302555466)" style="" class="basic label-container" d="M0,10.355495350369774 a44.1953125,10.355495350369774 0,0,0 88.390625,0 a44.1953125,10.355495350369774 0,0,0 -88.390625,0 l0,73.35549535036978 a44.1953125,10.355495350369774 0,0,0 88.390625,0 l0,-73.35549535036978"></path><g transform="translate(-36.6953125, -14)" style="" class="label"><rect></rect><foreignObject height="48" width="73.390625"><p><span></span></p><p>Remote<br>Service C</p><p></p></foreignObject></g></g></g></g></g></svg>
- **MCP Hosts**: Programs like Claude Desktop, IDEs, or AI tools that want to access data through MCP
- **MCP Clients**: Protocol clients that maintain 1:1 connections with servers
- **MCP Servers**: Lightweight programs that each expose specific capabilities through the standardized Model Context Protocol
- **Local Data Sources**: Your computer’s files, databases, and services that MCP servers can securely access
- **Remote Services**: External systems available over the internet (e.g., through APIs) that MCP servers can connect to

## Get started

Choose the path that best fits your needs:

#### Quick Starts## [For Server Developers](https://modelcontextprotocol.io/quickstart/server)

[

Get started building your own server to use in Claude for Desktop and other clients

](https://modelcontextprotocol.io/quickstart/server)For Client Developers

Get started building your own client that can integrate with all MCP servers

[View original](https://modelcontextprotocol.io/quickstart/client)For Claude Desktop Users

Get started using pre-built servers in Claude for Desktop

[View original](https://modelcontextprotocol.io/quickstart/user)

#### Examples## [Example Servers](https://modelcontextprotocol.io/examples)

[

Check out our gallery of official MCP servers and implementations

](https://modelcontextprotocol.io/examples)Example Clients

View the list of clients that support MCP integrations

[View original](https://modelcontextprotocol.io/clients)

## Tutorials## [Building MCP with LLMs](https://modelcontextprotocol.io/tutorials/building-mcp-with-llms)

[

Learn how to use LLMs like Claude to speed up your MCP development

](https://modelcontextprotocol.io/tutorials/building-mcp-with-llms)Debugging Guide

Learn how to effectively debug MCP servers and integrations

[View original](https://modelcontextprotocol.io/docs/tools/debugging)MCP Inspector

Test and inspect your MCP servers with our interactive debugging tool

[View original](https://modelcontextprotocol.io/docs/tools/inspector)MCP Workshop (Video, 2hr)

![](https://www.youtube.com/watch?v=kQmXtrmQ5Zg)

[View original](https://www.youtube.com/watch?v=kQmXtrmQ5Zg)

## Explore MCP

Dive deeper into MCP’s core concepts and capabilities:## [Core architecture](https://modelcontextprotocol.io/docs/concepts/architecture)

[

Understand how MCP connects clients, servers, and LLMs

](https://modelcontextprotocol.io/docs/concepts/architecture)Resources

Expose data and content from your servers to LLMs

[View original](https://modelcontextprotocol.io/docs/concepts/resources)Prompts

Create reusable prompt templates and workflows

[View original](https://modelcontextprotocol.io/docs/concepts/prompts)Tools

Enable LLMs to perform actions through your server

[View original](https://modelcontextprotocol.io/docs/concepts/tools)Sampling

Let your servers request completions from LLMs

[View original](https://modelcontextprotocol.io/docs/concepts/sampling)Transports

Learn about MCP’s communication mechanism

[View original](https://modelcontextprotocol.io/docs/concepts/transports)

## Contributing

Want to contribute? Check out our [Contributing Guide](https://modelcontextprotocol.io/development/contributing) to learn how you can help improve MCP.

Here’s how to get help or provide feedback:

- For bug reports and feature requests related to the MCP specification, SDKs, or documentation (open source), please [create a GitHub issue](https://github.com/modelcontextprotocol)
- For discussions or Q&A about the MCP specification, use the [specification discussions](https://github.com/modelcontextprotocol/specification/discussions)
- For discussions or Q&A about other MCP open source components, use the [organization discussions](https://github.com/orgs/modelcontextprotocol/discussions)
- For bug reports, feature requests, and questions related to Claude.app and claude.ai’s MCP integration, please see Anthropic’s guide on [How to Get Support](https://support.anthropic.com/en/articles/9015913-how-to-get-support)