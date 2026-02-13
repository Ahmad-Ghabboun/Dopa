# ADHD Focus Workflow — Mini Benchmark

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

---

## Test Cases

### Test Case 1 — Run 1 (Real Input, First Attempt)
**Input:**
- Tasks: Suggest team project idea, HW2, Final project demo, Review team documents
- Deadlines: Feb 13, Feb 14, Feb 21, Feb 28
- Available Time: 9am to 3pm

**Output Summary:**
- Correctly picked team idea as #1 priority (Feb 13 deadline)
- Time blocks were realistic
- Check-in questions were specific and actionable
- ❌ Final project (Feb 21) and team project (Feb 28) were missing from the schedule

**Scores:**
| Metric | Score | Notes |
|---|---|---|
| Task Coverage | 2/5 | Only 2 of 4 tasks appeared in schedule |
| Deadline Accuracy | 4/5 | Correct order for tasks that appeared |
| Time Block Fit | 4/5 | Fit within 9am-3pm |
| Actionability | 4/5 | Clear steps |
| Hallucination Rate | 5/5 | No hallucinated content |

---

### Test Case 2 — Run 2 (Real Input, More Detailed)
**Input:**
- Tasks: 1. Suggest team project idea, 2. Complete MSIS 549 HW2, 3. Prepare final project demo, 4. Review team project documents
- Deadlines: Suggest team idea: Feb 13, HW2: Feb 14, Final project demo: Feb 21, Team project: Feb 28
- Available Time: 9am to 3pm

**Output Summary:**
- All 4 tasks included ✅
- Correct deadline ordering ✅
- Multi-day scheduling across Feb 12, 13, 14 ✅
- ❌ HALLUCINATION DETECTED: System generated specific team project ideas (AI-powered collaboration tool, IoT gardening system, mental wellness app) that the user never asked for

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
**Change made:** Added bold strict rule at the very top of the prompt, before all other instructions:
> "**STRICT RULE: You are a scheduling assistant only. Never generate ideas or content beyond what the user provided. Treat task names as labels only.**"

**Result (Run 4):** Hallucination persisted — system again generated 3 specific project ideas (AI-Powered Hyper-Personalization, Sustainable-by-Design IT, Blockchain for AI Accountability)

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
The hallucination on task name "Suggest team project idea" is the **worst and most persistent failure** in the system. Despite two prompt iterations explicitly instructing the model not to generate content, the model continued to interpret ambiguous task names as content generation requests. This is a known LLM behavior called **instruction following failure** — where the model's tendency to be helpful overrides explicit constraints. 

**Root cause:** The task name itself ("Suggest...") reads as a content generation prompt to the model. A simple workaround for users: rename ambiguous tasks (e.g., "Work on team idea submission" instead of "Suggest team project idea") to avoid triggering this behavior.

**Lesson learned:** Prompt constraints alone cannot fully prevent hallucination when task names are ambiguous. Future versions should add a pre-processing step that sanitizes task names before passing them to the scheduling node.

---

## Test Case 3 — Simple Input (Edge Case: Minimal Input)
**Input:**
- Tasks: Write a reflection essay
- Deadlines: Feb 15
- Available Time: 10am to 12pm

**Expected Output:** A simple 2-hour focus plan for one essay task

**Actual Output:** System completely ignored the new inputs and returned the previous run's tasks (team project idea, HW2, final demo, document review) with the previous deadlines (Feb 13-28). The essay task never appeared.

**Failure Type:** State Bleed — system used cached data from previous run instead of new inputs. Input fields were cleared before running.

**Scores:**
| Metric | Score | Notes |
|---|---|---|
| Task Coverage | 0/5 | Wrong tasks entirely — previous run's data |
| Deadline Accuracy | 0/5 | Previous run's deadlines used |
| Time Block Fit | 0/5 | Ignored stated 10am-12pm window |
| Actionability | 0/5 | Irrelevant output |
| Hallucination Rate | 0/5 | Both state bleed and hallucinated project ideas |

**Worst failure in the benchmark.** System is not stateless between runs, making it unreliable for repeated use without a full page refresh.

**Workaround:** Fully refresh the Opal preview page between test runs.

---

## Test Case 4 — Edge Case (10 Tasks, 1 Hour)
**Input:**
- Tasks: 1. Reply to emails, 2. Review lecture slides, 3. Write essay outline, 4. Read 2 articles, 5. Update resume, 6. Message teammate, 7. Submit form online, 8. Review feedback, 9. Prep quiz notes, 10. Organize desktop files
- Deadlines: All due today
- Available Time: 9am to 10am tomorrow

