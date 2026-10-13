---
name: plan-a-multi-city-trip-with-bookings-to-approve
description: "Plan a multi-city trip and line up every booking for you to approve. You get a day-by-day itinerary with one chosen option per leg and per night, each checked against the live booking page, and you pay for each booking yourself."
---

# Plan a multi-city trip and line up every booking for you to approve

Source: https://agentshandbook.com/p/plan-a-multi-city-trip-with-bookings-to-approve (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/plan-a-multi-city-trip-with-bookings-to-approve.md

Give a browser agent your fixed dates, cities, budget and rules, and ask it for a day-by-day itinerary with live options for each flight, train and hotel. Let it fill booking forms up to the payment page, then take over and pay yourself. Testers report good itineraries but also wrong dates, wrong star ratings and long runs, so check every leg against the booking site before you pay.

## Stop and ask the user

- Confirm the fixed constraints (dates, cities, budget, travellers) before the agent searches.
- Approve the itinerary and the chosen option for each leg and night before any booking form is filled.
- Take over at every login, CAPTCHA, personal details page and payment page.
- Check dates, names, price and refund terms on the final booking page before you pay.

## Steps

1. **Write down the fixed facts.** Dates, cities in order, nights per city, travellers, budget, and must-have rules such as free cancellation. Put these in the prompt as facts the agent must not change. Check: You have one short list of facts and preferences.
2. **Answer the agent's questions.** Paste the prompt. A good run starts with questions about anything unclear. If the agent starts searching with guessed dates, stop it and restate the dates. Check: The agent repeats your dates and cities back correctly.
3. **Review the day-by-day plan.** Read each leg and hotel option. Open two or three of the cited pages and compare price, star class and distance with what the agent wrote. Check: The values you checked match the live pages.
4. **Pick one option per leg and per night.** Tell the agent your choices. Prefer refundable rates while the plan can still change. Check: The agent lists exactly the options you picked.
5. **Let the agent fill each booking form.** The agent opens each booking page and fills it up to payment. When it asks, take over to log in or solve a CAPTCHA, then hand back. Check: The agent stops at each payment page and reads back dates, names, room and total.
6. **Check and pay yourself.** On each payment page, check the dates, traveller names, room type, total price and cancellation terms. Pay only when everything matches the approved plan. Check: You receive a confirmation email for each booking with the right dates.
7. **Build the final itinerary.** Ask the agent to put confirmation numbers, addresses and times into one document, or use the calendar playbook to add the bookings to your calendar. Check: Every booking appears once in the itinerary with a confirmation number.

## Known failures

- The agent enters wrong dates or picks its own dates and places. Fix: State dates as fixed facts, tell the agent to stop and ask rather than change them, and read the dates on the final page yourself.
- The agent misdescribes a hotel, for example its star rating or the walk to a terminal. Fix: Ask for values exactly as shown on the site, with "not shown" for gaps, and check the hotel page yourself before you choose.
- Vague requests run for a long time and then crash. Fix: Give detailed rules, a named booking site and the filters to use. One blogger reports this cut runs to 5-10 minutes.
- The agent stops at logins, CAPTCHAs, email codes or bank 3D Secure checks. Fix: Expect to take over at these points. Testers report handing over at payment, one blogger says UK banks blocked 3D Secure for the agent, and one tester reports an agent that would not enter email 2FA codes.
- The agent asks for confirmation again and again, so the run takes longer than doing it yourself. Fix: Let the agent do research and form filling in one batch per booking, and do quick bookings yourself.
- Times in the itinerary are in the wrong time zone. Fix: Ask for local times with the city named for each departure and arrival.

## Starting prompt

```text
Plan a trip for [2 adults]. Fixed facts that you must never change: we leave [Lisbon] on [2026-11-12] and are home by [2026-11-22]. Cities in order: [Madrid (3 nights), Barcelona (3 nights), Paris (3 nights)]. Total budget [EUR 2,500] for transport and hotels. If any fixed fact looks impossible, stop and ask me. Do not pick other dates or cities on your own.

Preferences: [trains over flights when the trip is under 5 hours; hotels rated 8+ on the booking site, walkable to the old town, free cancellation; no flights before 9 AM].

Step 1. Ask me any questions you need before you search.
Step 2. Build a day-by-day plan. For each travel leg give 2 options with operator, depart and arrive times (local), duration, price, and the page where you saw it with the time you checked. For each city give 2 hotel options with nightly price, rating as shown on the site, star class as shown on the site, cancellation terms and distance to [the old town]. Do not round, guess or fill gaps. If you could not see a value, write "not shown".
Step 3. Check the plan: transfer times between station and hotel, arrival time against hotel check-in, and opening days for any [museum or sight] I named.
STOP. Show me the plan and wait for me to pick one option per leg and per night.
Step 4. For each choice I make, open the booking page and fill it up to the payment page with the dates, names and room I approved. Before you hand over, read the dates, names, room type, total price and cancellation terms back to me from that page.
STOP at any login, CAPTCHA, personal details form or payment step and ask me to take over. Never enter card details. Never accept a non-refundable rate unless I say so.
Step 5. When I confirm each booking, add it to a final itinerary document with confirmation numbers.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"plan-a-multi-city-trip-with-bookings-to-approve","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.