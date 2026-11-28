**MODE A: Advanced Reasoning**

**Plan →** মাস্তার, এবার আমি “কেউ ইচ্ছা করে করেছে” এমন সিদ্ধান্ত দিচ্ছি না—কারণ live repository state আমি এখানে যাচাই করতে পারছি না। কিন্তু আপনার বর্ণিত ঘটনাকে **security/forensic incident + repository recovery problem** হিসেবে ধরলে পথটা পরিষ্কার। সবচেয়ে গুরুত্বপূর্ণ: **আগে প্রমাণ সংরক্ষণ, তারপর branch recovery; আগে recovery, পরে blame নয়।**

আপনি যে দুইটি খসড়া চেয়েছেন, আমি আলাদা রাখছি:

1. **Draft–1:** GitHub-এ দেওয়া হবে—canonical main branch পুনঃস্থাপন ও governance lock।
2. **Draft–2:** আলাদা incident record—Zero Civilization Engine, COSMOS, M99, Miracle Code এবং access/OTP/API-সংক্রান্ত ঘটনাগুলো পরে evidence দিয়ে পূরণ করা হবে।

---

## Deliverable → মহাজাগতিক পরিকল্পনা

### মহাজাগতিক কাঠামো

```text
                         TRUTH
                           │
                    EVIDENCE LOCK
                           │
                ┌──────────┴──────────┐
                ↓                     ↓
          REPOSITORY STATE       ACCESS STATE
                │                     │
          BRANCH / COMMITS      EMAIL / OTP / API
                │                     │
                └──────────┬──────────┘
                           ↓
                    CANONICAL SOURCE
                           ↓
                   MAIN BRANCH RESTORE
                           ↓
                  IMMUTABLE PROTECTION
                           ↓
                 COSMOS HISTORY RECORD
                           ↓
                     VALIDATION
                           ↓
                        M99 CORE
```

### প্রথম মহাজাগতিক নিয়ম

**কোনো branch-কে “আসল” ধরে নিয়ে force-reset করা যাবে না।**

আগে:

```text
WHO OWNS?
WHAT IS CANONICAL?
WHICH COMMIT IS TRUSTED?
WHAT CHANGED?
WHEN CHANGED?
WHO/WHAT ACTOR?
```

তারপর recovery।

বিশেষ করে আপনি বলেছেন `zero-civilization-engine` আগে immutable—তাই সেটিকে **recovery source হিসেবে ব্যবহার করলেও তার ভেতরে কোনো পরিবর্তন করা যাবে না।**

---

# Draft–1 — GitHub Main Branch Recovery & Governance Instruction

এটা GitHub/Copilot-এর জন্য ব্যবহারযোগ্য **policy instruction** হিসেবে লিখলাম। এটি নিজে কোনো branch পরিবর্তন করবে না; বরং AI-কে **audit → confirm → recover** করতে বাধ্য করবে।

# M99 CANONICAL REPOSITORY RECOVERY

## READ-ONLY RECOVERY AUDIT CHECKLIST

**STATUS:** READ-ONLY AUDIT MODE\
**DEFAULT:** DENY-BY-DEFAULT\
**PRIMARY RULE:** COLLECT AND PRESERVE EVIDENCE BEFORE ANY MUTATION\
**RECOVERY RULE:** NO RESET / NO REBASE / NO FORCE-PUSH / NO DELETE\
**HISTORY RULE:** PRESERVE HISTORY FIRST\
**IMMUTABLE LEGACY:** `zero-civilization-engine/` REMAINS READ-ONLY

### Standard execution format

Every audit item must use the following structure:

- **Prerequisites:** What must be known or confirmed before inspection begins.
- **Evidence to collect:** The exact facts, records, outputs, or references to capture.
- **Stop conditions:** Conditions that require immediate suspension and clarification.
- **Expected output:** The record or classification that must exist when the item is complete.

No item is complete unless its expected output is recorded.

---

## 1. AUDIT SCOPE

### 1.1 Confirm read-only scope

- **Prerequisites:**
  - The audit purpose is stated.
  - The inspecting actor is identified.
  - The repository and local path, if any, are identified.
  - No mutation has been authorized.
- **Evidence to collect:**
  - Audit start time and timezone.
  - Operator or actor identity.
  - Repository URL.
  - Local repository path.
  - Stated audit purpose.
  - Read-only command or inspection plan.
