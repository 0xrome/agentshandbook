---
name: find-and-book-a-restaurant-or-appointment
description: "Find and book a restaurant table or local appointment with a shortlist you approve. You have a confirmed booking at a place you chose, at the right date, time and party size, with the cancellation terms known."
---

# Find and book a restaurant table or local appointment with a shortlist you approve

Source: https://agentshandbook.com/p/find-and-book-a-restaurant-or-appointment (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/find-and-book-a-restaurant-or-appointment.md

Ask an assistant for a shortlist that matches your date, time, party size, area and needs, with live open slots from the booking site. Pick one yourself, then let the agent fill the booking form and stop before it confirms, so you check the details and any deposit. Testers report that agents can search the wrong area and get stuck when a place only takes bookings by phone, so check the location and have a phone fallback ready.

## Stop and ask the user

- Pick the place and slot yourself from the shortlist.
- Check date, time, party size, name and any deposit or no-show fee before the booking is confirmed.
- Approve any phone call or message to the business before it happens.

## Steps

1. **Set the hard facts.** Write the date, time window, party size, area and must-haves. Add your ZIP code or a full address so the search stays local. Check: You have one line with date, time, party size and location.
2. **Get a shortlist with live slots.** Paste the prompt. The agent returns up to five places with slots it saw and how each one takes bookings. Check: Every place is in the right area and shows a real slot or says "not shown".
3. **Choose a place and slot.** Open the booking page for your top pick yourself if you want to double-check. Tell the agent your choice. Check: You have picked one place and one slot.
4. **Let the agent fill the form.** The agent enters the booking details and stops before the confirm button. Take over for any login or CAPTCHA. Check: The agent reads back place, date, time, party size, name and any fee.
5. **Confirm it yourself.** Check the page, enter card details yourself if the place needs a deposit, and confirm. Check: You receive a confirmation email or text with the right details.
6. **Handle phone-only places yourself.** If your choice only takes phone bookings, call with the script the agent wrote, or pick the next place on the list. Check: You have a booking or a clear next choice.

## Known failures

- The agent searches the wrong area. Fix: Give a ZIP code or full address and a maximum distance, and ask it to check each address before it lists a place.
- The place only takes bookings by phone, and the agent gets stuck on the "call for reservations" link. Fix: Ask the agent to list the booking method, skip phone-only places or give you the number and a short script.
- The agent offers alternatives you did not ask for after it fails. Fix: Ask it to report the failure and stop rather than switch to another place on its own.
- A booking needs a card hold or deposit that you did not expect. Fix: Ask the agent to report any deposit, hold or cancellation fee in the shortlist, and enter card details yourself.

## Starting prompt

```text
Find me a [restaurant table / haircut / dental cleaning] in [neighbourhood, city, ZIP code] on [Saturday 2026-10-24] between [19:00 and 20:30] for [4 people]. Needs: [vegetarian options, step-free access, under USD 40 a head]. Only use places within [2 km] of [address].

Step 1. Make a shortlist of up to 5 places. For each give: name, address, distance from [address], the open slots you actually saw on the booking site or the place's own site, price level, the booking method (online site name, or phone only), and any deposit, card hold or cancellation fee you saw. Mark anything you did not see as "not shown". Check the address is in [city] before you list a place.
STOP and wait for me to choose a place and a slot.
Step 2. Open the booking page for my choice and fill in the date, time, party size and my name [name]. Use my phone number and email only if the form needs them: [phone, email].
STOP before the final confirm button. Read back the place, date, time, party size, name, and any deposit or fee, exactly as the page shows them. Do not enter card details. Do not confirm until I say "book it".
If the place only takes bookings by phone, do not call. Give me the number and a two-line script with my details.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"find-and-book-a-restaurant-or-appointment","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.