Epic 1 — Identity, Authentication, and Session Control

AUTH-001 / AUTH-002 Registration and email verification

Create users auth schema fields

Add unique email validation

Enforce password policy

Build registration endpoint

Generate verification token

Send verification email

Build verification endpoint

Mark account verified

Log registration and verification audit events

Add tests for expiry, reuse, duplicate email, invalid token

AUTH-003 / AUTH-004 Login and rate limiting

Build login endpoint

Validate credentials

Issue access token

Issue refresh token

Store hashed refresh-session record

Add login throttling middleware

Add failed-login audit logging

Add session revocation logic

Add tests for lockout and token expiry

AUTH-005 Password recovery

Build forgot-password request endpoint

Generate reset token

Send reset email

Build password reset endpoint

Invalidate old sessions after reset

Audit password reset actions

Test expired token, reused token, and invalid email cases

---

Epic 2 — Role, Permission, and Access Control

RBAC-001 Role assignment

Create roles/permissions tables or enums

Seed default role matrix

Build admin role assignment service

Add role-change audit logging

Validate only authorized HQ actions can assign roles

Add tests for each role edge case

RBAC-002 Authorization enforcement

Build permission middleware

Build ownership-check helper

Build resource-state guard helper

Standardize denied-response format

Apply guards to protected routes

Add tests for unauthorized, wrong-owner, wrong-state access

RBAC-003 Operator scope restriction

Add division/season scope mapping

Restrict operator queries by scope

Restrict operator actions by scope

Log scope violations

Add tests for cross-division access denial

---

Epic 3 — Core User and Player Profile System

PLAYER-001 Create player profile

Create player profile table

Link profile to user account

Add gamer tag validation

Add profile creation endpoint

Set default player status

Audit profile creation

Add tests for duplicate tag and invalid profile data

PLAYER-002 Public player profile

Build public player profile read endpoint

Hide private fields from guests

Expose stats and competition history

Add pagination for history

Add caching if needed

Add visibility tests

PLAYER-003 Profile edits

Define editable fields

Build profile update endpoint

Validate state and permissions

Preserve audit trail for edits

Add tests for restricted fields and invalid updates

---

Epic 4 — Club System

CLUB-001 Club creation

Create club schema

Link club to owner

Validate unique club name

Build club creation endpoint

Initialize club status

Audit club creation

Add tests for duplicates and unauthorized creation

CLUB-002 Club profile management

Build club update endpoint

Restrict edits to owner/manager scope

Add logo/banner upload hooks

Add status validation

Audit profile changes

Add tests for unauthorized edits

CLUB-003 Staff assignment and ownership handling

Create club role assignment logic

Build manager/staff assignment endpoints

Add ownership override rules

Audit role changes

Add tests for invalid assignment and permissions

---

Epic 5 — Club Applications and Membership Workflow

MEMBERSHIP-001 Apply to club

Create club application table

Add application endpoint

Prevent duplicate pending applications

Add recruitment pool query

Notify club staff on new application

Audit application submission

Add tests for duplicate and blocked applications

MEMBERSHIP-002 Review applications

Build approve/reject endpoints

Validate club manager/owner permissions

Create membership record on approval

Update application status

Notify player

Audit review decision

Add tests for invalid review states

MEMBERSHIP-003 Remove/suspend member

Build remove/suspend endpoints

Block self-removal edge cases if needed

Preserve membership history

Notify affected player

Audit member removal

Add tests for ownership and role restrictions

---

Epic 6 — Season and Division Management

SEASON-001 Create season

Create season schema

Add season creation endpoint

Validate dates and status

Seed initial season metadata

Audit creation

Add tests for invalid date ranges

SEASON-002 Publish/open season

Build season status transition service

Add registration-open endpoint or admin action

Trigger notifications

Prevent invalid transitions

Audit state change

Add tests for blocked transitions

SEASON-003 Close/archive season

Build close/archive transition flow

Freeze season data

Restrict post-close edits

Audit archive action

Add tests for immutable closed season records

DIVISION-001 Create and assign divisions

Create division schema

Build division creation endpoint

Link divisions to seasons

Add operator scope assignment logic

Audit division actions

Add tests for unauthorized creation

---

Epic 7 — Fixture and Match Operations

MATCH-001 Fixture generation

Build fixture schema

Create fixture generation service

Add admin/operator fixture endpoint

Prevent duplicate fixtures

Audit fixture publication

Add tests for schedule collisions

MATCH-002 Check-in open/close

Create check-in state fields

Build scheduled job to open check-in

Build scheduled job to close check-in

Add manual override endpoint

Notify participants

Audit every transition

Add tests for idempotent job runs

MATCH-003 No-show detection

Build no-show scan job

Add provisional no-show flag

Create operator review queue item

Block auto-final forfeit unless policy allows

Audit scan and decision

Add tests for late check-ins and edge timing

MATCH-004 Match lifecycle tracking

Implement match state machine storage

Add match detail endpoint

Track all state transitions

Block invalid transitions

Audit every mutation

Add tests for state integrity

---

Epic 8 — Result Submission and Verification

RESULT-001 Submit result

Create result submission schema

Build submission endpoint

Support evidence upload links

Validate match state before submission

Notify opponent and operator

Audit submission

Add tests for invalid match state and missing evidence

RESULT-002 Confirm/reject result

Build opponent confirmation endpoint

Build rejection endpoint with reason

Update result state on response

Trigger operator review on rejection

Audit response

