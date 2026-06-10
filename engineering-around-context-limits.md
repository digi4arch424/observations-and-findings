# Engineering Around Context Limits

## Practical Strategies for Managing Tokens, Memory, and Long-Running Claude Code Sessions

Free-tier users often hit usage limits and run out of GPT messages. This makes efficient token management essential, especially during long development sessions.

Every new message requires Claude to reread the conversation history, project memory, loaded files, tool outputs, and previous responses before generating an answer. As sessions grow longer, context accumulates and token consumption increases, making each additional turn more expensive than the last.

---

## Rule #1: Edit, Don't Append

### Bad

**Prompt A**

Claude gives wrong answer

**Prompt B**

"No, that's wrong because..."

### Better

Edit Prompt A and resend.

### Why?

Claude must process the entire conversation history before answering Prompt B. The longer the session, the more tokens are consumed simply reconstructing context.

Treat prompts like source code:

- Refactor prompts
- Improve prompts
- Retry prompts
- Avoid long correction chains

A clean prompt is cheaper than a long argument.

---

## Rule #2: Watch Context Like RAM

Use:

/usage

or

/cost

to monitor token consumption and session cost.

### Practical Threshold

When a session approaches roughly 120k–160k tokens, start planning a handover. Don't wait until the context window is nearly full.

Once a conversation passes this threshold, model performance can become less efficient. More tokens are spent processing historical context, response quality may become less consistent, and earlier instructions, decisions, or assumptions are more likely to be compressed, deprioritized, or overlooked.

Starting a fresh session with a concise handover helps preserve accuracy, reduce token consumption, and maintain response quality.

---

## Rule #3: Compact Before You Stall

Use:

/compact

Claude summarizes the conversation and replaces large portions of history with a condensed version. This frees context while preserving key decisions and technical reasoning.

Even better:

/compact focus on API redesign and database schema decisions

Focused compaction preserves the information that actually matters.

---

## Rule #4: Handover Long Projects

For large projects, periodically create a handover document containing:

- Current objective
- Completed work
- Architecture decisions
- Open issues
- Next actions
- Critical files

Then start a fresh session and paste the handover.

Fresh sessions start with a fresh context window and avoid dragging thousands of unnecessary tokens into future work.

---

## Rule #5: Plan Before Generating

Instead of:

> Implement everything

Start with:

1. Create a plan
2. List files
3. Describe changes
4. Wait for approval

A small planning step can save tens of thousands of wasted tokens caused by incorrect implementations and rewrites.

---

## Rule #6: Think Like a Context Engineer

A context window is not infinite memory.

It is a working desk.

Every file, prompt, command output, and response occupies space.

When the desk fills up, the system must either:

- Compact information  
- Forget information  
- Spend more tokens managing information  

Good Claude Code users don't just write better prompts.

They manage context like engineers manage CPU, RAM, and storage.

---

## The Golden Rule

> Every token spent reading old context is a token not spent solving your current problem.

Treat tokens as a finite engineering resource.  
Treat context as working memory.  
Treat prompt design as performance optimization.
