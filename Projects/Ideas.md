## Natural language to SQL generation project
The idea with this project is that I want to build essentially MentiMentor. I
want people outside of DNA being able to ask question of our data in natural
language and then have the MentiMentor answer those questions. Even if it does
not answer them correctly, just having the stakeholder writing down their
thoughts in clear text and have the bot generate something that an analyst can
build on top of, is valuable.

In the ideal case this same bot should be able to answer questions that are
based on our own internal documentaion also, here im thinking mostly of guru
docs, but maybe even coda docs. 

#### Research material

https://docs.langchain.com/docs/ Their docs are pretty good and contain quite a
bit of technical terms etc that is good to get familiar with before exploring
further. 

https://python.langchain.com/docs/use_cases/sql this is langchains own
tutorial/documentation and should be the first thing to try out and play around
with I would say.

https://www.pinecone.io/learn/series/langchain/langchain-agents/ this seems to
be a crazy good webiste with many good tutorials around LLMs and langchains.

https://medium.com/dataherald/how-to-langchain-sqlchain-c7342dd41614

https://medium.com/vectrix-ai/creating-your-own-ai-powered-database-interface-1456b72eb36e

https://walkingtree.tech/natural-language-to-query-your-sql-database-using-langchain-powered-by-llms/

https://blog.langchain.dev/llms-and-sql/

https://www.patterns.app/blog/2023/01/18/crunchbot-sql-analyst-gpt/?ref=blog.langchain.dev
https://github.com/patterns-app/patterns-components/tree/master/patterns_templates/Featured%20and%20Starter/Crunchbot this is the code for the blogpost above it.

From this point and down the materials are not strictly related to generating
sql from natural language, and sending it as a query against db/dw but they are
more focused on feeding a llm with documentation like guru etc. 
https://www.patterns.app/blog/2022/12/21/finetune-llm-tech-support
