# MCP Firewall
## Introduction
The MCP Firewall is a lightweight, API-driven security layer designed to monitor and control tool usage within Model Context Protocol (MCP) environments. By inspecting incoming requests and analyzing tool metadata in real time, the firewall can dynamically block or allow tools based on configurable policies. This allows developers and operators to prevent misuse, enforce security rules, and stop suspicious or redundant MCP tools from being executed. The firewall exposes a simple REST API, enabling seamless integration with external agents, dashboards, and automated security workflows.


## How It Works
The **MCP Firewall** is built on top of the **FastMCP 2.0 framework**, leveraging its modular architecture and support for modern MCP protocols. At its core, the firewall acts as a **proxy** that filters tool access in real time.

### Key Components and Flow
- **Transport Bridging** 
  The firewall fully supports the **streamable-http** transport and suppts transport bridging to SSE, stdio, streamable-http , ensuring compatibility with the latest MCP clients and agents.
- **Security Boundary**: 
  - When an external agent or user queries `tools/list`, the request is intercepted by the firewall.  
  - The firewall checks the request against a dynamic **allow/block list** (also called an **exclude list**), which can be maintained via API or configuration file.  
  - The response from the backend MCP server is then **sanitized**, with any excluded tools **removed** from the returned list.
- **API-Driven Control**  
  - The filtering can be updated at runtime using a simple REST API.  
  - This makes it easy to automate defenses, apply policy updates, or integrate with detection systems (e.g., flagging tools with overlapping or malicious behavior).

This design ensures that **untrusted or redundant tools are hidden from the agent**, without requiring changes to the underlying MCP server. The result is a secure, adaptable layer of control for any MCP-based system.
