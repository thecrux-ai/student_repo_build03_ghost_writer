# Build 3: Conceptual Map — What Just Happened (and Why)

**Read time:** 10 minutes | **When to read:** After completing Build 3, or if you want to understand why voice capture and slash commands change how you use AI.

---

## The One-Sentence Version

You taught Claude to write like a specific human — not by describing a style, but by showing it examples and letting it reverse-engineer the patterns.

---

## The Three Mental Models Behind This Session

### 1. Voice Is a Pattern, Not a Feeling

Most people describe their writing style in vague terms: "professional but friendly," "direct," "casual." These descriptions are useless for an AI because they're useless for anyone. Tell a new hire to write "professional but friendly" emails for you and you'll get generic corporate mush.

What you did in this session was different. You gave Claude **examples** and asked it to find the **patterns** — the specific, observable habits that make writing sound like a particular person.

```
VAGUE DESCRIPTION                    VOICE FINGERPRINT
"Write in a direct,                  - Opens with data, never "I'm writing to..."
professional tone"                   - Sentences average 8-12 words
                                     - Uses "My read:" before giving opinions
    |                                - Parenthetical asides for context (like this)
    v                                - Closes with specific next step + question
Generic professional email.          - Admits mistakes with "Just being transparent"
Could be from anyone.                    |
                                         v
                                     Email that sounds like Arjun.
                                     Recognizably him.
```

This is the core insight: **voice is not a feeling you describe — it's a set of patterns you can observe and replicate.** Opening patterns. Sentence length. Signature phrases. Punctuation habits. How someone handles bad news versus good news. These are concrete, measurable things.

**The principle:** When you want AI to match someone's style, don't describe the style — show examples and let the AI reverse-engineer the patterns. This works for your voice, your CEO's voice, your company's brand voice, a client's tone. Anyone whose writing you can collect 5-10 samples of.

---

### 2. Skills Turn Conversations Into Capabilities

Here's the problem with getting Claude to write in your voice through conversation: it works, but it's ephemeral. Tomorrow you'd have to explain your voice patterns all over again. Next week, the analysis is gone.

Slash commands (skills) solve this. A skill is a markdown file that Claude reads every time you invoke it. The voice fingerprint, the formatting rules, the "what to never do" list — all captured in a file, all loaded automatically.

```
WITHOUT A SKILL                      WITH A SKILL
    |                                    |
    v                                    v
"Write an email to Deepak.          /email-ghostwriter Follow up with
Use a direct tone. Open with         Deepak about the renewal. Mobile
data. Don't be too formal.           fix shipped, crash rate down 94%.
End with next steps. Make it
sound like me..."
    |                                    |
    v                                    v
Re-explain your voice               Skill file loads your voice
every single time.                   fingerprint automatically.
    |                                    |
    v                                    v
Inconsistent results.                Consistent results.
Context lost between sessions.       Context preserved forever.
```

**The architecture is simple:**

```
~/.claude/commands/              <-- Global: works in every project
    email-ghostwriter.md
    linkedin-ghostwriter.md
    meeting-followup.md

.claude/commands/                <-- Project: works only in this folder
    generate-api-docs.md
    code-review.md
```

A skill file is just markdown — instructions for Claude with a `$ARGUMENTS` placeholder where your specific request goes. No code. No configuration. No API calls. Just a text file in the right folder.

**The principle:** If you give Claude the same instructions twice, make it a skill. Every repeated instruction is a skill waiting to be built. Capture it once, use it forever.

**The mental model for when to use which location:**

| Location | When to use | Example |
|----------|-------------|---------|
| Global (`~/.claude/commands/`) | Skills that are about YOU — your voice, your habits, your formats | `/email-ghostwriter`, `/weekly-update`, `/meeting-followup` |
| Project (`.claude/commands/`) | Skills specific to one workspace or project | `/generate-changelog`, `/review-pr`, `/draft-release-notes` |

---

### 3. The A/B Test Reveals the Gap

The most convincing moment in this session wasn't building the skill. It was the **side-by-side comparison** — the same email written with the skill and without it.

Without the skill, Claude writes a perfectly competent professional email. Correct grammar. Clear structure. Appropriate tone. And completely generic. It could be from anyone. It sounds like AI.

With the skill, Claude writes an email that sounds like a specific human. It opens the way that person opens. It uses their phrases. It handles difficult topics the way they handle difficult topics. It closes the way they close. You could forward it and the recipient wouldn't know you didn't write it.

**Why the gap matters:**

The generic email is what everyone gets from AI. It's the baseline. It's useful but undifferentiated — your AI emails sound like everyone else's AI emails.