- **Stop conditions:**
  - Any proposed action would modify files, branches, tags, remotes, permissions, deployments, or history.
  - The audit purpose is unclear.
  - The actor cannot be identified.
- **Expected output:**
  - A completed read-only scope record confirming that the activity is limited to inspection.

### 1.2 Confirm that recovery is not authorized

- **Prerequisites:**
  - The user request and authorization scope are available for review.
- **Evidence to collect:**
  - User request text.
  - Authorization record.
  - Authorized action scope.
  - Explicit confirmation that reset, rewrite, deletion, migration, deployment, and recovery actions are excluded.
- **Stop conditions:**
  - Authorization is absent, ambiguous, expired, or broader than the requested action.
  - A plan, simulation, or proposal is being represented as executed recovery.
- **Expected output:**
  - A recorded authorization boundary stating `AUDIT_ONLY`.

---

## 2. CANONICAL SOURCE IDENTIFICATION

Record the user-confirmed values:

```text
CANONICAL_REPOSITORY:
[USER-CONFIRMED REPOSITORY]

CANONICAL_BRANCH:
main

CANONICAL_PROJECT:
[USER-CONFIRMED PROJECT]

CANONICAL_OWNER:
[USER-CONFIRMED OWNER]
```

### 2.1 Identify the canonical repository

- **Prerequisites:**
  - The user can identify the intended repository.
  - Repository access is available for read-only inspection.
- **Evidence to collect:**
  - Exact repository URL.
  - Hosting provider.
  - Owner or organization.
  - Repository name.
  - User confirmation timestamp.
  - Any competing repository references.
- **Stop conditions:**
  - The repository is unspecified, inaccessible, duplicated, or disputed.
  - Canonical status is inferred only from a local folder name, deployment, or external project.
- **Expected output:**
  - One explicitly identified canonical repository, or a recorded unresolved conflict.

### 2.2 Confirm the canonical branch

- **Prerequisites:**
  - The canonical repository has been identified.
  - The user has stated the intended branch.
- **Evidence to collect:**
  - User-confirmed branch name.
  - Observed default branch.
  - Branch metadata from the hosting provider.
  - Exact branch reference and commit SHA.
- **Stop conditions:**
  - The user-confirmed branch differs from the observed default branch and no decision exists.
  - Branch intent is unclear.
  - The branch cannot be read reliably.
- **Expected output:**
  - A confirmed canonical branch, normally `main`, with its observed reference.

### 2.3 Confirm the canonical project and owner

- **Prerequisites:**
  - The repository and branch have been identified.
  - Ownership metadata is available for inspection.
- **Evidence to collect:**
  - User confirmation.
  - Repository ownership metadata.
  - Organization membership or equivalent ownership evidence.
  - Project references associated with the repository.
- **Stop conditions:**
  - Ownership, project identity, or authority conflicts with observed metadata.
  - The actor cannot establish sufficient read access to ownership information.
- **Expected output:**
  - A recorded project-owner identity with supporting evidence, or an unresolved ownership conflict.

### 2.4 Compare confirmed values with observed state

- **Prerequisites:**
  - User-confirmed repository, branch, project, and owner values exist.
  - Repository metadata can be inspected.
- **Evidence to collect:**
  - Repository metadata.
  - Remote URLs.
  - Owner and organization information.
  - Default branch.
  - Project references.
  - Comparison table showing confirmed versus observed values.
- **Stop conditions:**
  - Any value conflicts with observed metadata.
  - The conflict cannot be resolved without user direction.
- **Expected output:**
  - A match report or a preserved conflict report requesting clarification.

---

## 3. REPOSITORY IDENTITY AND ACCESS

### 3.1 Inventory repository remotes

- **Prerequisites:**
  - The local repository path is known.
  - Read-only inspection of configuration is permitted.
- **Evidence to collect:**
  - Remote names.
  - Fetch URLs.
  - Push URLs.
  - Hosting provider.
  - Access mode.
  - Whether each remote is expected and authorized.
- **Stop conditions:**
  - A remote points to an unexpected, unauthorized, or conflicting repository.
  - Inspection would require changing remote configuration.
- **Expected output:**
  - A complete remote inventory with an `EXPECTED`, `UNEXPECTED`, or `UNKNOWN` classification for each remote.

