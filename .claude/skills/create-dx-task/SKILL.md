---
name: create-dx-task
description: Create a Developer Experience GitHub issue for ThunderID. Use when filing a new SDK tracking issue, ecosystem SDK issue, individual SDK issue, or integration issue in the thunder-id/thunderid repo.
allowed-tools: Bash(gh issue create *), Bash(gh issue list *), Bash(gh issue view *), Bash(gh api *)
---

# ThunderID DX Issue Creator

You are creating a Developer Experience GitHub issue in the `thunder-id/thunderid` repository.

## Step 0 — Identify the issue type

Ask the user which type of DX issue they want to create:

> **What kind of Developer Experience issue do you want to file?**
>
> 1. **Umbrella / Tracking** — a high-level tracking issue covering an entire SDK suite or DX initiative (e.g., "[UMBRELLA ☂️] Thunder SDK Suite"). Use `Type/Task` + `Developer Experience` labels.
> 2. **Ecosystem SDK** — a parent issue for a whole language/platform ecosystem that groups individual SDKs (e.g., "Thunder JavaScript SDKs"). Use `Type/New Feature` + `Developer Experience` labels.
> 3. **Individual SDK** — an issue for a single SDK package (e.g., "Thunder Next.js SDK (@thunderid/nextjs)"). Use `Developer Experience` label; link to a parent ecosystem issue.
> 4. **Integration** — an issue for a third-party auth integration (e.g., "Thunder Auth.js Provider"). Use `Developer Experience` label; link to the umbrella issue.
>
> Reply with 1, 2, 3, or 4.

Wait for the answer. Then collect the remaining information in a single follow-up question (see per-type guides below). Do not create the issue until you have all required fields confirmed.

---

## Type 1 — Umbrella / Tracking Issue

### Information to collect

Ask the user (in one message):
- **Suite name** — what area does this umbrella cover? (e.g., "Thunder SDK Suite", "Thunder Mobile SDKs")
- **Subtitle** — a short descriptor after the dash (e.g., "Coverage, Integrations, and Roadmap")
- **Categories and SDKs** — a list of categories (Language/Runtime, Platform, Frameworks, Libraries, Mobile, Official Integrations) and the SDKs/integrations that belong in each, with initial Status (🟢 Completed / 🟡 In Progress / ⚪ Not Started / 🔴 Blocked) and Priority (⭐ through ⭐⭐⭐⭐⭐)
- **Goals** — 3–5 bullet points
- **Scope** — what this umbrella is and is not for

### Title format

```
[UMBRELLA ☂️] <Suite Name> – <Subtitle>
```

### Body template

```markdown
## Overview

<Brief description of what this umbrella covers and its goal.>

## <Category 1 Name>

| SDK | Status | Priority | Assignee | Notes |
|-----|--------|----------|----------|-------|
| <SDK name> | ⚪ Not Started | ⭐⭐⭐⭐⭐ | — | — |

## <Category N Name>

| SDK | Status | Priority | Assignee | Notes |
|-----|--------|----------|----------|-------|
| <SDK name> | ⚪ Not Started | ⭐⭐⭐ | — | Sub-issue / tracking link |

---

## Legend

[1] 🟢 **Completed** – Production-ready, stable, and documented
[2] 🟡 **In Progress** – Actively being developed or partially shipped
[3] ⚪ **Not Started** – Planned but no implementation yet
[4] 🔴 **Blocked** – Requires architectural decision, redesign, or dependency resolution

[5] ⭐ Priority scale:
- ⭐ = low priority
- ⭐⭐⭐ = medium priority
- ⭐⭐⭐⭐⭐ = highest priority / strategic focus

## Goals

- <goal 1>
- <goal 2>
- <goal 3>

## Scope

This umbrella issue is intended for:

- <scope item 1>
- <scope item 2>

Individual SDKs or integrations should be discussed and implemented in their respective linked issues.
```

### Labels

`Type/Task` + `Developer Experience`

### Milestone

None (umbrella issues are roadmap-level; do not set a milestone unless the user explicitly provides one).

---

## Type 2 — Ecosystem SDK Issue

### Information to collect

