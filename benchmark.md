# Dopa — Mini Benchmark
## ADHD Focus Workflow — MSIS 549 HW2

## Success Criteria (defined before testing)
- All input tasks appear in the output plan
- Deadlines are correctly ordered by urgency
- Time blocks fit within the user's stated available hours
- Check-in questions are specific and actionable (not generic)
- No hallucinated content (tasks, ideas, or information not provided by the user)

---

## Metrics
| Metric | Description | Scale |
|---|---|---|
| Task Coverage | Did all input tasks appear in the plan? | 0-5 |
| Deadline Accuracy | Are tasks ordered correctly by deadline? | 0-5 |
| Time Block Fit | Does the schedule fit within available hours? | 0-5 |
| Actionability | Are the steps clear and immediately actionable? | 0-5 |
| Hallucination Rate | Did the system add information not provided by the user? | 0 (hallucinated) / 5 (clean) |

**Scoring Anchors:**
- 5 = Perfect, no issues
- 4 = Minor issues, still usable
- 3 = Partially correct, needs manual fix
- 2 = Significant gaps or errors
- 1 = Unusable output
- 0 = Complete failure

---

## Test Cases

### Test Case 1 — Run 1 (Real Input, Simplified)
**Input:**
- Tasks: Suggest team project idea, HW2, Final project demo, Review team documents
- Deadlines: Feb 14, Feb 14, Feb 21, Feb 28
- Available Time: 9am to 2pm

**Output Summary:**
- Correctly identified Feb 14 tasks as highest priority
- Time blocks fit within 9am-2pm window
- ❌ Only 2 of 4 tasks appeared — final demo (Feb 21) and team project (Feb 28) were missing

**Scores:**
| Metric | Score | Notes |
|---|---|---|
| Task Coverage | 2/5 | Only 2 of 4 tasks appeared in schedule |
| Deadline Accuracy | 4/5 | Correct order for tasks that appeared |
| Time Block Fit | 4/5 | Fit within 9am-2pm |
| Actionability | 4/5 | Clear steps |
| Hallucination Rate | 5/5 | No hallucinated content |

---

### Test Case 2 — Run 2 (Real Detailed Input — Demo Run)
**Input:**
- Tasks: 1. Marketing analysis for MSIS 521 where I need to suggest a team project idea. 2. MSIS 549 HW2 where I build Dopa as an agentic workflow. 3. MSIS 549 Final Demo where I present Synaps, a project quality assurance advisor built using dual-LLM cross-validation. 4. MSIS 5212 team assignment — full marketing analysis for Blendo Games using internet campaign.
- Deadlines: 521 team project idea: Feb 14, HW2 (Dopa): Feb 14, Final Demo (Synaps): Feb 21, Blendo Games assignment: Feb 28
- Available Time: 9am to 2pm

**Output Summary:**
- All 4 tasks included ✅
- Correct deadline ordering ✅
- Multi-day scheduling across Feb 14, 16, 23 ✅
- ❌ HALLUCINATION DETECTED: System generated specific project ideas (Agentic Commerce Analytics, GEO Tracker, Predictive Real-Time Retention) that the user never asked for

**Scores:**
| Metric | Score | Notes |
|---|---|---|
| Task Coverage | 5/5 | All 4 tasks in the plan |
| Deadline Accuracy | 5/5 | Correctly ordered |
| Time Block Fit | 5/5 | Multi-day, realistic |
| Actionability | 4/5 | Clear and structured |
| Hallucination Rate | 1/5 | Generated unsolicited project ideas |

---

## Hallucination Analysis (Persistent Failure)
**What happened:** The system interpreted "Suggest team project idea" as a request to *generate* project ideas, rather than just *schedule time* to work on that task.

**Why it matters:** For an ADHD user, unexpected content adds cognitive load and could be distracting or misleading.

---

### Prompt Iteration 1 — Failed
**Change made:** Added to Requirements section:
> "Do not generate or suggest content not provided by the user. Only schedule and prioritize existing tasks."

**Result (Run 3):** Hallucination persisted — system still generated 3 specific project ideas (Green AI Auditor, Circular Economy Digital Passport, Vertical AI Compliance Agent)

**Scores (Run 3):**
| Metric | Score | Notes |
|---|---|---|
| Task Coverage | 5/5 | All 4 tasks in the plan |
| Deadline Accuracy | 5/5 | Correctly ordered |
| Time Block Fit | 5/5 | Multi-day, realistic |
| Actionability | 4/5 | Clear and structured |
| Hallucination Rate | 1/5 | Still generating unsolicited project ideas |

---

### Prompt Iteration 2 — Failed
**Change made:** Added bold strict rule at the very top of the prompt:
> "**STRICT RULE: You are a scheduling assistant only. Never generate ideas or content beyond what the user provided. Treat task names as labels only.**"

**Result (Run 4):** Hallucination persisted — system generated 3 more project ideas (AI-Powered Hyper-Personalization, Sustainable-by-Design IT, Blockchain for AI Accountability)

