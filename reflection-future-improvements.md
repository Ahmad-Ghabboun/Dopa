# Reflection & Future Improvements
## ADHD Focus Workflow — MSIS 549 HW2

---

## What Worked Well
- First run produced a realistic, well-structured focus plan
- Correctly prioritized tasks by deadline urgency
- Multi-day scheduling was smarter than expected
- Time blocks fit naturally within the 9am-3pm window
- Check-in questions were specific and actionable, not generic

---

## What Did Not Work
- **Hallucination:** System interpreted ambiguous task names (e.g., "Suggest team project idea") as content generation requests, producing unsolicited ideas
- **State Bleed:** System cached previous run's data server-side — persisted even in fresh incognito sessions, making repeated use unreliable
- **Two prompt iterations failed** to fix the hallucination — instruction following failure when task names are ambiguous

---

## Would I Keep Using This System?
In its current form — partially. The first run is genuinely useful and saves 10-15 minutes of manual planning. However, the state bleed issue makes it unreliable for daily repeated use, which is exactly the use case it was designed for. It needs a session reset mechanism before it becomes a dependable daily tool.

---

## Future Improvements

### Near-Term (Realistic Next Steps)
1. **Voice Input Integration**
   - Allow user to speak their tasks and deadlines instead of typing
   - Use Whisper API (OpenAI) or Google Speech-to-Text to transcribe voice to text
   - Critical for ADHD users — typing requires executive function to organize thoughts first, while voice is faster and more natural when the brain is scattered
   - Removes the biggest cognitive barrier to using the tool daily

2. **Google Calendar Integration**
   - Connect via n8n to automatically pull events and deadlines
   - No manual input needed — system reads your calendar directly
   - Eliminates the biggest friction point: having to type your tasks every day

2. **Assignment File Upload**
   - Allow user to upload a PDF or document (e.g., assignment brief, syllabus)
   - AI node extracts deadlines, requirements, and task names automatically
   - Removes manual data entry entirely — just upload and go

3. **Scheduled Reminders**
   - n8n can trigger Gmail or Slack notifications at set times
   - Example: "Your 10am focus block starts in 15 minutes — your task is HW2"
   - Helps ADHD users transition between tasks without losing track of time

### Medium-Term (Requires More Setup)
4. **Assignment Checklist Tracker**
   - After generating the focus plan, Dopa automatically creates a checklist of deliverables for each task
   - Example: For HW2 it would ask "Did you finish the demo video? Did you upload it? Did you submit on Canvas?"
   - Prevents ADHD users from forgetting small but critical submission steps

5. **Google Drive Auto-Organization**
   - Connect to Google Drive and automatically create folders for each assignment
   - User drags and drops files — Dopa places them in the correct folder automatically
   - Example: Drop a screen recording → Dopa moves it to the correct assignment folder instantly

6. **Session Reset Mechanism**
   - Add a "Start Fresh" button that clears server-side context before each run
   - Critical fix for the state bleed issue discovered in benchmarking

5. **End-of-Day Check-In**
   - A second workflow node that runs at 3pm asking: "What did you complete? What drifted?"
   - Builds a log of daily focus patterns over time

6. **Drift Alert**
   - Hourly notification that asks one check-in question from the workflow
   - Catches drifting in real time, not just at the start of the day

### Long-Term (Complex, High Impact)
7. **Location-Based Notifications**
   - Notify user when they arrive home to switch into study mode
   - Requires phone GPS + iOS Shortcuts or Zapier webhook integration
   - Most powerful for ADHD users who lose track of time during transitions

8. **Desktop Widget / Mac App**
   - Wrap the Opal workflow into a small always-visible desktop window using Fluid or Unite
   - Reduces friction of opening a browser tab every morning

9. **Multi-Platform Integration**
   - Connect to Canvas LMS to auto-import assignment deadlines
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
- Practical thinking about real-world automation and integration