### 3.2 Record visibility and ownership

- **Prerequisites:**
  - Repository metadata is accessible.
- **Evidence to collect:**
  - Public or private status.
  - Owner or organization.
  - Creation, transfer, or archival metadata where available.
  - Repository identifier.
- **Stop conditions:**
  - Ownership or visibility cannot be established sufficiently.
  - Metadata conflicts with the stated canonical identity.
- **Expected output:**
  - A repository identity record with supporting metadata and unresolved conflicts, if any.

### 3.3 Record inspecting actor and permissions

- **Prerequisites:**
  - The actor is authenticated or the access method is known.
- **Evidence to collect:**
  - Authenticated account.
  - Role or permission level.
  - Token scope summary without exposing secrets.
  - Access method.
  - Read-access result.
- **Stop conditions:**
  - The actor lacks read access.
  - Credentials, tokens, private keys, or recovery material would need to be exposed.
- **Expected output:**
  - An access record confirming the actor, access method, and read permission without secret values.

---

## 4. MAIN BRANCH STATE

### 4.1 Record local `main`

- **Prerequisites:**
  - The local repository has been identified.
  - Read-only reference inspection is available.
- **Evidence to collect:**
  - Exact local `main` commit SHA.
  - Symbolic reference.
  - Repository path.
  - Inspection timestamp.
  - Whether the branch is checked out, tracked, or merely present as a reference.
- **Stop conditions:**
  - Local `main` is missing, detached, ambiguous, or unreadable.
  - Reading the reference would require mutation.
- **Expected output:**
  - A local `main` state record with an exact SHA or an explicit `UNKNOWN` result.

### 4.2 Record remote `main`

- **Prerequisites:**
  - The canonical remote has been identified.
  - Remote read access is available.
- **Evidence to collect:**
  - Exact remote `main` commit SHA.
  - Remote name.
  - Fetch or observation timestamp.
  - Hosting-provider reference.
- **Stop conditions:**
  - Remote `main` is missing, inaccessible, ambiguous, or inconsistent across observed remotes.
  - Obtaining the state would require an unauthorized mutation.
- **Expected output:**
  - A remote `main` state record with an exact SHA or an explicit unresolved status.

### 4.3 Compare local and remote `main`

- **Prerequisites:**
  - Local and remote `main` references have been recorded.
- **Evidence to collect:**
  - Exact SHAs.
  - Ahead and behind counts.
  - Divergent commit ranges.
  - Ancestor relationship.
  - Observation timestamps.
- **Stop conditions:**
  - The relationship cannot be determined reliably.
  - Comparison would require changing repository state.
- **Expected output:**
  - One classification: `MATCH`, `LOCAL_AHEAD`, `REMOTE_AHEAD`, `DIVERGED`, or `UNKNOWN`.

### 4.4 Record the observed default branch

- **Prerequisites:**
  - Repository metadata is accessible.
- **Evidence to collect:**
  - Hosting-provider default-branch setting.
  - Repository metadata.
  - Comparison with the user-confirmed canonical branch.
- **Stop conditions:**
  - The default branch is not `main` and no explicit decision has been provided.
- **Expected output:**
  - A default-branch record with a match or an unresolved discrepancy.

---

## 5. COMMIT AND HISTORY INVENTORY

### 5.1 Inventory recent local `main` commits

- **Prerequisites:**
  - Local `main` is readable.
- **Evidence to collect:**
  - Commit SHA.
  - Parent SHA or SHAs.
  - Author.
  - Committer.
  - Author and committer timestamps.
  - Commit message.
  - Changed-file summary.
- **Stop conditions:**
  - Commit metadata is incomplete, inconsistent, or unreadable.
- **Expected output:**
  - A chronological local commit inventory with exact references.

### 5.2 Inventory recent remote `main` commits

- **Prerequisites:**
  - Remote `main` is readable.
- **Evidence to collect:**
  - The same metadata collected for local `main`.
  - Exact remote references.
  - Observation timestamp.
- **Stop conditions:**
  - Remote history cannot be inspected reliably.
- **Expected output:**
  - A chronological remote commit inventory with exact references.

### 5.3 Inventory branches

- **Prerequisites:**
  - Local and remote references are readable.
- **Evidence to collect:**
  - Local branch names.
  - Remote branch names.
  - Current tip SHAs.
  - Tracking relationships.
  - Last-update metadata where available.
