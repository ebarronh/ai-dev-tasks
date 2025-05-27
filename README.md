# 🚀 AI Dev Tasks for Claude 🤖

Welcome to **AI Dev Tasks**! This repository provides a collection of `.md` (Markdown) files designed to supercharge your feature development workflow using [Claude Code custom slash commands](https://docs.anthropic.com/en/docs/claude-code/tutorials#create-custom-slash-commands). By leveraging these commands with Claude Code, you can systematically approach building features, from ideation to implementation, with built-in checkpoints for verification.

Stop wrestling with monolithic AI requests and start guiding your AI collaborator step-by-step!

## ✨ The Core Idea

Building complex features with AI can sometimes feel like a black box. This workflow aims to bring structure, clarity, and control to the process by:

1.  **Defining Scope:** Clearly outlining what needs to be built with a Product Requirement Document (PRD).
2.  **Detailed Planning:** Breaking down the PRD into a granular, actionable task list.
3.  **Iterative Implementation:** Guiding the AI to tackle one task at a time, allowing you to review and approve each change.

This structured approach helps ensure the AI stays on track, makes it easier to debug issues, and gives you confidence in the generated code.

## Workflow: From Idea to Implemented Feature 💡➡️💻

Here's the step-by-step process using the `.md` files in this repository:

### 1️⃣ Create a Product Requirement Document (PRD)

First, lay out the blueprint for your feature. A PRD clarifies what you're building, for whom, and why.

You can create a lightweight PRD directly within Claude Code:

1.  Ensure you have the `create-prd.md` file from this repository inside `~/.claude/commands/` for personal (global) commands or inside `[your-project/.claude/commands]` for project-based commands.
2.  In Claude Code CLI, initiate PRD creation:

    ```
    /user:create-prd [Describe what you want to build in detail]
    ```
    *(Pro Tip: Press `/` to see all your slash commands then `tab` to enter the details that will be read as arguments.)*

    ![Example of initiating PRD creation](https://pbs.twimg.com/media/Go6DDlyX0AAS7JE?format=jpg&name=large)

### 2️⃣ Generate Your Task List from the PRD

With your PRD drafted (e.g., `250527-prd-myfeature.md`), the next step is to generate a detailed, step-by-step implementation plan for your AI Developer.

1.  Ensure you have `generate-tasks.md` on the same commands folder as before.
2.  In Claude Code CLI, use the PRD to create tasks:

    ```
    /project:generate-tasks use my PRD located @MyFeature-PRD.md
    ```
    *(Note: Replace `@MyFeature-PRD.md` with the actual filename of the PRD you generated in step 1.)*

    ![Example of generating tasks from PRD](https://pbs.twimg.com/media/Go6FITbWkAA-RCT?format=jpg&name=medium)

### 3️⃣ Examine Your Task List

You'll now have a well-structured task list, often with tasks and sub-tasks, ready for the AI to start working on. This provides a clear roadmap for implementation.

![Example of a generated task list](https://pbs.twimg.com/media/Go6GNuOWsAEcSDm?format=jpg&name=medium)

### 4️⃣ Instruct the AI to Work Through Tasks (and Mark Completion)

To ensure methodical progress and allow for verification, we'll use `task-list.md`. This command instructs the AI to focus on one task at a time and wait for your go-ahead before moving to the next.

1.  Create or ensure you have the `task-list.md` file accessible.
2.  In Claude Code CLI, tell the AI to start with the first task (e.g., `1.1`):

    ```
    /user:task-list Start on task 1.1
    ```
    *(Important: You only need to reference `@task-list.md` for the *first* task. The instructions within it guide the AI for subsequent tasks.)*

    The AI will attempt the task and then prompt you to review.

    ![Example of starting on a task with task-list.mdc](https://pbs.twimg.com/media/Go6I41KWcAAAlHc?format=jpg&name=medium)

### 5️⃣ Review, Approve, and Progress ✅

As the AI completes each task, you review the changes.
*   If the changes are good, simply reply with "yes" (or a similar affirmative) to instruct the AI to mark the task complete and move to the next one.
*   If changes are needed, provide feedback to the AI to correct the current task before moving on.

You'll see a satisfying list of completed items grow, providing a clear visual of your feature coming to life!

![Example of a progressing task list with completed items](https://pbs.twimg.com/media/Go6KrXZWkAA_UuX?format=jpg&name=medium)

While it's not always perfect, this method has proven to be a very reliable way to build out larger features with AI assistance.

## 🗂️ Files in this Repository

*   **`create-prd.md`**: Guides the AI in generating a Product Requirement Document for your feature.
*   **`generate-tasks.md`**: Takes a PRD markdown file as input and helps the AI break it down into a detailed, step-by-step implementation task list. Examples based on Next.js.
*   **`task-list.md`**: Instructs the AI on how to process the generated task list, tackling one task at a time and waiting for your approval before proceeding. (This file also contains logic for the AI to mark tasks as complete).

## 🌟 Benefits

*   **Structured Development:** Enforces a clear process from idea to code.
*   **Step-by-Step Verification:** Allows you to review and approve AI-generated code at each small step, ensuring quality and control.
*   **Manages Complexity:** Breaks down large features into smaller, digestible tasks for the AI, reducing the chance of it getting lost or generating overly complex, incorrect code.
*   **Improved Reliability:** Offers a more dependable approach to leveraging AI for significant development work compared to single, large prompts.
*   **Clear Progress Tracking:** Provides a visual representation of completed tasks, making it easy to see how much has been done and what's next.

## 🛠️ How to Use

1.  **Clone or Download:** Get these `.md` files into your project or a central location where Cursor can access them.
2.  **Follow the Workflow:** Systematically use the `.md` files in Cursor's Agent chat as described in the 5-step workflow above.
3.  **Adapt and Iterate:**
    *   Feel free to modify the prompts within the `.md` files to better suit your specific needs or coding style.
    *   If the AI struggles with a task, try rephrasing your initial feature description or breaking down tasks even further.

## 💡 Tips for Success

*   **Be Specific:** The more context and clear instructions you provide (both in your initial feature description and any clarifications), the better the AI's output will be.
*   **Correct File Tagging:** Always ensure you're accurately tagging the PRD filename (e.g., `@MyFeature-PRD.md`) when generating tasks.
*   **Patience and Iteration:** AI is a powerful tool, but it's not magic. Be prepared to guide, correct, and iterate. This workflow is designed to make that iteration process smoother.

## 🤝 Contributing

Got ideas to improve these `.md` files or have new ones that fit this workflow? Contributions are welcome!
Please feel free to:
*   Open an issue to discuss changes or suggest new features.
*   Submit a pull request with your enhancements.

---

Happy AI-assisted developing!
