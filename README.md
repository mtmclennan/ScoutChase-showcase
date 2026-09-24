# ScoutChase

**AI-assisted prospecting and outreach for sales teams, job seekers, and recruiters.**

Scout researches and ranks opportunities. **You decide who moves forward.** Chase helps turn approved opportunities into personalized outreach and follow-up.

[Website](https://scoutchase.com) · **Status:** Working prototype · **Source:** Private application repo

![ScoutChase dashboard](images/screens/dashboard.png)

---

## What is ScoutChase?

ScoutChase is a working full-stack product prototype built around two AI-assisted agents and one deliberate human approval boundary.

Most prospecting tools tend toward one of two extremes:

- give the user a huge list and leave them to research it manually, or
- automate outreach at volume and risk turning prospecting into spam.

ScoutChase takes a different approach.

The user defines a **playbook** describing what they sell or what they are looking for, who is a good fit, what signals matter, and how outreach should be handled.

**Scout** uses that context to discover, research, and rank opportunities.  
**You** decide which opportunities are worth pursuing.  
**Chase** helps draft outreach, manage follow-up, and move approved prospects toward a real conversation.

```text
PLAYBOOK
   ↓
SCOUT
Discover · Research · Rank
   ↓
MATCHES + REASONS
   ↓
HUMAN APPROVAL
   ↓
CHASE
Draft · Follow up · Assist
   ↓
CONVERSATION
   ↓
QUALIFIED / HANDOFF
```

![Scout finds. You approve. Chase follows up.](images/diagrams/workflow.png)

---

## The core idea

**Use software to do more of the repetitive research and drafting without handing over the decisions that affect reputation, relationships, or trust.**

### Scout

Scout is the discovery and research side of the product. It interprets the playbook, searches available sources, evaluates fit, ranks opportunities, and explains why each match deserves attention.

### You

The user controls the approval boundary. A prospect does not move from Scout to Chase simply because an algorithm gave it a high score.

### Chase

Chase is the outreach and follow-up side. It prepares personalized drafts, supports review, helps organize conversations, suggests replies, and keeps the next action visible.

![AI does the research and drafting. You make the calls.](images/diagrams/ai-and-you.png)

---

## From a brief to a ranked list

### 1. Build the playbook

Onboarding captures the context Scout and Chase need: the offer or objective, target audience, geography, useful signals, positioning, objections, outreach rules, and communication boundaries.

Scout uses the playbook to evaluate opportunities. Chase uses the same context when preparing outreach.

![ScoutChase onboarding](images/screens/onboarding.png)

![ScoutChase playbook](images/screens/playbook.png)

### 2. Send Scout out

The user describes what Scout should look for in plain language and can narrow the search using filters such as geography, company size, keywords, and result count.

![Scout search](images/screens/scout-search.png)

### 3. Review ranked results

Scout returns a prioritized set of opportunities rather than an undifferentiated database dump.

Each result includes the reasoning behind the match so the user can see **why** it was surfaced instead of trusting a mystery score.

![Scout ranked results](images/screens/scout-results.png)

Opening a company shows the evidence behind the match, relevant signals, associated contacts, and the outreach direction Chase can use.

![Company detail](images/screens/company-detail.png)

---

## Scout → approval → Chase

Approval is part of the product architecture, not an afterthought.

Selected opportunities are handed from Scout to Chase in an explicit step. The user can review what is being moved forward before outreach work begins.

![Scout to Chase handoff](images/screens/handoff.png)

Chase creates a review queue where drafts can be inspected, edited, rewritten, approved, or skipped.

![Chase review queue](images/screens/chase-review-queue.png)

Approved prospects can then move through the working pipeline as outreach progresses.

![Prospect pipeline](images/screens/prospects.png)

The dashboard keeps Scout and Chase visible as separate responsibilities: **Scout finds and evaluates opportunities; Chase works the approved ones.**

![ScoutChase dashboard](images/screens/dashboard.png)

---

## One workflow, three use cases

ScoutChase is built around a reusable workflow. What changes is the playbook, the source data, and who the user ultimately wants to reach.

| Use case | Scout looks for | Chase supports |
|---|---|---|
| **Sales prospecting** | Companies that match the ideal customer profile and show useful signals | Personalized outreach to relevant decision-makers |
| **Job search** | Open roles and companies that match the user's skills, goals, and constraints | Outreach to hiring teams and relevant contacts |
| **Recruiting** | Hiring companies, searches, and candidate-related opportunities | Personalized recruiting outreach and follow-up |

![One workflow, three playbooks](images/diagrams/use-cases.png)

---

## How AI and external services fit

ScoutChase does not treat an LLM as the entire product. The AI layer sits inside a broader workflow that also handles research, enrichment, persistence, approvals, and background execution.

### OpenAI API

Used for AI-assisted interpretation, reasoning, ranking, explanation, personalization, and draft generation within the Scout and Chase workflows.

### Firecrawl

Used for web research and extraction so Scout can work with information from company websites and other public web sources instead of relying only on static records.

### Prospeo

Used for contact enrichment, helping connect approved companies with relevant people and available contact data.

### Trigger.dev

Used for background and long-running workflow execution so research, enrichment, and agent tasks do not have to depend on a single browser request remaining open.

The human approval layer sits between research and outreach.

```text
PLAYBOOK
   ↓
SCOUT
   ├── Firecrawl → web research / extraction
   ├── OpenAI API → interpretation / ranking / reasoning
   └── Prospeo → contact enrichment
   ↓
RANKED OPPORTUNITIES
   ↓
HUMAN APPROVAL
   ↓
CHASE
   └── OpenAI API → outreach / reply assistance
   ↓
FOLLOW-UP WORKFLOWS
   └── Trigger.dev → background execution
   ↓
POSTGRESQL
```

---

## Product architecture

ScoutChase is a **working prototype with a real application layer, authentication, persistent data, external providers, background workflows, AI-assisted reasoning, and automated testing**.

| Layer | Technology |
|---|---|
| Application | Next.js · React · TypeScript |
| Styling | Tailwind CSS |
| Authentication | Clerk |
| Database | PostgreSQL |
| ORM | Prisma |
| AI / reasoning | OpenAI API |
| Background workflows | Trigger.dev |
| Web research / extraction | Firecrawl |
| Contact enrichment | Prospeo |
| Testing | Vitest · Playwright |
| Deployment | Docker configuration |

![Product architecture](images/diagrams/architecture.png)

### Current application capabilities

- Client Prospecting and Job Search playbooks
- plain-language Scout searches
- company and opportunity discovery workflows
- ATS and structured job-source adapters
- structured matching, filtering, and ranking logic
- evidence and fit explanations
- company and contact workflows
- Firecrawl-backed web research
- Prospeo contact enrichment
- OpenAI-assisted analysis and draft generation
- explicit Scout → Chase handoff
- Chase review queue
- suggested-reply and qualification workflows
- prospect pipeline progression
- background workflow support with Trigger.dev
- authenticated, persistent application data
- automated unit and end-to-end testing

---

## Job-source discovery

The Job Search workflow is designed to do more than keyword-match a generic jobs feed.

The prototype includes adapters for structured job sources and ATS platforms, including:

- Greenhouse
- Lever
- Ashby
- structured / JSON-LD job data

Matching logic can evaluate factors such as role family, seniority, work arrangement, geography, and compensation before an opportunity is surfaced.

The longer-term direction is broader **company-first discovery**: finding organizations worth approaching even when the right role has not been publicly advertised yet.

---

## What works today

ScoutChase is not only a UI concept. The current prototype demonstrates the core product loop:

1. define a playbook
2. run a Scout search
3. research and evaluate opportunities
4. receive ranked results with reasons
5. inspect companies, evidence, and contacts
6. approve selected opportunities
7. hand them to Chase
8. review personalized outreach drafts
9. track prospects through the workflow

The application also has a real backend, authentication, PostgreSQL persistence, external provider integrations, background workflow support, and automated tests.

The screenshots in this repository use fictional demo data so the product can be shown without exposing real prospect or customer information.

---

## What comes next

The next development work is focused on making the existing workflow more useful and production-ready rather than simply adding more screens.

- broader company-first discovery
- stronger decision-maker discovery and enrichment
- deeper research and provider integrations
- expanded Chase conversation workflows
- production outreach infrastructure
- stronger multi-tenant controls
- observability, rate limiting, and operational hardening
- billing and account administration

---

## Why I built ScoutChase

I built ScoutChase because sales prospecting and job searching share the same underlying problem: **too much information, too little context, and too much repetitive manual work.**

The interesting problem is not generating another list.

It is determining:

- which opportunities are actually worth pursuing
- why they fit
- which signals support that conclusion
- who the relevant person is
- what the next action should be

ScoutChase is my attempt to use AI and automation for the repetitive research, filtering, enrichment, organization, and drafting while keeping the human responsible for judgment and communication.

It also gave me a practical project for exploring full-stack product development, agent-style workflows, third-party APIs, asynchronous jobs, data modeling, authentication, testing, and human-in-the-loop product design in one system.

---

## Project status

**ScoutChase is an actively developed working prototype and portfolio case study.**

The current build demonstrates the core Scout → approval → Chase workflow with real application logic and provider integrations. It is not being presented as a finished production SaaS product.

This public repository contains the case study and screenshots. The application source code, configuration, credentials, and private implementation details remain in a private repository.

---

**ScoutChase** · [scoutchase.com](https://scoutchase.com)

