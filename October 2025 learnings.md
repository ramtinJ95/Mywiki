## Research notes

### Random soon to be scrapped notes
Yeah, the biggest advantages MCP has over terminal tooling is that MCP works
without needing a full blown sandboxed Linux style environment - and MCP can
also work with much less capable models.
You can drive one or two MCPs off a model that happily runs on a laptop (or even
a phone). I wouldn't trust those models to go read a file and then successfully
make a bunch of curl requests!

I've been able to build the equivalent of skills with a few markdown files. I
need to remind my agent every so often to use a skill but usually once per
session at most.
I don't get what's so special about Claude doing this?

Part of it is that they gave a name to a useful pattern that people had already
been discovering independently. Names are important, because they mean we can
start having higher quality conversations about the pattern.
Anthropic also realized that this pattern solves one of the persistent problems
with coding agents: context pollution. You need to stuff as little material as
possible into the context to enable the tool to get things done. AGENTS.md and
MCP both put too much stuff in there - the skills pattern is a much better fit.

I'm more excited about this than I was about MCP.
MCP was conceptually quite complicated, and a pretty big lift in terms of
implementation for both servers and clients.
Skills are conceptially trivial, and implementing them is easy... provided you
have a full Linux-style sandbox environment up and running already. That's a big
dependency but it's also an astonishingly powerful way to use LLMs based on my
past 6 months of exploration.

I remain afraid of prompt injection. If I'm telling Claude Code to retrieve data
from issues in public repos there's a risk someone might have left a comment
that causes it to steal API keys or delete files or similar.
I'm also worried about Claude Code making a mistake and doing something like
deleting stuff that I didn't want deleted from folders outside of my direct
project

How is it different from subagents?

They complement each other.
Subagents are mainly a token context optimization hack. They're a way for Claude
Code to run a bunch of extra tools calls (e.g. to investigate the source of a
bug) without consuming many tokens in the parent agent loop - the subagent gets
its own loop, can use up to ~240,000 tokens exploring a problem and can then
reply back up to the parent agent with a short description of what it did or
what it figured out.
A subagent might use one or more skills as part of running.
A skill might advise Claude Code on how best to use subagents to solve a problem

It seems to me that MCP and Skills are solving 2 different problems and provide
solutions that compliment each other quite nicely.
MCP is about integration of external systems and services. Skills are about
context management - providing context on demand.
As Simon mentions, one issue with MCP is token use. Skills seem like a
straightforward way to manage that problem: just put the MCP tools list inside a
skill where they use no tokens until required.

## Summarized understanding