The skill-based email is what happens when you invest 30 minutes in teaching Claude your voice. It's personalized. It's distinctive. It saves you the hardest part of writing — not the facts or the structure, but the *voice*. Getting the words to sound like you.

**The principle:** AI's default output is competent and generic. A skill file is how you move from generic to personal. The investment is small (30 minutes to build, 5 minutes to refine). The payoff is permanent (every email, every post, every draft starts from "sounds like you" instead of "sounds like AI").

---

## What's Actually Happening Under the Hood

**Voice analysis as pattern recognition:** When Claude read 10 writing samples and identified Arjun's patterns, it was doing large-scale pattern recognition across multiple documents. It wasn't looking for what Arjun *said* — it was looking for *how he said it*. The difference between content analysis ("Arjun talked about Project Alpha") and style analysis ("Arjun opens with data, uses parenthetical asides, and admits mistakes with specific phrases") is fundamental. Style analysis requires comparing patterns across multiple documents to find what's consistent regardless of topic.

**$ARGUMENTS as a simple but powerful pattern:** The `$ARGUMENTS` placeholder in a skill file is elegant because it separates the *how* from the *what*. The skill file captures how you write (voice, structure, rules). The argument captures what you want to write about (the specific email or post). This separation means the skill works for any topic — a client follow-up, a team update, a difficult conversation — without modification.

**The iteration loop:** When you asked Claude to compare its generated emails against the original samples and identify gaps, you created a feedback loop. Claude evaluates its own output against a reference standard and updates its own instructions. This is a pattern worth remembering: Claude can critique its own work and improve the system that produced it.

**Why 5-10 samples is the sweet spot:** Fewer than 5 samples and Claude doesn't have enough data to distinguish personal patterns from situational ones. (Did Arjun use "My read:" because that's his style, or because that one email called for it?) More than 10 samples shows diminishing returns — by 10, the stable patterns have emerged and additional samples mostly confirm what Claude already found. The exception: if the person writes very differently across contexts (formal client emails vs. casual team Slack), you may need samples from each context.

---

## The Repeatable Pattern

The process you used today works for any writing voice, not just yours:

```
1. GATHER       Collect 5-10 writing samples across different contexts
                (formal, casual, good news, bad news, short, long)

2. ANALYZE      Claude reads all samples and identifies distinctive patterns
                Not "what did they say" but "HOW do they say it"

3. FINGERPRINT  Structure the patterns into a reference document
                Tone, openings, sentence structure, phrases, closings

4. BUILD        Convert the fingerprint into a skill file with $ARGUMENTS
                Include "what to never do" — the anti-patterns are as important
                as the patterns

5. TEST         Generate content and compare against original samples
                Does it pass the "would the person recognize this as theirs?" test

6. ITERATE      Claude critiques its own output against originals
                Update the skill file to close gaps
```

**This pattern applies beyond writing.** The same logic — analyze examples, extract patterns, encode them, test, iterate — works for:

- **Analysis style** — How does your CFO want financial analysis structured?
- **Decision frameworks** — How does your team evaluate proposals?
- **Feedback style** — How does your manager give code reviews?
- **Presentation format** — How does your company structure pitch decks?

Anywhere there's a "how we do things" that you currently carry in your head, the pattern applies: show Claude examples, let it extract the patterns, encode them in a skill file.

---

## Why This Matters More Than It Looks

Ghost writing might seem like a narrow use case — "okay, Claude can write emails that sound like me, that's nice." But the underlying capability is much bigger.

What you actually built is a system for **encoding tacit knowledge**. Your writing voice is tacit knowledge — you know it when you see it, but you've never written it down. The voice fingerprint made it explicit. The skill file made it executable. The iteration loop made it accurate.

This is the same pattern that makes CLAUDE.md powerful (encode your preferences), that makes the second brain work (encode your organizational system), and that will make Build 4 and 5 powerful (encode your workflows and creative process). **The skill file is just the most tangible example of a general principle: make the implicit explicit, and Claude can use it.**

---

## The Takeaway

You didn't build an email template today. You built something more fundamental:

> **A system for capturing how a specific human communicates — and making it reproducible on demand. The voice fingerprint is the insight. The skill file is the mechanism. The iteration loop is what makes it accurate.**

The draft Claude produces isn't the final product — you are. But now your editing starts from something that already sounds like you, not like a robot. That's the difference between AI that replaces your voice and AI that amplifies it.

---

*This document is a reference. Come back to it when you want to build a new skill, capture someone else's voice, or understand why your skill file isn't producing the right output.*
