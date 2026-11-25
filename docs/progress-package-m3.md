# Progress Package: Milestone 3, Definition

**Creation:** Project Zero, moving Village UpKeep off Bubble. **Closed:** 2026-11-25.
**North Star check:** the tools are chosen once, written down with reasons, and are all ones Spark owns or controls. That keeps the creation moving toward ownership.

## Checklist items

- [x] App framework: **Next.js with TypeScript** (decision 12)
- [x] Database: **PostgreSQL with Prisma** (decision 12)
- [x] Sign-in: **Better Auth**, with email and password, Google and member codes (decision 13). This changes the plan's Auth.js; see the reason in decisions.md.
- [x] Write docs/decisions.md: decisions 11 to 14 were added in this milestone
- [x] Brand basics for Creatency: [brand.md](brand.md), with the full system in the design system artifact

## Also decided

- Village UpKeep's code gets its own private repo (decision 11).
- Hosting stays AWS us-east-2: Amplify Hosting for the app, RDS for the database (decision 12).
- The first piece to build is the foundation: households, people, roles and sign-in (decision 14).

## What the foundation must get right (from Discovery)

- Member codes are stored as hashes, with limited tries. A code is never sent back to the browser.
- Only the server changes roles, and only an Owner can do it. Sponsor, Partner and Referring agency need approval first (decision 10).
- Every record starts private, and every page checks access on the server.

## Still to do before building

- Spark creates the empty private repo **village-upkeep** on GitHub, then it gets copied to `C:\Users\tctay\Projects\village-upkeep`.

## Next: Milestone 4, Milestones (data model)

Model the foundation's data in Prisma, run Postgres on the laptop, and seed Spark's own household.
