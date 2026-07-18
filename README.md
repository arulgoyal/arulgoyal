<!-- ══════════════════════════════════════════════════════════════ -->
<!--        arul-goyal.service  ·  a live production status page       -->
<!-- ══════════════════════════════════════════════════════════════ -->

<div align="center">

![banner](https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=200&section=header&text=Arul%20Goyal&fontSize=54&fontColor=ffffff&animation=fadeIn&fontAlignY=38&desc=%E2%97%8F%20arul-goyal.service%20%C2%B7%20All%20Systems%20Operational&descAlignY=58&descSize=16)

[![telemetry](https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=20&pause=1200&color=2EA043&center=true&vCenter=true&width=830&lines=%E2%97%8F+all+systems+operational;reconciliation+%CE%94+holds+at+0.00+%C2%B7+books+tie+out;dead-letter+queue+draining+%C2%B7+retries+idempotent;the+retry+that+fires+at+3am+%E2%80%94+that+is+the+job)](https://github.com/arulgoyal)

<!-- status / contact strip -->
<img src="https://img.shields.io/badge/status-operational-2ea043?style=for-the-badge&labelColor=161b22" alt="status"/>
<img src="https://img.shields.io/badge/on--call-payments%20%2F%20reconciliation-7AA2F7?style=for-the-badge&labelColor=161b22" alt="on-call"/>
<img src="https://img.shields.io/badge/region-Bengaluru,%20IN-BB9AF7?style=for-the-badge&labelColor=161b22" alt="region"/>
<img src="https://komarev.com/ghpvc/?username=arulgoyal&label=uptime%20checks&color=2ea043&style=for-the-badge" alt="uptime checks"/>
<br/>
<a href="mailto:arulgoyal6@gmail.com"><img src="https://img.shields.io/badge/email-arulgoyal6@gmail.com-EA4335?style=for-the-badge&logo=gmail&logoColor=white&labelColor=161b22" alt="email"/></a>
<!-- TODO: replace with your real LinkedIn slug -->
<a href="https://linkedin.com/in/arul-goyal"><img src="https://img.shields.io/badge/LinkedIn-connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white&labelColor=161b22" alt="linkedin"/></a>

</div>

<!-- ══════════════════════════════════════════════════════════════ -->

## `GET /whoami`

I'm a backend engineer who likes the *unglamorous* parts of software — the retry that fires at
3 a.m., the reconciliation job that catches the one rupee that didn't match, and the queue that
never drops a message. I build money movement that doesn't need babysitting.

```http
GET /api/engineers/arul HTTP/1.1
Host: rupeek.com
Accept: application/json

HTTP/1.1 200 OK
X-Powered-By: caffeine, idempotency-keys

{
  "role":        "SDE · Payments & Reconciliation @ Rupeek",
  "focus":       ["reliability", "money movement", "removing manual ops"],
  "stack":       ["NestJS", "TypeScript", "PostgreSQL", "Redis", "BullMQ"],
  "also_speaks": ["Java / Spring Boot", "React / Next.js", "Python"],
  "building":    "Cashroom — a student-lending backend, in the open",
  "philosophy":  "the retry that fires at 3am matters more than the happy path",
  "status":      "operational"
}
```

<!-- ══════════════════════════════════════════════════════════════ -->

## `● service health`

> Systems I operate. All green — that's the whole point.

| service | status | SLO | notes |
| :--- | :--- | :--- | :--- |
| `reconciliation-engine` | 🟢 operational | source of truth: **Razorpay** | books tie out, Δ = 0.00 |
| `dlq-retry` | 🟢 operational | **0** manual re-pushes | auto-recovers failed & stuck transfers |
| `payout-retry` | 🟢 operational | **0** ops intervention | modeled on the transfers flow |
| `sqs-consumers` | 🟢 hardened | no dup / dropped msgs | fixed 3 reliability bugs |
| `lender-integrations` | 🟢 operational | SIB · Federal · Axis · **DCB** | onboarded DCB, the 4th partner |

<!-- ══════════════════════════════════════════════════════════════ -->

## `📈 telemetry`

<div align="center">

<img height="165" src="https://arulgoyal-readme-stats.vercel.app/api?username=arulgoyal&show_icons=true&theme=tokyonight&hide_border=true&include_all_commits=true&count_private=true&title_color=7AA2F7&icon_color=BB9AF7&bg_color=1A1B27" alt="stats"/>
<img height="165" src="https://streak-stats.demolab.com/?user=arulgoyal&theme=tokyonight&hide_border=true&background=1A1B27&ring=7AA2F7&fire=BB9AF7&currStreakLabel=7AA2F7" alt="streak"/>

<img height="150" src="https://arulgoyal-readme-stats.vercel.app/api/top-langs/?username=arulgoyal&layout=compact&theme=tokyonight&hide_border=true&title_color=7AA2F7&bg_color=1A1B27&langs_count=8" alt="top langs"/>

</div>

<!-- ══════════════════════════════════════════════════════════════ -->

## `📒 general journal` — impact, double-entry

> Every line item balances: toil removed on the debit side, a system shipped on the credit side.

| # | debit — *toil removed* | credit — *system shipped* | ✓ |
| :--- | :--- | :--- | :---: |
| J1 | BizOps re-pushing failed transfers, **daily** | DLQ retry that auto-recovers | ✅ |
| J2 | manual disbursal recovery | automated payout retry | ✅ |
| J3 | ~10 hrs/week of manual work | a WhatsApp automation | ✅ |
| J4 | ticket creation taking ~5 min | dashboard for **4,000+** leads → instant | ✅ |
| J5 | duplicate & dropped messages | SQS consumer hardening (3 fixes) | ✅ |

**Trial balance:** `debits (toil) === credits (shipped)` → **Δ = 0.00** · `reconciled: true` ✅

<details>
<summary><b>🔧 &nbsp;incident postmortems — resolved &nbsp;(click to expand)</b></summary>
<br/>

**`INC-001` · daily manual re-push · SEV-2 → resolved**
- **Impact:** BizOps identified and re-pushed failed transfers by hand, every single day.
- **Root cause:** no automated recovery path for failed or stuck transfers.
- **Fix:** reconciliation with Razorpay as the source of truth + a dead-letter-queue retry that auto-recovers. Daily manual effort → **0**. Also squashed 3 recurring gateway edge cases (duplicate capture, order-already-paid, fee-bearer config).

**`INC-002` · duplicate & dropped messages · SEV-2 → resolved**
- **Impact:** SQS consumers double-processing and silently dropping messages.
- **Root cause:** visibility-timeout expiry, async/await mixed with callbacks, and unintended restarts.
- **Fix:** all three hardened — consumers now process exactly what they should, once.

**`INC-003` · onboard 4th lender · planned change → shipped**
- **Scope:** brought **DCB** online across disbursal, settlement & fee flows — alongside SIB, Federal, and Axis — for multiple gold-loan types, plus 3 lifecycle ops (repledge, part-release, delinking) keeping balances, collateral & ledger consistent.

</details>

<details>
<summary><b>🏷️ &nbsp;changelog — my career as semver</b></summary>
<br/>

- **`v3.0.0`** — SDE · Payments & Reconciliation @ **Rupeek** *(Jul 2025 → now)* — own payments features end-to-end; gold-loan lifecycle ops; reconciliation + DLQ retry.
- **`v2.0.0`** — SDE Intern · Personal Loans, Backend **(0 → 1)** @ Rupeek *(Jan 2025)* — built the PL backend from scratch; **15+** features shipped; DigiTap PAN verification in a 10-day turnaround.
- **`v1.0.0`** — B.Tech, Computer Science · **VIT** · CGPA **8.67** *(2021 → 2025)* — E-Cell Design Lead, ran 5+ events.
- **`v0.1.0`** — `git init` · first commit.

</details>

<!-- ══════════════════════════════════════════════════════════════ -->

## `🧱 runtime dependencies`

<div align="center">

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![NestJS](https://img.shields.io/badge/NestJS-E0234E?style=for-the-badge&logo=nestjs&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)
![BullMQ](https://img.shields.io/badge/BullMQ-EF4444?style=for-the-badge&logo=redis&logoColor=white)
![Amazon SQS](https://img.shields.io/badge/AWS%20SQS-FF4F8B?style=for-the-badge&logo=amazonsqs&logoColor=white)
![TypeORM](https://img.shields.io/badge/TypeORM-FE0803?style=for-the-badge&logo=typeorm&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)
![Tailwind](https://img.shields.io/badge/Tailwind-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)

</div>

<!-- ══════════════════════════════════════════════════════════════ -->

## `🚧 currently deploying`

> ### 🪙 [Cashroom](https://github.com/arulgoyal/cashroom) — *Student Lending Platform*
> A production-grade lending backend, built from scratch and in the open.
>
> **Queue-driven workflows** (BullMQ) · **TypeORM + PostgreSQL** · **Redis** caching · **Docker** — core
> lending flows (application, eligibility, disbursal, repayment scheduling) as modular NestJS services
> with DTO-validated REST APIs.
>
> ![NestJS](https://img.shields.io/badge/NestJS-E0234E?style=flat-square&logo=nestjs&logoColor=white)
> ![BullMQ](https://img.shields.io/badge/BullMQ-EF4444?style=flat-square&logo=redis&logoColor=white)
> ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
> ![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
> ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)

<!-- ══════════════════════════════════════════════════════════════ -->

## `📊 throughput`

<div align="center">

[![activity](https://github-readme-activity-graph.vercel.app/graph?username=arulgoyal&theme=tokyo-night&hide_border=true&bg_color=1A1B27&color=7AA2F7&line=BB9AF7&point=FFFFFF&area=true)](https://github.com/arulgoyal)

<!-- queue drain 🐍 -->
![snake](https://raw.githubusercontent.com/arulgoyal/arulgoyal/output/snake.svg)

</div>

<details>
<summary><b>🌙 &nbsp;off-hours services (degraded, by design)</b></summary>
<br/>

| service | status |
| :--- | :--- |
| `sleep-scheduler` | 🟡 degraded during release windows |
| `weekend-mode` | 🟢 operational |
| `coffee-supply` | 🔴 critical dependency |

</details>

<!-- ══════════════════════════════════════════════════════════════ -->

<div align="center">

```console
$ arul --status
● all systems operational
$ echo $?
0
```

![quote](https://quotes-github-readme.vercel.app/api?type=horizontal&theme=tokyonight)

*Thanks for checking the status page — let's ship something reliable.* ⚡

![footer](https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=120&section=footer)

</div>
