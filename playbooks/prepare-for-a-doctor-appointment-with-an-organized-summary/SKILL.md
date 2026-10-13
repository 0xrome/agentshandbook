---
name: prepare-for-a-doctor-appointment-with-an-organized-summary
description: "Prepare for a doctor's appointment with a one-page summary and question list. You bring a one-page summary of your symptoms, timeline and medicines, plus three to five questions, and your doctor makes every medical judgment."
---

# Prepare for a doctor's appointment with a one-page summary and question list

Source: https://agentshandbook.com/p/prepare-for-a-doctor-appointment-with-an-organized-summary (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/prepare-for-a-doctor-appointment-with-an-organized-summary.md

Tell a chat assistant your symptoms, timeline, medicines and worries in your own words, and ask it to sort them into a one-page summary and a short list of questions for your doctor. Ask it to organize only, not to diagnose. Patients report that this helps them use short appointments well. This is not medical advice: talk to your doctor about what anything means, and get urgent help for urgent symptoms.

## Stop and ask the user

- Remove your name, birth date, ID numbers and other identifying details before you paste anything.
- Read the whole summary and correct anything the assistant added, changed or left out.
- If any symptom feels urgent, call your doctor or emergency services instead of using a chatbot.
- Talk to your doctor about what the symptoms mean. Do not act on the assistant's view of them.

## Steps

1. **Write it down in your own words.** List the main concern, when it started, what changed, your medicines with doses, and your questions. Rough notes are fine. Leave out your name, birth date and ID numbers. Check: You have one page of rough notes with no identifying details.
2. **Ask the assistant to organize, not diagnose.** Paste the prompt and your notes. If the reply suggests causes or treatments, ask it to remove them and stick to your facts. Check: The draft summary contains only facts you gave and no guesses about causes.
3. **Answer the follow-up questions.** The assistant marks unclear points and lists facts your doctor may ask about. Find the missing facts, such as dates or doses, from your records. Check: No [ASK ME] markers remain.
4. **Cut it down.** Keep the summary to one page and the questions to three to five. One patient describes trimming about ten observations down to the few that matter most for each specialist. Check: You can read the summary aloud in about two minutes.
5. **Check every line yourself.** Read the final summary against your notes. Fix any dose, date or word that the assistant changed. Check: Every fact in the summary matches your notes.
6. **Share it with your doctor.** Print it, bring it on your phone, or send it to the clinic ahead of time if they accept that. Talk to your doctor about what the symptoms mean and what to do next. Check: You go into the appointment with the summary and your questions ready.

## Known failures

- The assistant drifts into explaining causes or suggesting treatments. Fix: Tell it at the start to organize only. Delete any medical interpretation from the summary and ask your doctor instead.
- The summary changes a dose, date or detail, or adds a fact you never gave. Fix: Ask it to use only your facts and mark gaps, then check every line against your notes.
- The summary is too long for a short appointment. Fix: Set a one-page limit and three to five questions, and ask it to rank what matters most to you.
- You use the chatbot to decide whether a symptom is urgent. Fix: Do not. A Nature Medicine study reported by NBC News found ChatGPT Health under-triaged 51.6% of emergency scenarios. Call your doctor or emergency services.
- You paste identifying health details into a tool you have not checked. Fix: The AMA warns that chatbots do not follow the same privacy rules as a doctor's office. Remove identifying details and check the tool's data settings.

## Starting prompt

```text
Help me prepare for a [15]-minute appointment with my [GP / specialist type] on [date]. Your job is to organize what I tell you. Do not diagnose, do not suggest what the cause might be, do not suggest treatments or changes to my medicines, and do not tell me whether something is serious. If I ask for any of that, remind me to ask my doctor.

Here is what I know, in my own words:
- Main concern: [describe]
- When it started and how it changed: [describe]
- What makes it better or worse: [describe]
- Medicines and supplements with doses: [list]
- Relevant history: [list]
- Notes or readings I have: [paste, or say none]

Please produce:
1. A summary of at most one page, in my words where possible: main concern, timeline, current medicines, and what I have already tried. Use only facts I gave you. Mark anything unclear as [ASK ME].
2. The three to five questions I most want answered, in order of importance to me.
3. A list of facts my doctor may ask about that I have not given you, so I can find them before the visit.
4. If the appointment is more than a week away, a simple daily log table I can fill in until then.

Before you write the final version, ask me about every [ASK ME] item. Keep the summary short enough to read in two minutes.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"prepare-for-a-doctor-appointment-with-an-organized-summary","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.