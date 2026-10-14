---
name: enrich-and-qualify-inbound-leads
description: "Enrich and qualify new inbound leads, then route them with a reason a person can check. Each new lead gets a researched summary, a score, a route and a draft reply, and a person approves the action before anything changes in the CRM or reaches the lead."
license: CC-BY-4.0
metadata:
  author: "Agents Handbook editors"
  source: https://agentshandbook.com/p/enrich-and-qualify-inbound-leads
  version: "2026-10-13"
---

# Enrich and qualify new inbound leads, then route them with a reason a person can check

Source: https://agentshandbook.com/p/enrich-and-qualify-inbound-leads (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/enrich-and-qualify-inbound-leads.md

When a lead fills in your form, an agent researches the company and the person, scores the lead against rules you wrote, and posts a short summary with its reasons to your sales channel or CRM. A person approves the route and any reply. Vercel and Anthropic describe running versions of this. Their warnings are that models do not always follow long rule lists, enrichment data is often stale, and quality drifts unless someone keeps sampling the output.

## Stop and ask the user

- Approve the qualification rules and routes before the agent scores any lead.
- Approve each CRM update and each reply in the first weeks (shadow mode).
- Review a sample of routed leads every week after shadow mode ends.

## Steps

1. **Write the rules with your best salesperson.** List the routes (for example qualified, follow up, support, not a fit) and the rules for each one. Keep hard rules short and testable. Mark which rules depend on judgement. Check: Every route has at least one rule, and every rule can be checked by reading a lead.
2. **Put hard rules in code and judgement in the prompt.** Region, company size thresholds and existing-owner lookups belong in code or a CRM lookup. Let the model handle only the parts that need reading, like what the form message asks for. Check: The code step routes test leads correctly without the model.
3. **Run in shadow mode.** Let the agent research and score every new lead while your team keeps working leads the old way. Compare the agent's route with the human route each day. Vercel describes several weeks of this with its best SDR checking every output. Check: You have a log of agent route against human route for each lead.
4. **Fix the disagreements.** Read every lead where the agent and the human differ. Add or sharpen a rule, or add the case to the prompt as an example. Watch for junior people at good companies, personal email domains, and wrong company size data. Check: Disagreements drop and each one has a known cause.
5. **Turn on approval mode.** The agent now posts its summary, route and draft to your review channel. A person clicks approve before the CRM changes or the reply is sent. Check: Nothing reaches the CRM or a lead without an approval click in the log.
6. **Keep sampling.** After you trust the output, review a sample of routed leads each week. Vercel reports moving from reviewing all output to sampling, and adding a second agent that watches for rule breaches. Check: You have a weekly sample with a pass rate you write down.

## Known failures

- The model does not always follow the rules in a long prompt, so some leads get the wrong route. Fix: Move hard rules into code or CRM lookups. Keep the prompt short. Vercel's COO said their prompt grew to about 1,000 lines before they moved logic into 14 code rules.

- Enrichment cannot resolve personal email domains or returns stale company size and funding data. Fix: Route unresolved leads to human review. Show the source and date of each enrichment fact so the reviewer can judge it.

- Scoring on headcount alone misroutes leads, for example a junior signup at a large company. Fix: Include the person's role and the form message in the rules, not only firmographics.
- Output quality drops slowly and nobody notices. Fix: Keep a weekly sample review and log the pass rate. One vendor test names silent scoring drift as a failure mode, and SaaStr's write-up of Vercel warns that agents degrade quietly.

- An existing customer or open deal gets treated as a new lead. Fix: Look up the domain in the CRM first and route to the current owner before any scoring.

## Starting prompt

```text
You qualify inbound leads for [company], which sells [offer] to [buyer].

Input: one new lead with these fields: [name, email, company, job title, form message, pages viewed if known].

Do this:
1. Research. Read the company's website and up to two other public sources. Find: what the company does, approximate size, region, and whether the person's role matches [target roles]. Record the URL for each fact. If the email domain is personal (gmail.com and similar) or the company cannot be found, say so and do not guess.
2. Check the CRM. Look up [the domain] in [CRM]. If there is an open deal or a named owner, route to that owner and stop.
3. Score. Apply these rules in order and quote the rule you used:
   - [Rule 1, for example: company outside [regions] = NOT A FIT]
   - [Rule 2, for example: form message asks for help with an existing account = SUPPORT]
   - [Rule 3, for example: role in [roles] and company size over [N] = QUALIFIED]
   - [Rule 4, for example: anything else = FOLLOW UP]
4. Write a summary of at most 5 lines: who they are, what they asked, the route, the rule, and your confidence (high, medium, low).
5. Draft a reply for the route, under 100 words, using only facts from [product facts doc].

Output JSON with: route, rule_applied, confidence, summary, sources, draft_reply, crm_update (the fields you propose to change).

Rules:
- Do not write to the CRM and do not send anything. Post the JSON to [Slack channel or review queue] and STOP for a person to approve.
- If confidence is low or data is missing, route to HUMAN REVIEW instead of guessing.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"enrich-and-qualify-inbound-leads","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
