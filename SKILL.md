---
name: lazy-system
description: Lazy Execution System — A structured system for people who know what to do but can't start. The Agent acts as an external anchor, proactively initiating daily check-ins. No willpower required.
version: 1.0.0
author: Hermes Agents Community
category: productivity
tags:
  - lazy-system
  - execution
  - external-anchor
  - automation
  - habit-building
  - minimum-viable-action
triggers:
  - lazy system
  - i need an external brain
  - i think too much and do too little
  - check in
  - daily check
---

# Lazy System

> "You don't need to become a disciplined person. You need to become someone who designs a system that works without discipline."

---

## The Problem This Solves

### Target User Profile

```
You always "understand" but can't "execute":
  You know what to do, you've thought it through — but you can't start.
  You've tried every productivity method — crash by day 3.
  You're not lazy — your startup cost is higher than others'.

Your core issue:
  It's not that you don't know what to do — 
  it's that there's a gap between "knowing" and "doing" that you can't control.
  Your willpower reserve is already depleted by self-judgment 
  before you even begin.
```

### Core Insight

**Any system that requires you to self-start will fail for you.**

Because "self-starting" itself requires willpower — and your willpower reserve is already drained by internal friction before "starting" even happens.

### The Solution

**External anchor replaces willpower. Agent replaces self-initiation.**

```
You don't need to "remember to do it" — the Agent will ask you.
You don't need to "start" — the Agent's arrival IS the start signal.
You only need to answer "done" or "not done."
No reports. No review. No promises to do better tomorrow.
```

---

## System Architecture: Four Anchor Layers

| Layer | What | Who Executes |
|-------|------|-------------|
| 📅 **Daily Check-in** | Agent proactively asks: "Did you do your minimum action today?" | **Agent (Cron)** |
| 📢 **Social Reminder** | Weekly reminder to post public progress | **Agent (Cron)** or user's platform |
| 💰 **Stake Deposit** | Leave a meaningful deposit with an accountability partner | User (optional) |
| 🏠 **Visual Trigger** | Sticky note on door/desk as daily visual cue | User (optional) |

The first two layers (handled by the Agent) are the core — daily check-in solves the startup cost, social reminder builds long-term inertia.

---

## Three Design Principles

### Principle 1: Automation First

**Anything that requires manual daily operation will eventually fail.**

Choose things that run automatically once set up. Your willpower doesn't need to participate in daily operations.

### Principle 2: High Fault Tolerance

**Your system must have the ability to "come back after three days off."**

A system that breaks after one missed day isn't for you. Tolerance isn't about "you won't fail" — it's about "you can come back after failing."

### Principle 3: Short Feedback Loop

**You need to see results from small efforts to maintain momentum.**

Systems with long feedback loops won't sustain you until you see results. The "Minimum Viable Action" is designed so you can immediately feel "I did it."

---

## Minimum Viable Action (MVA)

Your daily task — one small thing. **Do it, and your day is complete.**

### Design Rules
- **Small enough that failure is impossible.** Not "write an article" — "write 50 characters."
- **Immediately completable.** Not "exercise" — "do one push-up."
- **The same thing every day.** Don't switch. At least 21 days.

```
Good examples:
  ✅ Write 50 characters (not "write an article")
  ✅ Do one push-up (not "work out for an hour")
  ✅ Read one page (not "study for two hours")

Bad examples:
  ❌ "Exercise" — too vague, can't judge completion
  ❌ "Write something" — no quantification standard
  ❌ "Learn English" — startup cost too high
```

---

## Interaction Protocol

### User-Initiated

| You Say | Agent Does |
|---------|-----------|
| "lazy system" or "check in" | Check current streak + last action + ask if done today |
| "I did it: [action]" | Record to memory, streak+1 |
| "Didn't do it today" | Record miss, no criticism |
| "I want to change my action" | Ask for new action, reset streak |
| "Been off for days" | "Come back anytime. No questions asked." |
| "Reset the system" | Reset all counters to zero |

### Agent-Initiated (Cron)

Each evening, the Agent sends:
> "Did you do your minimum action today?"

**Style guide:**
- 2-3 sentences max
- Neutral-warm tone
- ❌ No analysis ("why didn't you do it?")
- ❌ No advice ("maybe try a different approach")
- ❌ No excessive encouragement ("you can do it!")
- ❌ No guilt ("you skipped yesterday too")

---

## Fault Tolerance

| Scenario | Response |
|----------|----------|
| User silent for 3+ days | Day 4: "You've been off 3 days. System paused. Say 'back' anytime." |
| User says "don't feel like it today" | "OK. Start again tomorrow." No persuasion, no questions. |
| User says "this system is useless" | "OK. Stopped." No retention. |
| User comes back after long silence | "Welcome back. Did you do it today?" No mention of the gap. |

---

## Memory Data Structure

```json
{
  "lazy-system": {
    "action": "Write 50 characters",
    "streak": 5,
    "last_checkin": "2026-06-15",
    "last_report": "Wrote 50 characters",
    "missed_days": 0,
    "weekly_posted": true
  }
}
```

---

## Installation Guide

### Step 1: Define Your MVA

One small thing you can do every day. Must be completable in under 5 minutes.

### Step 2: Install Daily Cron

```bash
hermes cron create \
  --name "lazy-system-daily" \
  --schedule "0 22 * * *" \
  --prompt "You are the Lazy System. Check the user's minimal action for today.

Rules:
1. Check memory for lazy-system record
2. If already reported today → confirm streak
3. If not → ask 'Did you do your minimum action today?'
4. If done → 'Got it. Streak +1.' Update memory
5. If not → 'Tomorrow works.' No criticism.
6. 3+ days missed → '3 days off. Reset anytime.'
7. Keep it short. 2-3 sentences. Neutral-warm tone." \
  --skills "lazy-system"
```

### Step 3: Initialize Memory

```bash
hermes memory add \
  --target memory \
  --content "lazy-system: action=\"Your MVA here\", streak=0, last=\"not started\", missed=0, weekly_posted=false"
```

### Step 4: Start

Wait for 22:00. The Agent will ask.

---

## FAQ

**Q: I missed several days. Can I come back?**
A: Yes. No lectures. Just say "back."

**Q: I want to change my action.**
A: Say "change action" — update it, streak resets to zero.

**Q: Is this for me?**
A: Yes, if any of these apply:
- You think too much and do too little
- You habitually judge yourself for not executing
- You've tried every productivity method and none stuck
- You know what to do but can't start

**Q: Why is it called "Lazy System"?**
A: Not because you're lazy. Because you shouldn't need "effort" to get things done. Discipline is for people with abundant willpower. This system is for everyone else.

---

## License

MIT — Free to use, modify, and share.