- **Stop conditions:**
  - Branch references appear unexpectedly deleted, rewritten, or inconsistent.
  - Branch state cannot be distinguished between local and remote.
- **Expected output:**
  - A complete branch inventory with reference type, tip SHA, and status.

### 5.4 Inventory tags

- **Prerequisites:**
  - Tag references are readable.
- **Evidence to collect:**
  - Tag names.
  - Target SHAs.
  - Tagger.
  - Timestamps.
  - Signatures and verification status where available.
- **Stop conditions:**
  - Tags conflict with branch history.
  - Tags appear to have moved unexpectedly.
- **Expected output:**
  - A tag inventory with target and verification status.

### 5.5 Inventory releases

- **Prerequisites:**
  - Release metadata is accessible.
- **Evidence to collect:**
  - Release names.
  - Tags.
  - Target SHAs.
  - Publication dates.
  - Authors.
  - Release notes.
- **Stop conditions:**
  - A release identifies a different canonical state than the observed branch without clarification.
- **Expected output:**
  - A release inventory linked to exact tags and SHAs.

### 5.6 Inventory reflog or equivalent reference history

- **Prerequisites:**
  - Local reference history is available.
  - Inspection does not alter or expire evidence.
- **Evidence to collect:**
  - Reference movements.
  - Previous SHAs.
  - Timestamps.
  - Actors.
  - Evidence of force-pushes, resets, deletions, or rewrites.
- **Stop conditions:**
  - Reference movement suggests history rewriting and the prior state cannot be preserved.
- **Expected output:**
  - A reference-movement timeline with each movement classified as `OBSERVED`, `SUSPECTED`, or `UNKNOWN`.

---

## 6. EXPECTED VERSUS ACTUAL CANONICAL STATE

### 6.1 Establish the expected canonical commit

- **Prerequisites:**
  - An authoritative source is available or the absence of one can be documented.
- **Evidence to collect:**
  - User-confirmed SHA.
  - Signed tag.
  - Release reference.
  - Protected reference.
  - Other explicitly authoritative record.
  - Source authority and timestamp.
- **Stop conditions:**
  - The expected commit is based only on assumption, memory, filename, deployment status, or an unverified claim.
- **Expected output:**
  - An expected canonical SHA with authority classification, or `UNKNOWN`.

### 6.2 Record the actual canonical commit

- **Prerequisites:**
  - The canonical repository and branch are confirmed.
  - The remote branch is readable.
- **Evidence to collect:**
  - Exact SHA for canonical remote `main`.
  - Inspection timestamp.
  - Source of observation.
- **Stop conditions:**
  - The actual SHA cannot be verified.
- **Expected output:**
  - A verified actual canonical SHA or `UNKNOWN`.

### 6.3 Compare expected and actual commits

- **Prerequisites:**
  - Expected and actual SHAs are recorded.
- **Evidence to collect:**
  - Exact SHAs.
  - Ancestor relationship.
  - Divergent ranges.
  - File-level diff summary.
  - Commit-count comparison.
- **Stop conditions:**
  - The expected commit is unknown.
  - The comparison is inconclusive.
  - Capturing the comparison could destroy or obscure evidence.
- **Expected output:**
  - A comparison record showing `MATCH`, `DIFFERS`, `UNKNOWN`, or `CONFLICTING`.

### 6.4 Classify the canonical-state result

- **Prerequisites:**
  - The comparison evidence is complete.
- **Evidence to collect:**
  - Classification basis.
  - Supporting SHAs.
  - Evidence references.
  - Unresolved assumptions.
- **Stop conditions:**
  - Classification would require inferring intent, cause, or ownership.
- **Expected output:**
  - Exactly one classification: `MATCH`, `DIFFERS`, `UNKNOWN`, or `CONFLICTING`.

---

## 7. SUSPICIOUS OR UNEXPECTED CHANGES

For each suspicious or unexpected change:

### 7.1 Record raw commit evidence

- **Prerequisites:**
  - The change has been identified by a specific commit or reference.
- **Evidence to collect:**
  - Commit SHA.
  - Parent SHA or SHAs.
  - Author.
  - Committer.
  - Author and committer timestamps.
  - Commit message.
  - Changed files and change types.
  - Branch or reference containing the commit.
  - Related merge request, pull request, issue, deployment, or workflow.
  - Signature or verification status.