Add tests for expired confirmation window

RESULT-003 Operator verification and HQ override

Build operator review queue

Add approve/reject/void endpoints

Add HQ override endpoint

Recompute affected standings

Capture before/after snapshots

Audit all overrides

Add tests for post-confirmation edits

---

Epic 9 — Disputes, Penalties, and Sanctions

DISPUTE-001 Open dispute

Create dispute schema

Build dispute creation endpoint

Attach match reference and reason

Support evidence upload

Move dispute to submitted state

Notify operator

Audit dispute creation

DISPUTE-002 Add evidence and case notes

Add evidence attachment endpoint

Lock evidence after submission

Add operator notes support

Preserve full case history

Audit evidence additions

Add tests for immutable evidence rules

DISPUTE-003 Review, resolve, appeal

Build dispute review queue

Add resolve endpoint

Add appeal endpoint

Restrict appeal window

Preserve original decision trail

Audit every decision

Add tests for invalid appeal timing

PENALTY-001 / PENALTY-002 / SANCTION-001 Discipline actions

Create warning/penalty/sanction tables

Build warning endpoint

Build penalty endpoint

Build HQ sanction endpoint

Link every action to rule reference

Apply audit logging and notification

Add tests for permission and severity boundaries

---

Epic 10 — Standings, Rankings, and Rewards

STANDINGS-001 Recalculate standings

Build standings calculation service

Trigger on confirmed results and penalties

Persist standings snapshot

Make calculation deterministic

Audit recomputation

Add tests for edge-case tie handling

STANDINGS-002 Public leaderboard

Build standings read endpoint

Add filters by season/division

Add pagination

Expose only public-safe fields

Add caching if needed

Add tests for visibility rules

STANDINGS-003 Manual correction and rewards

Build HQ correction endpoint

Require reason/source reference

Recompute rankings after correction

Add reward assignment tables or hooks

Audit corrections and rewards

Add tests for restricted access

---

Epic 11 — Notifications and Realtime

NOTIFY-001 In-app notifications

Create notifications table

Build notification creation service

Add read/unread state

Add notification center endpoint

Audit important notification triggers

Add tests for delivery and marking read

NOTIFY-002 Match and dispute notifications

Wire notifications to match events

Wire notifications to dispute events

Add reminder job output

Prevent duplicate notifications

Add delivery retry handling

Add tests for repeated triggers

REALTIME-001 Realtime delivery

Define realtime event payloads

Connect Pusher channels

Publish match/standings/dispute events

Add polling fallback

Ensure DB remains source of truth

Add tests for missed-event recovery

---

Epic 12 — Audit Logging and Admin Oversight

AUDIT-001 Append-only audit logging

Create audit log table

Add audit writer middleware/service

Capture actor, action, resource, before/after, reason

Block delete/update of audit rows

Add tests for write-only behavior

AUDIT-002 Audit search and filtering

Build audit search endpoint

Add filters by actor, action, resource, date

Add pagination

Restrict access to HQ/admin roles

Add tests for access control

AUDIT-003 Override tracking

Add override reason requirements

Capture original and final state snapshots

Log all HQ and operator overrides

Add tests for required audit fields

---

Epic 13 — Moderation and Support Tools

MOD-001 Content moderation

Create report/flag table

Build content flag endpoint

Build hide/unhide action for moderators

Restrict moderation scope

Audit all moderation actions

Add tests for permissions

MOD-002 Abuse reporting

Build user report endpoint

Attach evidence uploads

Route report to moderation queue

Notify moderator/support

Audit report creation

Add tests for duplicate report handling

SUPPORT-001 / SUPPORT-002 Case handling and account recovery

Create support case table

Build support queue endpoint

Add read-only account lookup

Add recovery workflow for locked accounts

Restrict recovery actions

Audit all support interventions

Add tests for unauthorized support edits

---

Epic 14 — Security, Abuse Prevention, and Rate Limiting

SECURITY-001 Password and OTP policy

Enforce password complexity in backend

Add OTP generation and expiry logic

Add resend throttling

Add failed-attempt counters

Audit security events

Add tests for invalid password and OTP expiry

SECURITY-002 Login and request throttling

Add IP/account rate limiter middleware

Add brute-force detection

Add temporary lockout logic

Add audit logging for throttles

Add tests for boundary thresholds

SECURITY-003 Fraud and abuse detection

Add duplicate-account heuristics

Add conflicting-submission detection

Add recruitment-abuse throttles

Add review queue generation

Audit suspicious activity

Add tests for false-positive-safe paths

SECURITY-004 Upload validation

Restrict file types and size

Add malware scan hook

Use signed upload URLs

Store files in object storage only

Audit upload attempts

Add tests for invalid files and oversized uploads

---

Epic 15 — Infrastructure, Deployment, and Operations

OPS-001 Environment setup

Define local/dev/staging/prod config

Load secrets from managed secret store

Add environment validation on boot

Document required env vars

Add tests for missing config

OPS-002 Database and storage

Provision PostgreSQL schema

Add migrations pipeline

Configure object storage buckets

Add backup schedule

Add restore verification task

OPS-003 Jobs and scheduling

Set up job runner/cron system

Schedule check-in and deadline jobs

Schedule standings recomputation jobs

Make jobs idempotent

Add job failure logging

OPS-004 Monitoring and release flow

Add structured logging

Add health checks

Add alerting for API/db/job failures

Define staging smoke test

Define production release steps

Add rollback procedure

---