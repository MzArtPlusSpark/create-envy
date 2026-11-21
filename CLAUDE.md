# Creatency — notes for Claude

## Who and what
- Founder: Tiara Taylor (goes by Spark). New to coding from source; came from Bubble. Explain steps plainly, one at a time, and say why.
- Creatency: a creation platform built on Ownership Through Progress. Tagline: Bring It. Build It. Own It. Full vision: docs/vision.md.
- North Star for every feature: Does this help a creation move from idea to ownership?
- Project Zero is Creation #1: moving Village UpKeep off Bubble into owned code. Tiara is both Bringer and Creator.

## Machine
- Windows, PowerShell. Project folder: C:\Users\tctay\Projects\Creatency (kept out of OneDrive on purpose).
- Git 2.56.1 and Node.js 26.13.1 installed 2026-11-21. VS Code installed.
- GitHub repo: https://github.com/MzArtPlusSpark/create-envy (private). Remote `origin`, branch `main` tracks `origin/main`.
- The GitHub CLI (`gh`) is not installed. For pushes, Spark may need to run `! git push` in the prompt.
- On 2026-11-21 a `git init` accidentally ran in C:\Users\tctay; it was removed. Always confirm the working directory before git commands.

## Plan
Six milestones, following the Creatency lifecycle:
1. Idea: workshop ready (folder, tools, GitHub repo, first commit)
2. Discovery: inventory Village UpKeep in Bubble; write docs/project-zero.md
3. Definition: lock the stack, log it in docs/decisions.md, brand basics
4. Milestones: data model (Creation, Milestone, Progress Package, Ownership records), Postgres + Prisma, seed Project Zero
5. Creation: first screens (landing, sign-in, My Creations, three-zone workspace, milestones, Dormant)
6. Ownership: ship on AWS us-east-2 (billing alarm, GitHub Actions CI, Amplify Hosting, RDS), optional Terraform

Proposed stack: Next.js + TypeScript, PostgreSQL + Prisma, Auth.js. See docs/decisions.md.

## Brand
Navy #1B1F3B, mustard gold #F2B84B, white, slate grey #4A4F6E (plus indigo #3236A8 for links). Space Grotesk for titles, Inter for body. Gold is earned: it means done, progress or Kee. Kee is the gold ownership companion; never redraw or recolour Kee.
- Design system: https://claude.ai/artifact/BEhVu9pbG7HLUUxn3CjqVX
- Live build checklist: https://claude.ai/artifact/RHdM8Z9eSYugyH7Vr8xKRb

## Rules
- Never commit secrets: .env files stay out (see .gitignore).
- Log every real decision as a new row in docs/decisions.md.
- Each milestone ends with its Progress Package (listed in the checklist).
