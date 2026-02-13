# ADHD Focus Workflow Agent
### An agentic AI workflow to help ADHD users prioritize tasks, build structured focus sessions, and reduce overwhelm.

---

## The Problem
Managing tasks with ADHD means constantly fighting two battles: knowing *what* to do, and staying on track long enough to do it. The typical experience looks like this:
- Open 6 tabs to find deadlines across Canvas, email, and notes
- Spend 10+ minutes making a plan that still feels overwhelming
- Start working, get sidetracked, and lose track of time entirely
- End the day having worked hard but finished the wrong things

This workflow was built to solve exactly that.

---

## What It Does
A 4-step agentic workflow that takes your tasks, deadlines, and available hours — and produces a structured, prioritized focus plan in under 2 minutes.

| Step | What It Does |
|---|---|
| 1. Input Collection | User provides tasks, deadlines, and available work hours |
| 2. Priority Sorting | AI ranks tasks by urgency and deadline proximity |
| 3. Focus Session Builder | Creates time-blocked schedule within available hours |
| 4. Drift Catcher | Generates hourly check-in questions to catch sidetracking |

---

## Built With
- **Google Opal** — visual agentic workflow builder
- **Gemini Pro** — AI model powering the scheduling and prioritization nodes
- **Markdown** — documentation and benchmarking

---

## Try It
👉 [Open the Workflow in Google Opal](https://opal.google/app/1Moy5oXNWV9c3q8FiVzsQWRPwdRXce_l2)

**How to use:**
1. Click the link above
2. Fill in your tasks, deadlines, and available work hours
3. Hit run and get your personalized focus plan

---

## Benchmark Results
The system was tested across 5 test cases with real and edge-case inputs.

| Test Case | Description | Avg Score | Key Finding |
|---|---|---|---|
| TC1 | Real input, first run | 3.8/5 | Missing 2 tasks in output |
| TC2 | Real input, detailed | 3.2/5 | Hallucination detected |
| TC3 | Simple 1 task | 0/5 | State bleed failure |
| TC4 | 10 tasks, 1 hour | 0/5 | State bleed failure |
| TC5 | Ambiguous input | 0.4/5 | State bleed + hallucination |

**Overall Average: 1.5/5**

### Key Failures Found
- **Hallucination:** System interprets ambiguous task names as content generation requests
- **State Bleed:** System caches previous run data server-side — persists even in fresh sessions

### Baseline Comparison
| Metric | Manual Planning | Opal Workflow |
|---|---|---|
| Time to plan | 8 min 11 sec | 1 min 16 sec |
| Structure | Messy | Clear time blocks |
| Stress level | Overwhelming | Reduced friction |

**The workflow is 6.5x faster than manual planning on first use.**

Full benchmark details → [benchmark.md](./benchmark.md)

---

## Repo Structure
```
adhd-focus-agent/
├── README.md                        ← You are here
├── benchmark.md                     ← Full test cases, scores, failure analysis
├── reflection-future-improvements.md ← What worked, what didn't, future roadmap
```

---

## Future Improvements
- 🎙️ Voice input via Whisper API (speak tasks instead of typing)
- 📅 Google Calendar integration (auto-pull deadlines)
- 📄 Assignment file upload (AI extracts deadlines from PDFs)
- 🔔 Scheduled reminders via Gmail or Slack
- 🏠 Location-based notifications when arriving home

Full roadmap → [reflection-future-improvements.md](./reflection-future-improvements.md)

---

## Built For
MSIS 549: AI and GenAI for Business Applications
Foster School of Business | University of Washington
Assignment 2 — Agentic AI for Real-World Impact
