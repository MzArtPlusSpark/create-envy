# Decisions

One line per choice, with the reason. Change a decision by adding a new line, not by deleting the old one.

| # | Date | Decision | Why |
|---|---|---|---|
| 1 | 2026-11-21 | Build Creatency from owned source code, not Bubble | Full ownership of the code; step by step, not a big-bang rewrite |
| 2 | 2026-11-21 | Brand: navy, mustard gold, white, slate grey; Space Grotesk + Inter; Kee as the ownership companion | Matches the lamination pack; recorded in the Creatency design system |
| 3 | 2026-11-21 | Proposed stack: Next.js + TypeScript, PostgreSQL + Prisma, Auth.js | One codebase for pages and server; widely used; easy to deploy on AWS. Confirm in Milestone 3 |
| 4 | 2026-11-21 | Hosting target: AWS, region us-east-2 | Learning AWS first; matches the AWS account already set up |
| 5 | 2026-11-25 | Village UpKeep starts fresh in the new code: no data migration from Bubble, no side-by-side run | No real households use it yet; the only real data is Spark's own, which Spark will re-enter |
| 6 | 2026-11-25 | Launch as a phone-friendly browser website; native app is a later milestone | A website is enough for now; the Bubble native mobile views are not rebuilt yet |
| 7 | 2026-11-25 | Coach chats: each parent chooses whether to see their kids' coach chats (a setting, not a fixed rule) | Families differ; the choice belongs to the parent |
| 8 | 2026-11-25 | Who sees bid pitch videos, perk redemptions and outsource requests is set per household by the person who created the household account | Each household decides its own privacy; the rebuild ships these as household settings |
| 9 | 2026-11-25 | Drop the `mock_2` page; it is not rebuilt | Leftover page with no real use |
| 10 | 2026-11-25 | Sponsor, Partner and Referring agency need a check before the role is given; they are no longer self-chosen at sign-up | These roles can put items and offers in front of kids, so they must be approved first |
| 11 | 2026-11-25 | Village UpKeep's new code gets its own private GitHub repo; create-envy keeps Creatency and the Project Zero record | Each app stays one simple project, and Village UpKeep can be owned or handed off on its own |
| 12 | 2026-11-25 | Stack confirmed (replaces the "proposed" in decision 3): Next.js with TypeScript, PostgreSQL with Prisma, hosted on AWS us-east-2 (Amplify Hosting and RDS) | Checked against today's tools: all still current, and Amplify runs current Next.js. Same stack for Creatency and Village UpKeep |
| 13 | 2026-11-25 | Sign-in: Better Auth, not Auth.js (changes decision 3) | Auth.js handed new work to Better Auth in September 2025 and now gets security fixes only. Better Auth runs in our own code and database, and has email and password, Google, username sign-in (for kids' member codes) and limits on wrong tries built in |
| 14 | 2026-11-25 | Rebuild order confirmed; the first piece is the foundation: households, people, roles and sign-in (including kids' member codes) | Everything else needs to know who someone is and which household they're in, and Discovery found the biggest risks here (plain-text passwords, unchecked role changes) |
