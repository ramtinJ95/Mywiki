## Book notes
* AI models can be sensitive to formatting tricks. Capitalization and structured
  prompts i.e task, context, constraints can help quite a bit
* Tools are a major key to success
  * What is the list of all tools that you will need?
  * what will each of them do?
* Memory managment is importan. Working memory stores relevant persistant long
term charachteristics of users. Hierarchical memory is essentially about using
recent messags along with relevant long-term memories. In practice this can look
lie the agent having access to the immediate context + using a tool to RAG
longer memory relevant info based on user query.
  * Tool call Filter is a tool to remove tool calls from memory sent to the llm.
    this usually improves performance.

