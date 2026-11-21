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

## Next passes

1. **Pass 2, data:** read every data type's fields and privacy rules, and every option set's values. This becomes the starting point for the Prisma data model in milestone 4.
2. **Pass 3, logic:** read the steps of each backend workflow and the API Connector calls, especially anything that touches money (Stripe, tokens, payouts).
3. **Pass 4, screens:** note what each page shows and does, so milestone 5 knows what to rebuild first.
