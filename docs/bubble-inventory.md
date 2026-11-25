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
- Privacy: was open to everyone, including the photos. **Locked down 2026-11-25, on Live** (see Privacy findings, item 4).

### Tokens, store and rewards

**Transaction** (the token ledger: every earn and spend)
- kid_user (→ User), amount (number), note (text)
- transaction_type (→ transactiontype), transaction_category (→ Transaction Category)
- What it came from: chore (→ Chore), task (→ Task), job (→ Job)
- No household field: the household is only known through kid_user.
- Privacy: was open to everyone, even logged out. **Fixed 2026-11-25 and on Live** (see Privacy findings, item 7).

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
- The creator rule had **auto-binding** on for user, store_item, tokens_spent and status. **Turned off 2026-11-25, on Live** (see Privacy findings, item 8).

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

### Effort and scoring

**Effort Event** (one logged piece of effort, the raw input to monthly scores)
- member (→ User), household (→ Household), day (date), kind (→ Effort Kind), label (text), minutes, step (numbers)
- is_private (yes/no): private effort is hidden from approvers
- Privacy: The member, plus approvers in the household for non-private events.

**Household Score** (one household's score for one period, usually a month)
- household (→ Household), period_start, period_end (dates), member_count
- Targets: chore_target, agreement_target, share_target
- Progress: required_done, agreement_done, improvement_done, makeup_counted, house_total
- Lifecycle (yes/no): close_requested, finish_requested, finished, gap_closed
- Privacy: Same household only.

**Member Score** (one member's share of a Household Score)
- member (→ User), household (→ Household), household_score (→ Household Score), period_start
- Targets and progress: share_target, agreement_target, required_done, agreement_done, improvement_done, makeup_done, total, percent
- Outcome (yes/no): completed_share, closed, rewarded, reward_delivered
- Privacy: Same household only.

### Agreements, Keep and accountability

**House Agreement** (a household rule everyone acknowledges)
- title, agreement_text, is_active (yes/no), household (→ Household)
- acknowledged_by (→ User [list]), created_from_offense (→ Offense)
- Privacy: Household members only.

**Keep Item** (something a member owns or uses and must keep up, with a monthly cost)
- name, category (→ Keep Category), member (→ User), household (→ Household)
- duties (text [list]), monthly_cost, grace_hours (numbers), consequence (text), is_active (yes/no)
- Privacy: The member, plus approvers in the household.

**Keep Agreement** (one period's duties for a Keep Item)
- keep_item (→ Keep Item), member (→ User), household (→ Household)
- duties, duties_done (text [list]), expected_minutes, due_date, earned_date
- status (→ Keep Status), review_note (text)
- Privacy: The member, plus approvers in the household.

**Offense** (the "Make It Right" process: something went wrong at home)
- number, title, notice_text, impact_on_house (text), room (→ Room), scope (→ Offense Scope), status (→ Offense Status)
- People: reporter, owner (→ User), involved_members (→ User [list]), reporter_confirmed (yes/no), reporter_version (text)
- Evidence: evidence_photo (image)
- Process: own_it_deadline, owned_date, closed_date; reflection_questions, repair_checklist, prevention_tips (text [lists])
- Links: house_agreement (→ House Agreement), household (→ Household), is_private (yes/no)
- Privacy, thoughtfully designed:
  - The reporter and the owner see everything.
  - Involved members and the household (non-private only) see everything **except who the owner is**.

**Offense Response** (one member's response to an Offense)
- offense (→ Offense), member (→ User), offense_reporter (→ User), household (→ Household)
- their_side, personal_plan (text), reflection_answers, repair_steps_done (text [lists]), repair_proof (image [list])
- owned_it (yes/no), status (→ Response Status), acknowledged_date, completed_date
- Privacy: Only the responding member and the reporter. Parents who aren't the reporter can't see it.

**Formal Request** (a member asking permission for something bigger, such as an event or a purchase)
- title, details, kind (→ Request Kind), status (→ Request Status), requester, decided_by (→ User)
- Event: event_date, location, who_will_be_there, transportation, contact_name, contact_phone, link (text), photo (image)
- Money: estimated_cost, my_contribution (numbers), offer (text), earn_by (date)
- Conditions: conditions, conditions_done (text [lists]), approver_note, submitted_date
- Privacy: The requester, plus approvers in the household.

**Permission Type** (a household's kinds of pass, such as "go to a friend's house")
- name, description, is_active, always_manual (yes/no), household (→ Household)
- Requirements (yes/no): needs_duties_done, needs_room_photo, needs_school_standing
- Privacy: Household members only.

**Permission Request** (a member asking for a pass)
- member (→ User), permission_type (→ Permission Type), household (→ Household)
- details (text), reasons (text [list]), room_photo (image), requested_date, back_by
- status (→ Pass Status), decided_by (→ User), steward_note (text)
- Privacy: The member, plus approvers in the household.

### School

**School Plan** (a member's plan to catch up or stay on track at school)
- member, set_up_by (→ User), household (→ Household), is_active (yes/no)
- comeback_goal (text), expected_minutes (number), started, first_due, goal_check_date (dates)
- Privacy: The member, plus approvers ("Stewards") in the household.

**School Assignment** (one piece of schoolwork to turn in)
- title, class_name (text), due_date, member, added_by, verified_by (→ User)
- plan (→ School Plan), household (→ Household), status (→ Assignment Status)
- Proof: proof_photo (image), turned_in_date, steward_note (text)
- Privacy: The member, plus approvers in the household.

**Grade Check** (a regular check of grades and missing work)
- member, verified_by (→ User), plan (→ School Plan), household (→ Household), status (→ Grade Check Status)
- Evidence: grades_screenshot, missing_work_screenshot (images), missing_count (number)
- due, turned_in_date, verified_date (dates), turned_in_late (yes/no), member_note, steward_note (text)
- Privacy: The member, plus approvers in the household.

### Messages and activity

**Chat** (a conversation: household, job or other, by chat_type)
- title, chat_type (→ chattype), household (→ Household), job (→ Job)
- Access is controlled by each User's approved_chats list.
- Privacy: Approved participants and the Owner see everything. **Any signed-in user can see every chat's title, type and household.** That's minor, but it's a directory of everyone's chats.

**ChatParticipant** (someone in a chat, with adult approval for minors)
- chat (→ Chat), participant_user (→ User), household (→ Household), pending_approval, has_left (yes/no)
- Privacy: The participant, co-participants, the Owner, and Parents or Leaders in the participant's household. That last group is how parents approve kids joining chats.

**Message**
- chat (→ Chat), sender_user (→ User), sender_household (→ Household), message_text, attachment_file (file), attachment_image (image)
- Privacy: Approved participants, the sender and the Owner only.

**Coach Message** (a member's conversation with a coach; Coach is an option set, possibly an AI coach)
- member (→ User), household (→ Household), coach (→ Coach), from_coach (yes/no), message (text)
- Privacy: Only the member. Parents can't see their kids' coach chats. That's probably intended, but decide it on purpose.

**Activity** (outings or experiences kids can spend tokens on)
- name, description, image, provider (text), token_cost (number), audience (→ activityaudience)
- Approval: approval_status (→ approvalstatus), approved_by, created_by (→ User)
- Privacy: Signed-in users see approved activities. Approvers on the platform see all of them. The creator sees their own.

### Training

**Training Module** (staff and partner training)
- title, description, audience_role (→ userrole), created_by (→ User)
- Privacy: Users whose role matches the audience, plus the creator, the Training team and the Owner.

### Privacy findings so far

1. **HouseholdIntro was fully public.** Its photos and files could be seen and searched without signing in.
   - **Fixed 2026-11-21 in Bubble `test` (Main), on Live by 2026-11-25 (checked on Live).** Now only the sender and recipient households can see an intro. Everyone else sees nothing.
2. **TeamMember was fully public.** Anyone could see which kids accepted which job invitations.
   - **Fixed 2026-11-21 in Bubble `test`, deployed to Live with the 2026-11-25 deploy.** Now visible to the kid themselves, the kid leading the bid, the kid's own household and the household that posted the job. Everyone else sees nothing.
   - Known gap: teammates from *different* households can't see each other's TeamMember records. The bid leader still sees everyone on the team.
3. **Device can be searched by anyone**, which reveals which users have the phone app. Not changed yet: the Bubble connection can't edit this built-in type.
4. **ProgressPhoto was fully public.** Anyone, even logged out, could see and search kids' job photos, linked to the kid's account. **Fixed 2026-11-25 and on Live (checked).** Everyone else now sees nothing. Viewing is allowed for: the kid in the photo; the creator; the kid's household (all members, like Chore); and the household that posted the job. No auto-binding. Bubble's full issue check was clean afterwards. Its Owner and staff rule (named "c") checks Owner twice; Staff still needs adding.
5. **Bid pitch videos are visible to every adult on the platform**, not just the household that posted the job. Not changed yet. It may be intended, but it's worth deciding on purpose.
6. **Outsource Request is hidden from the household it's sent to.** Only its creator can see it. This might stop the target household from ever seeing the request. Check how the page uses it.
7. **Transaction was fully public. Fixed 2026-11-25 and deployed to Live (checked on Live).** Everyone else now sees nothing. Viewing is allowed for: the kid on the transaction; household approvers (through kid_user's household, since Transaction has no household field); the creator; and Owner and staff. No rule allows auto-binding.
8. **Auto-binding on money-like fields.** Redemption (tokens_spent and status), Perk Redemption, Reward Streak and Outsource Request (token_amount and status) let their creator auto-save these fields. A member could change their own spend, streak or status, if a page has a linked input.
   - **Redemption fixed 2026-11-25 and on Live.** No page had inputs linked to it: redemptions are made by button workflows on token_store and portal_inventory. So its auto-binding was turned off, and Bubble's full issue check was clean before and after. Redemption is not exposed through the Data API, so the leftover API create/modify/delete settings on its creator rule have no effect.
   - Perk Redemption, Reward Streak and Outsource Request are not changed yet. Pass 4 should check which pages actually have such inputs. In the rebuild, only server code should ever change balances and statuses.
9. **Perk Redemption is hidden from parents.** Only the person who redeemed it sees it, so parents may not see what their kids spent tokens on.
10. **The chat directory is open to every signed-in user**: titles, types and households of all chats, though not the messages. Minor.
11. **Coach Messages are hidden from parents.** Probably intended. Decide it on purpose for the rebuild.

**Summary after all 47 data types:** 4 types were fully public. HouseholdIntro, TeamMember and Transaction are fixed and on Live; ProgressPhoto is fixed and on Live too. Device can be searched by anyone. Everything else is limited to households, members or roles, and most of it is designed with care.

HouseholdIntro, TeamMember and Transaction also have an **Owner and staff** rule. Spark added it in the editor, because the Bubble connection can't write role checks.

Bubble savepoint taken before the fixes: `1795282240017` (to roll back if needed).

**For the rebuild:** privacy should be decided per record type from the start, with "nobody" as the default, never "everyone."

## Pass 3: logic (money first)

Read 2026-11-25 from the `test` version. This part covers the workflows that move tokens or real money. The other workflows (effort, scoring, school, keep, Make It Right, shopping, earn lookup) and the API Connector call setup are still to read.

### How a token balance works

Each User has a stored **Token Balance** (`wallet_balance`) and a **`ledger_carry`** number. Most money workflows follow the same three steps:

1. **Carry:** set `ledger_carry` = balance − the sum of that user's Transactions. This records any gap between the stored balance and the ledger before the change.
2. **Ledger:** create a Transaction for the amount (positive to earn or deposit, negative to spend or fund).
3. **Reconcile:** set the balance from the new numbers.

So the ledger plus the carry should always explain the balance. **Chore approval doesn't follow this pattern:** it adds to the balance and writes a Transaction, but skips the carry step.

**For the rebuild:** make the Transaction ledger the only source of truth. Work the balance out from it (or check it against it on every write), and do each money change in one database transaction so it can't half-happen.

### Buying tokens (Stripe Checkout)

- **wallet page, "Buy" button:** only Parents, Leaders and Owners, with an amount of at least $1. It creates a Stripe Checkout Session, with the amount × 100 in cents and `client_reference_id` = the user's id, then sends them to Stripe. Older "charge the card and add tokens right here" steps are still on the workflow but **disabled**.
- **Back from Stripe:** the wallet page, on load, calls `vu_checkout_fulfill` with the `session_id`.
- **`vu_checkout_fulfill`:**
  1. Asks Stripe for the session.
  2. **Stops (credits nothing) if** payment_status isn't "paid", the session has no client_reference_id, or a BundlePurchase with that session id already exists. That last check stops double-crediting on reload.
  3. Finds the buyer by client_reference_id, then does carry, a Deposit Transaction of amount × **TokensPerDollar**, a BundlePurchase (dollars, tokens, credit = amount × **CreditPerDollar**, session id) and reconcile.
- Tokens go to the **buyer's own balance** (the parent), not a kid's.
- Small gap: two loads at the same moment could both pass the "already credited?" check before either saves. A database unique key on the Stripe session id fixes this in the rebuild.

### Memberships (Stripe subscriptions)

- **`vu_subscription_fulfill`** (session_id, tier): asks Stripe for the session. It stops unless it's paid and client_reference_id = the household id + "__" + the tier name. Then it sets the Household's tier, Stripe customer id, subscription id, and `subscription_status` = "active".
- ⚠️ **Nothing ever updates the membership after that.** There's no Stripe webhook, so a cancelled subscription or a failed renewal still shows as "active" with the paid tier. **For the rebuild:** use Stripe webhooks (`customer.subscription.updated` / `deleted`, `invoice.payment_failed`) as the source of truth for tier and status.

### Earning

- **`vu_chore_approve`** (chore): stops unless the chore is *Waiting for approval*, it's in the approver's household, the approver is a Parent, Leader, Owner or Staff, and **the approver isn't the kid it's assigned to**. Then it marks the chore approved, adds `token_value` to the kid's balance (plus chores_approved and the Ward meters), and writes a "Chore approved" Reward Payout Transaction. *No carry step (see above).*
- **`vu_task_approve`** (task): runs only if the caller is logged in and **is the task's poster**, the task is Completed (not Paid Out or Cancelled), completed_by is set, payout_requested isn't already yes, and **the poster's balance covers base_reward**. Then it takes base_reward from the poster ("Reward Funding", negative) and gives it to the kid who completed it, with carry and reconcile on both sides. Finally it settles any Task Incentives.
- **`vu_task_myself`:** the poster marks a task done by themselves. No tokens move, but incentives are settled.
- **`vu_job_approve`** (job): runs if the job isn't already Completed and **the parent_user's balance covers pay_amount**. Then the parent pays pay_amount; the bid leader gets pay − (floor(pay ÷ (team + 1)) × team), and each teammate gets floor(pay ÷ (team + 1)) through `vu_job_team_share`. Any rounding remainder goes to the leader.
  - ⚠️ **It doesn't check who is calling it.** Unlike task and chore approval, there's no "caller is the job's parent" test inside the workflow. It isn't a public API, so it can only be started from the app's own pages, and those may check. But the check belongs in the workflow. **For the rebuild:** every money action checks permission on the server.

### Spending

- **Token store, "Redeem"** (token_store page): runs on the page, not in a backend workflow. It checks that the user is logged in, their balance ≥ token cost and the item is Approved. Then it does carry, creates a Redemption, writes a spend Transaction and reconciles. Perks and activities follow the same pattern.
  - Stock goes down only when Inventory marks the redemption delivered (portal_inventory). A popular item can be redeemed more times than there's stock.
  - **For the rebuild:** do redemptions on the server, inside one database transaction that checks the balance and the stock.
- **"Record partner payout on a new redemption"** (a database trigger): when a Redemption is created, it sets the supplier to the Store Item's creator, payout_owed to the item's `partner_payout_per_item`, and payout_paid = no. **Nothing here pays the partner.** Paying out is done by hand, outside the app.
- **`vu_reward_unlock`** (wish list item): runs if the caller is the kid or a Parent, Leader or Owner in the kid's household, the item isn't already unlocked, **the kid's balance covers the price**, and parents have contributed at least the target credit. Then it unlocks the item, creates a Redemption and spends the tokens (carry, Transaction, reconcile).

### The other money helpers

- **`vu_task_incentive_settle`** (incentive, earner): stops if the amount is 0 or less, or the contributor can't cover it. Otherwise it moves the amount from the contributor to the earner (carry, Transaction, reconcile on both sides).
- **`vu_job_team_share`** (member, job, share): stops if the share is 0 or less, or the member has no kid. Otherwise it pays the share to that teammate. **The amount is passed in by the caller.** Only `vu_job_approve` calls it, but the rebuild should work the share out on the server, not accept it as input.
- **`vu_reward_delivered`** (wish list item): only a Parent, Leader or Owner in the kid's household, for an unlocked item not yet delivered. It marks the item and its Redemption delivered. No tokens move.
- **"Grant Parent Contribution Credit for a bundle"** (database trigger on a new BundlePurchase): adds `credit_granted` to the buyer's `parent_contribution_credit`.
- **"Log Parent Contribution Credit on a wish list goal"** (database trigger): when a wish list item's parent_contributed_credit goes up, it writes a Transaction to log it. The contribution itself is made on the wallet page, which changes the item and the parent's credit straight from the page.
- **`effort_from_payout`** (database trigger on a new Reward Payout Transaction): logs Effort Events for the kid, so earning feeds the effort score.
- **`earn_task_verified`** (database trigger): when a Payback Task becomes Verified, it logs an Effort Event and updates its Formal Request.
- **Chore transfers:** `vu_transfer_accepted` runs only if the caller is the request's `to_user` in the same household, the request is still Requested with from_agreed = yes, the chore is still assigned to the from_user and Pending Transfer, and **the from_user can cover the offered tokens**. Then it moves the chore and pays the offer from the from_user to the to_user. `vu_transfer_declined` gives the chore back.

### Outside services (API Connector)

| Call | Goes to | Key | Used by |
|---|---|---|---|
| Stripe Checkout: Create Checkout Session, Create Subscription Checkout Session, Retrieve Checkout Session | api.stripe.com | Set on the collection, so it can't be read here. **Test mode:** the saved example session id starts with `cs_test_`. | Wallet (tokens), membership page, the two fulfil workflows |
| "Claude Coach" API Call | api.anthropic.com, model claude-sonnet-5-5 | `x-api-key` marked **private** | The coach chat, and `shop_read_receipt` (reading shopping receipts) |
| "Product Page: Read page" | Any web address: `https://[page]` | None | `earn_lookup`, which reads a product page from a Formal Request's link to find a price |

- **The coach is an AI** (Claude), with a written system prompt: plain and warm, no blame, no diagnosing, and a hand-off to a Lantern Steward if safety comes up. That answers part of open question 1 in project-zero.md. Kids' coach messages and receipt photos are sent to Anthropic, so the rebuild needs a privacy note that says so.
- Spark should check in Bubble (Plugins → API Connector → Stripe Checkout) that the Stripe key is **marked private** and is a **test** key (`sk_test_…`). The tool can't see keys set on the collection.
- "Read page" fetches any address a user types into a Formal Request link. It's low risk, but the rebuild should only allow `https` and block private network addresses.
- The saved example values in these calls (an email address, version-test URLs, a Stripe price id) are only used to set the calls up. The workflows pass real values.

### Sign-in, households and roles

- **Code sign-in (`vu_code_login`):** given an 8-character code, it returns that member's **login email and actual password ("secret")** to the page, which then signs in with them. `vu_add_member` and `vu_new_member_code` create the account, set a temporary password, and save the code, email and password in a **Member Login** record. Member Login is private to everyone, and only workflows read it.
  - ⚠️ So the password is stored as plain text, sent to the browser, and anyone who has a code has the full password. There's also no limit on how many codes someone can try.
  - **For the rebuild:** treat the code as a password. Store only a hash, check it on the server, never send a password to the browser, and limit failed tries. Auth.js can do this with a custom "member code" sign-in.
- **Joining a household (`vu_join_household`):** it needs an unused, unexpired invite code. It puts the user in that household **as a Kid** and marks the invite used.
- **Roles:**
  - `vu_set_user_role` changes a role only if the caller is an **Owner**.
  - **`vu_admin_set_role` had no check at all. Fixed by Spark 2026-11-25 and on Live (checked): it now runs only when Current User's role is Owner.** Before the fix, it set any user's role to whatever it was given, so anyone who could start it from a page could have made themselves Owner.
  - "Keep approval permission aligned with role" (`vu_role_sync`) updates `is_approver` whenever a role changes.
- **Connected households (`vu_trust_sync`):** when a HouseholdIntro links two households, it updates both households' `connected_households`. This is what lets tasks with "Connected households" visibility be seen.
- **Chat access (`vu_chat_grant`, `vu_chat_revoke`):** when a ChatParticipant is approved (not pending, not left), it adds the chat to the user's `approved_chats`. That list is what the Message privacy rule checks. Pass 4 should check that only an approver can set pending_approval to no.

### Scheduled and repeating work

- **Chore periods:** a new weekly or monthly chore sets its due date and starts a Bubble **recurring event**, "Start the next chore period". Each period it sets "Done this period" chores back to Active and moves the due date on.
- **Chore rotation (`vu_rotation_day`):** creates one chore, then schedules itself again for the next one (i + 1 < total), spreading a rotation across members.
- **Monthly scores (`vu_month_cycle`):** closes this month's scores, schedules `vu_month_finish` 10 minutes later, updates households, then **schedules itself for 5 minutes past the start of next month**. Something has to start it the first time. Check Bubble's Logs → Scheduler that it's queued on Live.
- **Score triggers:** opening a household's score (score_open_household and score_open_member) creates Household and Member Scores. Every new Effort Event (`effort_score`) adds to the member's score. Closing a score (score_close_*, score_finish_household) totals it.
- **Keep (`keep_due`, `keep_grace_end`):** on the due date, it closes this Keep Agreement period, creates the next one, schedules the next `keep_due`, and schedules `keep_grace_end` for when the grace hours run out.
- **School (`school_week_close`):** closes this week's Grade Check, creates next week's, and schedules itself again.
- The rebuild needs a scheduler for all of these, for example EventBridge Scheduler on AWS calling the app. Each job should be safe to run twice.

### Not read in detail

These were read at the name and trigger level only. They don't move tokens or money: the 10 effort_* workflows other than effort_score and effort_from_payout, mir_add_member, mir_owned, mir_check_done (Make It Right), school_notify_steward, school_plan_started, school_check_turned_in, school_work_turned_in, walk_add_finding, vu_ward_help, shop_price_line, earn_lookup_read, earn_lookup_fallback, earn_plan_start, earn_plan_line, vu_check_email, vu_check_invite. Read them in detail when their area is rebuilt.

## Pass 4: screens (first slice first)

Read 2026-11-25 from `test`. This pass read in detail the pages the first rebuild slice needs (sign-in, households, chores, approvals, wallet, store), plus the chat pages for the approval question from pass 3. Other pages are listed at the end, to read when their area is rebuilt.

**How every page is protected:** each portal and work page has a "Page is loaded" guard. Signed-out visitors go to `index`, and the wrong role goes to `index` (or `portal_minor` for kids on adult pages). New adults and kids who haven't chosen a Ward are sent to `choose-ward` first. These are page-level redirects only. The real protection is the privacy rules and the checks inside backend workflows. **For the rebuild:** check the role on the server for every page and action, not just with a redirect.

### Sign-in and onboarding

- **`get-started`** (3 steps):
  1. **Create your account:** pick an Account Type, then enter name, email and password, and sign up. The role is set from the account type: any type with `creates_household` → **Leader**; Staff → **Training** (not Staff); Sponsor, Partner and Referring agency go to their own portals.
  2. **Set up your household:** a name and a plan create the Household.
  3. **Add your family:** name and birthday, one at a time, through `vu_add_member`. Each person gets a member code shown on screen ("write it down"). Adults are sent to `portal_adult` when done.
  - Account types: Adult homemaker, Minor homemaker admin, Staff, Sponsor, Partner, Referring agency. **Sponsor, Partner and Agency are self-chosen with no vetting.** Their store items still need approval, but decide on purpose whether these roles need a check.
- **`member-login`:** a single "Member code" box (for example AB12CD34). It calls `vu_code_login`, logs in with the email and password that come back, then goes to `portal_minor` (kids) or `portal_adult`. See pass 3 for why this must change in the rebuild.
- **`index`, `reset_pw`:** the public home and password reset (not read in detail).

### Households

- **`household-setup`** (adults only; kids are sent to portal_minor):
  - Verification: submit a trusted adult's name and contact, or upload a verification document. **Staff** verify or send back on `portal_staff`.
  - Connections: send a HouseholdIntro to another household, and approve or decline incoming intros (`vu_trust_sync` then links them).
  - Members: add a member (`vu_add_member`), make a new member code (`vu_new_member_code`), copy it, and generate a minor join code (a Household Invite).
- **`portal_adult`** (Parent and Leader): generate a minor join code, **approve or decline a minor's request to join community chat**, and links to chores, approvals and household-setup.
- **`portal_minor`** (Kids): links to the wish list (wallet), chores, jobs and team chat, and an "ask to join community chat" button.

### Chores and approvals

- **`chores`:** a week calendar of chores.
  - Parents add chores (a token minimum is enforced with an alert), build a **rotation** (`vu_rotation_day`), edit or delete one chore or a list, and **approve** (`vu_chore_approve`, then a "Token Burst" celebration popup).
  - Kids mark chores done with proof and **request a transfer** (a ChoreTransferRequest with a token offer; the chore becomes Pending Transfer). The other kid accepts (`vu_transfer_accepted`, with an alert if the offerer can't pay) or declines.
- **`approvals`:** approve or reject **Activities, Perks and Store Items**. Chore approval happens on the chores page, not here.
- **`wallet`** and **`token_store`:** read in pass 3 (buying tokens, the wish list, parent credit, redeeming).
- **`portal_inventory`** (Inventory and Owner): update reward stock, and mark redemptions delivered (stock goes down at delivery).

### Chat (answers the pass 3 question)

- **Kids can't let themselves into a chat.** When a Kid presses "Join" on `team-chat`, or "ask to join" on `portal_minor`, their ChatParticipant is created with **pending_approval = yes**. Adults joining a chat from a verified household (Community, or a Household chat from their own or a connected household) are approved straight away. When a job lead invites a kid to a team chat, the kid also starts pending.
- Only **Parents and Leaders in the kid's household** approve or decline, on `portal_adult`. ChatParticipant has no auto-binding, so a kid can't flip pending from an input.
- When an approval clears pending, `vu_chat_grant` adds the chat to the kid's approved_chats, and Message privacy follows from that.
- **One rule of Bubble to remember:** privacy rules control what people can *see*. They don't stop a page workflow from *changing* something the user can see. Who can change what in Bubble is set by each page's workflow conditions. The rebuild must check every change on the server.

### Pages not read in detail yet

`index`, `profile`, `reset_pw`, `tasks`, `jobs`, `calendar`, `requests`, `passes`, `effort`, `make-it-right`, `my-keep`, `membership`, `choose-ward`, `my-ward`, `my-people`, `school`, `got-your-back`, `show-me`, `shopping`, `walkthrough`, `payback`, `portal_owner`, `portal_partner`, `portal_sponsor`, `portal_training`, `404`, `mock_2`, plus the 4 mobile views and the reusable header, sidebar, offline_banner and phone_bar. Read each one when its area is rebuilt.

Also still open from pass 2: whether any page has inputs auto-saving into **Perk Redemption, Reward Streak or Outsource Request** money fields. Since Live has no users, turn their auto-binding off at the next Bubble session, the same way as Redemption, and let Bubble's issue check name anything that breaks.

## Next passes

1. **Pass 2, data:** done.
2. **Pass 3, logic:** done 2026-11-25 (see above). Non-money workflows were read at overview level only.
3. **Pass 4, screens:** first-slice pages done 2026-11-25 (see above). The other pages are read when their area is rebuilt.
