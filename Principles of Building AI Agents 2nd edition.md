## Book notes
* AI models can be sensitive to formatting tricks. Capitalization and structured
  prompts i.e task, context, constraints can help quite a bit

* Tools are a major key to success
  * What is the list of all tools that you will need?
  * what will each of them do?

* Memory management is important. Working memory stores relevant persistent long
term characteristics of users. Hierarchical memory is essentially about using
recent messages along with relevant long-term memories. In practice this can look
like the agent having access to the immediate context + using a tool to RAG
longer memory relevant info based on user query.
  * Tool call Filter is a tool to remove tool calls from memory sent to the llm.
    this usually improves performance.

* RAG pipeline setup. Key thing to choose is strategy and an overlap window.
Chunking strategies includes recursive, character based, token aware and format
specific splitting. Pretty much when setting up RAG first pick the embedding.
Then provide the capability to upsert vectors in the vector store. Indexing is
needed for performance on vector similarity search. Querying in this context
means converting user input into an embedding and finding similar vectors in
your vector store, essentially running cosine similarity. Re-ranking is a
post-processing step that improves result relevance by applying more
sophisticated scoring methods. It considers semantic relevance, vector similarity
and position bias to reorder results for better accuracy.

* Agentic RAG, instead of searching through documents you can give your agent a
  set of tools to help reason about a domain. For example imagine you are
building a financial advisor agent which might have access to market data apis,
calculators and portfolio analysis tools. 
  * Advantage of this approach is that it can be more precise than RAG. It can
  compute exact answers instead of searching for similarity.
  * Downside is having to build and maintain the tools and the agent needs to
  know how to use them effectively. Creating a bundle of tools and prompt and
  exposing as a MCP or a Skill could be the way to go.
  
* Multi agent systems
  * Agent Supervisor is a specialized agent that coordinate and manage other
  agents
  * Workflows approach
    * **Control workflow**: An agent that engages with you on the architectural and
      planning level first. Asking questions and helping you break down the
    feature or whatever into small tasks / steps
    * **Task workflows**: Each task should be small and human readable once
    implemented, so no 1000 line code edit diffs. Then the execution should be
    reviewed based on task description and review standard of the repo, and only
    once it passes the review should the actual final diff be shown to the human
    for final review and verification.
* Evals with a focus on textual evals:
  * Accuracy and reliability:
    * **Hallucination**. Do responses contain fact or claims not present in the
    provided context? This is especially important for RAG applications
    * **Faithfulness**. Do responses accurately represent provided context?
    * **Content similarity**. Do responses maintain consistent information across
    different phrasings?
    * **Completeness**. Do responses include all necessary information from the
    input or context?
    * **Answer relevancy**. How well do responses address the original query?
  * Understanding context, how well does the agent use provided context etc:
    * **Context position**. Where does the context appear in responses? (Usually the
    correct position for context is at the top)
    * **Context precision**. Are context chunks grouped logically? Does the response
      maintain the original meaning?
    * **Context relevancy**. Does the response use the most appropriate pieces of
    context?
    * **Contextual recall**. Does the response completely recall context provided?
  * Output, how well does the model deliver final answer in line with
  requirements around format, clarity, style and alignment:
    * **Tone consistency**. Do responses maintain the correct level of formality,
    technical complexity, emotional tone and style?
    * **Prompt Alignment**. Do responses follow explicit instructions like length
    restrictions, required elements, and specific formatting requirements?
    * **Summarization Quality**. Do responses condense information accurately?
    Consider for example information retention, factual accuracy and
    conciseness.
    * **Keyword coverage**. Does a response include technical terms and terminology
      use?