**Scores (Run 4):**
| Metric | Score | Notes |
|---|---|---|
| Task Coverage | 5/5 | All 4 tasks in the plan |
| Deadline Accuracy | 5/5 | Correctly ordered |
| Time Block Fit | 5/5 | Multi-day, realistic |
| Actionability | 4/5 | Clear and structured |
| Hallucination Rate | 1/5 | Persistent hallucination despite two fix attempts |

---

### Worst Failure Summary
The hallucination on "Suggest team project idea" is the worst and most persistent failure. Despite two prompt iterations, the model continued interpreting ambiguous task names as content generation requests — a known LLM behavior called **instruction following failure**.

**Root cause:** The task name itself ("Suggest...") reads as a content generation prompt. A simple workaround: rename ambiguous tasks (e.g., "Work on team idea submission").

**Lesson learned:** Prompt constraints alone cannot fully prevent hallucination when task names are ambiguous. A pre-processing sanitization step is needed as a structural fix.

---

### Test Case 3 — Edge Case: Minimal Input
**Input:**
- Tasks: Write a reflection essay
- Deadlines: Feb 15
- Available Time: 10am to 12pm

**Actual Output:** State bleed — system returned previous run's tasks entirely. Essay task never appeared.

**Scores:**
| Metric | Score | Notes |
|---|---|---|
| Task Coverage | 0/5 | Wrong tasks entirely |
| Deadline Accuracy | 0/5 | Previous run's deadlines |
| Time Block Fit | 0/5 | Ignored 10am-12pm window |
| Actionability | 0/5 | Irrelevant output |
| Hallucination Rate | 0/5 | State bleed + hallucinated ideas |

---

### Test Case 4 — Edge Case: 10 Tasks, 1 Hour
**Input:**
- Tasks: 10 tasks all due today (emails, slides, essay, articles, resume, etc.)
- Available Time: 9am to 10am

**Actual Output:** State bleed — system returned previous run's 4 tasks, ignored all 10 new inputs.

**Scores:**
| Metric | Score | Notes |
|---|---|---|
| Task Coverage | 0/5 | Wrong tasks |
| Deadline Accuracy | 0/5 | Previous deadlines |
| Time Block Fit | 0/5 | Ignored 1-hour window |
| Actionability | 0/5 | Irrelevant output |
| Hallucination Rate | 0/5 | State bleed + hallucination |

---

### Test Case 5 — Ambiguous Input (Fresh Incognito Session)
**Input:**
- Tasks: "Do the thing for class, follow up with people, finish the stuff from last week"
- Deadlines: "Soon"
- Available Time: "A few hours"

**Actual Output:** State bleed persisted even in fresh incognito — confirmed server-side caching at workflow level.

**Scores:**
| Metric | Score | Notes |
|---|---|---|
| Task Coverage | 1/5 | Vague inputs partially mapped to old tasks |
| Deadline Accuracy | 0/5 | Previous deadlines used |
| Time Block Fit | 0/5 | Ignored "a few hours" |
| Actionability | 1/5 | Partially actionable by accident |
| Hallucination Rate | 0/5 | State bleed + hallucination |

---

## Aggregate Results Summary

| Test Case | Description | Avg Score | Key Failure |
|---|---|---|---|
| TC1 | Real input, first run | 3.8/5 | Missing 2 tasks |
| TC2 | Real input, detailed (demo run) | 3.2/5 | Hallucination |
| TC3 (Iter 1) | After scope constraint added | 3.2/5 | Hallucination persisted |
| TC4 (Iter 2) | After STRICT RULE added | 3.2/5 | Hallucination persisted |
| TC5 | Edge case: 1 task | 0/5 | State bleed |
| TC6 | Edge case: 10 tasks | 0/5 | State bleed |
| TC7 | Ambiguous input | 0.4/5 | State bleed + hallucination |

**Overall Average: 1.5/5**

---

## Baseline Comparison (A/B Test)

| Metric | Manual Planning | Dopa | Winner |
|---|---|---|---|
| Time to plan | 8 min 11 sec | 1 min 16 sec | Dopa (6.5x faster) |
| Structure | Messy, unformatted | Clear time blocks | Dopa |
| Stress level | Overwhelming | Reduced friction | Dopa |
| Deadline ordering | User-dependent | Automatic | Dopa |
| Reliability across sessions | Consistent | State bleed risk | Manual |
| Time saved per session | — | ~7 minutes | — |

**Projected weekly savings (5 days): ~35 minutes**

**Conclusion:** Dopa is significantly faster and produces more structured output than manual planning. However, state bleed makes it unreliable for repeated daily use — manual process wins on consistency.

---

## Evaluation Method
Primary: **Human Rubric Scoring** (gold standard for small test set)
Secondary: **LLM-as-Judge** using Gemini to cross-validate scores on TC2 and TC5
