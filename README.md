# Gemini Specs

This project implements a **Spec-Driven Development (SDD)** workflow powered by a Gemini agent. It's designed to help you define, plan, and execute software projects with a high degree of clarity and automation.

## Getting Started

To get started with this project, you need to configure the agent's "constitution." This is the set of rules and principles that the agent will follow when generating code and making technical decisions.

1.  **Edit the Constitution**: Open `.specify/memory/constitution.md` and define your project's engineering principles. This is the most important step, as it will guide all future work.

2.  **Specify a Feature**: Once the constitution is in place, you can start your first feature:

    ```bash
    gemini specify "Your feature description here"
    ```

## The Spec-Driven Workflow

The workflow is broken down into three distinct phases, each with its own command:

### 1. `gemini specify`

*   **Purpose**: To create a new feature specification.
*   **Usage**: `gemini specify "<feature description>"`
*   **What it does**: This command will create a new feature branch and a `spec.md` file. The agent will populate the spec based on your description and the templates in the `.specify/templates` directory.

### 2. `gemini plan`

*   **Purpose**: To create a detailed implementation plan for a feature.
*   **Usage**: `gemini plan`
*   **What it does**: After a spec is created, this command will generate a `plan.md` file. The plan will outline the technical approach, data models, API contracts, and other necessary details.

### 3. `gemini tasks`

*   **Purpose**: To break down a plan into executable tasks.
*   **Usage**: `gemini tasks`
*   **What it does**: This command takes the `plan.md` and generates a `tasks.md` file. The tasks are designed to be small and specific enough for an LLM to execute them.

## How it Works

This repository is configured to use a Gemini agent to automate the SDD process. The core components are:

*   **`.gemini/commands/`**: This directory contains the definitions for the `specify`, `plan`, and `tasks` commands. These files tell the agent what to do for each step of the workflow.
*   **`.specify/`**: This directory contains the supporting files for the agent.
    *   **`memory/`**: Contains the `constitution.md` file, which acts as the agent's long-term memory and rulebook.
    *   **`scripts/`**: A collection of shell scripts that the agent uses to perform tasks like creating branches and files.
    *   **`templates/`**: Contains the templates for the `spec.md`, `plan.md`, and `tasks.md` files.

By editing the files in the `.specify` directory, you can customize the agent's behavior to fit your project's needs.