- **Stop conditions:**
  - The commit cannot be identified precisely.
  - Evidence collection would modify or obscure history.
- **Expected output:**
  - A complete provenance record for the change.

### 7.2 Classify the change

- **Prerequisites:**
  - Raw metadata and supporting records have been collected.
- **Evidence to collect:**
  - Classification basis.
  - Raw metadata.
  - Command output.
  - Provider records or screenshots where appropriate.
  - Separation between observed facts and interpretations.
- **Stop conditions:**
  - Anyone is labeled malicious without direct supporting evidence.
  - Cause or intent is asserted without evidence.
- **Expected output:**
  - Exactly one classification:
    - `CONFIRMED`
    - `OBSERVED`
    - `SUSPECTED`
    - `UNKNOWN`

---

## 8. IMMUTABLE LEGACY AUDIT

The following path is immutable:

```text
zero-civilization-engine/
```

### 8.1 Confirm path existence

- **Prerequisites:**
  - The repository tree can be inspected read-only.
- **Evidence to collect:**
  - Read-only directory listing.
  - Repository tree reference.
  - Path status: present, absent, or unknown.
- **Stop conditions:**
  - Inspection would require modifying, generating, formatting, renaming, or migrating files.
- **Expected output:**
  - A path-existence record without any file mutation.

### 8.2 Record tree and history

- **Prerequisites:**
  - The path exists or its absence has been established.
  - Read-only history inspection is available.
- **Evidence to collect:**
  - Path listing.
  - File hashes where appropriate.
  - Containing commit SHAs.
  - References that include the path.
  - Relevant change history.
- **Stop conditions:**
  - The path is unexpectedly changed.
  - The path is missing when it was expected to exist.
  - Its history cannot be established.
- **Expected output:**
  - An immutable-legacy status record with tree, hashes, history, and unresolved issues.

### 8.3 Confirm non-interference

- **Prerequisites:**
  - The audit command plan and execution log are available.
- **Evidence to collect:**
  - Read-only command plan.
  - Execution log.
  - File-operation summary.
  - Confirmation that no action targeted the path.
- **Stop conditions:**
  - Any action would edit, delete, rename, format, refactor, migrate, generate, or rewrite history involving the path.
- **Expected output:**
  - A non-interference confirmation stating that `zero-civilization-engine/` remained unchanged.

---

## 9. BRANCH PROTECTION AND GOVERNANCE

### 9.1 Record branch protection

- **Prerequisites:**
  - Administrative or equivalent read access is available.
  - The canonical branch is identified.
- **Evidence to collect:**
  - Required reviews.
  - Required status checks.
  - Force-push restrictions.
  - Deletion restrictions.
  - Administrator bypass settings.
  - Rulesets.
- **Stop conditions:**
  - Protection status cannot be verified.
  - Observed settings conflict with the stated governance model.
- **Expected output:**
  - A branch-protection record for `main`.

### 9.2 Record rulesets and privileged access

- **Prerequisites:**
  - Repository governance metadata is accessible.
- **Evidence to collect:**
  - Active rulesets.
  - Bypass actors.
  - Deployment restrictions.
  - Administrative controls.
  - Privileged roles.
- **Stop conditions:**
  - Privileged access or bypass authority is unknown.
- **Expected output:**
  - A governance-access record identifying controls and unknowns.

### 9.3 Confirm protection remains unchanged

- **Prerequisites:**
  - Protection settings have been recorded.
  - No mutation is authorized.
- **Evidence to collect:**
  - Before-and-after settings comparison.
  - Provider activity log where available.
  - Audit execution log.
- **Stop conditions:**
  - Any protection mutation is requested without explicit, action-specific authorization.
  - A protection change is detected during the audit.
- **Expected output:**
  - A confirmation that branch protection and rulesets remained unchanged.

---

## 10. WORKFLOW AND DEPLOYMENT REFERENCES

### 10.1 Inventory workflow activity

- **Prerequisites:**
  - Workflow history is accessible.
  - Repository and branch identity are established.
- **Evidence to collect:**
  - Workflow names.
  - Run IDs.
  - Commit SHAs.
  - Actors.
  - Timestamps.
  - Statuses.
  - Logs or summaries.
  - Triggered events.
- **Stop conditions:**
  - Workflow evidence points to an unexpected repository, branch, actor, or commit and the conflict is unresolved.
