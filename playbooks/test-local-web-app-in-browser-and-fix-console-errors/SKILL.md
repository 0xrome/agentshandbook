---
name: test-local-web-app-in-browser-and-fix-console-errors
description: "Test your local web app in a real browser and fix console errors in one loop. You get a table of the console errors and failed requests on each route you named, a small fix for each one, and proof from a reload that the error is gone. "
license: CC-BY-4.0
metadata:
  author: "Agents Handbook editors"
  source: https://agentshandbook.com/p/test-local-web-app-in-browser-and-fix-console-errors
  version: "2026-10-13"
---

# Test your local web app in a real browser and fix console errors in one loop

Source: https://agentshandbook.com/p/test-local-web-app-in-browser-and-fix-console-errors (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/test-local-web-app-in-browser-and-fix-console-errors.md

Give a coding agent a browser tool, such as Playwright MCP, Chrome DevTools MCP, Claude Code's Chrome integration or Cursor's built-in browser. The agent opens your local dev server, clicks through the pages you name, reads console errors and failed network requests, fixes the code, and reloads to prove each fix. Keep the pages small and the list of routes short, because browser snapshots fill the context fast. Review every fix before you commit, because agents sometimes silence an error instead of fixing it.

## Stop and ask the user

- Approve the list of routes and the test account before the agent opens the browser.
- Review the diff for each fix before it is committed.

## Steps

1. **Pick one browser tool and connect it.** Choose Playwright MCP for repeatable clicks and forms, Chrome DevTools MCP for console, network and performance detail, Claude Code's `--chrome` flag to use your own Chrome window, or Cursor's built-in browser. Install it and check that the agent lists its tools (in Claude Code run /mcp, in Gemini CLI run /mcp). Check: The agent lists browser tools such as browser_console_messages or list_console_messages.
2. **Start the dev server and choose a small set of routes.** Start the app yourself or let the agent start it. Write down three to six routes and the clicks that matter on each. Use a test account. If a page is very large, make a trimmed test page, because one tester hit the tool's token limit on a full page. Check: The app loads at the local URL and you have a short list of routes.
3. **Ask for a console and network audit first.** Run the prompt but stop after step 2 of the loop the first time. Ask only for errors, warnings and failed requests. Do not ask for full logs or full page snapshots. Check: You see a short table of errors per route, with file and line where the stack trace gives one.
4. **Let the agent fix one error at a time.** The agent edits the code, reloads the route and reads the console again. For layout bugs, ask it to measure elements with a script in the page or take a screenshot, instead of guessing CSS. Check: Each fix comes with a before and after console reading from a fresh reload.
5. **Review the diff for hidden errors.** Search the diff for new try/catch blocks, empty catch handlers, console overrides, !important rules and disabled lint rules. These make the console quiet without fixing the cause. Check: Every change fixes a cause you can name. Nothing only hides a message.
6. **Run your normal checks, then commit yourself.** Run the test suite, type checker and linter. Commit the fixes yourself. If you want this loop to keep working, add the routes and the debugging instructions to CLAUDE.md or AGENTS.md. Check: Tests, types and lint pass, and the console is clean on every route in your list.

## Known failures

- The browser tool returns more tokens than the agent can take, and the session stops. Fix: Test smaller pages, ask for console and network output only, and avoid full snapshots. The Playwright MCP README says the Playwright CLI with skills uses less context than MCP for coding agents.

- The agent makes several CSS fixes in a row without ever looking at the rendered page. Fix: Make it open the page, take a screenshot and measure the element sizes with a script before it edits again. One developer reports five failed commits that ended once the agent could measure the DOM.

- The fix silences the symptom, for example many !important rules or a try/catch around the failing call. Fix: Ban those patterns in the prompt and check the diff for them. Ask a human who knows the front end to review style fixes.
- Some browser actions fail or time out, such as resizing the page or typing into a field. Fix: Ask the agent to report the tool error instead of retrying forever, and test that part by hand. A LogRocket walkthrough reports that resize_page kept failing and typing timed out.

- Claude Code's browser tools stop working in a long session. Fix: Run /chrome and pick Reconnect extension. Anthropic's docs say the extension's service worker can go idle. A JavaScript alert on the page can also block it, so dismiss it by hand.

## Starting prompt

```text
You have a browser tool. Use it to test my local app and fix front-end errors.

App: [http://localhost:3000], started with [npm run dev]. If it is not running, start it.
Routes to test: [/, /login, /dashboard, /settings].
Test account: [test@example.com / password from .env.local]. Never use a real customer account.

Loop for each route:
1. Open the route. Wait for the page to load. Click the main controls once: [open the modal, submit the form with empty fields, switch tabs].
2. Read the console messages and the network requests. Keep only errors, warnings and requests with status 400 or higher. Do not paste the full page snapshot back to me.
3. For each error, find the source file and line. Explain the root cause in one sentence.
4. Make the smallest fix. Do not wrap code in try/catch, add !important, or suppress a warning just to make the console quiet. If the only fix is to hide the error, stop and ask me.
5. Reload the route and check the console again. Report the before and after.

Rules:
- Do not change tests, lint rules or TypeScript config to make an error go away.
- Do not touch [src/payments/, the database schema].
- Do not commit, push or deploy. Stop when the table is done.

At the end, give me a table: route, error, root cause, file changed, fixed (yes/no), evidence from the reload.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"test-local-web-app-in-browser-and-fix-console-errors","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
