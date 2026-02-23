# Reflection & Future Improvements
## Dopa — ADHD Focus Workflow — MSIS 549 HW2

---

## What Worked Well
- First run produced a realistic, well-structured focus plan
- Correctly prioritized tasks by deadline urgency
- Multi-day scheduling was smarter than expected
- Time blocks fit naturally within the 9am-2pm window
- Check-in questions were specific and actionable, not generic
- Packaging as a macOS desktop app (via Opal Share App → Add to Dock) made Dopa feel like a real product

---

## What Did Not Work
- **Hallucination:** System interpreted ambiguous task names (e.g., "Suggest team project idea") as content generation requests, producing unsolicited ideas
- **State Bleed:** System cached previous run's data server-side — persisted even in fresh incognito sessions, making repeated use unreliable
- **Two prompt iterations failed** to fix the hallucination — instruction following failure when task names are ambiguous

---

## Would I Keep Using This System?
In its current form — partially. The first run is genuinely useful and saves 7-10 minutes of manual planning. However, the state bleed issue makes it unreliable for daily repeated use, which is exactly the use case it was designed for. It needs a session reset mechanism before it becomes a dependable daily tool.

---

## Current Implementation
- ✅ **macOS Desktop App** — packaged using Opal's Share App feature and pinned to dock with custom AI-generated logo (brain + lightning bolt, teal gradient)

---

## Future Improvements

### Near-Term (Realistic Next Steps)
1. **Session Reset Mechanism**
   - Add a "Start Fresh" button that clears server-side context before each run
   - Critical fix for the state bleed issue discovered in benchmarking

2. **Voice Input Integration**
   - Allow user to speak their tasks and deadlines instead of typing
   - Use Whisper API (OpenAI) or Google Speech-to-Text
   - Critical for ADHD users — voice is faster and requires less executive function than typing

3. **Google Calendar Integration**
   - Connect via n8n to automatically pull events and deadlines
   - Eliminates the biggest friction point: having to type your tasks every day

4. **Assignment File Upload**
   - Allow user to upload a PDF (e.g., assignment brief, syllabus)
   - AI node extracts deadlines, requirements, and task names automatically

5. **Scheduled Reminders**
   - n8n triggers Gmail or Slack notifications at set times
   - Example: "Your 10am focus block starts in 15 minutes — your task is HW2"

### Medium-Term (Requires More Setup)
6. **Assignment Checklist Tracker**
   - After generating the focus plan, Dopa automatically creates a checklist of deliverables
   - Prevents ADHD users from forgetting small but critical submission steps

7. **End-of-Day Check-In**
   - A second workflow node that runs at 3pm: "What did you complete? What drifted?"
   - Builds a log of daily focus patterns over time

8. **Google Drive Auto-Organization**
   - Automatically creates folders for each assignment
   - User drags files — Dopa places them in the correct folder

### Long-Term (Complex, High Impact)
9. **Location-Based Notifications**
   - Notify user when they arrive home to switch into study mode
   - Requires phone GPS + iOS Shortcuts or Zapier webhook

10. **Canvas LMS Integration**
    - Auto-import assignment deadlines — zero manual input required

11. **Multi-Platform Integration**
    - Connect to Google Drive to scan documents for due dates
    - Full automation — zero manual input required

---

## Biggest Lesson Learned
Prompt engineering alone cannot solve all failure modes. The hallucination persisted through two iterations because the model's helpfulness instinct overrides explicit constraints when task names are ambiguous. Future versions need a **pre-processing sanitization step** that normalizes task names before passing them to the scheduling node — a structural fix, not just a prompt fix.

---

## For the Portfolio
This project demonstrates:
- Agentic workflow design from scratch
- Real benchmarking with failure analysis
- Prompt iteration and honest reflection
- Understanding of LLM failure modes (hallucination, state bleed, instruction following failure)
- Product thinking — packaging a workflow as a real macOS desktop app with custom branding
- Practical thinking about real-world automation and integration