- **Expected output:**
  - A workflow inventory linked to exact repository, branch, actor, and commit references.

### 10.2 Inventory deployment references

- **Prerequisites:**
  - Deployment-provider metadata is accessible.
  - The deployment system is treated as a separate source until linkage is proven.
- **Evidence to collect:**
  - Provider.
  - Project.
  - Deployment ID.
  - Source commit SHA.
  - Branch.
  - Timestamp.
  - Status.
  - Environment.
- **Stop conditions:**
  - Deployment state is treated as proof of canonical ownership or source without repository evidence.
- **Expected output:**
  - A deployment inventory with explicit linkage status.

### 10.3 Verify external-system linkage

- **Prerequisites:**
  - External systems are identified.
  - Evidence of linkage can be inspected.
- **Evidence to collect:**
  - Explicit linkage between GitHub, v0, Vercel, Vercel Blob, cloud services, local repositories, and AI tooling.
  - Shared repository identifiers.
  - Commit or branch references.
  - Ownership and authorization records.
- **Stop conditions:**
  - Synchronization, ownership, or canonical status is inferred solely from a project existing in another system.
- **Expected output:**
  - A linkage matrix classifying each relationship as `PROVEN`, `UNPROVEN`, or `CONFLICTING`.

---

## 11. ACCESS OR OTP INCIDENTS

If authentication, email, OTP, API access, or account recovery appears unavailable:

### 11.1 Record the incident

- **Prerequisites:**
  - The affected service and account can be identified without exposing secrets.
- **Evidence to collect:**
  - Affected service.
  - Affected account identifier without credentials.
  - Observed failure message or behavior.
  - Time and timezone.
  - Available non-secret evidence.
  - Documented recovery options.
  - Access status: `CONFIRMED`, `OBSERVED`, `SUSPECTED`, or `UNKNOWN`.
- **Stop conditions:**
  - Recording the incident would expose credentials, tokens, recovery codes, or private keys.
  - Access failure is being treated as proof of compromise.
- **Expected output:**
  - A non-secret access-incident record with evidence and uncertainty clearly separated.

### 11.2 Prevent repeated automated attempts

- **Prerequisites:**
  - The provider’s lockout and recovery behavior is known or treated as unknown.
- **Evidence to collect:**
  - Attempt count.
  - Attempt timestamps.
  - Provider guidance.
  - Existing lockout or rate-limit messages.
- **Stop conditions:**
  - Repeated attempts could trigger lockout, alter account state, or expose credentials.
- **Expected output:**
  - A decision to stop automated attempts and preserve the current incident state.

### 11.3 Prevent secret exposure

- **Prerequisites:**
  - Evidence-collection methods have been reviewed for secret handling.
- **Evidence to collect:**
  - Secret-handling confirmation.
  - Security incident record if exposure occurred.
  - Confirmation that no secret was written to repository history.
- **Stop conditions:**
  - A proposed method would expose or commit credentials, tokens, recovery codes, or private keys.
- **Expected output:**
  - A secret-safety confirmation or an incident report.

---

## 12. EVIDENCE PRESERVATION

### 12.1 Preserve the current `main` reference

- **Prerequisites:**
  - The current canonical `main` SHA is known or its unknown status is recorded.
  - Preservation method is read-only or explicitly authorized.
- **Evidence to collect:**
  - Exact SHA.
  - Provider reference.
  - Timestamp.
  - Read-only export or record where permitted.
- **Stop conditions:**
  - Preservation would require creating or moving a reference without authorization.
- **Expected output:**
  - A preserved `main` reference record.

### 12.2 Preserve relevant commits and divergent ranges

- **Prerequisites:**
  - Relevant commits and ranges have been identified.
- **Evidence to collect:**
  - SHAs.
  - Parent relationships.
  - Commit metadata.
  - Range summaries.
- **Stop conditions:**
  - Relevant history cannot be identified or preserved.
- **Expected output:**
  - A preserved history index covering all relevant ranges.

### 12.3 Preserve the current diff

- **Prerequisites:**
  - Expected and actual states are known sufficiently for comparison.
- **Evidence to collect:**
  - Diff between expected and actual states.
  - File paths.
  - Change statistics.
  - Comparison timestamp.
- **Stop conditions:**
  - The diff cannot be captured without mutation.
