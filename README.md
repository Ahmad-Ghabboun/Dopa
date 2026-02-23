# Dopa
### An agentic AI workflow that helps ADHD users prioritize tasks, build structured focus sessions, and reduce overwhelm.

![Dopa Logo](./dopa_logo.png)

---

## The Problem
Managing academic, professional, personal, and family tasks with ADHD means constantly fighting two battles: knowing *what* to do, and staying on track long enough to do it. The typical experience looks like this:
- Open 6 tabs to find deadlines across Canvas, email, and notes
- Spend 10+ minutes making a plan that still feels overwhelming
- Start working, get sidetracked by a personal or family obligation, and lose track of time entirely
- End the day having worked hard but finished the wrong things

This workflow was built to solve exactly that — for real, daily personal use.

---

## What It Does
A 4-step agentic workflow that takes your tasks, deadlines, and available hours — and produces a structured, prioritized focus plan in under 2 minutes.

| Step | What It Does |
|---|---|
| 1. Input Collection | User provides tasks, deadlines, and available work hours |
| 2. Priority Sorting | AI ranks tasks by urgency and deadline proximity |
| 3. Focus Session Builder | Creates time-blocked schedule within available hours |
| 4. HTML Output | Renders a clean, styled focus plan webpage |

---

## Built With
- **Google Opal** — visual agentic workflow builder
- **Gemini 3 Flash** — AI model powering the Plan Workflow node (scheduling + prioritization)
- **Gemini Pro** — AI model powering the Generate Focus Plan node (HTML output)
- **Search Web (built-in)** — live web search tool used inside the Plan Workflow node

---

## macOS Desktop App
Dopa was packaged as a macOS desktop app using Opal's Share App → Add to Dock feature, with a custom AI-generated logo (brain + lightning bolt, teal gradient). This makes Dopa launch like a native productivity app with no browser tab required.

---

## Try It
👉 [Open the Workflow in Google Opal](https://opal.google/app/1Moy5oXNWV9c3q8FiVzsQWRPwdRXce_l2)

**How to use:**
1. Click the link above
2. Fill in your tasks, deadlines, and available work hours (e.g., 9am to 2pm)
3. Hit run and get your personalized focus plan

---

## Demo Video
📹 [Watch the Demo](https://drive.google.com/file/d/1XMI3e9u99EyTtD0Lu6bj3q6FxcOFy12S/view?usp=sharing)

---

## Benchmark Results
The system was tested across 7 test cases with real, edge-case, and ambiguous inputs.

| Test Case | Description | Avg Score | Key Finding |
|---|---|---|---|
| TC1 | Real input, first run | 3.8/5 | Missing 2 tasks in output |
| TC2 | Real input, detailed (demo run) | 3.2/5 | Hallucination detected |
| TC3 | After prompt iteration 1 | 3.2/5 | Hallucination persisted |
| TC4 | After prompt iteration 2 | 3.2/5 | Hallucination persisted |
| TC5 | Edge case: 1 task, 2-hour window | 0/5 | State bleed failure |
| TC6 | Edge case: 10 tasks, 1 hour | 0/5 | State bleed failure |
| TC7 | Ambiguous input | 0.4/5 | State bleed + hallucination |

**Overall Average: 1.5/5**

> Note: The low average is driven entirely by state bleed in repeated sessions — a platform limitation. On first use (fresh session), Dopa scores ~3.8/5 and is genuinely useful.

### Key Failures Found
- **Hallucination:** System interprets ambiguous task names as content generation requests
- **State Bleed:** System caches previous run data server-side — persists even in fresh incognito sessions

### Baseline Comparison
| Metric | Manual Planning | Dopa | Winner |
|---|---|---|---|
| Time to plan | 8 min 11 sec | 1 min 16 sec | Dopa (6.5x faster) |
| Structure | Messy | Clear time blocks | Dopa |
| Stress level | Overwhelming | Reduced friction | Dopa |
| Reliability | Consistent | State bleed risk | Manual |

**Dopa is 6.5x faster than manual planning on first use.**

Full benchmark details → [benchmark.md](./benchmark.md)

---

## Repo Structure
```
dopa/
├── README.md                          ← You are here
├── benchmark.md                       ← Full test cases, scores, failure analysis
├── reflection-future-improvements.md  ← What worked, what didn't, future roadmap
```

---

## Future Improvements
- 🎙️ Voice input via Whisper API (speak tasks instead of typing)
- 📅 Google Calendar integration (auto-pull deadlines)
- 📄 Assignment file upload (AI extracts deadlines from PDFs)
- 🔔 Scheduled reminders via Gmail or Slack
- 🔄 Session reset mechanism (fix for state bleed)

Full roadmap → [reflection-future-improvements.md](./reflection-future-improvements.md)

---

## Built For
MSIS 549: AI and GenAI for Business Applications
Foster School of Business | University of Washington
Assignment 2 — Agentic AI for Real-World Impact
