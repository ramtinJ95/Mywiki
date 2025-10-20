## Research notes
#### jampa.dev things i've learned in my 7 years implementing AI
main take aways of this article:

AI as a product isn't viable: It's either a tool or a feature
This AI hype cycle is missing the mark by building ChatGPT-like bots and "✨" 
buttons that perform single OpenAI API calls.

For example, Notion, Slack, and Airtable now lead with "AI" in their page titles 
instead of the core value they provide. Slack calls itself "AI Work Management & 
Productivity Tools," but has anyone chosen Slack for its AI features?

Most of these companies seem lost on how to implement AI. A simple vector 
semantic search on Slack would outperform what they've shipped as "AI" so far.

People don't use these products due to these "✨" AI solutions. The best AI 
applications work beneath the surface to empower users

AI skeptics ask, "If AI is so good, why don't we see a lot of new startups?" 
Ask any founder. Coding isn't even close to the most challenging part of 
creating a startup.

What I do see is a boom in internal tools.

This year alone, I shipped projects that would never have been viable. As an 
engineering manager, spending weeks coding means neglecting the team.

The "Nice to have" bucket is when a project dies. It means there is no 
engineering capacity to tackle it, so it goes into the backlog limbo—until now.

Now, I can build these projects using Claude, running prompts, and reviewing the 
output between meetings. I see many people releasing new things that are 
incredibly helpful and productive, which would not have happened without Claude 
or Cursor.

Creating AI models is hard, but working with them is simple. I put off 
implementing earlier AI tools because I couldn't grasp how neural networks, 
sigmoids, and all that worked. Then someone said, "What are you doing? If you 
want to apply the technology, just use Scikit-learn."

If you've never used AI for coding, install Claude Code and start using it for 
small tasks. That gets you 70% of AI's current benefits without diving into 
prompt optimization or chain-of-thought mechanics.

Eventually, you'll need to learn to leverage LLMs better when you hit 
bottlenecks. You will realize that you will still need to review code and CLI 
commands. You will naturally be better at prompting. You will know when and 
when not to use it.

AI is the new Agile: something simple, that makes you faster but has limits, 
yet people will position it as the solution for every problem, preaching: "Oh, 
you're using (AI / Agile) wrong. In fact, it seems like what you need is even 
more of (AI / Agile)"

The tool has limits, especially when breaking new ground. LLMs are limited by 
their training data. For example, when I tried to vibecode a mod for a recently 
released Unity game, the AI failed to complete even a basic hook.

#### claudflare the better way to use mcp article
The main take aways of this article is:

Most agents today use MCP by directly exposing the "tools" to the LLM.

We tried something different: Convert the MCP tools into a TypeScript API, and 
then ask an LLM to write code that calls that API.

The results are striking:

We found agents are able to handle many more tools, and more complex tools, when 
those tools are presented as a TypeScript API rather than directly. Perhaps this 
is because LLMs have an enormous amount of real-world TypeScript in their 
training set, but only a small set of contrived examples of tool calls.

The approach really shines when an agent needs to string together multiple calls. 
With the traditional approach, the output of each tool call must feed into the 
LLM's neural network, just to be copied over to the inputs of the next call, 
wasting time, energy, and tokens. When the LLM can write code, it can skip all 
that, and only read back the final results it needs.

In short, LLMs are better at writing code to call MCP, than at calling MCP 
directly.

The special tokens used in tool calls are things LLMs have never seen in the 
wild. They must be specially trained to use tools, based on synthetic training 
data. They aren't always that good at it. If you present an LLM with too many 
tools, or overly complex tools, it may struggle to choose the right one or to 
use it correctly. As a result, MCP server designers are encouraged to present 
greatly simplified APIs as compared to the more traditional API they might 
expose to developers.

Meanwhile, LLMs are getting really good at writing code. In fact, LLMs asked to 
write code against the full, complex APIs normally exposed to developers don't 
seem to have too much trouble with it. Why, then, do MCP interfaces have to 
"dumb it down"? Writing code and calling tools are almost the same thing, but 
it seems like LLMs can do one much better than the other?

The answer is simple: LLMs have seen a lot of code. They have not seen a lot of 
"tool calls". In fact, the tool calls they have seen are probably limited to a 
contrived training set constructed by the LLM's own developers, in order to try 
to train it. Whereas they have seen real-world code from millions of open source 
projects.

MCP is designed for tool-calling, but it doesn't actually have to be used that 
way.

The "tools" that an MCP server exposes are really just an RPC interface with 
attached documentation. We don't really have to present them as tools. We can 
take the tools, and turn them into a programming language API instead.

But why would we do that, when the programming language APIs already exist 
independently? Almost every MCP server is just a wrapper around an existing 
traditional API – why not expose those APIs?

Well, it turns out MCP does something else that's really useful: It provides a 
uniform way to connect to and learn about an API.

An AI agent can use an MCP server even if the agent's developers never heard 
of the particular MCP server, and the MCP server's developers never heard of 
the particular agent. This has rarely been true of traditional APIs in the 
past. Usually, the client developer always knows exactly what API they are 
coding for. As a result, every API is able to do things like basic connectivity, 
authorization, and documentation a little bit differently.

This uniformity is useful even when the AI agent is writing code. We'd like the 
AI agent to run in a sandbox such that it can only access the tools we give it. 
MCP makes it possible for the agentic framework to implement this, by handling 
connectivity and authorization in a standard way, independent of the AI code. 
We also don't want the AI to have to search the Internet for documentation; MCP 
provides it directly in the protocol.

### Random soon to be scrapped notes
Yeah, the biggest advantages MCP has over terminal tooling is that MCP works 
without needing a full blown sandboxed Linux style environment - and MCP can 
also work with much less capable models.
You can drive one or two MCPs off a model that happily runs on a laptop (or 
even a phone). I wouldn't trust those models to go read a file and then 
successfully make a bunch of curl requests!

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
have a full Linux-style sandbox environment up and running already. That's a 
big dependency but it's also an astonishingly powerful way to use LLMs based 
on my past 6 months of exploration.

I remain afraid of prompt injection. If I'm telling Claude Code to retrieve data 
from issues in public repos there's a risk someone might have left a comment 
that causes it to steal API keys or delete files or similar.
I'm also worried about Claude Code making a mistake and doing something like 
deleting stuff that I didn't want deleted from folders outside of my direct 
project

How is it different from subagents?

They complement each other.
Subagents are mainly a token context optimization hack. They're a way for 
Claude Code to run a bunch of extra tools calls (e.g. to investigate the 
source of a bug) without consuming many tokens in the parent agent loop - the 
subagent gets its own loop, can use up to ~240,000 tokens exploring a problem 
and can then reply back up to the parent agent with a short description of 
what it did or what it figured out.
A subagent might use one or more skills as part of running.
A skill might advise Claude Code on how best to use subagents to solve a 
problem

It seems to me that MCP and Skills are solving 2 different problems and 
provide solutions that compliment each other quite nicely.
MCP is about integration of external systems and services. Skills are about 
context management - providing context on demand.
As Simon mentions, one issue with MCP is token use. Skills seem like a 
straightforward way to manage that problem: just put the MCP tools list inside 
a skill where they use no tokens until required.

## Summarized understanding

