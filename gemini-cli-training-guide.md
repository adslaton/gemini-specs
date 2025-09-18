# Gemini CLI Hands-On Session Guide

### **Objective:**
To clarify how Gemini CLI works, address common misconceptions, and provide best practices for an efficient workflow.

---

### **1. Getting Context from External Sources (like Jira)**

**The Challenge:** Gemini CLI doesn't have direct integrations with external tools like Jira. It primarily interacts with your local filesystem.

**Solution/Workflow (Direct Copy/Paste):**

1.  **Bring the context locally:** Copy the relevant information from the Jira ticket (e.g., user story, bug report, comments).
2.  **Create a context file:** Paste the information into a local file, like `jira-context.md`.
3.  **Reference the file in your prompt:** Start your session with a prompt that directs Gemini to use this file for context.

**Example Prompt (Copy/Paste):**

> "I'm working on a task described in `jira-context.md`. Please read the file and help me create a plan to implement the required changes."

**Alternative Workflow (Atlassian Remote MCP Server):**

For more structured or automated context retrieval from Atlassian products, the **Atlassian Remote MCP Server** can act as a bridge.

1.  **Set up MCP Server:** Follow the official documentation to set up and configure the Atlassian Remote MCP Server: [Getting started with the Atlassian Remote MCP Server](https://support.atlassian.com/atlassian-rovo-mcp-server/docs/getting-started-with-the-atlassian-remote-mcp-server/)
2.  **Extract Context:** Use the MCP Server to extract relevant information from Jira tickets, Confluence pages, or other Atlassian sources.
3.  **Save to Local File:** Save the extracted context (e.g., as Markdown or JSON) to a local file within your project (e.g., `mcp-context.md`).
4.  **Reference with Gemini:** Refer to this local file in your Gemini CLI prompts.

**Example Prompt (MCP Server):**

> "Using the Atlassian Remote MCP Server, please review Jira ticket [TICKET-ID] and then suggest an implementation approach for a new feature based on its details."

---

### **2. Providing Code Context (and IDE Integration)**

**The Challenge:** Gemini asks for code to be pasted, especially when using it within an IDE.

**Explanation:**

*   **Gemini CLI vs. IDE Extensions:** It's important to distinguish between the Gemini CLI and IDE extensions (like Gemini Code Assist). They are separate tools. The IDE extension should have access to the open files, but if it's asking for code, it might be a limitation or misconfiguration of the extension itself.
*   **Gemini CLI and Local Files:** The Gemini CLI *can* and *should* access local files directly. If it's asking you to paste code, it means it doesn't know which file you're referring to.

**Solution/Workflow:**

*   **Be explicit with file paths:** Always refer to files by their path.
*   **Use file-reading tools:** Use the built-in tools to give Gemini context.

**Example Prompts:**

> "Read the file `src/components/MyComponent.js` and tell me what it does."

> "I want to add a feature. Read the following files to get the full context: `src/service.js`, `src/controller.js`, and `src/routes.js`."

---

### **3. Why Changes Don't Seem to Persist**

**The Challenge:** A user's experience of changes feeling "in-memory" and not affecting the actual files.

**The Core Misconception:** This is likely due to not approving the final execution step.

**Explanation:**

1.  **The "Okay to do?" Prompt:** Gemini CLI operates on a principle of explicit user consent for any action that modifies the filesystem. When Gemini is ready to make a change, it will propose a tool call (a code snippet wrapped in `...`) and wait for your approval.

2.  **The Approval Step is Crucial:** If you don't explicitly approve the tool call (by typing "yes" or clicking "approve"), the proposed change will **not** be executed. The file will remain untouched on your disk. This is why it feels like the changes are "in-memory"—they exist as a proposal within the chat session but haven't been applied to the actual file.

**Troubleshooting Steps:**

*   When you see the `...` block, you must approve it to apply the changes.
*   If you have approved it and it's still not working, it might be a bug, but it's most likely a missed approval.
*   Once the file is modified, the changes will be visible in all terminal windows and other applications.

---

### **4. Accessing GitHub Repositories**

**The Challenge:** How to get Gemini to access code in a GitHub repository.

**Solution/Workflow:**

1.  **Clone the repository:** Use `git clone` to download the repository to your local machine.
2.  **Navigate to the directory:** `cd` into the repository's directory.
3.  **Interact with Gemini:** Now you can use Gemini CLI to interact with the files in the repository just like any other local files.

---

### **5. Managing the Context Window**

**The Challenge:** Long conversations can exceed the model's context window, leading to loss of information.

**Explanation:** The context window is the short-term memory of the model for the current conversation.

**Solutions/Best Practices:**

*   **/clear:** Use this command to wipe the conversation history and start fresh. This is useful when switching tasks.
*   **/chat save & /chat restore:** These commands allow you to save your current session and restore it later. This is great for managing different projects or tasks without losing context.
*   **Proactive Context Management:** Be mindful of how much information you're feeding the model. Instead of asking it to read a whole directory, start with the most relevant files.
*   **/compress (Hypothetical):** While not a standard feature, the idea of a `/compress` command is to summarize the conversation to free up space. You can achieve a similar result by manually summarizing the progress so far in a prompt.

**Example Prompt for manual compression:**

> "Let's summarize our progress. We have implemented the user authentication feature and now we need to work on the profile page. Please keep this summary in mind for the next steps."