Ask the user (in one message):
- **Ecosystem name** — e.g., "JavaScript", "Python", "Go"
- **Persona** — who is the primary developer audience? (e.g., "JavaScript Developers (Frontend, Backend, and Full-stack)")
- **Problem** — what pain does the lack of an official SDK create?
- **Why now** — value to persona and value to org
- **Proposed solution** — high-level description of the SDK ecosystem to build
- **Assignee** — GitHub username (optional; default is the current user)
- **Parent umbrella issue number** — if this ecosystem issue should reference the main SDK umbrella (#1895)

### Title format

```
Thunder <Ecosystem> SDKs
```

### Body template

```markdown
### What problem are we solving?

<Problem description — what gap exists without an official SDK ecosystem for this language/platform.>

### Who are we solving this for?

**Primary:** <Developer persona>

* **Goal:** <what they want to achieve>
* **Pain:** <what friction they face without this SDK>

### Why should we solve this now?

**Why now:**

* **Value to Persona:** <direct benefit to the developer>
* **Value to Org:** <strategic value — adoption, market position, etc.>

### Proposed Solution

<Description of the SDK ecosystem to build — package names, capabilities, TypeScript support, documentation, etc.>

### Alternatives

<What developers do today instead, and why that's insufficient.>
```

If a parent umbrella issue number was provided, append:

```markdown
---
Parent issue: #<number>
```

### Labels

`Type/New Feature` + `Developer Experience`

### Milestone

None unless the user specifies one.

---

## Type 3 — Individual SDK Issue

### Information to collect

Ask the user (in one message):
- **SDK name** — full human-readable name (e.g., "Next.js")
- **Package name** — npm/Maven/SwiftPM/etc. identifier (e.g., `@thunderid/nextjs`)
- **Persona** — primary developer audience
- **Problem** — what specific rendering contexts, language patterns, or platform constraints make this SDK necessary?
- **Why now** — value to persona and value to org
- **Proposed solution** — mention which lower-level ThunderID SDKs it builds on (e.g., "built on `@thunderid/node` and `@thunderid/react`")
- **Parent issue number** — the ecosystem or umbrella issue this belongs to
- **Assignee** — GitHub username (optional)
- **Milestone** — milestone title to attach (e.g., `0.47.0`); if unsure, run `gh api repos/thunder-id/thunderid/milestones --jq '.[].title'` to list open milestones

### Title format

```
Thunder <SDK Name> SDK (<package-name>)
```

### Body template

```markdown
### What problem are we solving?

<Specific problem — rendering contexts, platform-specific auth complexity, etc.>

### Who are we solving this for?

**Primary:** <Developer persona>

* **Goal:** <what they want to accomplish with this SDK>
* **Pain:** <the specific complexity this SDK removes>

### Why should we solve this now?

**Why now:**

* **Value to Persona:** <concrete benefit — e.g., "can protect pages, API routes, and server actions with a single SDK">
* **Value to Org:** <market/adoption argument — e.g., "Next.js is the leading full-stack React framework">

### Proposed Solution

<Technical description — package name, which ThunderID SDKs it wraps, key features (middleware, server components, hooks), TypeScript support, documentation.>

### Alternatives

<What developers do today (raw HTTP, custom implementations, unofficial libraries) and why that falls short.>

---
Parent issue: #<parent-issue-number>
```

### Labels

`Developer Experience`

### Milestone

Set to the milestone the user provided. To look up the current open milestones:

```bash
gh api repos/thunder-id/thunderid/milestones --jq '.[] | select(.state=="open") | .title'
```

---

## Type 4 — Integration Issue

There are two delivery models for integrations. Identify which applies before collecting details:

- **Upstream contribution** — ThunderID is contributed as a provider/strategy/plugin directly to the host package's repository (e.g., Auth.js, Passport, Backstage). No `@thunderid/*` package is shipped; the code lives in the host package.
- **Standalone package** — ThunderID ships and maintains its own adapter package (`@thunderid/integration-<name>`) in the ThunderID repo. The host package is a peer dependency.

If the user has not said, ask:

> Is this an **upstream contribution** to `<framework>`'s repo, or a **standalone `@thunderid/*` package** that ThunderID ships and maintains?

Use the matching sub-guide below.

---

### Type 4a — Upstream Contribution

Use when ThunderID will submit a PR to the host package's repository to add ThunderID support there. No `@thunderid/*` package is released.

#### Information to collect

Ask the user (in one message):
- **Integration name** — human-readable name (e.g., "Auth.js", "Passport")
- **Host repo** — the upstream repository receiving the PR (e.g., `nextauthjs/next-auth`)
- **Interface to implement** — the provider/strategy/plugin contract (e.g., `OIDCConfig` in `@auth/core`)
- **Problem** — what friction developers face today
- **Why now** — adoption argument
- **Parent umbrella issue number** — typically `#1895`
- **Assignee** — GitHub username (optional)
- **Milestone** — milestone title (optional)

#### Title format

```
Thunder <Integration Name> Provider/Strategy/Plugin
```

No package name in the title — there is no `@thunderid/*` release.

Use "Provider" for OAuth/OIDC provider frameworks (Auth.js, NuxtAuth), "Strategy" for Passport-style frameworks, "Plugin" for platform plugins (Backstage).

#### Body template

```markdown
### What problem are we solving?

<What friction developers face when trying to use ThunderID with <framework> — manual token wiring, missing provider config, etc.>

### Who are we solving this for?

**Primary:** <Developer persona — e.g., "Full-stack developers building with Auth.js v5">

* **Goal:** <what they want — e.g., "use ThunderID as a built-in Auth.js provider with zero boilerplate">
* **Pain:** <what they face today — e.g., "must hand-roll OIDC config and keep it in sync with ThunderID changes">

### Why should we solve this now?

**Why now:**

* **Value to Persona:** <e.g., "drop-in ThunderID support importable from the framework itself">
* **Value to Org:** <e.g., "Auth.js is the de-facto auth library for Next.js; a built-in listing gives ThunderID visibility to a large developer audience">

### Proposed Solution

Contribute a ThunderID <Provider/Strategy/Plugin> to [<host-repo>](https://github.com/<host-repo>) implementing the `<Interface>` contract. This involves:

1. **Upstream PR** — implement the provider/strategy/plugin and submit a PR to `<host-repo>`.
2. **Host package documentation** — submit a PR to the <framework> docs to add ThunderID to the providers/strategies list.
3. **ThunderID documentation** — add a <framework> integration guide to the ThunderID docs.

### Alternatives

<Developers today use the framework's generic OIDC/OAuth2 escape hatch with manual configuration — this works but is undiscoverable, requires internal knowledge of ThunderID's endpoint structure, and breaks when either side changes.>

---
Parent issue: #<umbrella-issue-number>
```

---

### Type 4b — Standalone Package

Use when ThunderID ships and owns the integration as `@thunderid/integration-<name>`.

#### Information to collect

Ask the user (in one message):
- **Integration name** — human-readable name (e.g., "Passport", "Backstage")
- **Package name** — `@thunderid/integration-<name>` (e.g., `@thunderid/integration-passport`)
- **Target framework** — the auth framework being integrated
- **ThunderID SDK dependency** — which ThunderID SDK this wraps (almost always `@thunderid/node`)
- **Problem** — what friction developers face today
- **Why now** — adoption argument
- **Proposed solution** — describe the provider/strategy/plugin to implement
- **Parent umbrella issue number** — typically `#1895`
- **Assignee** — GitHub username (optional)
- **Milestone** — milestone title (optional)

#### Title format

```
Thunder <Integration Name> Provider/Strategy/Plugin (<package-name>)
```

#### Body template

```markdown
### What problem are we solving?

<What friction developers face when trying to use ThunderID with <framework>.>

### Who are we solving this for?

**Primary:** <Developer persona>

* **Goal:** <what they want>
* **Pain:** <what they face today>

### Why should we solve this now?

**Why now:**

* **Value to Persona:** <direct benefit>
* **Value to Org:** <strategic value>

### Proposed Solution

Implement `<package-name>` as a ThunderID <Provider/Strategy/Plugin> for <framework>, built on `<thunderid-sdk-dependency>`. The package will expose a <ProviderConfig/Strategy/Plugin> that handles <key responsibilities>.

### Alternatives

<Developers today must manually configure the integration — error-prone and difficult to maintain.>

---
Parent issue: #<umbrella-issue-number>
```

### Labels

`Developer Experience`

### Milestone

Set if the user provides one.

---

## Step N — Confirm before creating

Before calling `gh issue create`, show the user a preview:

```
## Issue preview

**Repo:** thunder-id/thunderid
**Title:** <title>
**Labels:** <labels>
**Assignee:** <assignee or none>
**Milestone:** <milestone or none>

---
<body>
```

Then ask:

> Ready to create this issue? Reply **yes** to proceed or tell me what to change.

Only run `gh issue create` after explicit confirmation.

---

## Creating the issue

Use this command shape (adjust flags as needed):

```bash
gh issue create \
  --repo thunder-id/thunderid \
  --title "<title>" \
  --body "<body>" \
  --label "Developer Experience" \
  --label "<additional label if any>" \
  --assignee "<username>" \
  --milestone "<milestone title>"
```

Omit `--assignee` if none was provided. Omit `--milestone` if none was provided.

After creation, output the issue URL so the user can open it directly.

---

## Post-creation: umbrella update reminder

If the newly created issue should be tracked in an umbrella issue (Types 3 and 4), remind the user:

> Issue created: <url>
>
> Don't forget to update the umbrella issue (#<number>) to link this issue in the relevant table row and change the status from "Sub-issue / tracking link" to the issue URL.
