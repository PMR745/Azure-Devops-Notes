# DevOps, CI/CD, Agile & Azure DevOps — Foundations

> Comprehensive study notes based on **Day 1** of the *Azure DevOps Zero to Hero* series by *Tech Tutorials with Piyush*. These notes are written to let you fully understand and revise the material without re-watching the video.

---

## Table of Contents

1. [Overview](#overview)
2. [Cloud Computing](#1-cloud-computing)
3. [IaaS vs PaaS vs SaaS](#2-iaas-vs-paas-vs-saas)
4. [Lift and Shift Migration](#3-lift-and-shift-migration)
5. [Shared Responsibility Model](#4-shared-responsibility-model)
6. [Traditional SDLC & the Waterfall Model](#5-traditional-sdlc--the-waterfall-model)
7. [Agile](#6-agile)
8. [DevOps and CI/CD](#7-devops-and-cicd)
9. [Azure DevOps — Platform Walkthrough](#8-azure-devops--platform-walkthrough)
10. [Azure DevOps — Hosting Options & Pricing](#9-azure-devops--hosting-options--pricing)
11. [Quick Revision](#quick-revision)

---

## Overview

**What this covers:** The foundational concepts a beginner needs before working with Azure DevOps — cloud computing, cloud service models, the problems with older software delivery approaches, and how **Agile**, **DevOps**, and **CI/CD** solve them. It ends with a hands-on tour of the Azure DevOps platform.

**What you will learn:**

- What cloud computing is and why organizations move to it (CapEx vs OpEx).
- The three cloud service models: **IaaS**, **PaaS**, **SaaS**.
- The **shared responsibility model** between a customer and a cloud provider.
- Why the **traditional (waterfall) SDLC** was slow and error-prone.
- How **Agile** and **DevOps** improve delivery, and what **CI/CD** means.
- How to sign up for **Azure DevOps**, create organizations and projects, and what each built-in service does.

**Why it matters:** DevOps and cloud skills are core to modern software engineering roles. Understanding *why* these practices exist (not just the tools) is what makes the tooling make sense.

**Prerequisites:** None strictly required. Basic familiarity with software development (writing code, testing, deploying) and version control (e.g., Git/GitHub) will help.

---

## 1. Cloud Computing

### Definition

**Cloud computing** is a way to access computing resources and services (compute, storage, networking, databases, etc.) **over the internet**, renting them from a provider instead of buying and managing the hardware yourself.

> **Key idea:** *Buying* hardware is "old school." *Renting* hardware and services on demand is what cloud computing is all about.

### Why We Need It — The Business Problem

Imagine you own a small IT firm and want to scale. Expanding the traditional way requires large investments:

- **CapEx (Capital Expenditure)** — large **one-time, upfront** costs.
  - Examples: office space, hardware/servers, furniture.
- **OpEx (Operational Expenditure)** — **recurring** running costs.
  - Examples: hardware maintenance, employee salaries, electricity, monthly building rent.

These costs are **roadblocks to expansion**. The goal is to **minimize CapEx and OpEx** while building a system that is:

- **Highly scalable** — can grow/shrink with demand.
- **Highly available** — stays up with minimal downtime.
- **Fault tolerant** — keeps working even when a component fails.
- **Secure** — has built-in security.
- **High performance**.

Cloud computing addresses all of these by turning heavy upfront capital costs into flexible, usage-based operating costs.

### How It Works

Instead of buying and maintaining physical equipment, you **rent** the equivalent service over the internet and use it remotely.

### Example

You need to store a large number of files.

- **Old way:** Buy a physical hard disk drive, install it, maintain it.
- **Cloud way:** Rent a storage service and use it over the internet:
  - **AWS S3** (Amazon)
  - **Azure Storage** (Microsoft)
  - **GCP Blob Storage** (Google — commonly *Cloud Storage*)

You get access instantly, pay for what you use, and the provider handles the underlying hardware.

### Important Points

- Cloud shifts spending from **CapEx → OpEx** (pay-as-you-go).
- Core benefits: **scalability, availability, fault tolerance, security, performance**.
- The three major public cloud providers referenced: **AWS, Azure, GCP**.

> **Additional Context:** The main service (or "deployment") models of cloud are typically described as **public cloud** (shared infrastructure owned by a provider, e.g., Azure), **private cloud** (dedicated to one organization), and **hybrid cloud** (a mix of on-premises and public cloud). The video focuses on the public cloud usage pattern.

---

## 2. IaaS vs PaaS vs SaaS

These are the three main **cloud service models**. They differ in **how much the provider manages** versus **how much you manage**.

### Definitions

- **IaaS — Infrastructure as a Service:** You rent raw infrastructure (virtual machines, storage, networking) and configure it yourself. You install your own **operating system** and applications and handle all administration. **You have full control.**
- **PaaS — Platform as a Service:** The provider gives you a ready **runtime environment**, platform, and development tools to deploy your application. You **do not** get access to the underlying operating system — you just deploy and run your app.
- **SaaS — Software as a Service:** The provider gives you a finished **application** hosted and run on their cloud. You simply use it as an **end user**; you don't deploy anything.

### How It Works — Who Manages What

| Aspect | **IaaS** | **PaaS** | **SaaS** |
| --- | --- | --- | --- |
| What you rent/use | Infrastructure (VMs, storage, network) | Platform + runtime + dev tools | Finished application |
| Operating system access | **You manage it** | Provider manages it | Provider manages it |
| Admin tasks (patching, upgrades, backups) | **You do them** | Provider does them | Provider does them |
| Level of control | Full control | Limited to your app + config | Just usage |
| Typical billing | **Pay-per-use** (per duration used) | Mostly **service-based** | Mostly **subscription-based** |
| Examples | Amazon EC2, Azure VMs, GCP Compute Engine | Azure Web App (App Service) | Gmail, Office 365, Dropbox |

> **Definition — Patching:** Keeping your software and OS packages **up to date** so they include the latest fixes for **security vulnerabilities** and bugs. In IaaS this is *your* job; in PaaS/SaaS the provider handles it.

### When to Use Each

- **Choose IaaS** when you need **full control** over the OS and want to customize the environment/application.
- **Choose PaaS** when you **don't want to manage admin tasks** or the OS, and just want to focus on deploying your app.
- **Choose SaaS** when the **standard version** of an application is enough and you need no customization (e.g., just use Gmail — you can't and wouldn't deploy your own copy of it).

### Example

- **IaaS:** Rent an Azure VM, install Linux, deploy a custom app, and manage patching yourself.
- **PaaS:** Push your web app to Azure App Service; Microsoft runs the servers and OS for you.
- **SaaS:** Log into Gmail or Office 365 and start working — no deployment, no servers to manage.

### Important Points

- The trade-off is **control vs convenience**: more control (IaaS) means more responsibility; more convenience (SaaS) means less control.
- **Pay-per-use** (IaaS) → charged for the duration of resources used.
- **Subscription** (SaaS) → charged per user/plan.

> **Additional Context:** A common way to remember the split is the "pizza as a service" analogy: IaaS = you're given the kitchen and ingredients; PaaS = the kitchen is set up and heated for you; SaaS = the pizza is delivered ready to eat. There is also a newer model, **FaaS / Serverless** (e.g., Azure Functions, AWS Lambda), where you deploy only code and the provider manages everything else including scaling.

---

## 3. Lift and Shift Migration

### Definition

**Lift and shift** means moving applications currently hosted **on-premises** to the **cloud** **without changing the application itself** — you "lift" the app as-is and "shift" it to cloud infrastructure to gain cloud benefits.

### How It Works & Best Fit

Because you want to keep the application unchanged but still control the OS and environment, **IaaS is the ideal target** for lift-and-shift. You get full control over the operating system and can run the app the same way it ran on-premises.

### Example

A company runs a legacy app on physical servers in its own data center. Instead of rewriting it, they provision Azure VMs (IaaS), install the same OS and dependencies, and move the app over largely unchanged.

### Important Points

- Goal: gain cloud benefits (scalability, availability) with **minimal application changes**.
- **IaaS** is the natural fit because it preserves OS-level control.

> **Additional Context:** Lift-and-shift (also called **rehosting**) is often the *first* step of a longer cloud journey. Later stages may include **re-platforming** (small optimizations, e.g., moving to a managed database) and **re-architecting/refactoring** (redesigning the app to be cloud-native, e.g., microservices or serverless). Lift-and-shift is fast but may not fully use cloud-native cost and scaling advantages.

---

## 4. Shared Responsibility Model

### Definition

The **shared responsibility model** is an agreement between the **customer** and the **cloud provider** (here, **Microsoft/Azure**) defining who is responsible for which parts of security and operations. Some responsibilities are the provider's, some are the customer's, and some are **shared** — and the split **shifts depending on the service model** (on-prem, IaaS, PaaS, SaaS).

### How It Works — Responsibility Shifts by Model

As you move from on-premises → IaaS → PaaS → SaaS, **more responsibility transfers to the provider**.

| Responsibility layer | On-Prem | IaaS | PaaS | SaaS |
| --- | --- | --- | --- | --- |
| Physical data center, network, hosts | Customer | **Provider** | Provider | Provider |
| Operating system | Customer | **Customer** | **Provider** | Provider |
| Network controls | Customer | Customer/Shared | Shared | Provider |
| Applications | Customer | Customer | Shared | Provider |
| Identity & directory infrastructure | Customer | Shared | Shared | Shared |
| Information & data | Customer | **Customer** | **Customer** | **Customer** |
| Devices (endpoints) | Customer | **Customer** | **Customer** | **Customer** |
| Accounts & identities | Customer | **Customer** | **Customer** | **Customer** |

Key transitions highlighted in the video:

- **On-prem:** The customer (or a hired third party) manages **everything** — physical data center, physical network, physical host, OS, networking, and application.
- **IaaS:** The provider takes over the **physical infrastructure** (data center, network, hosts). You still manage the **OS**, your app, and network controls.
- **PaaS:** The provider manages the physical infrastructure **and the operating system**. This is the **main difference between IaaS and PaaS** — *in IaaS you manage the OS; in PaaS Azure manages the OS.*
- **SaaS:** The provider manages physical infra, OS, **application, and network controls**. You are left mainly responsible for your **information/data**, **devices**, and **accounts/identities** (e.g., configuring **single sign-on / OAuth / LDAP**).

> **Clarification:** In the video the identity/application/network-controls layer is described as "shared responsibilities between you and the customer." This is a slip of the tongue — the split is between **you (the customer)** and **Microsoft (the provider)**. Also, per Microsoft's official model, **information & data, devices, and accounts & identities are *always* the customer's responsibility** regardless of the service model; **physical hosts, physical network, and physical datacenter are *always* the provider's**; and **OS, network controls, applications, and identity/directory infrastructure vary** by service type.

### Important Points

- Responsibility is **not** entirely handed off in the cloud — customers **always** own their data, identities, and endpoint devices.
- The higher up the stack you go (IaaS → SaaS), the **less** you manage and the **more** the provider manages.

> **Key Takeaway:** "The cloud is secure" does **not** mean "your workload is automatically secure." Security is *shared* — misconfiguring your own data access, identities, or app settings is still your responsibility.

---

## 5. Traditional SDLC & the Waterfall Model

### Definition

The **traditional software development life cycle (SDLC)** historically followed the **Waterfall model** — a strictly **linear, top-to-down** sequence of phases where **you cannot return to a previous phase** once you move on (like water falling and never flowing back up).

### The Old Delivery Workflow (Multiple Siloed Teams)

Typical teams involved: **Developers, Operations (Ops), Quality Assurance (QA)/Testing, and Production Support**.

A representative flow:

1. Multiple developers **commit code** to a version control system.
2. Once committed and approved, someone from **Ops creates a build** from the committed code.
3. The build is placed on a **shared folder / network drive / environment**.
4. Ops **deploys the build to a lower environment** (e.g., QA).
5. The **testing team is notified** and runs their test cases against the build.
6. **Reports** go back to developers and stakeholders.
7. Developers **fix bugs**, re-commit, and the cycle repeats for other environments (e.g., **SIT**, performance test — there could be many more).
8. After **change management approval**, **Production Support deploys** the tested build to **production**.

### The Waterfall Phases

1. **Requirement gathering** — with all parties (pre-sales, business, customer, stakeholders).
2. **System design**.
3. **Development/Implementation** — developers code the **entire** software all at once, over days/hours.
4. **Testing** — QA runs performance, integration, smoke tests, etc.
5. **Deployment** — Ops deploys to environments including **production** (the app goes **live** and end users start using it).
6. **Maintenance** — ongoing bug fixes and operational support.

### Problems with Waterfall

| Problem | Explanation |
| --- | --- |
| **Time-consuming** | The entire application is delivered at once; any fix takes a long delivery cycle. |
| **Unproductive / rigid** | You can't go backward; teams are heavily dependent on each other (e.g., testing can't start until *all* code is developed; deployment can't start until *all* testing is done). |
| **Costly changes** | Any change must go through the entire life cycle again. |
| **Lack of transparency** | Customer involvement is limited, so problems surface late. |
| **Management bottlenecks** | No scope to pivot or re-prioritize; everyone rigidly follows the fixed process. |

> **Important:** The core flaw of Waterfall is its **rigidity** — a single top-to-down pass with no easy way to revisit earlier steps, causing tight dependencies between siloed teams.

### Results of the Old Approach

Unhappy customers, over-budget projects, burned-out teams, and long delivery times for both features and fixes.

> **Additional Context:** Waterfall is not always "bad" — it can suit projects with **fixed, well-understood, unchanging requirements** (e.g., some regulated or hardware-bound projects). Its weakness shows most in software where requirements evolve frequently. Intermediate improvements like **RAD (Rapid Application Development)** and iterative/spiral models were created to address Waterfall's limitations before Agile became dominant.

---

## 6. Agile

### Definition

**Agile** is a modern, **iterative** development approach built on **continuous feedback at all stages**. Instead of delivering the whole product at once, you deliver it in **small iterations**, improving each cycle by asking *"How can we do better this time?"*

### How It Works

- Follows steps similar to traditional SDLC **but with an improvement mindset** and feedback loops at every stage.
- Work is delivered in **small increments (iterations)** rather than one big release.
- If **requirements change**, new **bugs** appear, or a **high-priority feature** is needed, you handle it in the **next iteration** using the same repeatable process.

### Example

Rather than spending six months building an entire application and then testing it, an Agile team ships a small working slice every couple of weeks (a "sprint"), gets customer feedback, and adjusts priorities for the next slice.

### Benefits (Results)

- **Happy customer** (continuous involvement and feedback).
- **Less time to market**.
- **More cost-effective**.
- **Happy, less burned-out team**.
- **On-time delivery** with the ability to **re-prioritize** changes as needed.

### Important Points

- Core philosophy: **continuous feedback + incremental delivery + adaptability**.
- Agile primarily improves the **development** side of building software.

> **Additional Context:** Agile is a *mindset* defined by the **Agile Manifesto** (2001), which values individuals and interactions, working software, customer collaboration, and responding to change. Popular **frameworks** that implement Agile include **Scrum** (sprints, roles like Product Owner/Scrum Master) and **Kanban** (continuous flow via a board). Note the video's key limitation point: **Agile focuses on development, not operations/production** — which is exactly the gap DevOps fills.

---

## 7. DevOps and CI/CD

### Definition

**DevOps** solves the same delivery problems as the traditional SDLC, but where **Agile was limited to the *development* of the application**, **DevOps extends the improvements to *operations* and *production*** as well. It does this by **bringing teams together** and applying **automation, monitoring, and feedback at every stage** of the life cycle.

### How It Works — The DevOps Life Cycle (the "Infinity Loop")

DevOps is drawn as an **infinity symbol (∞)** to show it is a **continuous, ongoing** process. The stages and how they group into CI/CD:

1. **Plan**
2. **Code**
3. **Build** (package/compile the code)
4. **Test**
   → **Plan → Code → Build → Test** is referred to as **CI — Continuous Integration**.
5. **Release**
6. **Deploy**
   → **Release → Deploy** is referred to as **CD — Continuous Deployment**.
7. **Operate**
8. **Monitor**
   → **Operate → Monitor** is referred to as **Continuous Monitoring**.

The word **"continuous"** is used for each group because the process flows endlessly from one stage to the next — hence the infinity loop.

> **Clarification — CI, Continuous Delivery vs Continuous Deployment:**
> - **CI (Continuous Integration):** Developers frequently merge code into a shared repository; each change is **automatically built and tested**. (Technically CI centers on the automated **build + test** on every commit; "plan" and "code" are the human steps that feed it.)
> - **CD** can mean two different things, and they are often confused:
>   - **Continuous *Delivery*** — every validated change is automatically prepared and can be released to production **with a manual approval/click**.
>   - **Continuous *Deployment*** — every validated change is **automatically released to production with no manual step**.
> The video uses "CD = Continuous Deployment"; in interviews you should be able to explain **both** meanings.

### It's Not Just "Dev" + "Ops"

While **Developers** and **Operations** are central, the DevOps life cycle deliberately involves **many teams working together (breaking silos)**:

- **Security team** → helps with **vulnerability scanning** and **container image scanning** (this collaboration is often called **DevSecOps**).
- **QA / Testing team** → helps create and **automate test cases** as part of **continuous testing**.
- **Business** → provides requirements and other SDLC inputs.

> **Key Takeaway:** DevOps is a **culture + set of practices** that unites **all** teams (Dev, Ops, Security, QA, Business) with **automation and feedback** to reach organizational goals **efficiently and without silos** — not merely a mix of developers and operations.

### Comparison: Traditional SDLC vs Agile vs DevOps

| Feature | Traditional (Waterfall) | Agile | DevOps |
| --- | --- | --- | --- |
| **Delivery style** | Everything at once (linear) | Small iterations | Continuous, automated flow |
| **Feedback** | Late, limited | Continuous, per iteration | Continuous, at every stage |
| **Scope of improvement** | N/A (rigid process) | Mainly **development** | **Development + operations + production** |
| **Team structure** | Siloed, dependent | Cross-functional dev teams | All teams unified (Dev, Ops, Sec, QA, Business) |
| **Automation** | Minimal/manual | Some | Central (CI/CD, testing, monitoring) |
| **Ability to change** | Costly, hard | Easy, re-prioritize per sprint | Continuous and automated |
| **Typical result** | Slow, costly, unhappy customers | Faster, adaptive delivery | Fast, reliable, monitored delivery |

---

## 8. Azure DevOps — Platform Walkthrough

### Definition

**Azure DevOps** is Microsoft's **all-in-one set of integrated tools** that implements the modern DevOps/CI-CD workflow. Instead of stitching together separate tools (repos, artifact stores, boards, pipelines), everything is **integrated in a single platform**.

### Getting Started (Sign-up & Structure)

1. Go to the Azure DevOps start page and click **Start free**, then **sign up**.
2. You're redirected to **`dev.azure.com`**, where a **default organization** and a **test project** are created for you.

**Hierarchy:** `Organization → Project(s) → Services (Boards, Repos, Pipelines, etc.)`

- You can have **multiple organizations**, and **multiple projects inside each organization**.
- **Organizations are logically separated:** resources in one organization **cannot access** resources in another unless **explicit access** is granted.

**Example — organizing by business:** A bank has different lines of business (retail banking, commercial banking, foreign exchange). Each can be a **separate organization** (separate entities under the same parent). Within an organization, you can split **projects** by environment (dev/test/prod), by team, or by application — whatever hierarchy fits.

### Settings

- **Organization settings:** bottom-left corner → **Organization settings**. Applies at the organization level.
- **Project settings:** bottom-left inside a project → **Project settings**. Similar look to org settings but scoped to that **project only**.

### Creating a New Project

Click **New project** and configure:

- **Name** (e.g., "Day One Project").
- **Visibility:**
  - **Public** — accessible by anyone on the internet (like a public GitHub repo).
  - **Private** — restricted access (this is the **default**).
- **Advanced options:**
  - **Version control:** **Git**-based or **TFVC** (Team Foundation Version Control). *(Both explained later in the series.)*
  - **Work item process:** the project-management framework — **Agile, Basic, CMMI, or Scrum**.

Then click **Create**.

> **Definition — Work item process:** A template that defines the types of work items and workflow states your project uses. Options: **Basic** (simplest), **Agile**, **Scrum**, and **CMMI** (most formal/structured).

### The Core Azure DevOps Services

| Service / Tab | What it is | Comparable tool |
| --- | --- | --- |
| **Overview** | Project dashboard: stats, widgets, members. | — |
| **Dashboards** | Configurable **widgets** for a quick project overview. | — |
| **Wiki** | Collaborative documentation you share across the project. | **Confluence** |
| **Boards** | Create/track **work items**, run stand-ups, track progress/blockers. | **Jira** |
| **Repos** | Source code repositories (Git-based by default). Supports **multiple** repos. | GitHub / GitLab |
| **Pipelines** | CI/CD automation. **Build pipeline = CI**; **Release pipeline = CD**. | Jenkins |
| **Test Plans** | Service to plan and perform testing in Azure DevOps. | — |
| **Artifacts** | **Artifact repository** for storing build packages, later consumed by release pipelines to deploy across environments. | **Nexus**, **JFrog Artifactory** |

> **Important:** In Azure Pipelines, there are **two pipeline types**:
> - **Build pipeline → Continuous Integration (CI)** — compiles/tests code.
> - **Release pipeline → Continuous Deployment (CD)** — deploys the built packages to environments.

**How Artifacts fit the flow:** After a build compiles the code, the resulting **packages** are stored in the **Artifacts** repository. The **release pipeline** then pulls those packages to deploy the **same package** across different environments (dev/test/prod), ensuring consistency.

### Key Takeaway on Azure DevOps

> **Key Takeaway:** Azure DevOps is essentially a **single, integrated toolset** that maps the entire traditional development life cycle onto modern, automated processes — so you don't have to manually integrate separate tools for source control, boards, CI/CD, artifacts, and testing.

---

## 9. Azure DevOps — Hosting Options & Pricing

### Two Hosting Solutions

| Option | Description |
| --- | --- |
| **Azure DevOps Services** | The **cloud** (SaaS) offering hosted by Microsoft at `dev.azure.com`. This is what the course uses. |
| **Azure DevOps Server** | The **on-premises** implementation, installed and run in **your own data center**. |

### Pricing (Azure DevOps Services)

*(Figures as stated in the video; verified still current as of 2026.)*

- **Basic plan:**
  - **First 5 users are free.** (So with your default user, you can add 4 more for free.)
  - **$6 per user / month** for each additional user beyond 5.
  - 5 free users are more than enough to complete this course.
- **Basic + Test Plans:**
  - **$52 per user / month**, with a **30-day free trial** (used if you need Test Plans).

**Service-level limits on the free/basic tier:**

- **1 free Microsoft-hosted** CI/CD agent (parallel job).
- **1 free self-hosted** agent (parallel job).
- **2 GB** of Azure Artifacts storage free; **$2 per GB** beyond that.

**Visual Studio subscription perk:** If your organization has a **Visual Studio subscription**, you can access Azure DevOps **for free** with **no limit on the number of organizations**, and those users **don't count against** your 5-user limit.

> **Additional Context (2026 details & clarifications):**
> - The video's figures still hold in 2026: **Basic = first 5 users free, then $6/user/month**; **Basic + Test Plans = $52/user/month** with a 30-day trial.
> - The free **Microsoft-hosted parallel job** includes roughly **1,800 minutes/month** for **private** projects; the free **self-hosted** job has unlimited minutes. Extra Microsoft-hosted parallel jobs cost about **$40/parallel job/month**.
> - There is also a **free unlimited Stakeholder** plan for non-technical users who only need visibility into boards/backlogs (not emphasized in the video).
> - **Cloud pricing changes over time** — always confirm current numbers on Microsoft's official Azure DevOps pricing page before budgeting.

### Comparison: Azure DevOps Services vs Server

| Feature | Azure DevOps **Services** (Cloud) | Azure DevOps **Server** (On-Prem) |
| --- | --- | --- |
| Hosting | Microsoft cloud (`dev.azure.com`) | Your own data center |
| Maintenance/patching | Microsoft manages | You manage |
| Model | SaaS-style, always up to date | Self-hosted, you control updates |
| Best for | Most teams; fast start, no infra | Strict data-residency / compliance needs |
| Used in this course | ✅ Yes | ❌ No |

---

# Quick Revision

### Key Concepts

- **Cloud computing** = renting compute/storage/services over the internet instead of buying hardware; shifts **CapEx → OpEx**.
- Cloud goals: **scalable, available, fault-tolerant, secure, high-performance**.
- **Service models:** IaaS (you manage OS + app), PaaS (provider manages OS; you deploy app), SaaS (provider manages everything; you just use the app).
- **Lift and shift** = move an app to the cloud unchanged; **IaaS** is the ideal target.
- **Shared responsibility model:** responsibility shifts from customer → provider as you go IaaS → PaaS → SaaS; **data, devices, and identities always remain the customer's**.
- **Waterfall** = rigid, linear, no going back → slow, costly, siloed.
- **Agile** = iterative delivery + continuous feedback (improves **development**).
- **DevOps** = Agile extended to **operations & production** via automation, monitoring, feedback, and unified teams.
- **CI/CD:** Plan→Code→Build→Test = **CI**; Release→Deploy = **CD**; Operate→Monitor = **Continuous Monitoring** (drawn as an ∞ loop).
- **Azure DevOps** = integrated toolset: **Boards, Repos, Pipelines, Test Plans, Artifacts** (+ Overview, Dashboards, Wiki).

### Important Definitions

- **CapEx:** Large one-time, upfront capital costs (hardware, office, furniture).
- **OpEx:** Recurring operating costs (maintenance, salaries, rent, electricity).
- **IaaS:** Rent raw infrastructure; you control the OS and admin tasks.
- **PaaS:** Provider supplies runtime/platform; you deploy the app, no OS access.
- **SaaS:** Ready-to-use hosted application; you're just the end user.
- **Patching:** Keeping software/OS updated with the latest security and bug fixes.
- **Lift and Shift:** Migrating an app to the cloud with no application changes.
- **Shared Responsibility Model:** Agreement splitting security/ops duties between customer and provider.
- **CI (Continuous Integration):** Frequent code merges, each auto-built and auto-tested.
- **Continuous Delivery:** Auto-prepared release, deployed with a manual approval.
- **Continuous Deployment:** Auto-release to production with no manual step.
- **Artifact:** A build output/package stored (e.g., in Azure Artifacts) for later deployment.
- **Work item process:** Project-management template — Basic, Agile, Scrum, or CMMI.

### Important Comparisons

**Service models**

| | IaaS | PaaS | SaaS |
| --- | --- | --- | --- |
| You manage OS? | Yes | No | No |
| Admin tasks | You | Provider | Provider |
| Billing | Pay-per-use | Service-based | Subscription |
| Example | Azure VM / EC2 | Azure App Service | Gmail / Office 365 |

**Delivery approaches**

| | Waterfall | Agile | DevOps |
| --- | --- | --- | --- |
| Delivery | All at once | Iterations | Continuous/automated |
| Scope | Rigid | Development | Dev + Ops + Prod |
| Feedback | Late | Per iteration | Every stage |

### Common Mistakes / Misconceptions

- **"The cloud is automatically secure."** No — security is **shared**; your data, identities, and devices are always **your** responsibility.
- **Confusing Continuous *Delivery* with Continuous *Deployment*.** Delivery needs a manual approval to go live; Deployment is fully automatic.
- **Thinking DevOps = just Dev + Ops.** It unites **all** teams (Security, QA, Business too) and is a **culture/practice**, not a single tool.
- **Assuming Agile covers operations.** Agile mainly improves **development**; DevOps extends improvement to **operations and production**.
- **Mixing up IaaS and PaaS OS responsibility.** In **IaaS you manage the OS**; in **PaaS the provider does**.
- **Confusing CapEx and OpEx.** CapEx = one-time upfront; OpEx = recurring.

### Interview / Exam Points

- Explain **CapEx vs OpEx** and how cloud shifts spending.
- Differentiate **IaaS / PaaS / SaaS** with examples and "who manages the OS."
- Describe the **shared responsibility model** and what **always** stays with the customer.
- Explain **why Waterfall fails** for changing requirements and how **Agile** fixes it.
- State the **difference between Agile and DevOps** (dev-only vs dev+ops+prod).
- Map the **CI/CD stages** to the infinity loop and define **CI, Continuous Delivery, Continuous Deployment**.
- Name the **five core Azure DevOps services** and their open-source/third-party equivalents (Boards≈Jira, Wiki≈Confluence, Repos≈GitHub, Pipelines≈Jenkins, Artifacts≈Nexus/Artifactory).
- Difference between **build pipeline (CI)** and **release pipeline (CD)**.
- Difference between **Azure DevOps Services (cloud)** and **Azure DevOps Server (on-prem)**.
- What is **lift and shift**, and why is **IaaS** the best fit?

### Final Takeaways

1. Cloud computing turns expensive, fixed hardware costs (**CapEx**) into flexible, usage-based costs (**OpEx**).
2. **IaaS → PaaS → SaaS** trades **control** for **convenience**; the key differentiator is who manages the **OS**.
3. In the cloud, **you never fully hand off security** — data, identities, and devices always remain yours.
4. **Waterfall's rigidity** (no going back, siloed teams) caused slow, costly delivery.
5. **Agile** brought iterative delivery and continuous feedback, but focused on **development**.
6. **DevOps** extends those gains to **operations and production** through **automation, monitoring, feedback, and unified teams**.
7. **CI/CD** is a continuous (∞) flow: **Plan→Code→Build→Test (CI)**, **Release→Deploy (CD)**, **Operate→Monitor (monitoring)**.
8. Know the CI/CD nuance: **Continuous Delivery** (manual approval) vs **Continuous Deployment** (fully automatic).
9. **Azure DevOps** is an **integrated toolset** (Boards, Repos, Pipelines, Test Plans, Artifacts) organized as **Organization → Project → Services**.
10. It's **essentially free** for small teams (**5 users free**, then $6/user/month), and comes in **cloud (Services)** and **on-prem (Server)** flavors.
