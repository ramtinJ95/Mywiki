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
* RAG pipeline setup. Key thing to choose is strategy and an overlap window.
Chunking strategies includes recursive, charachter based, token aware and format
specific splitting. Pretty much when setting up RAG first pick the embedding.
Then provide the capability to upsert vectors in the vector store. Indexing is
needed for performance on vector similiarity search. Quering in this context
means converting user input into an embedding and finding similar vectors in
your vector store, essentially running cosine similarity. Re-ranking is a
post-processing step that immproves result relevance by applying more
sophistacted scoring methods. It considers smenatic relevance, vector similarity
and position bias to reorder seults for better accuracy.
* Agentic RAG, instead of searching through documents you can give your agent a
  set of tools to help reason about a domain. For example imagine you are
building a financial advisor agent which might have access to market data apis,
calculators and portfolio analysis tools. 
  * Advantage of this approach is that it can be more precise than RAG. It can
  compute exact answers instead of searching for similarity.
  * Downside is having to build and maintain the tools and the agent needs to
  know how to use them effectively. Creating a bundle of tools and prompt and
  exposing as a MCP or a Skill could be the way to go.