- **Expected output:**
  - A read-only diff record or an explicit `UNAVAILABLE` result with reason.

### 12.4 Preserve tags, releases, and references

- **Prerequisites:**
  - Relevant tags, releases, and references have been inventoried.
- **Evidence to collect:**
  - Names.
  - Target SHAs.
  - Signatures.
  - Timestamps.
  - Provider records.
- **Stop conditions:**
  - A reference may move or disappear before evidence is captured.
- **Expected output:**
  - A preserved reference inventory with movement risks identified.

### 12.5 Confirm that no destructive action occurred

- **Prerequisites:**
  - Audit logs and before-state records exist.
- **Evidence to collect:**
  - Audit log.
  - Command history.
  - Provider activity log.
  - Before-and-after reference comparison.
  - File-operation record.
- **Stop conditions:**
  - Any unauthorized mutation is detected.
- **Expected output:**
  - A non-mutation confirmation, or an incident report if mutation occurred.

---

## 13. COSMOS HISTORY RECORD

Create a read-only audit record containing:

```text
event_id
timestamp
actor
request
authorization
repository
branch
before_state
observations
evidence_references
validation
status
```

### 13.1 Record audit-only status

- **Prerequisites:**
  - The audit evidence index is complete or its gaps are documented.
  - No recovery action has been executed.
- **Evidence to collect:**
  - Completed audit record.
  - Evidence index.
  - Mutation-status confirmation.
- **Stop conditions:**
  - A proposed recovery is recorded as executed.
  - The record omits unresolved conflicts or unknowns.
- **Expected output:**
  - `status = AUDIT_ONLY`

### 13.2 Record non-execution

If no recovery is executed, record:

```text
status = NOT_EXECUTED
```

- **Prerequisites:**
  - The audit has remained read-only.
- **Evidence to collect:**
  - Explicit statement that no mutation occurred.
  - Command and provider activity review.
- **Stop conditions:**
  - The record implies that a plan, proposal, or simulation was an executed recovery.
- **Expected output:**
  - `status = NOT_EXECUTED` with a non-mutation statement.

---

## 14. READ-ONLY AUDIT OUTPUT

### 14.1 Required report contents

- **Prerequisites:**
  - Each applicable audit section has been completed or marked `UNKNOWN`, `UNAVAILABLE`, or `CONFLICTING`.
- **Evidence to collect:**
  - Canonical repository identification.
  - Canonical branch identification.
  - Canonical project and owner.
  - Local and remote `main` SHAs.
  - Default branch.
  - Recent commits.
  - Branch list.
  - Tags and releases.
  - Branch-protection settings.
  - Workflow activity.
  - Deployment references.
  - Expected canonical commit and evidence source.
  - Actual canonical commit.
  - Difference between expected and actual state.
  - Commit provenance for suspicious or unexpected changes.
  - Immutable legacy status.
  - Access or OTP incident details, if applicable.
  - Evidence-preservation status.
  - Unresolved conflicts and unknowns.
- **Stop conditions:**
  - The report presents assumptions as facts.
  - Missing evidence is omitted instead of marked.
  - A recovery action is represented as completed.
- **Expected output:**
  - A complete read-only audit report with evidence references and uncertainty labels.

### 14.2 Final recommendation

- **Prerequisites:**
  - All mandatory stop conditions have been reviewed.
  - Conflicts and unknowns are explicitly listed.
- **Evidence to collect:**
  - Decision basis.
  - Blocking conflicts.
  - Evidence completeness.
  - Authorization status.
- **Stop conditions:**
  - A recommendation would require inferring intent or bypassing unresolved authority.
- **Expected output:**
  - Exactly one recommendation:
    - `PROCEED TO PLANNING`
    - `REQUEST CLARIFICATION`
    - `STOP`

---

## 15. MANDATORY STOP CONDITIONS

Stop immediately and request clarification if any of the following applies:

