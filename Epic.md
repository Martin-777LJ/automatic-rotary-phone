Epic 1 — Identity, Authentication, and Session Control

Build the account foundation first. This covers signup, login, email verification, password rules, refresh tokens, logout, session revocation, and basic profile access. The spec is explicit that access tokens are short-lived and refresh tokens are server-side revocable sessions. 

Outcome: a user can register, sign in, verify email, stay signed in safely, and recover access.

---

Epic 2 — Role, Permission, and Access Control

Implement RBAC properly, with ownership checks on top. This is not optional. The spec separates Guest, User, Player, Club Owner, Club Manager, Club Staff, League Operator, Moderator, Support Staff, HQ Admin, and Super Admin, and it explicitly says backend enforcement is the source of truth. 

Outcome: every route, action, and admin panel is protected by role + ownership + state checks.

---

Epic 3 — Core User and Player Profile System

Build user profiles and player profiles. This includes public-facing identity, gamer tag, career data, stats, verification flags, and player status. The player profile is tied to the user account and is not transferable. 

Outcome: players have a real competitive identity, not just a login account.

---

Epic 4 — Club System

Build club creation, approval, ownership, staff roles, roster management, recruitment, membership state, and club profile management. The document treats club ownership as a controlled resource with explicit transfer and approval rules. 

Outcome: clubs can exist as managed organizations, not just team labels.

---

Epic 5 — Club Applications and Membership Workflow

Build the player-to-club flow: apply, review, approve, reject, join, remove, suspend, and manage recruitment pools. The spec is clear that club owners and managers handle this, while players can apply and track status. 

Outcome: players can join clubs through a controlled workflow, and clubs can manage rosters cleanly.

---

Epic 6 — Season and Division Management

Build season creation, opening, closing, archiving, division setup, scope assignment, and season lifecycle controls. HQ owns season authority, and operators only act within assigned scope. 

Outcome: the competition structure exists before fixtures are generated.

---

Epic 7 — Fixture and Match Operations

Build fixture generation, match scheduling, check-in open/close, match state transitions, no-show handling, and match completion flow. The spec says automated jobs should handle timing, while manual judgment stays with operators. 

Outcome: match day runs end to end without developers babysitting it.

---

Epic 8 — Result Submission and Verification

Build result submission, evidence upload, opponent confirmation/rejection, operator review, result finalization, and HQ override. The spec treats result changes as sensitive and audit-heavy. 

Outcome: match outcomes are verifiable, traceable, and hard to fake.

---

Epic 9 — Disputes, Penalties, and Sanctions

Build dispute opening, triage, escalation, resolution, appeal, warnings, penalties, and sanctions. The document makes this a human-driven workflow with clear escalation rules and immutable history. 

Outcome: contested matches have a formal path instead of chaotic back-and-forth in chat.

---

Epic 10 — Standings, Rankings, and Rewards

Build standings recalculation, rankings, leaderboard views, and any MVP-level reward logic. The spec says standings must recalculate on confirmed results and penalty events, and manual changes are tightly restricted. 

Outcome: league tables stay accurate and update from verified competition data.

---

Epic 11 — Notifications and Realtime Updates

Build in-app notifications plus realtime updates for standings, match status, dispute status, and admin counters. The spec chooses Pusher for realtime delivery and says realtime is not the source of truth. 

Outcome: users and operators see meaningful updates without refreshing constantly.

---

Epic 12 — Audit Logging and Admin Oversight

Build append-only audit logs, override history, privileged action logging, and admin visibility into critical events. The spec is strict that every action affecting competitive truth must leave a durable trace. 

Outcome: the system can explain what happened later. That matters a lot in leagues.

---

Epic 13 — Moderation and Support Tools

Build moderator and support workflows: content moderation, report triage, user assistance, account recovery, and escalation paths. These roles are explicitly separated from competitive control. 

Outcome: support staff can help users without touching match integrity.

---

Epic 14 — Security, Abuse Prevention, and Rate Limiting

Build password rules, OTP controls, login throttles, duplicate-account checks, upload restrictions, CSRF/XSS protections, and abuse detection. The spec spells these out in detail, and they should be enforced in backend and middleware, not only UI. 

Outcome: the MVP is hard to spam, hard to abuse, and not embarrassingly insecure.

---

Epic 15 — Infrastructure, Deployment, and Operations

Build the actual runtime: frontend hosting, backend API, PostgreSQL, storage, job runner, environment configs, backups, monitoring, staging, and production release flow. The doc recommends a modular monolith on Cloud Run with PostgreSQL, object storage, and one job system. 

Outcome: the product can actually run in the real world.