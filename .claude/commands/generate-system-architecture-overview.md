# 🧩 System Architecture Overview Generator Prompt

You are a software architect. Given the following requirements document and available wireframes, generate a concise **System Architecture Overview** for the MVP.

Use **Sequential Thinking (MCP)** to reason step by step:
- First, identify the distinct user-facing experiences, roles, and responsibilities.
- Then, group functionality into logical system components based on ownership and separation of concerns.
- After that, define how these components interact with each other — including direction of data flow and dependencies.
- Finally, highlight architectural insights and trade-offs relevant to the MVP scope.

You have access to **all technical documentation files in the `technical/` directory**, including infrastructure and tech stack. **Do not restate or duplicate information from those files** — especially detailed technology versions, deployment configs, or infrastructure setups.

If needed, you may briefly mention the **main technology per component** (e.g., “React Native”, “React”, “Node.js”) — but avoid listing versions, libraries, or implementation-level details already covered elsewhere.

The output should include:

1. **High-level system components**, with:
   - Component name
   - Role in the system
   - Brief description of responsibilities
   - *(Optional)* Main technology used — no versions or low-level details

2. **Component interaction model**, either as a diagram (textual or ASCII) or narrative description

3. **Key architectural considerations**, such as:
   - MVP constraints or shortcuts (e.g., monolith instead of microservices)
   - Shared services (e.g., centralized authentication)
   - Assumptions or dependencies on external systems

Output must be formatted as a **Markdown file** named `system-architecture-overview.md`, suitable for inclusion in the technical documentation repository.

Base your reasoning on:
- Functional scope from the requirements
- Role segmentation and feature access from the wireframes
- Technical constraints and decisions found in the `technical/` directory
