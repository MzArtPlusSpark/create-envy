# Project Zero: Village UpKeep

Creation #1 on Creatency. Moving Village UpKeep off Bubble and into code Spark owns.

- **Bringer:** Spark (Tiara Taylor), who brings the need: own Village UpKeep outright.
- **Creator:** Spark, with Claude Code, who builds it.
- **Status:** Milestone 2, Discovery. Passes 1 and 2 of the inventory are done. Passes 3 and 4 are still to come.
- **Details:** the full inventory is in [bubble-inventory.md](bubble-inventory.md). Choices are logged in [decisions.md](decisions.md).

## Why this creation comes first

Village UpKeep is a working product, but it lives inside Bubble, so Spark rents it rather than owns it. Moving it into owned code is the first real test of Creatency's own promise: **no meaningful progress is lost.** Every feature Village UpKeep has today should survive the move, be documented along the way and end up fully owned.

It is also the proving ground for Creatency itself. The workshop, the stack and the deploy pipeline built here are the ones Creatency will run on.

## What Village UpKeep is

A household app where kids earn tokens for real effort at home, at school and in their community, and parents guide, approve and reward that work.

| Area | What it does |
|---|---|
| **Households and people** | Families sign up, invite members, label relationships and connect with trusted households. Members can sign in with a code. Each person has a role (adult, minor, staff, partner, sponsor and others). |
| **Chores, duties and tasks** | Chores with token values, photo proof and parent approval. Chores rotate and can be traded for tokens. There are also daily house duties with check-ins, and one-off tasks that can be shared with connected households. |
| **Jobs and bids** | A community job board. Kids pitch for jobs (text, video and price), work in teams, post progress photos and get paid as progress is made. Households can pass a job to another household. |
| **Tokens, store and rewards** | A token ledger, a sponsor-supplied store, household-made perks, wish lists that parents can help fund, streaks, and token bundles bought with real money through Stripe. |
| **Effort and scoring** | Every piece of effort is logged, and households and members get monthly scores against targets. |
| **Ward** | A care companion each member looks after (fed, dressed, fresh, cozy, geared), with care items that members can gift each other. |
| **Keep** | Things a member owns or uses and must keep up, each with duties, a monthly cost and a grace period. |
| **Make It Right** | A careful, private process for when something goes wrong at home: notice, owning it, reflection, repair and prevention, which can turn into a new house agreement. |
| **Passes and requests** | Kids ask for passes (such as going to a friend's) with set requirements, and make formal requests for bigger things like events or purchases. |
| **School** | Catch-up plans, assignments with proof, and regular grade checks, verified by a Steward. |
| **Chat and coach** | Household and job chats, where parents approve their kids joining. There are also private chats with a coach. |
| **Portals** | Separate areas for adults, minors, inventory, owner, partners, sponsors, staff and training. |

## How big it is

| Part | Count |
|---|---|
| Data types | 47 |
| Option sets | 47 |
| Pages | 34 (plus 4 mobile views and 4 reusable elements) |
| Backend workflows | 60 |
| Plugins | 3 (Stripe, API Connector, Copy to Clipboard) |

These counts are from the passes on 2026-11-21. On 2026-11-25 the `test` version had grown to 57 data types, 52 option sets, 39 pages, 77 backend workflows and 4 plugins (a camera plugin was added). Passes 3 and 4 should work from the current `test` version.

This is a large app. It will be rebuilt in pieces, not all at once (decision 1).

## What we learned in Discovery so far

1. **The design is thoughtful.** Most privacy rules are careful and clearly intended, especially Make It Right, school and chat approvals. The rebuild should keep these, not reinvent them.
2. **Some kids' data was public on Live.** Transaction (every kid's token history), HouseholdIntro, TeamMember and ProgressPhoto (kids' job photos) are now fixed and on Live (checked 2026-11-25). Live has no users yet, so no real family's data was exposed.
3. **Money-like values can be changed from the page.** Several spend, streak and status fields auto-save from the person who created the record. Redemption's auto-binding is now off on `test` (no page used it). Perk Redemption, Reward Streak and Outsource Request still have it. In the rebuild, **only server code changes balances and statuses.**
   - Checked 2026-11-25: buying tokens is safe. The wallet's old "charge the card and add tokens on the page" steps are switched off. Buying goes through Stripe Checkout, and `vu_checkout_fulfill` adds tokens only after it verifies the session.
4. **Money logic (pass 3, money part done 2026-11-25):** buying tokens and memberships check with Stripe before giving anything, and most approvals check who's approving. Three gaps carry into the rebuild:
   - **Memberships are never updated after they start:** there's no Stripe webhook, so a cancelled plan still shows "active".
   - **Job approval doesn't check who's calling it.**
   - **Store redemptions run on the page**, and stock isn't checked.

   The balance is a stored number kept in step with the ledger by a "carry" step. The rebuild should make the ledger the only source of truth. Details: [bubble-inventory.md, Pass 3](bubble-inventory.md#pass-3-logic-money-first).
5. **Some privacy rules may be blocking real features.** For example, Outsource Request is hidden from the household it's sent to, and Perk Redemption is hidden from parents. These need a decision, not just a copy.
6. **There's some cleanup to do.** Perk has two "active" fields, and `mock_2` looks like a leftover page.

**Rules for the rebuild that come from this:**
- Every record type starts private ("nobody"), and access is added on purpose.
- Tokens, credit and payouts change only on the server, and every change is written to the ledger.
- Every kid's data is treated as sensitive by default.

## Rebuild plan (proposed)

The rebuild follows Creatency's own lifecycle. Milestones 3 to 6 are in CLAUDE.md. Inside Milestone 5, the app is rebuilt one area at a time, each one usable before the next starts.

**Proposed order** (confirm after passes 3 and 4):

1. **Foundation:** households, people, roles, sign-in (including member codes) and privacy rules.
2. **The core loop:** chores, approvals and the token ledger. This is the heart of the app: work, proof, approval and tokens.
3. **Spending:** store, perks, wish lists and redemptions.
4. **Real money:** Stripe bundles and subscriptions, plus partner payouts. This waits until pass 3 has mapped every money workflow.
5. **Community:** tasks shared with other households, the job board, bids, teams, progress photos and outsourcing.
6. **Growth systems:** effort, monthly scoring, Ward, Keep, passes and requests.
7. **Care systems:** Make It Right, school and chat with the coach.
8. **Portals:** owner, staff, partner, sponsor, inventory and training.

Each step ends with a Progress Package: working code, notes and a list of what's still in Bubble.

## What's left in Discovery

- [x] **Fix live privacy:** Transaction, HouseholdIntro and TeamMember are fixed and on Live.
- [x] **ProgressPhoto:** locked down on `test` (2026-11-25).
- [x] **Deployed to Live (checked 2026-11-25):** ProgressPhoto and Redemption fixes are live. All four once-public types are now private on Live.
- [ ] **Spark:** ProgressPhoto's Owner and staff rule (named "c") says "role is Owner or role is Owner". Change the second Owner to Staff and rename the rule, then deploy. Staff can't see progress photos until then; nothing is exposed.
- [x] **Pass 3, money part:** token purchases, memberships, chore/task/job approval, store redemptions, partner payouts and wish list unlocks.
- [ ] **Pass 3, the rest:** the remaining money helpers, the API Connector call setup (which Stripe key), and every non-money workflow (now 77 in total).
- [ ] **Pass 4, screens:** what each page shows and does, and which pages have inputs linked to money fields.
- [ ] **Answer the open questions below.**
- [ ] **Milestone 2 Progress Package:** this file plus the finished inventory.

## Answers so far

- **Live users (2026-11-25): none.** Village UpKeep hasn't launched, so there's nobody to move and no real data to bring over.
- **The switch (decided 2026-11-25, decision 5):** start fresh. Nothing runs side by side and no data moves. The only real data in Bubble is Spark's own, and Spark will re-enter it. Build the new app, test it, launch it, and retire the Bubble app.
- **The phone app (decided 2026-11-25, decision 6):** launch as a phone-friendly website. A native app is a later milestone (see the [parking lot](parking-lot.md)).
- **Stripe:** Village UpKeep is part of the Art Plus Spark organization. Bubble already connects to Stripe (the Stripe plugin, plus Stripe Checkout through the API Connector). Still to check: which Stripe account those keys belong to, and whether they're test-mode keys. The rebuild uses test-mode keys until launch, kept in `.env` and never committed.

## Open questions for Spark

These shape the plan, and only Spark can answer them.

1. **Coach:** is the coach an AI, a person or scripted messages? Should parents be able to see coach chats?
2. **Privacy choices to make on purpose:** should bid pitch videos be visible to every adult or only the household that posted the job? Should parents see perk redemptions? Should the target household see outsource requests?
3. **`mock_2`:** keep it or drop it?
