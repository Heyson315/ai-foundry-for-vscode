# Copilot Instructions for AI Foundry for VS Code

## Project Overview

- This project is a Visual Studio Code extension for Azure AI Foundry, enabling deployment and development of LLMs and AI agents directly from VS Code.
- Major features: model catalog, agent configuration, playground, and multi-agent workflow visualization.
- Key directories:
  - `guide/`: Usage guides and advanced features (e.g., multi-agent visualization)
  - `samples/agents/` and `samples/tools/`: Example YAMLs for agents and tools
  - `schema/agent/1.0.0/schema.json`: Agent YAML schema

## Agent and Tool Patterns

- Agents are defined in YAML (`samples/agents/*.agent.yaml`) using schema in `schema/agent/1.0.0/schema.json`.
- Each agent specifies a model, instructions, and tools. Example:
  ```yaml
  version: 1.0.0
  name: bing agent
  model:
    id: gpt-4o
    options:
      temperature: 1
      top_p: 1
  tools:
    - type: bing_grounding
      options:
        tool_connections:
          - { your bing connection id }
  ```
- Tools are modular and defined in `samples/tools/`. Reference by type in agent YAML.

## Developer Workflows

- To visualize multi-agent workflows, add in Python:
  ```python
  from agent_framework.observability import setup_observability
  setup_observability(vs_code_extension_port=4319)
  ```
  Then run `Microsoft Foundry: Open Visualizer for Hosted Agents` from the VS Code command palette.
- .NET workflows require OpenTelemetry setup (see `guide/Multi-agent-visualization.md`).

## Conventions & Integration

- Use the provided YAML schema for validation (`$schema` property in YAML).
- Metadata fields (authors, tags) are arrays in agent YAMLs.
- Models are referenced by ID (e.g., `gpt-4o`, `gpt-4.1`).
- Tool options must match the tool type (see `samples/tools/`).
- For new agent/tool types, provide a sample YAML in `samples/` and update schema if needed.

## External Dependencies

- Requires VS Code extensions: Azure Resources, AI Toolkit for VS Code.
- Integrates with Azure AI Foundry backend and model catalog.

## Key Files

- `README.md`: High-level overview and getting started
- `guide/Multi-agent-visualization.md`: Advanced visualization
- `samples/agents/`, `samples/tools/`: Example configurations
- `schema/agent/1.0.0/schema.json`: Agent config schema

---

For further details, see the main `README.md` and guides in the `guide/` directory.
