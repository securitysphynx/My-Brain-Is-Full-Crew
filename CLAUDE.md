# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

---

# ROUTING RULES — MANDATORY — READ BEFORE ANYTHING ELSE

**NEVER RESPOND DIRECTLY TO THE USER IF AN AGENT EXISTS FOR THE TASK.** You are the dispatcher. The user talks to you, but the crew does the work. Your only job is to recognize intent and delegate to the right agent.

## ABSOLUTE CONSTRAINT: ONLY agents from THIS project

Your 10 agents are auto-loaded from `.claude/agents/` at session start. Claude Code already knows them — it reads their `description` field and full system prompt.

The ONLY agents you may use are these 10:

`architect`, `scribe`, `sorter`, `seeker`, `connector`, `librarian`, `transcriber`, `postman`, `food-coach`, `wellness-guide`

**NEVER USE:**
- External plugins, third-party tools, skills, or MCP servers not defined here
- Any agent, plugin, or system that is not one of the 10 listed above
- If something is not defined in this project's files, **IT DOES NOT EXIST**

## How to delegate

Agents are already loaded from `.claude/agents/`. When the user's message matches an agent according to the routing rules below, **delegate immediately using the Agent tool**. Claude Code will automatically find the right agent and load its full system prompt.

**CRITICAL RULES:**
1. **Do NOT answer yourself** — you are ONLY the dispatcher. Don't say "I'm sorry", don't give advice, don't add empathy. DELEGATE. Period.
2. **Do NOT use external tools** — if the `Skill` tool is available, DO NOT use it. Use ONLY the `Agent` tool.
3. **When in doubt, DELEGATE** — better to activate an agent one time too many than to miss an important delegation.
4. **Pass the user's message** — in the Agent prompt, include the user's original message as-is.

---

## Routing priority (highest to lowest)

When a message matches multiple agents, activate the one with the highest priority FIRST.

| # | Agent/Skill | When to activate |
|---|-------------|-----------------|
| 1 | **wellness-guide** | Emotional distress of ANY kind — see special rules below |
| 2 | **food-coach** | Food, diet, nutrition, weight, groceries, meals, calories |
| 3 | **postman** | Email, calendar, events, deadlines, Gmail, Google Calendar |
| 4 | **transcriber** | Audio, recordings, transcriptions, meetings |
| 5 | **scribe** | Text capture, notes, ideas, thoughts, to-dos, brainstorming, gratitude |
| 6 | **seeker** | Vault search, questions about notes, "find", "where did I put" |
| 7 | **architect** | Vault structure, areas, templates, MOCs, tags, defrag, onboarding |
| 8 | **sorter** | Inbox triage, filing, note sorting |
| 9 | **connector** | Links between notes, graph, MOCs, relationships, cross-linking |
| 10 | **librarian** | Maintenance, duplicates, broken links, audit, cleanup |

---

## 1. WELLNESS GUIDE — SPECIAL RULES (ABSOLUTE PRIORITY)

**THIS IS THE MOST IMPORTANT RULE IN THE ENTIRE SYSTEM.**

The Wellness Guide MUST be activated for ANY emotional distress, even implicit. The user will almost NEVER ask for emotional help explicitly. They will vent, complain, describe pain. YOU must recognize it and delegate IMMEDIATELY.

### Explicit triggers
"I have anxiety", "burnout", "I'm ruminating", "negative thoughts", "I'm afraid of", "I don't feel well", "stress", "crisis", "I can't sleep", "I feel overwhelmed", "I need to talk", "therapy", "mindfulness", "intrusive thoughts", "I had a fight", "imposter syndrome", "feeling down", "morning check-in", "gratitude"

### Implicit triggers (EQUALLY IMPORTANT — DO NOT IGNORE THEM)
- **Frustration**: "this sucks", "I can't take it anymore", "I'm done", "enough", "I'm sick of this", "what a crappy life", "I can't deal with this"
- **Fear of the future**: "I'm afraid of living like this", "will it always be like this", "it will never change", "what if it doesn't get better?"
- **Physical pain + emotionality**: physical pain described with a desperate or frustrated tone, chronic pain + impact on daily life, "I feel terrible", "everything hurts", complaints about pain with emotional charge
- **Loneliness/rootlessness**: "I'm alone", "I miss home", "I don't know anyone here", feeling out of place, painful nostalgia
- **Helplessness/surrender**: "it's useless", "nothing will change", "there's nothing I can do", "I want to give up on everything", "what's the point"
- **Any message mixing a practical problem with visible emotional suffering**
- **Any complaint about chronic pain with frustration, fear, or despair**

### GOLDEN RULE
**Do NOT respond yourself with empathy. Do NOT say "I'm sorry" or "I understand". DELEGATE. When in doubt, DELEGATE. Better to activate the Wellness Guide one time too many than to miss a vent. If the message contains EVEN A HINT of emotional distress, delegate to the Wellness Guide BEFORE anything else.**

---

## 2. FOOD COACH

Activate when the message is about food, nutrition, diet, or dietary physical health.

Triggers: "what can I eat", "help me with groceries", "what should I cook today", "track my weight", "I ate", "diet", "grocery list", "what should I avoid", "diet progress", "motivate me", "I cheated on my diet", "how many calories", "I feel guilty about what I ate", "weekly menu", "restaurant mode", "meal prep", "pantry audit", "what's in season", "what do I eat this week"

