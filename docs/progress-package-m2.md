# Progress Package: Milestone 2, Discovery

**Creation:** Project Zero, moving Village UpKeep off Bubble. **Closed:** 2026-11-25.
**North Star check:** Discovery turns "rent it in Bubble" into a written, owned plan. Nothing about the app now lives only inside Bubble.

## What's in the package

| Piece | Where |
|---|---|
| Project Zero written as a Creation: the need, Bringer and Creator, findings, rebuild order | [project-zero.md](project-zero.md) |
| Full Bubble inventory: data types, option sets, privacy, logic (pass 3), screens (pass 4) | [bubble-inventory.md](bubble-inventory.md) |
| Every choice made, with the reason (decisions 5 to 11 came from Discovery) | [decisions.md](decisions.md) |
| Ideas set aside for later | [parking-lot.md](parking-lot.md) |

## Checklist items

- [x] List Village UpKeep's data types, fields and option sets (passes 1 and 2)
- [x] List its pages and key workflows (passes 3 and 4)
- [x] Decide: one codebase or two? **Two.** Village UpKeep gets its own repo (decision 11)
- [x] Write Project Zero as a Creation

## What Discovery decided

- Start fresh: no data moves from Bubble, nothing runs side by side (5).
- A phone-friendly website first; a native app later (6).
- Parents choose whether to see coach chats (7).
- Households set who sees bid videos, perk redemptions and outsource requests (8).
- `mock_2` is dropped (9).
- Sponsor, Partner and Referring agency need approval (10).
- Village UpKeep's code lives in its own repo (11).

## What was fixed in Bubble along the way (all on Live)

- Kids' data that was public is now private: Transaction, HouseholdIntro, TeamMember and ProgressPhoto.
- Pages can no longer auto-save token amounts or statuses on Redemption, Perk Redemption, Reward Streak and Outsource Request.
- `vu_admin_set_role` now requires an Owner.
- ProgressPhoto's staff rule now really checks for Staff.
- Checked: Stripe uses a test key, kept private.

## What carries into the rebuild

These are the gaps the new code must close, not copy:
- Only the server changes balances, statuses and roles. The token ledger is the source of truth.
- A Stripe webhook keeps memberships up to date.
- Job approval, store redemptions and team shares check who's asking and what's in stock.
- Member codes are stored as hashes, with limited tries.
- Every page and every change is checked on the server, not only by redirects.
- Every record type starts private.

## Still in Bubble

Everything. Village UpKeep keeps running on Bubble (test mode, no users) until the new app launches, then Bubble is retired.

## Next: Milestone 3, Definition

Lock in the stack (decisions 3 and 4 are still "proposed"), set the brand basics, create Village UpKeep's new repo, and pick the first piece to build: the foundation (households, people, roles, sign-in).
