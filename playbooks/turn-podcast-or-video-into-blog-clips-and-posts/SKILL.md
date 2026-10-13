---
name: turn-podcast-or-video-into-blog-clips-and-posts
description: "Turn a long podcast or video into a blog post, a timestamped clips list and social posts. You get a blog draft, a list of clip candidates with start and end times, and a set of social posts, all checked against a timestamped transcript."
---

# Turn a long podcast or video into a blog post, a timestamped clips list and social posts

Source: https://agentshandbook.com/p/turn-podcast-or-video-into-blog-clips-and-posts (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/turn-podcast-or-video-into-blog-clips-and-posts.md

Transcribe the episode first, with timestamps, and fix names in the transcript. Then give the transcript and a few samples of your own writing to Claude or another assistant and ask for a blog draft, a clips list and social posts. Every quote and timestamp must come from the transcript. People report that models change quotes, invent timestamps and misspell names, so you check each one against the source before you publish.

## Stop and ask the user

- Read the corrected transcript's names and terms before the agent writes anything.
- Check every quote and timestamp against the transcript before you publish.
- Approve each social post before it goes out.

## Steps

1. **Get a timestamped transcript.** Export the transcript from your recording or hosting tool, or run Whisper locally. Do not ask a model to summarise an episode it has not been given. Clean audio helps: one developer fixed odd punctuation from a quiet channel by converting to 16 kHz mono first. Check: You have a text or JSON file with a timestamp on each segment.
2. **Fix names and terms.** Speech-to-text spells names by sound. Give the agent your list of correct names and let it flag likely errors. Confirm each fix yourself. Check: Every guest, company and product name is spelled right in the transcript.
3. **Generate the drafts.** Paste the prompt with the transcript and your writing samples. For episodes over an hour, ask for the blog post and the clips list in separate turns. Check: You get a blog draft, a clips list with start and end times, and social posts.
4. **Check quotes and numbers.** Search the transcript for each quote in the blog post and posts. Fix or remove any quote that is not word for word. Check every number against its timestamp. Check: Every quote appears in the transcript exactly as written.
5. **Check clip times in the player.** Open each clip time in your audio or video editor. Long files are where people report timestamps drifting by seconds or minutes. Check: Each clip starts and ends where the list says.
6. **Edit for voice and publish yourself.** Rewrite lines that do not sound like you. Remove filler phrases. Publish the blog post and schedule the social posts yourself. Check: You would sign every line, and you posted each item by hand.

## Known failures

- Quotes in the output do not match what the speakers said, or the transcript is silently paraphrased. Fix: Always work from a transcript. Ask for quotes copied word for word, then search the transcript for each one. Ask for "check" marks instead of guesses.

- Timestamps are wrong, sometimes by many minutes on long episodes. Fix: Use segment timestamps from the transcript, not times the model infers. Split long files into chunks with a time offset. Check each clip in the player.

- Names, brands and places come out misspelled because transcription spells by sound. Fix: Give a list of correct names and run a correction pass that lists fixes rather than rewriting the whole transcript.
- A statistic is worded wrongly in a social post. Fix: Ask the agent to tag every number with its timestamp and check each one against the transcript or the original report.
- The model stops partway, times out or cuts the output short on a long transcript. Fix: Raise the output limit if your tool allows it, or split the job into the blog post, clips and posts as separate requests.
- The draft sounds generic and the time saved is unclear. Fix: Give real samples of your writing, and treat the output as a first draft you edit, not a finished post.

## Starting prompt

```text
I am giving you a timestamped transcript of [show name], episode [number or title], with [host] and [guest]. I am also giving you three samples of my own writing so you can match my voice.

Correct spellings for names and terms: [list names, companies, products, places].

Do these four things:
1. Name check. List any word in the transcript that looks like a misheard name or term, with its timestamp and your suggested fix. Do not change the transcript itself. STOP and wait for me to confirm the fixes.
2. Blog post. After I confirm, write a [800-1200] word post for [audience] built on the [3] strongest ideas in the episode. Use only claims made in the transcript. Quote the speakers word for word, and put the timestamp in brackets after each quote. Do not add facts, numbers or quotes that are not in the transcript.
3. Clips list. List [8] clip candidates of 30 to 90 seconds. For each: start time, end time, speaker, the first and last sentence of the clip copied exactly from the transcript, and one line on why it works alone.
4. Social posts. Write [3] posts for [LinkedIn], [3] for [X] and [1] thread. Each post makes one point from the episode and links to [episode URL].

Rules:
- Every quote and every timestamp must be copied from the transcript. If you are not sure of a timestamp, write "check" instead of guessing.
- Flag any number you use with its timestamp.
- Do not publish or post anything. Give me the drafts.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"turn-podcast-or-video-into-blog-clips-and-posts","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.