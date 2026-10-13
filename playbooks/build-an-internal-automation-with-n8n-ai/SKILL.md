---
name: build-an-internal-automation-with-n8n-ai
description: "Build a small internal automation with n8n's AI builder and test it before it goes live. You have a working workflow that has passed test runs, asks a person before it sends or changes anything important, and alerts you when a step fails."
---

# Build a small internal automation with n8n's AI builder and test it before it goes live

Source: https://agentshandbook.com/p/build-an-internal-automation-with-n8n-ai (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/build-an-internal-automation-with-n8n-ai.md

Write a one-page spec first: the trigger, each step, what may be written or sent, and what must never happen. Then let n8n's AI workflow builder, or Claude Code with an n8n MCP server, draft the workflow in a copy. Check every node's settings and credentials, run it on test data, and add an approval step before any message or record change. Users report broken nodes, loops and agents that claim actions they never took.

## Stop and ask the user

- Approve the spec, including the list of actions that need approval, before anything is built.
- Review every node's credentials and parameters before the first test run.
- Approve each send or record change through an approval step until the workflow has run cleanly for [two weeks].
- Activate the workflow yourself.

## Steps

1. **Write the spec.** Describe the trigger, steps, what the workflow may write or send, what needs approval and what must never happen. Keep the first version under 15 nodes. Check: Someone else could read the spec and say what the workflow does with a broken input.
2. **Approve the node plan.** Paste the prompt. The agent lists nodes, operations and credentials before it builds. Check: Every node in the plan maps to a step in the spec, and no node sends or deletes outside the allowed list.
3. **Build in a draft.** Let the builder or the coding agent create the draft workflow. For a large workflow, build it in parts. One user reports the builder kept only part of an 84-node workflow when saving. Check: The draft opens in the editor with every node connected and no red warnings.
4. **Review every node.** Open each node. Check credentials, the exact operation and fields the AI filled in. Replace guessed values with fixed ones. Check: You have looked at every node and changed or confirmed each guessed value.
5. **Run the three test cases.** Run with test data or pinned data. Watch the execution log, not the AI's summary of what happened. Check: Each case does what the spec says, and the broken row goes to the error branch.
6. **Test failure paths.** Break a credential or force an error and see that the error workflow alerts you. Check that the item and loop limits stop a runaway run. Check: You receive the failure alert in Slack or email.
7. **Activate with approvals on.** Turn it on with approval steps in place. Check executions daily for the first week. Check: The first week of executions shows no surprise sends, loops or silent failures.

## Known failures

- The generated workflow uses the wrong nodes, misses connections or fills in wrong parameter values. Fix: Approve a node plan first, give a coding agent node documentation through an MCP server, and review every node before the first run.
- An AI agent node calls the same tool again and again, and token use grows fast. Fix: Set a maximum number of iterations and item limits, and watch token use in the first runs. One user worked around a looping case by pinning an older node version.
- The agent says an email was sent or a refund processed, but the action never happened. Fix: After each important action, check the returned id and stop with an error if it is missing. Run a daily reconciliation against the external system.
- The builder saves only part of a large workflow, or generation hangs with no error. Fix: Build large workflows in parts and keep the published version as a backup. Export the JSON before each big AI edit.
- AI-written text breaks save rules, such as a description that is too long. Fix: Read save errors closely and shorten or remove AI-written fields by hand.
- An update to the platform or a node version changes behaviour in a workflow that worked. Fix: Keep an error workflow that alerts you, and re-run your test cases after upgrades.
- Zapier agents guess field values. Fix: Zapier's help page says to switch those fields from "Let agent decide" to fixed values or write clearer instructions.

## Starting prompt

```text
Build an n8n workflow from this spec. Work in a new workflow named "[name] (draft)". Do not edit or activate any existing workflow.

Spec
- Trigger: [new row in Google Sheet "Requests" / form submission / every weekday at 09:00].
- Steps: [1. read the row 2. look up the customer in HubSpot by email 3. ask an LLM to classify the request as A, B or C 4. post a summary to Slack channel #ops 5. create a task in Asana for type A].
- Data the workflow may write: [Slack #ops, Asana project "Ops"].
- Actions that need human approval: [any email to a customer, any CRM update]. Use a "send and wait for approval" step for these.
- Never: [delete records, email anyone outside the company, run more than 50 items per execution].

1. Before you build, list the nodes you plan to use, each node's operation, and which credential it needs. Stop and wait for my OK.
2. Build the workflow. Use fixed values for fields that should not change, not values the AI decides.
3. Where an LLM step returns data that later nodes use, require structured JSON output and validate it. If it is invalid, route to an error branch.
4. After every node that sends or writes, check the returned id. If there is no id, stop with an error. Do not trust the AI's text that it succeeded.
5. Add an error workflow that posts the failed node and error to [Slack DM to me].
6. Add a limit so one run cannot process more than [50] items, and no loop can repeat more than [3] times.
7. Give me test data for three cases: [normal type A], [type C], [a broken row with a missing email]. Tell me what each case should do.
Do not activate the workflow. I will run the tests and activate it.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"build-an-internal-automation-with-n8n-ai","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.