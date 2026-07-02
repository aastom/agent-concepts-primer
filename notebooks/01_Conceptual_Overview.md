# 01 - Conceptual Overview: The Anatomy of an Agent

Before we write a single line of code, it's essential to understand the core, framework-agnostic concepts that make up an AI agent. An ADK like LangChain is just a library that helps us assemble these fundamental building blocks.

As we outlined in the `docs/architecture.md`, an agent is a system that combines several key components:

1.  **The Brain (LLM)**: The reasoning part.
2.  **The Senses & Hands (Tools)**: The action part.
3.  **The Mind's Eye (Reasoning Loop)**: The decision-making process.
4.  **The Memory**: The ability to recall past events.

Let's briefly revisit these in the context of what we're about to build.

### 1. The Brain: The Large Language Model (LLM)

This is the core of our agent. We will be using a powerful LLM from OpenAI. When we give the agent a task, it's the LLM that "thinks" about how to accomplish it. It breaks the problem down and decides if it needs to use a tool.

In our notebooks, you will see this represented by an object, often called `llm` or a `chat_model`.

### 2. The Senses & Hands: Tools

A tool is just a function that the agent can decide to call. It's the most important concept for making agents useful. Without tools, the LLM is trapped in its own world of text. With tools, it can interact with the real world.

- In `03_Agents_with_Tools.ipynb`, we will create a simple Python function to get the current date and give it to our agent as a tool.
- In `05_Final_Project_Simple_Researcher.ipynb`, we will give the agent a pre-built web search tool.

This is the key to unlocking the power of agents: you can turn any function, any API, any data source into a tool that your agent can use.

### 3. The Mind's Eye: The Reasoning Loop (ReAct)

How does the agent decide *when* to use a tool? It follows a reasoning process. The most common one, and the one we'll use, is **ReAct (Reasoning and Acting)**.

It works like this:

1.  **Prompt**: The agent is given a task (e.g., "What day of the week is it?").
2.  **Reason (Thought)**: The LLM thinks, "The user wants to know the day of the week. I cannot know this from my internal knowledge alone. I need to use a tool that can tell me the current date."
3.  **Act (Tool Call)**: The agent decides to call the `get_todays_date` tool.
4.  **Observe (Tool Output)**: The tool returns the date, for example, "2024-07-29".
5.  **Reason (Thought)**: The LLM receives this output and thinks, "The tool returned 2024-07-29. Now I can answer the user's question about the day of the week. Monday." 
6.  **Final Answer**: The agent gives the final response to the user.

In the notebooks, you will see us create an **Agent Executor**, which is the component that runs this loop. By enabling verbose logging, we can see these "Thought" and "Action" steps unfold in real-time.

### 4. Memory

For this introductory primer, our agents will have a very basic **short-term memory**. The `AgentExecutor` automatically remembers the previous steps within the *same* ReAct loop. However, once it gives a final answer, it will start the next query with a blank slate.

More advanced forms of memory (e.g., remembering entire past conversations or storing information in a database) are a key part of building more sophisticated agents, and are a great topic to explore in the "Beyond This Module" section.

---

With these concepts in mind, you are ready to proceed to the first hands-on notebook: `02_Hello_Agent.ipynb`. First, however, you must complete the setup in `00_Setup_and_Cost_Management.ipynb`.
