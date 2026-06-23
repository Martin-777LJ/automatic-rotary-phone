Epic 1 — Identity, Authentication, and Session Control

Features:

Sign up

Email verification

Login

Logout

Refresh token rotation

Session revocation

Forgot password / reset password

Device/session listing

Basic account status checks

This maps directly to the spec’s JWT + revocable refresh-session model, token lifetimes, verification rules, and rate limits. 

Epic 2 — Role, Permission, and Access Control

Features:

Role assignment

Permission matrix enforcement

Ownership checks

State-based access checks

Operator scope restriction

HQ override paths

Super admin break-glass access

Backend permission denial logging

This is one of the most important epics because the spec explicitly says UI hiding is not security; the backend must enforce role, ownership, account status, and state. 

Epic 3 — Core User and Player Profile System

Features:

User account profile

Player profile creation

Gamer tag management

Public player profile

Private player data

Career stats

Verification flags

Suspension / restriction flags

Profile edit requests

The player profile is tied to the user account and is not transferable, so this feature set stays narrow and controlled. 

Epic 4 — Club System

Features:

Club creation

Club profile management

Club ownership

Manager assignment

Staff assignment

Club settings

Club suspension

Club dissolution

Club public page

The spec treats clubs as owned resources with explicit transfer and override rules, not as casual team records. 

Epic 5 — Club Applications and Membership Workflow

Features:

Apply to club

View recruitment pool

Approve club application

Reject club application

Invite player to club

Accept invite

Remove member

Suspend member

Pending application tracking

Membership status history

This is the operational path from player identity to active club participation. It is owned by club-side roles, with restrictions on who can approve or remove members. 

Epic 6 — Season and Division Management

Features:

Create season

Open season

Close season

Archive season

Create division

Assign divisions to seasons

Assign operator scope

Freeze season state

View season status

Season authority sits with HQ, while operators only act inside assigned scope. That boundary is already formalized in the spec. 

Epic 7 — Fixture and Match Operations

Features:

Fixture creation

Fixture publishing

Match scheduling

Check-in open

Check-in close

Match state tracking

No-show detection

Forfeit review

Match cancellation / voiding

Match operational logs

The doc explicitly pushes timing tasks to automation and keeps judgment calls manual, which is the right split. 

Epic 8 — Result Submission and Verification

Features:

Submit result

Upload evidence

Validate submission

Opponent confirmation

Opponent rejection

Operator review

HQ override

Result correction history

Result finalization

The spec treats result changes as sensitive, audit-heavy actions with before/after snapshots and strong override controls. 

Epic 9 — Disputes, Penalties, and Sanctions

Features:

Open dispute

Escalate dispute

Add evidence to dispute

Review dispute

Resolve dispute

Appeal dispute

Issue warning

Issue penalty

Issue sanction

Track disciplinary history

This is a human-driven workflow in the spec, with automation only for reminders, deadline movement, and routing. 

Epic 10 — Standings, Rankings, and Rewards

Features:

Standings calculation

Rankings calculation

Live standings refresh

Manual standings correction

Penalty impact on standings

Public leaderboard

Season table views

Reward assignment hooks

Standings must recalculate on confirmed results and penalties, and manual edits are tightly restricted. 

Epic 11 — Notifications and Realtime Updates

Features:

In-app notifications

Match status push updates

Result status push updates

Dispute status push updates

Admin dashboard counters

Reminder notifications

Notification read/unread state

Realtime fallback to polling

The spec chooses Pusher for realtime delivery and clearly says realtime is not the source of truth. 

Epic 12 — Audit Logging and Admin Oversight

Features:

Append-only audit log

Privileged action logging

Override logging

Before/after state snapshots

Resource + actor traceability

Audit search

Audit retention

Immutable history for competition records

The document is strict here: anything that changes competitive truth must leave a durable trace. 

Epic 13 — Moderation and Support Tools

Features:

Flag content

Hide content

Triage abuse reports

Issue conduct warnings

View limited support context

Help account recovery

Escalate serious cases

Read-only case access for support staff

This is intentionally separated from competitive control, which is correct. Support staff should not be able to touch results or standings. 

Epic 14 — Security, Abuse Prevention, and Rate Limiting

Features:

Password policy enforcement

OTP request throttling

Login throttling

Duplicate account prevention

Match manipulation detection

Result fraud detection

Recruitment abuse throttling

File upload validation

CSRF protection

XSS protection

Injection prevention

The spec gives concrete limits and controls here, so this should be built as middleware and backend policy, not as frontend decoration. 

Epic 15 — Infrastructure, Deployment, and Operations

Features:

Frontend hosting

Backend API deployment

PostgreSQL setup

Object storage setup

Job scheduling

Environment management

Logging and monitoring

Backups and recovery

Staging / production releases

Migration and rollback flow

The spec already picked the practical stack: Next.js, Cloud Run, PostgreSQL, object storage, one job system, and a clean release flow.