1. The canonical repository cannot be identified with sufficient confidence.
2. The canonical branch cannot be identified with sufficient confidence.
3. The canonical owner or project is disputed or unknown.
4. The expected canonical commit is not supported by evidence.
5. The actual `main` commit cannot be verified.
6. Local and remote `main` states conflict and the conflict is unresolved.
7. Repository ownership, remotes, or permissions are unexpected.
8. History appears rewritten and the prior state cannot be preserved.
9. A proposed action could delete, overwrite, or obscure evidence.
10. A proposed action would affect `zero-civilization-engine/`.
11. A force-push, reset, rebase, deletion, branch replacement, or history rewrite is proposed.
12. User authorization is absent, ambiguous, or not specific to the proposed action.
13. External project state is being used as proof of canonical repository state without explicit linkage.
14. Access failure is being treated as proof of compromise.
15. An unexpected change is being treated as malicious without evidence.
16. Credentials, tokens, recovery codes, or private keys could be exposed.
17. The audit cannot distinguish observed facts from assumptions.
18. The audit cannot determine whether recovery would destroy evidence.

For every stop condition:

- **Prerequisites:** Identify the triggering condition and preserve the evidence already collected.
- **Evidence to collect:**
  - Triggering observation.
  - Relevant timestamps.
  - Affected references.
  - Supporting records.
  - Unresolved question requiring user clarification.
- **Stop conditions:** Do not continue if clarification, preservation, or evidence integrity is unavailable.
- **Expected output:** Use the following sequence:

```text
STOP
↓
PRESERVE CURRENT EVIDENCE
↓
REPORT THE CONFLICT OR UNKNOWN
↓
DO NOT MUTATE
↓
REQUEST EXPLICIT USER CLARIFICATION
```

---

## 16. RECOVERY IS OUT OF SCOPE FOR THIS CHECKLIST

### 16.1 Prohibited actions

- **Prerequisites:**
  - The activity is classified as read-only audit mode.
- **Evidence to collect:**
  - Command plan.
  - Authorization boundary.
  - Execution log confirming that no prohibited action occurred.
- **Stop conditions:**
  - Any prohibited action is proposed, attempted, or detected.
- **Expected output:**
  - A recorded prohibition against the following actions:

```text
RESET
REBASE
FORCE-PUSH
DELETE
BRANCH REPLACEMENT
HISTORY REWRITE
FILE EDIT
FILE GENERATION
MIGRATION
REFACTOR
FORMAT
DEPLOYMENT CHANGE
BRANCH-PROTECTION CHANGE
REMOTE CHANGE
```

No recovery plan may be executed until:

1. The audit is complete.
2. Evidence is preserved.
3. The canonical state is identified.
4. Conflicts and unknowns are resolved or explicitly accepted.
5. The user provides explicit authorization for the specific action.
6. The proposed action is reviewed separately from this audit.

---

## 17. M99 READ-ONLY AUDIT LAW

```text
TRUTH
 ↓
EVIDENCE
 ↓
CANONICAL STATE
 ↓
CONFLICT REVIEW
 ↓
PRESERVATION
 ↓
USER DECISION
 ↓
ONLY THEN: SEPARATE RECOVERY AUTHORIZATION
```

### Required distinctions

```text
OBSERVED ≠ PROVEN CAUSE

ACCESS FAILURE ≠ COMPROMISE

UNEXPECTED CHANGE ≠ MALICIOUS CHANGE

CLAIM ≠ EVIDENCE

AUDIT ≠ RECOVERY

PROPOSAL ≠ EXECUTION

RECOVERY ≠ DELETION
```

### Execution rule

- **Prerequisites:** Authority, repository identity, branch identity, and evidence sources are identified.
- **Evidence to collect:** The records required by the applicable audit section.
- **Stop conditions:** Any unresolved authority conflict, evidence gap, mutation risk, or secret-exposure risk.
- **Expected output:** A read-only audit result that distinguishes facts, evidence, interpretations, unknowns, and user decisions.

---

# FINAL COMMANDMENT

> AUDIT THE TRUTH BEFORE TOUCHING THE BRANCH.

> PRESERVE THE HISTORY BEFORE PLANNING REPAIR.

> NEVER SACRIFICE EVIDENCE FOR SPEED.

> ZERO-CIVILIZATION-ENGINE REMAINS IMMUTABLE.

> MAIN BRANCH REMAINS UNCHANGED DURING THIS AUDIT.

**M99 — READ-ONLY EVIDENCE BEFORE MUTATION.**

---

# Draft–2 — আলাদা Incident / Evidence Ledger

এটা আমি **অভিযোগের প্রমাণ হিসেবে লিখছি না**। আপনি যা জানিয়েছেন, সেগুলোকে “reported/claimed observation
