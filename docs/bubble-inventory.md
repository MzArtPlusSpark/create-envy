# Village UpKeep: Bubble inventory

What Village UpKeep already is in Bubble, written down before it is rebuilt as owned code (Project Zero, Creation #1).

- Bubble app: `kidgig` (display name: Village UpKeep), development version
- Read on: 2026-11-21, through the Bubble connection, read only. Nothing in Bubble was changed.
- Status: **Pass 1, names only.** Fields, page contents and workflow steps come in later passes.

## At a glance

| Part | Count |
|---|---|
| Pages | 34 |
| Mobile views | 4 |
| Reusable elements | 4 |
| Data types | 47 |
| Option sets | 47 |
| Backend workflows | 60 |
| Styles | 48 |
| Global expressions | 2 |
| Plugins | 3 |

## Data types (47)

Grouped by what they appear to do, judging from their names. Pass 2 will confirm each group by reading its fields.

**People and households (8):** User, Household, HouseholdIntro, Household Invite, Relationship, TeamMember, Member Login, Device

**Chores, tasks and jobs (10):** Chore, ChoreTransferRequest, House Duty, Duty Checkin, Task, TaskIncentive, Job, Bid, Outsource Request, ProgressPhoto

**Tokens, store and rewards (9):** Transaction, Store Item, Redemption, BundlePurchase, Perk, Perk Redemption, Reward Streak, WishListItem, Ward Gift

**Effort and scoring (3):** Effort Event, Household Score, Member Score

**Agreements, Keep and accountability (8):** House Agreement, Keep Agreement, Keep Item, Offense, Offense Response, Formal Request, Permission Request, Permission Type

**School (3):** School Plan, School Assignment, Grade Check

**Messages and activity (5):** Chat, ChatParticipant, Message, Coach Message, Activity

**Training (1):** Training Module

## Option sets (47)

Room, Ward, Coach, Cal Day, Cal Week, chattype, userrole, workkind, bidstatus, Care Kind, Duty Kind, jobstatus, Ward Item, Chore Level, chorestatus, Effort Kind, introstatus, Keep Status, Pass Status, Account Type, Request Kind, Task Category, Chore Catalog, Effort Weight, Funding Source, jobdifficulty, jobtimewindow, Keep Category, Offense Scope, approvalstatus, intromediatype, Offense Status, Request Status, taskstatus_new, transferstatus, Membership Tier, Outsourcestatus, Response Status, transactiontype, activityaudience, Redemption Status, Assignment Status, Grade Check Status, verificationmethod, verificationstatus, Recurrence Frequency, Transaction Category

## Pages (34)

**Sign-in and onboarding (7):** index, get-started, member-login, reset_pw, household-setup, choose-ward, membership

**Daily work (9):** chores, tasks, jobs, approvals, requests, calendar, effort, passes, school

**Money and rewards (2):** wallet, token_store

**People and home (6):** profile, my-people, my-ward, my-keep, make-it-right, team-chat

**Role portals (8):** portal_adult, portal_minor, portal_inventory, portal_owner, portal_partner, portal_sponsor, portal_staff, portal_training

**Other (2):** 404, mock_2 (looks like a leftover mock-up; check before rebuilding)

**Mobile views (4):** Home, Home1, update_app, reset_password

**Reusable elements (4):** header, sidebar, offline_banner, phone_bar

## Backend workflows (60)

**Roles and access (6):** vu_role_sync (keep approval permission aligned with role), vu_set_user_role, vu_admin_set_role, vu_trust_sync (synchronize mutually approved households), vu_chat_grant, vu_chat_revoke

**Households and sign-in (7):** vu_check_invite, vu_join_household, vu_add_member, mir_add_member, vu_code_login, vu_check_email, vu_new_member_code

**Chores (6):** vu_chore_reset (start the next chore period), vu_chore_schedule (weekly and monthly resets), vu_chore_approve, vu_transfer_accepted, vu_transfer_declined, vu_rotation_day

**Tasks and jobs (5):** vu_task_approve, vu_task_myself, vu_task_incentive_settle, vu_job_approve, vu_job_team_share

**Rewards and payments (7):** vu_reward_unlock, vu_reward_delivered, vu_bundle_credit (Parent Contribution Credit for a bundle), vu_contribution_log (Parent Contribution Credit on a wish list goal), Record partner payout on a new redemption, vu_checkout_fulfill, vu_subscription_fulfill

**Effort and monthly scoring (19):** effort_duty_checkin, effort_keep, effort_cond, effort_req, effort_log, effort_own, effort_side, effort_refl, effort_rep, effort_plan, effort_score, effort_from_payout, vu_month_cycle, vu_month_finish, score_open_household, score_open_member, score_close_household, score_close_member, score_finish_household

**Keep and Make It Right (4):** keep_due, keep_grace_end, mir_owned, mir_check_done

**School (5):** school_plan_started, school_work_turned_in, school_check_turned_in, school_week_close, school_notify_steward

**Ward (1):** vu_ward_help

## Plugins and outside services

- **Stripe:** payments (checkout and subscriptions, per the workflows above)
- **API Connector:** calls to outside services; pass 3 will list which ones
- **Copy to Clipboard**

Global expressions: CreditPerDollar, TokensPerDollar (the exchange rates between money, credit and tokens).

## Pass 2: data (fields and privacy)

Every type also has Bubble's built-in fields: Created By, Created Date, Modified Date and Slug. They are left out below. `→ Type` means a link to another record, and `[list]` means it holds many.

### People and households

**User**
- Identity: email, name, preferred_name, birthday (date), phone, contact_email, avatar_image (image), member_code
- Role: role (→ userrole), account_type (→ Account Type), household_role (text), is_approver (yes/no), coach (→ Coach)
- Household: household (→ Household), approved_chats (→ Chat [list])
- Tokens and credit: wallet_balance (number, shown as "Token Balance"), ledger_carry, parent_contribution_credit
- Ward: ward (→ Ward), ward_chosen (yes/no), ward_changes_used (number)
- Care meters (dates): fed_until, dressed_until, fresh_until, cozy_until, geared_until
- Care pieces (numbers): food_pieces, clothing_pieces, hygiene_pieces, room_pieces, gear_pieces
- Work profile: skills, tools_owned, availability (text), rating (number), promo_video (file), chores_approved (number)
- Scoring: score_open_for (→ Household Score)
- Privacy: 6 rules
  - Owner and Staff see everything.
  - Users see all of their own data.
  - Adults see most fields of people in their household.
  - Kids see household members' progress but not their credit.
  - Connected households see only names.
  - Everyone else sees a public work profile: name, avatar, skills, rating and promo video.

**Household**
- name, connected_households (→ Household [list])
- Membership: tier, pending_tier (→ Membership Tier), subscription_status (text)
- Stripe: stripe_customer_id, stripe_subscription_id (text)
- Verification: verification_method (→ verificationmethod), verification_status (→ verificationstatus), verification_document (file)
- Safety: trusted_adult_name, trusted_adult_contact (text)
- Scoring: score_open_requested (date)
- Privacy: Owner and Staff see everything. Household members see everything. Logged-in users see the name, connections and verification status. Everyone else sees nothing.

**HouseholdIntro** (one household introducing itself to another)
- sender_household, recipient_household (→ Household)
- sender_status, recipient_status (→ introstatus)
- media_type (→ intromediatype), media_file (file), media_image (image)
- Privacy: ⚠️ **Everyone sees everything, including the media, even when logged out.**

**Household Invite**
- code, household (→ Household), created_by (→ User), expiry_date, used (yes/no), used_by (→ User)
- Privacy: The creator and the household's Parents or Leaders see it. Everyone else sees nothing.

**Relationship** (how two members are related, such as "Mom")
- from_member, to_member (→ User), household (→ Household), label (text)
- Privacy: Household members only.

**TeamMember** (a kid on a team bidding for a Job)
- kid_user (→ User), bid (→ Bid), invited_at (date), accepted_invite, joined_mid_job (yes/no)
- Privacy: ⚠️ **Everyone sees everything, which reveals which kids are on which jobs.**

**Member Login** (code-based sign-in for members)
- member (→ User), household (→ Household), login_email, code, secret (text)
- Privacy: Nobody sees it on screen, so only backend workflows can use it. Good, because it holds a secret.

**Device** (phone app push notifications)
- current_user (→ User), device_type, push_notification_token (text)
- Privacy: Everyone can find a device and see its type and user. The token stays hidden.

### Chores, tasks and jobs

**Chore** (household chores, earned in tokens)
- title, description, room (→ Room), level (→ Chore Level), minutes, token_value (number)
- People: assigned_to, assigned_by, approved_by (→ User)
- Timing: frequency (→ Recurrence Frequency), due_date, submitted_date, last_completed_date, rotation_id (text)
- Proof: proof_photo (image), proof_note, sent_back_note (text)
- status (→ chorestatus), household (→ Household)
- Privacy: Household members only.

**ChoreTransferRequest** (one member offering tokens to pass a chore to another)
- chore (→ Chore), from_user, to_user (→ User), offer_tokens (number)
- from_agreed, to_agreed, settled (yes/no), status (→ transferstatus), household (→ Household)
- Privacy: Household members only.

**House Duty** (a recurring daily duty, such as cooking dinner on set days)
- name, kind (→ Duty Kind), member (→ User), days (→ Cal Day [list]), start_time (date), prep_minutes
- proof_required, is_active (yes/no), household (→ Household)
- Privacy: Household members only.

**Duty Checkin** (proof a duty was done on a given day)
- duty (→ House Duty), member (→ User), day (date), photo (image), household (→ Household)
- Privacy: Household members only.

**Task** (one-off work posted by a member, which can be shared with connected households)
- title, description, base_reward (number), visibility (text: own household or "Connected households")
- People: posted_by, claimed_by, completed_by (→ User)
- self_completion, payout_requested (yes/no), status (→ taskstatus_new), household (→ Household)
- Privacy: The household sees it. Connected households also see it when visibility is "Connected households."

**TaskIncentive** (extra tokens someone adds on top of a Task's reward)
- task (→ Task), contributor (→ User), amount (number), visibility (text), household (→ Household)
- Privacy: The same as Task.

**Job** (bigger paid work on the community job board)
- title, description, job_image (image), task_category (→ Task Category), difficulty (→ jobdifficulty), time_window (→ jobtimewindow)
- Pay: pay_amount, funding_source (→ Funding Source), progress_percent, released_percent (numbers: pay is released as progress is made)
- People: parent_user, assigned_to (→ User), accepted_bid (→ Bid), household (→ Household), is_household_assigned (yes/no)
- Repeats: is_recurring (yes/no), recurrence_frequency (→ Recurrence Frequency)
- requires_camera_proof (yes/no), status (→ jobstatus)
- Privacy: Owner and Staff see everything. **Any signed-in user who has a household sees every job on the platform**, including pay and who it's assigned to. That looks intended (it's the community board).

**Bid** (a kid's pitch for a Job)
- job (→ Job), kid_user (→ User), pitch_text, pitch_video (file), proposed_price (number), status (→ bidstatus)
- Privacy: The bidder sees it. **So does every Parent, Leader, Owner and Staff member on the platform, in any household**, including the kid's pitch video.

**Outsource Request** (one household asking another to take a Job for tokens)
- job (→ Job), requesting_household, target_household (→ Household), token_amount (number), status (→ Outsourcestatus)
- Privacy: Only the person who created it can see it. **The household it's sent to can't see it**, which may be a bug.

**ProgressPhoto** (a kid's photo showing progress on a Job)
- job (→ Job), kid_user (→ User), photo_image (image), caption (text), progress_percent (number), captured_via_camera (yes/no)
- Privacy: ⚠️ **Everyone sees everything, including the photos, even when logged out.**

### Tokens, store and rewards

**Transaction** (the token ledger: every earn and spend)
- kid_user (→ User), amount (number), note (text)
- transaction_type (→ transactiontype), transaction_category (→ Transaction Category)
- What it came from: chore (→ Chore), task (→ Task), job (→ Job)
- No household field: the household is only known through kid_user.
- Privacy: ⚠️ **Everyone sees everything, even when logged out.** That's every kid's earnings history.

**Store Item** (rewards kids can buy with tokens, often supplied by a sponsor or partner)
- item_name, description, item_image (image), token_cost, stock_quantity (numbers)
- Sponsor: sponsor_name (text), partner_payout_per_item (number)
- Approval: approval_status (→ approvalstatus), approved_by, created_by (→ User)
- Privacy:
  - Signed-in users see approved items.
  - Approvers (is_approver = yes) see every item, in any household.
  - The creator sees their own items.
  - Inventory, Owner and Staff see everything.

**Redemption** (a kid buying a Store Item)
- user (→ User), store_item (→ Store Item), tokens_spent (number), status (→ Redemption Status), activity (→ Activity)
- Delivery: delivered_by (→ User), delivered_date
- Partner payout: supplier (→ User), payout_owed (number), payout_paid (yes/no), payout_paid_date
- Privacy: The redeemer, the creator, and Inventory, Owner and Staff.
- ⚠️ The creator rule has **auto-binding** turned on for user, store_item, tokens_spent and status. If a page has an input linked to those fields, a kid could change what they spent, or mark their own redemption as delivered.

**BundlePurchase** (a parent buying a token bundle with real money)
- buyer (→ User), household (→ Household), bundle_name, dollars_paid, tokens_granted, credit_granted, stripe_charge_ref
- Privacy: The buyer, plus adults (not kids) in the same household.

**Perk** (household-made rewards, such as "pick the movie")
- name, description, token_cost, household (→ Household), created_by, approved_by (→ User), approval_status (→ approvalstatus)
- Two "active" fields: active? and is_active (yes/no). **Duplicate field**: the rebuild should keep only one.
- Privacy: Approved perks are visible to their household. Every approver on the platform sees all perks. The creator sees their own.

**Perk Redemption** (a member spending tokens on a Perk)
- perk (→ Perk), redeemed_by (→ User), redeemed_date, tokens_spent, status (→ Redemption Status)
- Privacy: Only the creator. **Parents in the household can't see it.**
- ⚠️ Auto-binding is on for every field, so the same tampering risk as Redemption applies.

**Reward Streak** (days in a row a member finished a task category)
- user (→ User), task_category (→ Task Category), current_streak, longest_streak (numbers), last_completed_date
- Privacy: Only the member.
- ⚠️ Auto-binding is on for every field, so a member could edit their own streak.

**WishListItem** (a kid saving up for something, which parents can help fund)
- kid_user (→ User), household (→ Household), item_name, item_image, price, store_item (→ Store Item)
- Saving: saved_amount, parent_target_credit, parent_contributed_credit (numbers)
- Outcome: unlocked (yes/no), unlocked_date, delivered (yes/no), redemption (→ Redemption), activity (→ Activity)
- Privacy: The kid, plus Parents and Leaders in the same household.

**Ward Gift** (one member giving another a care item for their Ward)
- given_by, member (→ User), item (→ Ward Item), household (→ Household)
- Privacy: Household members only.

### Privacy findings so far

1. **HouseholdIntro was fully public.** Its photos and files could be seen and searched without signing in.
   - **Fixed 2026-11-21 in Bubble `test` (Main), not yet deployed to Live.** Now only the sender and recipient households can see an intro. Everyone else sees nothing.
2. **TeamMember was fully public.** Anyone could see which kids accepted which job invitations.
   - **Fixed 2026-11-21 in Bubble `test`, not yet deployed to Live.** Now visible to the kid themselves, the kid leading the bid, the kid's own household and the household that posted the job. Everyone else sees nothing.
   - Known gap: teammates from *different* households can't see each other's TeamMember records. The bid leader still sees everyone on the team.
3. **Device can be searched by anyone**, which reveals which users have the phone app. Not changed yet: the Bubble connection can't edit this built-in type.
4. **ProgressPhoto is fully public.** Anyone, even logged out, can see and search kids' job photos, linked to the kid's account. Not changed yet.
5. **Bid pitch videos are visible to every adult on the platform**, not just the household that posted the job. Not changed yet. It may be intended, but it's worth deciding on purpose.
6. **Outsource Request is hidden from the household it's sent to.** Only its creator can see it. This might stop the target household from ever seeing the request. Check how the page uses it.
7. **Transaction is fully public.** Anyone, even logged out, can see and search every kid's token earnings and spending, with notes. Not changed yet. It has no household field, so a fix would go through kid_user's household.
8. **Auto-binding on money-like fields.** Redemption (tokens_spent and status), Perk Redemption, Reward Streak and Outsource Request (token_amount and status) let their creator auto-save these fields. A member could change their own spend, streak or status, if a page has a linked input. Pass 4 should check which pages actually have such inputs. In the rebuild, only server code should ever change balances and statuses.
9. **Perk Redemption is hidden from parents.** Only the person who redeemed it sees it, so parents may not see what their kids spent tokens on.

Both types also have an **Owner and staff** rule. Spark added it in the editor, because the Bubble connection can't write role checks.

Bubble savepoint taken before the fixes: `1795282240017` (to roll back if needed).

**For the rebuild:** privacy should be decided per record type from the start, with "nobody" as the default, never "everyone."

## Next passes

1. **Pass 2, data:** read every data type's fields and privacy rules, and every option set's values. This becomes the starting point for the Prisma data model in milestone 4.
2. **Pass 3, logic:** read the steps of each backend workflow and the API Connector calls, especially anything that touches money (Stripe, tokens, payouts).
3. **Pass 4, screens:** note what each page shows and does, so milestone 5 knows what to rebuild first.
