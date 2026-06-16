# Lazy System 🛋️

> **You don't need to become a disciplined person. You need to become someone who designs a system that works without discipline.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Hermes Agent](https://img.shields.io/badge/Hermes%20Agent-Skill-blue)](https://hermes-agent.nousresearch.com)

A **Lazy Execution System** for people who know what to do but can't start. The Agent (AI assistant) acts as an external anchor, proactively initiating daily check-ins — so you don't have to rely on willpower.

---

## The Problem

If you've ever:

- Known exactly what you need to do, but couldn't start
- Tried every productivity method and crashed by day 3
- Been told you're "lazy" when you know you're not
- Felt your willpower drained before you even begin

**This system is for you.**

The core insight is simple: **any system that requires you to self-start will fail for you.** Because "self-starting" itself requires willpower — and your willpower reserve is already depleted by internal friction before "starting" even happens.

---

## The Solution

**External anchor replaces willpower. Agent replaces self-initiation.**

```
┌─────────────────────────────────────────────────────────┐
│  You don't need to "remember to do it"   → Agent asks   │
│  You don't need to "start"              → Agent arrives │
│  You only answer: "done" or "not done"                  │
│  No reports. No reviews. No promises.                   │
└─────────────────────────────────────────────────────────┘
```

---

## How It Works

### System Architecture

| Layer | What | Who Executes |
|-------|------|-------------|
| 📅 **Daily Check-in** | Agent asks: "Did you do your minimum action today?" | **Agent (Cron)** |
| 📢 **Social Reminder** | Weekly public progress post | **Agent (Cron)** — optional |
| 💰 **Stake Deposit** | Meaningful financial stake with an accountability partner | You (optional) |
| 🏠 **Visual Trigger** | Sticky note on door/desk | You (optional) |

### Three Design Principles

| Principle | Why It Works |
|-----------|-------------|
| **⚡ Automation First** | Anything requiring manual daily ops will eventually fail. Set it once, let it run. |
| **🛡️ High Fault Tolerance** | The system must survive a 3-day break. One missed day shouldn't break everything. |
| **🎯 Short Feedback Loop** | You need to see results from small efforts. "Done" feels good immediately. |

---

## Getting Started

### Step 1: Define Your Minimum Viable Action (MVA)

One small thing, every day. **Small enough that failure is impossible.**

| ✅ Good Examples | ❌ Bad Examples |
|-----------------|----------------|
| Write **50 characters** (not "write an article") | "Exercise" — too vague |
| Do **one push-up** (not "work out for an hour") | "Study" — no completion criteria |
| Read **one page** (not "study for two hours") | "Work on project" — infinite scope |

### Step 2: Install the Daily Cron

```bash
hermes cron create \
  --name "lazy-system-daily" \
  --schedule "0 22 * * *" \
  --prompt "You are the Lazy System. Rules: 1. Check memory for lazy-system record. 2. If reported today → confirm streak. 3. If not → ask 'Did you do your minimum action today?' 4. If done → 'Got it. Streak +1.' 5. If not → 'Tomorrow works.' No criticism. 6. 3+ days missed → '3 days off. Reset anytime.' Keep it short. 2-3 sentences. Neutral-warm tone." \
  --skills "lazy-system"
```

### Step 3: Initialize Memory

```bash
hermes memory add \
  --target memory \
  --content 'lazy-system: action="Write 50 characters", streak=0, last="not started", missed=0, weekly_posted=false'
```

### Step 4: Wait for 22:00

The Agent will ask. You just answer.

---

## Interaction Reference

| You Say | What Happens |
|---------|-------------|
| `check in` or `lazy system` | See current streak + last action + today's status |
| `I did it: [action]` | Streak +1. Recorded to memory. |
| `Didn't do it today` | Miss recorded. No criticism. |
| `Change my action to: [new]` | Update your MVA. Streak resets. |
| `Reset` | All counters to zero. Fresh start. |
| `Back` | Resume after a break. Gap is ignored. |

---

## FAQ

### I missed several days. Can I come back?
Yes. No questions asked. Just say "back." The system doesn't shame.

### What if I want to change my action mid-cycle?
Say "Change my action to: [new thing]." Streak resets to zero — intentionally. This prevents you from keeping an action that's too big/too vague.

### Is this for me?
Yes, if any of these apply:
- You think too much and do too little
- You've tried every productivity system and none stuck
- You know what to do but can't start
- You beat yourself up for not executing

### Why is it called "Lazy System"?
Not because you're lazy — because you shouldn't need "effort" to get things done. Discipline is for people with abundant willpower. This is for everyone else.

### Does this work with other AI assistants?
Currently designed for **Hermes Agent**. The cron-based check-in pattern can be adapted to any AI assistant that supports scheduled tasks and cross-session memory.

---

## Contributing

This is a community skill. Feel free to fork, adapt, and improve. The core insight (external anchor > willpower) is universal — implementations will vary.

PRs welcome for:
- Support for other AI agents (Claude Code, Codex, etc.)
- Alternative delivery channels (Discord bot, SMS, etc.)
- Language translations
- Analytics / streak visualization

---

## License

MIT — Free to use, modify, and share.

---

*Made by people who think too much and do too little. For people who think too much and do too little.*