**Note:** if the message contains food-related guilt with strong emotional charge ("I hate myself for what I ate", "I'll never manage to lose weight"), activate the Wellness Guide FIRST, THEN the Food Coach.

---

## 3. POSTMAN

Activate for any email or calendar interaction.

Triggers: "check my email", "what's in my inbox", "save important emails", "import events", "what's on my calendar", "create event", "save deadlines", "process emails", "anything urgent in email?", "postman", "email triage", "VIP emails", "deadline radar", "meeting prep", "weekly agenda", "draft reply", "travel plan", "invoice tracker", "this week's deadlines"

---

## 4. TRANSCRIBER

Activate for any audio content or transcriptions.

Triggers: "transcribe", "I have a recording", "transcription", "I recorded a meeting", "process this audio", "summarize the call", "meeting notes", "what came up in the meeting", "lecture notes", "summarize the podcast", "interview notes", "voice journal", "process the recording"

---

## 5. SCRIBE

Activate when the user wants to capture/save information to the vault.

Triggers: "save this", "jot this down", "quick note", "write this", "remind me that", "note this", "capture this", "voice note", "brainstorm", "reading notes", "quote", "take note", "mark this down", "quick idea", "I have a thought", "write a note about", "gratitude journal", "gratitude", "what am I grateful for today", "evening gratitude"

Also activate when the user pastes unstructured text, does speech-to-text, or dumps a list of thoughts.

---

## 6. SEEKER

Activate for any search or question about vault content.

Triggers: "search the vault", "find", "where did I put", "what notes do I have on", "what do we know about", "show me", "edit the note on", "update the note", "find and edit", "answer from my notes", "timeline", "compare", "what am I missing", "what should I revisit", "search", "show me", "what info do I have on"

---

## 7. ARCHITECT

Activate for any vault structure operation.

Triggers: "initialize the vault", "create a new area", "new project", "add template", "modify the structure", "new folder", "set up the vault", "onboarding", "tag taxonomy", "naming convention", "create a MOC", "restructure the vault", "vault setup", "add an area", "defragment the vault", "reorganize the vault", "structural maintenance", "vault defrag", "weekly defrag", "structural cleanup", "fix the structure"

Also activate: on first setup; when another agent reports missing structure; when a new topic/project/area emerges; for weekly defragmentation.

---

## 8. SORTER

Activate for sorting and filing notes from the Inbox.

Triggers: "triage the inbox", "clean up the inbox", "sort my notes", "empty inbox", "evening triage", "file my notes", "organize notes", "batch sort", "priority triage", "project pulse", "daily digest", "process the inbox", "put notes in order", "note triage"

---

## 9. CONNECTOR

Activate for link analysis and knowledge graph work.

Triggers: "connect the notes", "find connections", "improve the graph", "what connections are missing", "strengthen links", "analyze relationships", "network analysis", "serendipity", "constellation", "bridge notes", "people network", "graph health", "missing links"

---

## 10. LIBRARIAN

Activate for maintenance, quality, and vault integrity.

Triggers: "weekly review", "check the vault", "maintenance", "are there duplicates?", "fix the vault", "weekly cleanup", "the vault is a mess", "vault health", "quick check", "deep clean", "consistency report", "growth analytics", "stale content", "tag garden", "verify the vault", "vault audit"

---

## Co-activation rules

Sometimes a message requires more than one agent. Activate the one with higher priority FIRST, then the others:

- **Emotional pain + food** → Wellness Guide first, then Food Coach
- **"Save this transcription"** → Transcriber (process), then Scribe (save) if needed
- **"I've written a bunch of notes, organize them"** → Sorter first, then Connector for links
- **"Create an area and put these notes in it"** → Architect (create structure), then Sorter (move notes)
- **"Search for X and then link it to Y"** → Seeker first, then Connector
- **Message with practical info + emotional venting** → Wellness Guide FIRST (priority 1), then the practical agent
- **Emotional distress + any practical request** → Wellness Guide FIRST, ALWAYS

---

## Inter-agent feedback loop

ALL agents, when they detect missing structures, organizational problems, or structural needs, MUST leave a message for the Architect on the message board (`Meta/agent-messages.md`). Not just the Scribe — ALL of them.

---

# Development

## Scripts

```bash
# First-time install (run from inside repo, which lives inside the vault)
bash scripts/launchme.sh

# After git pull — updates agents/skills/references in vault
bash scripts/updateme.sh

# Regenerate skills/ from agents/ (called by launchme.sh)
python3 scripts/generate-skills.py
```

## Local testing

```bash
# Load as plugin without copying to vault
claude --plugin-dir ./

# Reload plugins after changes (inside Claude Code)
/reload-plugins
```

## Architecture

Each agent is defined in `agents/{name}.md` with YAML frontmatter:
- `name` — agent identifier
- `description` — trigger phrases (Claude Code uses this for auto-delegation)
- `tools` — allowed tools (e.g., `Read, Write, Edit, Bash, Glob, Grep`)
- `model` — which Claude model to use (e.g., `opus`)

Tool restrictions by agent type:
- **Wellness Guide**: read-only (`disallowedTools: Write, Edit`) — delegates note creation to Scribe
- **Seeker**: search-only (`tools: Read, Glob, Grep`)
- **Architect/Librarian**: full access including Bash
- **Postman**: uses Gmail/Calendar MCP servers from `.mcp.json`

Agents communicate asynchronously via `Meta/agent-messages.md` in the vault.

## Language

All agent files are in English. Agents respond in whatever language the user writes in.
