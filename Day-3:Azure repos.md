# Azure Repos & Git — Source Control (Full Tutorial)

> Comprehensive study notes based on **Day 3** of the *Azure DevOps Zero to Hero* series by *Tech Tutorials with Piyush*. Written so you can understand and revise everything covered without re-watching the video.

---

## Table of Contents

1. [Overview](#overview)
2. [Introduction to Source Control & Azure Repos](#1-introduction-to-source-control--azure-repos)
3. [Git vs TFVC](#2-git-vs-tfvc)
4. [Configuring VS Code as a Git Client](#3-configuring-vs-code-as-a-git-client)
5. [Cloning a Repository](#4-cloning-a-repository)
6. [Committing Changes & the Staging Area](#5-committing-changes--the-staging-area)
7. [Reviewing History & Diffs](#6-reviewing-history--diffs)
8. [Branches](#7-branches)
9. [Managing Branches (Create, Delete, Prune, Restore, Lock)](#8-managing-branches-create-delete-prune-restore-lock)
10. [Tags & Releases](#9-tags--releases)
11. [Managing Repositories](#10-managing-repositories)
12. [Pull Requests](#11-pull-requests)
13. [Branch & Repository Policies](#12-branch--repository-policies)
14. [Quick Revision](#quick-revision)

---

## Overview

**What this covers:** How to use **Azure Repos** (the source-control service in Azure DevOps) with **Git** — configuring a client (VS Code), cloning, committing, reviewing history, branching, tagging, managing repositories, and using **pull requests** and **branch policies** to control code quality. All demonstrated on the **Parts Unlimited** sample app generated in Day 2.

**What you will learn:**

- What **source control** is and why it exists.
- The difference between **Git (distributed)** and **TFVC (centralized)**.
- The Git workflow: **clone → change → stage → commit → sync (push)**.
- **Local vs remote branches**, and how to create/delete/prune/restore/lock them.
- **Tags** for marking releases.
- **Pull requests** for reviewing and merging code.
- **Branch policies** (required reviewers, linked work items, auto-reviewers).

**Prerequisites:** Day 2 (an Azure DevOps project with the Parts Unlimited repo). Basic command-line familiarity and Git installed help.

> **Additional Context:** *Azure Repos* is one of the five core Azure DevOps services (Boards, **Repos**, Pipelines, Test Plans, Artifacts). It provides Git repositories that integrate with Boards (work items) and Pipelines (CI/CD).

---

## 1. Introduction to Source Control & Azure Repos

### Definition

**Source control** (a.k.a. **version control**) is a system that **tracks changes to code over time** and maintains the full history of a codebase. **Azure Repos** is Azure DevOps's source-control service.

### How It Works

When a user **commits** a change, the system takes a **snapshot** of the code, keeping older and newer versions plus complete history (who changed what, when, and why — with a **commit ID**).

### Why It Matters

Version control lets you:

- **Roll back** to any earlier commit/version.
- **Review** changes before merging (as a repository maintainer).
- **Collaborate** with teammates without overwriting each other.
- Stay **organized** with a clear, auditable history.

> **Important:** Before version control, developers kept code on a **shared drive**, which made collaboration, change tracking, and conflict resolution extremely difficult. Version control was introduced to solve exactly these problems.

### Example (Commit History)

A commit history shows each change: the **author**, the **description/comment**, the **commit ID**, and which lines changed — plus **approved merge requests**. You can click any commit to review or roll back to it.

---

## 2. Git vs TFVC

Azure Repos supports **two** version-control types:

### Definitions

- **Git — Distributed Version Control System (DVCS):** Every developer **clones the entire repository** — all files, all history, all versions — **locally**. You can work offline/remotely and later **sync** with the server. Git is the **most popular** VCS today, used by startups to large enterprises and for open-source/personal projects.
- **TFVC — Team Foundation Version Control — Centralized VCS:** Developers download **only one version** locally; **all history and other versions live on the central server**. Similar older systems include **Perforce** and **SVN**.

### How They Differ

| Feature | **Git (Distributed)** | **TFVC (Centralized)** |
| --- | --- | --- |
| Local copy | **Full repo** (all history/versions) | **One version** only |
| Offline work | Fully supported | Limited (needs server) |
| Collaboration | Multiple devs work in parallel easily | Harder; often uses **file locking** |
| Conflict handling | Merges well | More conflict pain |
| Popularity/trend | Dominant; industry standard | Declining; teams migrating away |
| Hosting examples | GitHub, GitLab, Bitbucket, **Azure Repos** | Perforce, SVN |

> **Definition — File locking (TFVC-style):** To edit a file you must **lock** it first so no one else can change it, then push; only then is it unlocked. This serializes work and causes bottlenecks — a key reason teams prefer Git.

> **Key Takeaway:** Git's distributed model (full local history, easy parallel work, better merging) is why most organizations use it and migrate off TFVC. This course focuses on **Git**.

> **Additional Context — Core Git terms you'll meet:**
> - **Repository (repo):** The project's version-controlled folder.
> - **Clone:** Copy a remote repo to your machine.
> - **Commit:** A saved snapshot of staged changes (with a message and unique hash/ID).
> - **Branch:** An independent line of development.
> - **Push / Pull / Fetch:** Send commits to / retrieve+merge from / retrieve-only from the remote.
> - **Merge:** Combine one branch's changes into another.

---

## 3. Configuring VS Code as a Git Client

The video uses **VS Code** as the Git client (any client works). Setup in the integrated terminal (switched to **Git Bash**):

```bash
# Save credentials on Windows so you aren't prompted every time (one-time)
git config --global credential.helper wincred

# Identify yourself on every commit
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

> **Additional Context:**
> - `--global` applies these settings to **all repos** for your user. Omit it (or use `--local`) to set per-repo.
> - `credential.helper wincred` is Windows-specific. On macOS use `osxkeychain`; on Linux use `store`, `cache`, or `libsecret`. Modern Git also offers the cross-platform **Git Credential Manager**.
> - Other Git clients: Git for Windows CLI, VS Code, Visual Studio, GitKraken, SourceTree, etc.

---

## 4. Cloning a Repository

### Steps

1. In Azure DevOps → open the project (**Parts Unlimited**) → **Repos** (left menu).
2. Click **Clone** (top-right). Options:
   - **Generate Git credentials** or copy the **repository URL**, or
   - **Clone in VS Code** (default IDE; a dropdown offers other IDEs).
3. Choose **Clone in VS Code** → confirm the prompt → pick/create a local folder.
4. **Authenticate** to your Microsoft account (one-time; credentials are then saved via `wincred`).
5. **Add to workspace** — the source code appears in VS Code, fully cloned.

> **Additional Context:** Cloning downloads the entire repo **and** its history to your machine, creating a `.git` folder that stores all versions and metadata. Equivalent CLI: `git clone <repository-url>`.

---

## 5. Committing Changes & the Staging Area

### The Workflow

Editing a file goes through distinct stages:

1. **Working directory** — you edit and **save** a file (e.g., add a comment `// first change`, Ctrl+S).
2. **Staging area** — the change appears under **Source Control** as ready to be **staged**. Staged changes are **local**, not yet on the remote.
3. **Commit** — record the staged snapshot **locally** with a **commit message**.
4. **Sync / Push** — send committed changes to the **remote** repository (e.g., `origin/master`).

> **Definition — Staging area:** A holding zone between your working files and a commit. You choose exactly which changes to include in the next commit. Staged ≠ committed; committed (locally) ≠ pushed (remote).

### Demonstrations

- **Simple commit:** Save a change → enter message *"my first change"* → **Commit** (VS Code offers "Stage all & commit") → **Sync changes** to push to `origin/master`. When the pending count shows **0**, the push is complete.
- **Partial staging (key concept):** Edit **two** files (*"my second change"*, *"my third change"*). Stage **only one** (click the **+** next to a file). Commit staged (**⋮ → Commit Staged**) with a message, then **Sync**. Result on the remote: **only the staged/committed file** appears; the unstaged file remains a **local-only** change until you stage, commit, and sync it too.

> **Key Takeaway:** Staging lets you commit a **subset** of your changes. A change reaches the remote only after **stage → commit → sync (push)** — each step is deliberate.

> **Additional Context — CLI equivalents:**
> ```bash
> git add <file>        # stage a specific file
> git add .             # stage everything
> git commit -m "msg"   # commit staged changes locally
> git push              # sync commits to the remote
> ```
> A **`.gitignore`** file lists paths Git should never track (build outputs, secrets, `node_modules`, etc.).

---

## 6. Reviewing History & Diffs

### In Azure Repos

- **Repos → Commits** shows the latest commit on top (e.g., *"my first change"*), the author, message, and **commit ID**.
- Opening a commit shows a **diff**: **added lines highlighted green**, **deleted lines highlighted red**.
- To retrieve an old version of a file: open the **previous commit → Browse files →** navigate (e.g., `src/models/...`) **→ Download** the file as it existed then.

### In VS Code

- Click a changed file to see inline diff markers (e.g., a **`+`** and green highlight in front of a changed line) — mirroring the Azure Repos view.

> **Additional Context:** A **diff** ("difference") compares two versions line-by-line. CLI equivalents: `git log` (history), `git show <commit>` (a commit's diff), `git diff` (unstaged changes). Every commit has a unique **hash** you can reference or revert to.

---

## 7. Branches

### Definition

A **branch** is an independent, parallel copy of the codebase. Changes in one branch **do not affect** other branches, even though they share the same repository.

### Local vs Remote Branches

- On clone, a **default local branch** (`master`) is created.
- The corresponding **remote branch** is `origin/master`.
- You commit to the **local** branch, then **sync** to push to the **remote** branch.

> **Important:** `master` (local) and `origin/master` (remote) are **distinct**. The naming convention (`origin/…`) distinguishes remote-tracking branches from local ones.

### How Branches Isolate Work — Example

- `master` has 2 files × 100 lines.
- Create `dev` **from** `master` → `dev` starts identical (2 files × 100 lines).
- Edit a file in `dev` → that change appears **only** in `dev`, not in `master`.
- Sync `dev` → changes go only to the **remote `dev`** branch.

### Why Branches Matter

Multiple developers can work on **separate branches** (e.g., **feature branches**) without impacting the main codebase, then open a **pull request** to merge into the main branch.

> **Additional Context — Common branching strategies:** *Feature branching* (one branch per feature), *GitHub Flow* (short-lived branches off `main` + PRs), and *Git Flow* (`main`, `develop`, `feature/*`, `release/*`, `hotfix/*`). Note: modern Git/hosts often default the main branch name to **`main`** rather than `master`; they're functionally the same.

---

## 8. Managing Branches (Create, Delete, Prune, Restore, Lock)

### Create a Branch — from VS Code

1. Click the branch name (bottom-left, e.g., `master`) → **Create new branch from…** → choose local `master`.
2. Name it (e.g., `dev`) → Enter. VS Code **switches** to `dev`; new commits go there.
3. **Sync** — this pushes both **code and the new branch** to the remote (the `dev` branch now appears in Azure Repos, authored by you).

### Create a Branch — from Azure Repos

- **Repos → Branches → New branch** → name it (e.g., `release`), base it on `master`, optionally link a **work item** → **Create**.
- Back in VS Code, run **Git: Fetch** (Command Palette, `Ctrl+Shift+P`) to see `origin/release`; select it to also create a matching **local** branch.

### Delete a Branch (and the sync nuance)

- In Azure Repos: **Branch → ⋮ → Delete branch** removes the **remote** branch.
- But VS Code may still show both `dev` and `origin/dev` until synced. To fully clean up locally:
  - Switch off the branch first (you can't delete the branch you're on) — e.g., switch to `master`.
  - **Command Palette → Git: Delete Branch** → select `dev` to remove the **local** branch.
  - The stale **remote-tracking** ref (`origin/dev`) is removed by **pruning**: **Command Palette → Git: Fetch** (which fetches latest and **prunes** unused remote branches).
- Verify in VS Code's **Output → Git** logs (switch the Output dropdown to **Git**) to see the `git fetch`/prune actions.

> **Definition — Prune:** Removing stale **remote-tracking** references for branches that no longer exist on the server. CLI: `git fetch --prune` (or `git remote prune origin`).

### Restore a Deleted Branch

- In Azure Repos → **Branches → search the exact branch name** (case-sensitive!) → it appears under **deleted branches** → **⋮ → Restore branch**.

> **Important:** You must know the **exact name (including case)** to restore a deleted branch.

### Lock a Branch (read-only)

- **Branch → ⋮ → Lock** makes it **read-only** — no new changes allowed. Used during a **code freeze** (e.g., year-end when changes are prohibited). **Unlock** the same way.

> **Additional Context — CLI branch commands:**
> ```bash
> git checkout -b dev        # create & switch to 'dev'
> git switch master          # switch branches (newer syntax)
> git branch -d dev          # delete a local branch
> git push origin --delete dev  # delete a remote branch
> git fetch --prune          # fetch + remove stale remote refs
> ```

---

## 9. Tags & Releases

### Definition

A **tag** marks a specific commit as a meaningful point — typically a **finalized release** — so you can reference or return to that exact state later.

### How to Create a Tag (Azure Repos)

- **Repos → Tags → New tag** → name (e.g., `1.1`), base it on `master` (the latest commit), add a description (e.g., *"release it now"*) → **Create**.
- Clicking the tag shows the commits it includes (e.g., *"my first change"*, *"my second change"*), confirming what's being released.

> **Additional Context:** Tags are commonly used for **semantic versioning** (e.g., `v1.0.0`). Git has **lightweight tags** (just a pointer) and **annotated tags** (with author, date, message — recommended for releases). CLI: `git tag -a v1.1 -m "release" && git push origin v1.1`. Azure Pipelines can trigger releases off tags.

---

## 10. Managing Repositories

### Create a Repository

- Click **+** next to the project → **New repository** → name it (e.g., `test`), optionally **add a README**, choose **Git** or **TFVC** → **Create**.

### Switch / Import / Manage

- Use the repo selector to **switch** between repos; you can also **create new** or **import** an existing repo.
- **Manage repositories → ⋮** lets you **rename** or **delete** a repo (deleting requires typing the repo name to confirm).

> **Additional Context:** Adding a **README** initializes the repo with a first commit (so it isn't empty). **Import** is useful for migrating an existing Git/TFVC repo (e.g., from GitHub) into Azure Repos.

---

## 11. Pull Requests

### Definition

A **pull request (PR)** is the mechanism for **controlling what code gets merged** into a protected branch (e.g., `master`/`main`). It ensures changes are **reviewed and tested** before merging.

### Why It Matters

With many developers collaborating, PRs guarantee that code entering the main branch has been **reviewed by a maintainer** and meets quality standards — preventing unreviewed or broken code from reaching production.

### The PR Workflow

1. A developer creates a **branch** and makes changes there.
2. They open a **pull request** to merge that branch into `master`.
3. A **repository maintainer/reviewer** reviews the code and file changes and chooses to:
   - **Approve**, **Approve with suggestions**, **Reject/Decline**, or **Wait for author**.
4. Once approved, the PR is **completed** (merged).

### Demo Steps

- In VS Code, stage a pending change (*"my third change"*), commit (*"pull request demo"*), **sync**.
- **Create pull request**: source branch **`release`** → target **`master`**; title *"pull request demo"*; add a **reviewer** (yourself) and link a **work item** (e.g., *"As a customer, I want to view new tutorials"*) → **Create**.
- Review the **Files** tab (changed files) and **Updates/Commits** tab (commit history).
- As reviewer: **Approve** (or approve-with-suggestions/reject). Add a comment (e.g., *"LGTM"* = "looks good to me").
- **Complete** the PR: choose a **merge type**, optionally **complete linked work items** (the attached work item is marked **Done** on merge) → **Complete merge**.
- With **no merge conflict**, the change merges; verifying in **Repos** shows the change now on `master`.

> **Definition — Merge conflict:** Occurs when two branches change the **same lines** of a file differently, so Git can't auto-combine them; a human must resolve which version wins. "No merge conflict" means no other developer edited the same code.

> **Additional Context — Merge strategies in Azure Repos PRs:**
> - **Merge (no fast-forward):** keeps all commits + a merge commit.
> - **Squash merge:** combines the branch's commits into one clean commit on the target.
> - **Rebase:** replays commits on top of the target for a linear history.
> **"LGTM"** is common review shorthand for approval.

---

## 12. Branch & Repository Policies

### Definition

**Policies** enforce rules on repositories and branches to strengthen security and code quality — especially on protected branches like `master` (where production code lives).

### Where to Configure

- **Project settings → Repositories →** select the repo.

### Repository-Level Settings

- **Forking:** whether users may **fork** the repo (enabled by default; can be disabled).

### Branch Policies (e.g., on `master`)

- **Require a minimum number of reviewers** — e.g., a PR needs **≥ 2 approvals** before it can merge.
- **Allow requestors to approve their own changes** — usually **disabled** (so authors can't self-approve).
- **Check for linked work items** — **blocks** completing a PR unless a work item is linked/completed, ensuring traceability.
- **Automatically include reviewers** — auto-add default reviewer(s) to every PR (optionally scoped to specific **folder paths** so certain folders require a specific reviewer). **Save** to apply.

> **Key Takeaway:** Branch policies turn PRs from optional courtesy into **enforced gates** — mandatory reviews, work-item linkage, and required reviewers protect the main/production branch.

> **Additional Context:** Other common Azure Repos branch policies include **requiring a successful build (CI) before merge**, **comment resolution**, **limiting merge types**, and **status checks** from external services. These tie Repos directly to **Pipelines** for automated quality gates.

---

# Quick Revision

### Key Concepts

- **Source control** tracks all changes/history so you can roll back, review, and collaborate safely.
- **Git = distributed** (full local history, parallel work, great merging); **TFVC = centralized** (one local version, file locking). Git is the industry standard.
- Git workflow: **working dir → stage → commit (local) → sync/push (remote)**.
- **Local vs remote branches:** `master` vs `origin/master`; branches isolate changes.
- **Branch operations:** create, delete, **prune** stale remote refs, **restore** (exact name), **lock** (code freeze).
- **Tags** mark releases (e.g., `1.1`).
- **Pull requests** gate merges into protected branches via review/approval.
- **Branch policies** enforce min reviewers, linked work items, auto-reviewers, and (commonly) required builds.

### Important Definitions

- **Source/Version Control:** System tracking code changes and history.
- **Commit:** A saved snapshot with a message and unique ID/hash.
- **Staging area:** Holding zone selecting what goes into the next commit.
- **Clone:** Copy a remote repo (with history) locally.
- **Branch:** Independent line of development.
- **Local vs remote branch:** On your machine vs on the server (`origin/…`).
- **Fetch / Pull / Push:** Retrieve-only / retrieve+merge / send commits.
- **Prune:** Remove stale remote-tracking references.
- **Tag:** A named pointer to a specific commit (usually a release).
- **Pull Request (PR):** Reviewed merge of one branch into another.
- **Merge conflict:** Same lines changed differently on two branches, needing manual resolution.
- **Branch policy:** Enforced rules protecting a branch.

### Important Comparisons

**Git vs TFVC**

| | Git | TFVC |
| --- | --- | --- |
| Model | Distributed | Centralized |
| Local copy | Full history | One version |
| Collaboration | Easy, parallel | File-locking, serialized |
| Trend | Standard | Declining |

**Stage vs Commit vs Push**

| Step | Scope | Meaning |
| --- | --- | --- |
| Stage (`git add`) | Local | Select changes for next commit |
| Commit (`git commit`) | Local | Save a snapshot |
| Sync/Push (`git push`) | Remote | Publish commits to server |

### Common Mistakes / Misconceptions

- **Assuming commit = pushed.** A commit is **local**; changes reach the remote only after **sync/push**.
- **Deleting a remote branch but still seeing it locally.** You must delete the **local** branch and **prune** (`git fetch --prune`).
- **Trying to delete the branch you're currently on.** Switch to another branch first.
- **Wrong-case branch name when restoring** — restore requires the **exact** name.
- **Editing directly on `master`/`main`** instead of a feature branch + PR.
- **Self-approving PRs** — disable "allow requestors to approve their own changes."
- **Forgetting `.gitignore`**, accidentally committing build artifacts/secrets.

### Interview / Exam Points

- Explain **distributed vs centralized** VCS (Git vs TFVC) with pros/cons.
- Describe the **stage → commit → push** flow and the role of the **staging area**.
- Difference between **local** and **remote** branches; what `origin/` means.
- How do **fetch**, **pull**, and **push** differ?
- What is **pruning**, and when is it needed?
- Purpose of **tags** vs **branches**.
- Walk through a **pull request** lifecycle and reviewer options.
- What is a **merge conflict** and how is it resolved?
- Name key **branch policies** and why they protect the main branch.
- **Squash** vs **merge** vs **rebase** merge strategies.

### Final Takeaways

1. Source control is essential for history, rollback, review, and safe collaboration.
2. **Git (distributed)** beats **TFVC (centralized)** for parallel work and merging — hence its dominance.
3. Changes progress deliberately: **edit → stage → commit (local) → sync/push (remote)**.
4. **Branches isolate work**; distinguish **local** (`master`) from **remote** (`origin/master`).
5. Manage branches fully: create, delete, **prune** stale refs, **restore** by exact name, **lock** for code freezes.
6. **Tags** cleanly mark releases for later reference.
7. **Pull requests** enforce review before code enters protected branches.
8. **Branch policies** (min reviewers, linked work items, auto-reviewers, required builds) turn best practices into enforced gates.
9. Azure Repos integrates tightly with **Boards** (link work items to PRs) and **Pipelines** (build validation).
10. **Do the hands-on** — Git concepts stick only with practice.
