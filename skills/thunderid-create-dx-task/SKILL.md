---
name:  thunderid-create-dx-task
description: Create a Developer Experience GitHub issue for ThunderID. Use when filing a new SDK tracking issue, ecosystem SDK issue, individual SDK issue, or integration issue in the thunder-id/thunderid repo.
allowed-tools: Bash(gh issue create *), Bash(gh issue list *), Bash(gh issue view *), Bash(gh api *), AskUserQuestion
---

# ThunderID DX Issue Creator

You are creating a Developer Experience GitHub issue in the `thunder-id/thunderid` repository.

## Defaults

- **Default assignee:** `brionmario` — use this unless the user specifies otherwise.
- **Default parent umbrella issue:** `#1895`

---

## Step 0 — Identify the issue type

Use `AskUserQuestion` to ask the user which type of DX issue they want to create:

```
question: "What kind of Developer Experience issue do you want to file?"
header: "Issue Type"
options:
  - label: "Umbrella / Tracking"
    description: "A high-level tracking issue covering an entire SDK suite or DX initiative (e.g., \"[UMBRELLA ☂️] Thunder SDK Suite\"). Labels: Type/Task + Developer Experience."
  - label: "Ecosystem SDK"
    description: "A parent issue for a whole language/platform ecosystem (e.g., \"Thunder JavaScript SDKs\"). Labels: Type/New Feature + Developer Experience."
  - label: "Individual SDK"
    description: "An issue for a single SDK package (e.g., \"Thunder Next.js SDK (@thunderid/nextjs)\"). Label: Developer Experience."
  - label: "Integration"
    description: "An issue for a third-party auth integration (e.g., \"Thunder Auth.js Provider\"). Label: Developer Experience."
```

Wait for the answer, then proceed to the matching type guide below.

---

## Step 1 — Collect remaining information

Use `AskUserQuestion` for any fields not already provided by the user. Group all missing fields into a single `AskUserQuestion` call (multiple questions at once). Do not ask for fields the user already supplied in their initial message.

### Milestone lookup

Before asking about milestones, fetch open milestones and present them as options:

```bash
gh api repos/thunder-id/thunderid/milestones --jq '.[] | select(.state=="open") | .title'
```

Present the results as options plus a "No milestone" option.

---

## Type 1 — Umbrella / Tracking Issue

### Fields to collect

- **Suite name** — what area does this umbrella cover? (e.g., "Thunder SDK Suite")
- **Subtitle** — a short descriptor after the dash (e.g., "Coverage, Integrations, and Roadmap")
- **Categories and SDKs** — list of categories and SDKs with Status and Priority
- **Goals** — 3–5 bullet points
- **Scope** — what this umbrella is and is not for

### Title format

```
[UMBRELLA ☂️] ThunderID <Suite Name> – <Subtitle>
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

### Fields to collect

- **Ecosystem name** — e.g., "JavaScript", "Python", "Go"
- **Persona** — who is the primary developer audience?
- **Problem** — what pain does the lack of an official SDK create?
- **Why now** — value to persona and value to org
- **Proposed solution** — high-level description of the SDK ecosystem to build
- **Parent umbrella issue number** — default `#1895`

### Title format

```
ThunderID <Ecosystem> SDKs
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

<High-level description of the SDK ecosystem to build.>

### Alternatives

<What developers do today instead, and why that's insufficient.>

---
Parent issue: #<number>
```

### Labels

`Type/New Feature` + `Developer Experience`

### Milestone

None unless the user specifies one.

---

## Type 3 — Individual SDK Issue

### Fields to collect

- **SDK name** — full human-readable name (e.g., "Next.js")
- **Package name** — npm/Maven/SwiftPM/etc. identifier (e.g., `@thunderid/nextjs`)
- **Persona** — primary developer audience
- **Problem** — what specific contexts or constraints make this SDK necessary?
- **Why now** — value to persona and value to org
- **Proposed solution** — high-level; mention which ThunderID SDKs it builds on only if it helps scope the issue
- **Parent issue number** — default `#1895`
- **Milestone** — fetch and present open milestones via `AskUserQuestion`

### Title format

```
ThunderID <SDK Name> SDK (<package-name>)
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

* **Value to Persona:** <concrete benefit>
* **Value to Org:** <market/adoption argument>

### Proposed Solution

<High-level description of the SDK and its key capabilities.>

### Alternatives

<What developers do today and why that falls short.>

---
Parent issue: #<parent-issue-number>
```

### Labels

`Developer Experience`

### Milestone

Set to the milestone the user provided.

---

## Type 4 — Integration Issue

Use `AskUserQuestion` to identify the delivery model if the user has not already stated it:

```
question: "Is this an upstream contribution or a standalone ThunderID package?"
header: "Delivery model"
options:
  - label: "Upstream contribution"
    description: "ThunderID is added as a provider/strategy/plugin directly to the host package's repo. No @thunderid/* package is shipped."
  - label: "Standalone package"
    description: "ThunderID ships and maintains its own @thunderid/integration-<name> adapter package."
```

Use the matching sub-guide below.

---

### Type 4a — Upstream Contribution

Use when ThunderID will submit a PR to the host package's repository. No `@thunderid/*` package is released.

#### Fields to collect

- **Integration name** — human-readable name (e.g., "Auth.js", "Better Auth")
- **Host repo** — the upstream repository (e.g., `better-auth/better-auth`)
- **Problem** — what friction developers face today
- **Why now** — adoption argument
- **Parent ecosystem issue number** — the ecosystem issue this integration belongs to (e.g., Auth.js → JavaScript ecosystem #2543). Look up the right issue if unsure: `gh issue list --repo thunder-id/thunderid --label "Developer Experience" --search "SDKs" --json number,title`
- **Milestone** — fetch and present open milestones via `AskUserQuestion`

Do **not** ask about or mention the internal provider interface or implementation contract — keep the issue at the product/DX level.

#### Title format

```
Integration: Contribute ThunderID as a <descriptor> <Framework> <provider/strategy/plugin>
```

Examples: `Integration: Contribute ThunderID as a built-in Auth.js provider`, `Integration: Contribute ThunderID strategy to Passport.js`.

Use "provider" for OAuth/OIDC provider frameworks (Auth.js, NuxtAuth, Better Auth), "strategy" for Passport-style frameworks, "plugin" for platform plugins (Backstage).

#### Body template

```markdown
### What problem are we solving?

<What friction developers face when trying to use ThunderID with <framework> — manual token wiring, missing provider config, etc.>

### Who are we solving this for?

**Primary:** <Developer persona>

* **Goal:** <what they want — e.g., "use ThunderID as a built-in provider with zero boilerplate">
* **Pain:** <what they face today>

### Why should we solve this now?

**Why now:**

* **Value to Persona:** <e.g., "drop-in ThunderID support importable from the framework itself">
* **Value to Org:** <e.g., "Auth.js is the de-facto auth library for Next.js; a built-in listing gives ThunderID visibility to a large developer audience">

### Proposed Solution

Contribute a ThunderID <Provider/Strategy/Plugin> to [<host-repo>](https://github.com/<host-repo>).

### Alternatives

<Developers today use the framework's generic OIDC/OAuth2 escape hatch with manual configuration — this works but is undiscoverable, requires internal knowledge of ThunderID's endpoint structure, and breaks when either side changes.>

---
Parent issue: #<umbrella-issue-number>
```

---

### Type 4b — Standalone Package

Use when ThunderID ships and owns the integration as `@thunderid/integration-<name>`.

#### Fields to collect

- **Integration name** — human-readable name
- **Package name** — `@thunderid/integration-<name>`
- **Target framework** — the auth framework being integrated
- **Problem** — what friction developers face today
- **Why now** — adoption argument
- **Proposed solution** — high-level description; no implementation details
- **Parent ecosystem issue number** — the ecosystem issue this integration belongs to (same lookup as Type 4a)
- **Milestone** — fetch and present open milestones via `AskUserQuestion`

#### Title format

```
Integration: Contribute ThunderID as a <descriptor> <Framework> <provider/strategy/plugin> (<package-name>)
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

<High-level description of the integration package and what it provides to developers.>

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

Show the user a preview using plain markdown (no tool call yet):

```
## Issue preview

**Repo:** thunder-id/thunderid
**Title:** <title>
**Labels:** <labels>
**Assignee:** <assignee>
**Milestone:** <milestone or none>

---
<body>
```

Then use `AskUserQuestion` to confirm:

```
question: "Ready to create this issue?"
header: "Confirm"
options:
  - label: "Create it"
    description: "Proceed and create the issue on GitHub"
  - label: "Make changes"
    description: "I want to edit something first"
```

Only run `gh issue create` after the user selects "Create it".

---

## Creating the issue

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

Omit `--assignee` if none was provided. Omit `--milestone` if none was provided. Omit `--label "<additional label if any>"` if there is no second label.

After creation, output the issue URL so the user can open it directly.

---

## Post-creation: umbrella update reminder

If the newly created issue should be tracked in an umbrella issue (Types 3 and 4), remind the user:

> Issue created: <url>
>
> Don't forget to update the umbrella issue (#<number>) to link this issue in the relevant table row.
