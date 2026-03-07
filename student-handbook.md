# Build 03: Ghost Writer — Student Handbook

## What You'll Build

In the next 60 minutes, you'll teach Claude Code to write like a specific person — first using a sample persona, then using YOUR own writing voice. You'll build two slash commands (skills) that generate emails and LinkedIn posts that sound authentically human.

**By the end of this session, you'll have:**
- Two working slash commands in `.claude/commands/`
- A repeatable process for capturing ANY writing voice
- Skills that write first drafts sounding like you (not like AI)

**Prerequisites:**
- Claude Code installed and working
- This repository cloned to your machine
- Familiarity with basic Claude Code usage (prompting, reading files)

---

## How This Session Works

| Part | Time | What You'll Do |
|------|------|----------------|
| Part 1 | 10 min | Claude reads Arjun's writing samples and discovers his voice patterns |
| Part 2 | 15 min | Build both ghost writer skills (email + LinkedIn) and test them |
| Part 3 | 20 min | Swap in YOUR voice |
| Part 4 | 15 min | Compare, refine, and make skills permanent |

---

## Before You Start

Clone the repository to your machine (if you haven't already):

```bash
git clone https://github.com/thecrux-ai/student_repo_build03_ghost_writer.git
```

Navigate into the repository:

```bash
cd student_repo_build03_ghost_writer
```

Open Claude Code:

```bash
claude
```

Take a quick look at what's in the repo:

```
Tell me what files are in this repository and give me a brief overview of its structure
```

You should see the `writing-samples/` directory with emails and LinkedIn posts, plus `casestudy.md` and this handbook. You should NOT see a `.claude/commands/` directory — you'll create that yourself.

---

# Part 1: Arjun's Voice — See What Claude Discovers (10 min)

## You Know Arjun

You already met Arjun Mehta in Build 1 — VP of Product, Series B B2B SaaS company, drowning in messy files. You organized his chaotic workspace. Now you're going to teach Claude to write like him.

Read the case study for a quick refresher on his voice patterns:

```
Read casestudy.md and give me a brief summary of Arjun's voice patterns
```

Arjun is direct, data-driven, and action-oriented. He leads with numbers, admits his mistakes, and always ends with next steps. He has a distinctive voice — and Claude is about to figure out exactly what makes it distinctive.

## Step 1: Claude Reads All Writing Samples

Ask Claude to read everything:

```
Read all 10 files in the writing-samples/ directory — both the emails/ and linkedin-posts/ folders. Don't summarize them yet, just read them all.
```

This loads all of Arjun's writing into Claude's context. Claude now has 10 different examples of his voice across different formats and situations.

## Step 2: Discover the Voice Patterns

Now ask Claude to analyze:

```
Based on all 10 writing samples you just read, identify the distinctive patterns in Arjun's writing voice. Look at:

- How he opens emails vs LinkedIn posts
- His sentence structure and rhythm
- Specific phrases or transitions he repeats
- How he uses numbers and data
- How he closes (emails vs posts)
- His punctuation habits (especially parenthetical asides)
- His tone and how it shifts across different contexts
- How he handles admitting mistakes or taking accountability

Be specific — quote examples from the samples to support each pattern you identify.
```

**What to watch for**: Claude should identify most (if not all) of Arjun's 7 voice patterns listed in `casestudy.md`. It might also find patterns you didn't expect — that's a feature, not a bug.

## Step 3: Create the Voice Fingerprint

Ask Claude to structure its findings:

```
Now organize those patterns into a structured "voice fingerprint" — a clear reference document that could be used to write new content in Arjun's voice. Format it as a markdown document with specific sections for tone, opening patterns, sentence structure, signature phrases, parenthetical style, closing patterns, and self-awareness patterns.
```

**Keep this fingerprint in your conversation** — you'll use it in the next step to build the skill file.

### Pause and Reflect

Look at the voice fingerprint Claude created. Compare it to the 7 patterns listed in `casestudy.md`.

- Did Claude catch all 7?
- Did it find anything extra that's genuinely insightful?
- Is there a pattern you see in the samples that Claude missed?

If Claude missed something, tell it! This is the iteration process.

---

# Part 2: Build Both Ghost Writer Skills (15 min)

## How Slash Commands Work (60-second explainer)

Claude Code slash commands (also called "skills") are markdown files that live in a `.claude/commands/` directory. When you type `/command-name` in Claude Code, it reads that file and uses it as instructions.

**Three things to know:**

1. **Location**: `.claude/commands/` in your project directory (project-level) or `~/.claude/commands/` in your home directory (global — works everywhere)
2. **Format**: Regular markdown files with instructions for Claude
3. **Arguments**: Use `$ARGUMENTS` in the file as a placeholder — whatever the user types after the slash command gets inserted there

Example: If `email-ghostwriter.md` contains "Write an email about: $ARGUMENTS" and you type `/email-ghostwriter follow up with Deepak about the renewal`, Claude sees "Write an email about: follow up with Deepak about the renewal".

That's it. No code. No configuration. Just a markdown file in the right folder.

**Important: Slash commands are loaded when Claude Code starts.** If you create a new command file during a session, you need to exit Claude Code and restart it before the new slash command will be available. This is a one-time thing — after restarting, the command works for all future sessions.

## Step 1: Create the Commands Directory

```
Create the .claude/commands/ directory in this project
```

## Step 2: Build the Email Skill

Now ask Claude to build the skill using the voice fingerprint from Part 1:

```
Using the voice fingerprint we created for Arjun, build a slash command skill file for writing emails in his voice.

The file should be saved as .claude/commands/email-ghostwriter.md and include:
- The voice profile (tone, openings, sentence structure, signature phrases, parenthetical style, closings, self-awareness)
- A $ARGUMENTS placeholder for the email request
- Guidance on adapting the voice for different email types (client, team, pushback, personal, difficult)
- A "what to never do" section

Make it detailed enough that someone who has never read Arjun's writing could use this skill and produce an email that sounds like him.
```

## Step 3: Build the LinkedIn Skill

Now build the second skill — same voice, different format:

```
Using the same voice fingerprint, build a slash command skill file for writing LinkedIn posts in Arjun's voice. Save it as .claude/commands/linkedin-ghostwriter.md.

LinkedIn posts are different from emails — they need a scroll-stopping hook, shorter paragraphs, and a closing question that drives engagement. Adapt Arjun's voice patterns to the LinkedIn format while keeping his core identity — especially the data-first framing, the honest self-awareness, and the signature phrases.

Include $ARGUMENTS, post type guidance, formatting rules for LinkedIn, and a "what to never do" section.
```

## Step 4: Restart Claude Code

Slash commands are loaded when Claude Code starts — so your new commands won't be available until you restart. The good news: we built both skills before restarting, so one restart loads both `/email-ghostwriter` and `/linkedin-ghostwriter`.

```bash
# Type /exit or press Ctrl+C to leave Claude Code, then reopen it:
claude
```

Once Claude restarts, both slash commands will be ready to use.

## Step 5: Test — Acme Follow-Up Email

Time to see if it works. Use the slash command:

```
/email-ghostwriter Write a follow-up email to Deepak Sharma at Acme Corp. The mobile fix shipped on time (crash rate down 94%), and Arjun wants to schedule a call to discuss the renewal pricing options before the March 31 deadline. Include the loyalty pricing adjustment and the Project Alpha early access offer.
```

**Evaluate the output**: Does it sound like Arjun? Check for:
- [ ] Opens with data or specific evidence (not "I'm writing to update you on...")
- [ ] Short declarative sentences, structured and direct
- [ ] "My read:" or "Just being transparent" used naturally
- [ ] Specific numbers used throughout
- [ ] Parenthetical asides for context and deadlines
- [ ] Ends with clear next steps and a specific question
- [ ] Honest and direct tone — no jargon

## Step 6: Test — Difficult Conversation with Suresh

Different email type, same voice:

```
/email-ghostwriter Write an email to Suresh about a new issue: the self-serve onboarding API changes are behind schedule. Rohit's platform team has a bandwidth conflict between Project Alpha and the payment gateway. Arjun needs Suresh to reallocate two engineers for 3 weeks. He knows this is a big ask and wants to make the case with data, not authority.
```

**Compare**: Does the voice hold across a completely different email type? The empathy-to-directness ratio should shift (more empathy here since it's a big ask), but the core patterns should remain.

## Step 7: Test — LinkedIn Post

Now test the LinkedIn skill:

```
/linkedin-ghostwriter Write a post about how Project Alpha (self-serve onboarding) just hit 82% completion rate after the team pivoted to video walkthroughs based on Meera's user research. This is a win for listening to data over assumptions. Keep it honest — mention the 34% completion rate they started with and what Arjun got wrong initially.
```

**Check**: Does it have a scroll-stopping opening? Does it end with a real question? Does it sound like Arjun's LinkedIn posts, not a generic corporate announcement?

## Step 8: Iterate

Claude will probably get 80% right on the first try. Let's improve it:

```
Read the two emails you just generated. Compare them against the original writing samples in writing-samples/emails/. Identify any gaps — places where the generated emails don't quite match Arjun's voice patterns. Then update the skill file at .claude/commands/email-ghostwriter.md to address those gaps.
```

This is the key insight: **Claude can critique its own output against the original samples and improve the skill file.**

---

# Part 3: Swap In YOUR Voice (20 min)

## THE SWAP: Your Voice Now

This is the part where it gets personal.

### Option A: You Have Writing Samples (Preferred)

If you have 5+ emails you've written (check your Sent folder), paste them into the conversation:

```
I'm going to paste 5 of my own emails below. I want you to analyze my writing voice the same way you analyzed Arjun's — identify my distinctive patterns, create a voice fingerprint, and then rebuild the email-ghostwriter.md skill file to match MY voice instead of Arjun's.

Here are my emails:

[Paste email 1]

---

[Paste email 2]

---

[Paste email 3]

---

[Paste email 4]

---

[Paste email 5]
```

**Tips for choosing your emails:**
- Pick emails from different contexts (formal, casual, good news, bad news)
- Don't cherry-pick your "best" writing — include normal everyday emails
- Remove sensitive information (client names, financial details) but keep the voice intact
- Longer emails give Claude more signal than one-liners

### Option B: No Writing Samples Handy

If you don't have emails ready, dictate your style to Claude:

```
I don't have writing samples handy, so I'll describe my writing style. Build a voice profile from this description:

- [How would you describe your writing tone?]
- [Do you use formal or casual language? Contractions?]
- [How do you typically open emails?]
- [Any phrases or words you use frequently?]
- [How do you close emails?]
- [Any punctuation habits? (em-dashes, ellipses, exclamation marks)]
- [What do you NEVER want your emails to sound like?]
```

Option A will produce a more accurate skill file, but Option B is a perfectly good starting point that you can refine over time.

### Step 3: Rebuild the Skill

After Claude analyzes your voice (or your description), tell it:

```
Now rebuild .claude/commands/email-ghostwriter.md to match MY voice instead of Arjun's. Keep the same structure but replace all the voice patterns with mine.
```

### Step 4: Test on a Real Email

Think of an email you actually need to write this week. Use the skill:

```
/email-ghostwriter [Describe the email you actually need to write]
```

**The moment of truth**: Does it sound like you? Not perfect-you, but recognizably-you?

If it's close but not quite right, tell Claude what's off:

```
That's close, but I would never [specific thing]. I tend to [your actual habit]. Update the skill file to reflect this.
```

### Step 5: LinkedIn (If You Post)

If you use LinkedIn, repeat the process:

```
Now rebuild .claude/commands/linkedin-ghostwriter.md for my voice. [Paste LinkedIn posts or describe your style]
```

If you don't post on LinkedIn, use this time to refine your email skill further. More iteration = better results.

---

# Part 4: Compare, Refine, Make Permanent (15 min)

## Step 1: Compare Against the Reference

Now you can peek at the reference files:

```
Read the files in reference-skills/ and compare them against my skill files in .claude/commands/. What are the key differences? What did the reference files include that mine are missing? What did mine include that the reference files don't have?
```

Neither version is "correct" — the reference files are one good approach. Your files might be better in some areas. The comparison is about learning, not scoring.

## Step 2: The A/B Test

This is the most convincing demonstration of what skills can do:

```
Write the same email two ways:

First, write a follow-up email to a client named Deepak Sharma who is considering switching to a competitor. We've fixed the mobile issues he raised, and we want to schedule a renewal discussion before March 31.

Write it ONCE using my /email-ghostwriter skill.

Then write it AGAIN as a generic, well-written professional email WITHOUT using the skill — just write it like a standard AI assistant would.

Show both versions side by side.
```

**Look at them side by side.** The skill version should sound like a specific human. The generic version should sound like... AI. This is the difference a skill file makes.

## Step 3: Make It Permanent

Your skills currently live in this project's `.claude/commands/` directory. They'll only work when you're in this project folder. To make them available everywhere:

```bash
# Create global commands directory if it doesn't exist
mkdir -p ~/.claude/commands

# Copy your skills to the global location
cp .claude/commands/email-ghostwriter.md ~/.claude/commands/
cp .claude/commands/linkedin-ghostwriter.md ~/.claude/commands/
```

Now `/email-ghostwriter` and `/linkedin-ghostwriter` will work in ANY project you open with Claude Code. (Remember: restart Claude Code after copying for the commands to load.)

**Project vs Global — when to use which:**

| Location | Path | When to Use |
|----------|------|-------------|
| Project | `.claude/commands/` | Skills specific to one project (e.g., "generate API docs for this codebase") |
| Global | `~/.claude/commands/` | Skills you want everywhere (e.g., your ghost writer, meeting notes formatter) |

## Step 4: Brainstorm More Skills

You've now built two skills and learned the pattern. What else could Claude build for you?

```
Based on the skill-building pattern we've used in this session (writing samples → voice analysis → skill file → test → iterate), brainstorm 5 other slash commands I could build for my daily work. Be specific and creative — think about repetitive writing tasks I probably do every week.
```

Some ideas to get you thinking:
- `/meeting-followup` — Generates follow-up emails from meeting notes
- `/code-review` — Reviews code in your team's feedback style
- `/weekly-update` — Writes your weekly status update in your voice
- `/slack-response` — Drafts Slack messages matching your team's communication style
- `/job-description` — Writes job postings in your company's voice

---

## Takeaways

### What Makes a Great Skill File

| Do This | Not This |
|---------|----------|
| Specific patterns with examples: "Uses parenthetical asides for deadlines" | Vague instructions: "Write naturally" |
| Concrete numbers: "Paragraphs of 1-3 sentences" | Ambiguous ranges: "Keep it concise" |
| "Never" list with specific anti-patterns | No guardrails — Claude will default to generic |
| Format-specific guidance (email vs post) | One-size-fits-all instructions |
| `$ARGUMENTS` for flexible input | Hardcoded topics or recipients |

### The Skill-Building Habit

Here's a simple rule:

> **If you give Claude the same instructions twice, make it a skill.**

Every time you find yourself typing "write this in a casual tone" or "make it sound more direct" or "don't use corporate jargon" — that's a skill waiting to be built. Capture it once, use it forever.

### The Repeatable Pattern

The process you used today works for any writing voice:

1. **Gather samples** — 5-10 examples of the target voice across different contexts
2. **Analyze** — Claude identifies distinctive patterns and creates a voice fingerprint
3. **Build** — Convert the fingerprint into a skill file with `$ARGUMENTS`
4. **Test** — Generate content and compare against original samples
5. **Iterate** — Claude critiques its own output and refines the skill

This works for your voice, your CEO's voice, your client's voice, your company's brand voice — anyone whose writing you can collect samples of.

### Where Your Skills Live

```
Project-level (this project only):
  .claude/commands/email-ghostwriter.md
  .claude/commands/linkedin-ghostwriter.md

Global (all projects):
  ~/.claude/commands/email-ghostwriter.md
  ~/.claude/commands/linkedin-ghostwriter.md
```

---

## Bonus: If You Have Time

### Build a Meeting Follow-Up Skill

If you finished early, try building one more skill from scratch:

```
Build a new slash command at .claude/commands/meeting-followup.md that takes meeting notes as $ARGUMENTS and generates a follow-up email in my voice. It should:

- Summarize key decisions and action items
- Use my writing voice (from the email-ghostwriter skill)
- Assign clear owners and deadlines for each action item
- End with a question about the next meeting or next steps

Test it with notes from your last meeting.
```

This reinforces the pattern: identify a repetitive writing task → build a skill → test → iterate.

---

## Quick Reference

**Create a project skill:**
```bash
mkdir -p .claude/commands
# Then ask Claude to create a .md file in that directory
```

**Create a global skill:**
```bash
mkdir -p ~/.claude/commands
# Copy or create .md files in that directory
```

**After creating or copying a skill file, restart Claude Code** — slash commands are loaded at startup and won't appear until you exit and reopen.

**Use a skill:**
```
/skill-name your arguments here
```

**The `$ARGUMENTS` placeholder:**
Whatever you type after `/skill-name` replaces `$ARGUMENTS` in the skill file.

**Iterate on a skill:**
```
Read the skill file at .claude/commands/[name].md, test it with a prompt, identify what's off, and update the skill file.
```

---

*You've just built your first AI ghost writer. The draft it produces isn't the final product — you are. But now your editing starts from something that already sounds like you, not like a robot. That's the difference.*