**Expected Output:** A prioritized plan acknowledging time constraints, selecting only the most urgent tasks

**Actual Output:** State bleed again — system returned previous run's 4 tasks completely ignoring all 10 new inputs

**Failure Type:** Persistent state bleed — confirmed systematic platform issue with Opal

**Scores:**
| Metric | Score | Notes |
|---|---|---|
| Task Coverage | 0/5 | Wrong tasks — previous run's data again |
| Deadline Accuracy | 0/5 | Previous deadlines used |
| Time Block Fit | 0/5 | Ignored 1-hour window entirely |
| Actionability | 0/5 | Irrelevant output |
| Hallucination Rate | 0/5 | State bleed + hallucinated project ideas |

---

## Systematic Failure Analysis — State Bleed
State bleed occurred in Test Cases 3 and 4 — both times after clearing input fields and re-entering new data. The system consistently reverted to the first successful run's data.

**Root cause:** Opal caches context from previous runs at the session level. Clearing input fields does not reset the model's context window.

**Impact:** Cannot be reliably used for multiple test cases in the same session — a significant limitation for an ADHD user who needs quick daily replanning.

**Recommendation:** Always open a fresh Opal session for each new use case.

---

## Test Case 5 — Ambiguous Input (Fresh Incognito Session)
**Input:**
- Tasks: "Do the thing for class, follow up with people, finish the stuff from last week"
- Deadlines: "Soon"
- Available Time: "A few hours"

**Expected Output:** System asks for clarification OR produces a reasonable generic plan based on vague inputs

**Actual Output:** State bleed persisted even in a fresh incognito session — system returned previous run's 4 tasks again. However, it partially mapped vague inputs onto old tasks (e.g., "finish the stuff from last week" mapped to HW2, "follow up with people" mapped to demo coordination).

**Critical Finding:** State bleed is stored **server-side in the Opal workflow itself**, not in the browser session. Opening incognito does not help. The cache persists at the workflow level.

**Scores:**
| Metric | Score | Notes |
|---|---|---|
| Task Coverage | 1/5 | Vague inputs partially mapped to old tasks |
| Deadline Accuracy | 0/5 | Used previous deadlines, ignored "soon" |
| Time Block Fit | 0/5 | Ignored "a few hours" entirely |
| Actionability | 1/5 | Partially actionable due to accidental mapping |
| Hallucination Rate | 0/5 | State bleed + hallucinated project ideas |

---

## Aggregate Results Summary

| Test Case | Description | Avg Score | Key Failure |
|---|---|---|---|
| TC1 | Real input, first run | 3.8/5 | Missing 2 tasks |
| TC2 | Real input, detailed | 3.2/5 | Hallucination |
| TC3 | Simple 1 task | 0/5 | State bleed |
| TC4 | 10 tasks, 1 hour | 0/5 | State bleed |
| TC5 | Ambiguous input | 0.4/5 | State bleed + hallucination |

**Overall Average: 1.5/5**

The system performs well on its first run but degrades significantly on repeated use due to persistent server-side state bleed. The hallucination issue with ambiguous task names is a secondary but consistent failure mode.

---

## Baseline Comparison (A/B Test)
**Method:** Same tasks and deadlines planned manually vs. using the Opal workflow

**Manual Process:**
- Opened Canvas to find deadlines
- Checked notes app and email for additional tasks
- Wrote out 10-day plan in Notes app (normally done by hand on paper)
- Juggled between multiple windows throughout
- Time taken: **8 minutes 11 seconds**
- Quality: Messy, overwhelming, no structured time blocks

**Opal Workflow (Fresh Session):**
- Filled in 3 input fields
- Waited for output to generate
- Time taken: **1 minute 16 seconds**
- Quality: Structured, time-blocked, prioritized by deadline

**Results:**
| Metric | Manual | Opal Workflow | Winner |
|---|---|---|---|
| Time to plan | 8 min 11 sec | 1 min 16 sec | Opal (6.5x faster) |
| Structure | Messy, unformatted | Clear time blocks | Opal |
| Stress level | Overwhelming | Reduced friction | Opal |
| Deadline ordering | User-dependent | Automatic | Opal |
| Reliability | Consistent | State bleed risk | Manual |

**Time saved per session: ~7 minutes**
**Projected weekly savings (5 days): ~35 minutes**

**Conclusion:** The Opal workflow is significantly faster and produces more structured output than manual planning. However, the state bleed issue makes it unreliable for repeated daily use — manual process wins on consistency.

---

## Evaluation Method
Primary: **Human Rubric Scoring** (gold standard for small test set)
Secondary: **LLM-as-Judge** using Gemini to score outputs against the rubric above
