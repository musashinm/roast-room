# Roast Room

This project is the Roast Room: a council of simulated advisors that debates a founder's business decision. Eighteen sit in this fork: a default board of seven (Steve Jobs, Bill Gates, Jason Lemkin, Seth Godin, Keith Rabois, Dan Martell, Buffett) and eleven on call (Bezos, Paul Graham, Hormozi, Gary Vaynerchuk, Gino Wickman, Naval Ravikant, Codie Sanchez, Leila Hormozi, Sara Blakely, Elon Musk, Mark Zuckerberg). Before each council the Chair recommends a board for the question and the user confirms it. The user can add more advisors.

- When the user brings a decision ("should I...", pricing, hiring, raising money, a new product, a pivot), run `/roast-room`. For a quick question to one advisor, use `/roast-room ask <seat> ...`.
- Every advisor and the default board live in `.claude/skills/roast-room/roster.json`. When the user wants to add an advisor ("add Naval", "I want X on my board"), run `/newroaster`. When they want to change who sits at the table by default, or be asked each time, run `/roast-room board`.
- The room runs in Docker and restarts on its own (`compose.yaml`). If the user asks to start or open it, check `docker compose ps`, run `docker compose up -d` if it isn't up, and tell them to open http://localhost:4730. Don't also run `npm start`: port 4730 is taken. After an `.env` change, run `docker compose restart`.
- Councils are saved in `sessions/<date>-<decision>/`. The room plays them live as those files land. Follow `.claude/skills/roast-room/references/live-room.md` exactly so the room can read them.
- The seats are simulations built from public work. Never present a seat's words as something the real person said unless it is a verbatim quote with a source id from that seat's brain.
- Write the Chair's parts in plain English: short sentences, no hype, no filler. Keep the verdict in chat short enough to decide from at a glance; the full report goes in `verdict.md`, and the room's "Download PDF" button turns it into a branded PDF.
