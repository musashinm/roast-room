# Seats

`roster.json` (one folder up) is the source of truth: every seat, its key, pillar, question, and scorecard dimension, plus the default board and how the board is picked. The seven seats that ship with the Roast Room:

| Seat | Agent | Pillar | Owns the question | Brain |
|---|---|---|---|---|
| Bezos | `council-bezos` | Strategy and decisions | Is this the right bet, and how reversible is it? | `brains/jeff-bezos/` |
| Graham | `council-graham` | Product and startups | Is this something people actually want, and is it growing? | `brains/paul-graham/` |
| Hormozi | `council-hormozi` | Offers, pricing, and sales | Will people pay, how much, and how do we close? | `brains/alex-hormozi/` |
| Gary V | `council-garyvee` | Marketing and attention | Where does the attention come from, and is it underpriced? | `brains/gary-vaynerchuk/` |
| Martell | `council-martell` | People, hiring, and founder time | Who does this, and what does it cost the founder's calendar? | `brains/dan-martell/` |
| Wickman | `council-wickman` | Operations and scaling | Can the business run this without the founder holding it together? | `brains/gino-wickman/` |
| Buffett | `council-buffett` | Money and capital | What does it do to cash, risk, and long-term value? | `brains/warren-buffett/` |

Brain paths are relative to `.claude/skills/roast-room/`. Seats added with `/newroaster` follow the same pattern: `council-<key>` and `brains/<slug>/`, listed in `roster.json`.

## Relevance weights

The Chair sets a weight per seat for each decision, before Round 1, and writes the reason in one line. Weights make the final score honest: a pricing call should lean on Hormozi, a hiring call on Martell.

| Weight | Meaning |
|---|---|
| 3 | This decision lives in the seat's pillar |
| 2 | The pillar is materially affected |
| 1 | The pillar is touched at the edges |

Every seat is at least 1. Exactly one or two seats get a 3.

## Quick council

`--quick` seats four (recommended per SKILL.md "Pick the board", then confirmed): the two highest-weight seats, the seat that guards the downside (Buffett or Bezos out of the box; otherwise the board's money, capital, or risk seat), and the seat most likely to disagree with the others (the Chair names why). Use quick for reversible, low-stakes calls. Full council for anything a founder cannot easily undo.

## Natural tensions to expect

- Bezos and Buffett (long horizon, downside first) against Hormozi and Gary V (speed to cash, volume, act now).
- Graham (do things that don't scale, stay close to users) against Wickman (systems, process, accountability).
- Buffett (stay in your circle, avoid leverage) against Gary V (bet on the underpriced platform now).
- Martell (buy back your time, hire early) against Graham and Buffett (stay small and frugal until it works).

Seats added with `/newroaster` append their own tension lines here.

On-call seats (in `roster.json`, off the default board; the Chair recommends them when the decision is in their lane):

| Seat | Agent | Pillar | Owns the question | Brain |
|---|---|---|---|---|
| Naval | `council-naval` | Leverage and wealth | Does this build leverage and equity you own, or does it just rent out your time? | `brains/naval-ravikant/` |
| Codie | `council-sanchez` | Buying and owning small businesses | Should you build this, or buy something that already works? | `brains/codie-sanchez/` |
| Sara | `council-blakely` | Consumer product and brand from zero | Will customers love it enough to sell it for you, without outside money? | `brains/sara-blakely/` |
| Leila | `council-leila` | Leadership and scaling teams | Can your team and your leadership carry this, and who has to change? | `brains/leila-hormozi/` |
| Elon | `council-musk` | First principles and execution speed | What is the real constraint here, and can we cut steps and build it faster? | `brains/elon-musk/` |
| Godin | `council-godin` | Marketing to the smallest viable audience | Who exactly is this for, and will they tell others? | `brains/seth-godin/` |
| Lemkin | `council-lemkin` | B2B sales and SaaS growth | Can you sell this repeatedly, and what does the first sales team look like? | `brains/jason-lemkin/` |
| Rabois | `council-rabois` | Operating cadence and hiring | Who's the barrel that ships this, and how do you know it's working? | `brains/keith-rabois/` |
| Jobs | `council-jobs` | Product taste and focus | Is this insanely great, and what do we say no to? | `brains/steve-jobs/` |
| Gates | `council-gates` | Platforms and long-term tech bets | Does this become a platform others build on, and where's the tech going in 10 years? | `brains/bill-gates/` |

- Naval (own the equity, tiny teams, self-fund) against Hormozi and Gary V (more volume, more offers, more output that the founder still has to rent their hours to).
- Codie (buy proven cash flow) against Graham and Naval (build something new people want).
- Sara (product good enough to sell itself, no ads, no outside money) against Gary V and Hormozi (attention and sales machines) and against any seat pushing to raise.
- Leila (fix lead flow and the founder's leadership before hiring) against Martell (hire early to buy back time). Leila and Wickman agree on accountability and split when process stands in for leadership.
- Elon (question the requirement, delete the step, attack the bottleneck now) against Wickman (give every process an owner and a cadence) and Buffett (keep cash, wait for the fat pitch). Elon and Graham agree on speed and split on whether a launch counts before the delivery system scales.
- Elon's aggressive dates are for the team, not for customers or lenders; Martell and Leila own what his pace costs the people.
- Godin (pick the smallest group that would be enough, earn trust, let them tell the others) against Gary V (attention at volume on the underpriced platform) and Hormozi (offers, closing, and paid lead flow). Godin and Sara agree on word of mouth over ads and split on whether the product or the audience comes first.
- Godin (never race to the bottom, price is a story) against any seat cutting price to win volume; Buffett and Hormozi own the unit economics he does not run.
- Lemkin (founder sells first, then two reps, then a VP of Sales who lifts revenue in one cycle) against Godin (let a small audience tell the others) and Hormozi (one great offer closes anyone). Lemkin and Martell agree on hiring early and split on whether the next hire buys back founder time or sells.
- Lemkin (venture growth bars: triple, triple, double, double) against Buffett (cash first, no growth bought at any price); Lemkin defers to Buffett on runway and downside.
- Rabois (count the barrels, hire undiscovered talent, judge inputs, no OKRs or pros and cons lists) against Wickman (a system of rocks, scorecards, and meeting pulse) and Martell (buy back founder time with the next hire). Rabois and Leila Hormozi agree on high standards and split on how hard to push: he criticizes in public and acts on the first signal.
- Rabois (in office, hypergrowth bars, hire young and unproven) against Buffett on what a steady business needs; Rabois defers to Buffett on cash and to the people seats on team health.
- Jobs (cut the line to a few great products, build what you would judge yourself, own the whole product) against Gary V and Hormozi (more content, more offers, ship and iterate in public). Jobs and Godin agree on being remarkable and split on who decides: Godin listens to the smallest viable audience, Jobs does not ask customers to design the leap.
- Jobs (do not ship until it is right, fund the product) against Buffett and Graham on cash and proof: Jobs defers to Buffett on what the company can afford and to Graham on testing sooner when the founder has no track record.
- Gates (license widely, win the developers, bet on where the technology is in ten years) against Jobs (control the whole product, few great products). The open platform against the integrated product is their oldest argument.
- Gates (long technology bets, patience for a decade) against Buffett, Hormozi, and Gary V on time horizon: they want cash and results this year. Gates agrees with Buffett on keeping a year of cash and defers to him on what the company can survive.
- Leila Hormozi and Alex Hormozi are different seats and different people. Name them "Leila" and "Hormozi".

If Round 1 comes back unanimous, the Chair should be suspicious and press the seat whose pillar is most at risk in Round 2.
