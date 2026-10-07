---
title: 'Founding and Engineering UniMate'
date: 2025-03-31
permalink: /posts/2025/03/founding-and-engineering-unimate/
tags:
  - software engineering
  - data engineering
  - design patterns
  - system architecture
---

I was a co-founder and sole engineer for UniMate in the second year of my degree. It was an event aggregation and data processing system that integrated distributed proxies for web scraping, GPT-based multi-label classification, modular I/O architecture, CLI interaction, dynamic HTML parsing, and a failure-tolerant data pipeline with partial restart. It ran on a no-code frontend. This was my first real-world system, and it taught me about design, trading off speed and quality, and minimal engineering for scalability.

Here, I want to share what I learned. I'll break down the technical side and explore the tension we faced between business and technology needs.

This document should be useful for founding engineers, students of systems architecture, and businesspeople struggling to understand the nerds.

*Note: Source code available in the appendix.*

---

## Table of Contents

1. [Introduction](#introduction)
2. [Table of Contents](#table-of-contents)
3. [The Business](#the-business)
4. [System Design & Architecture](#system-design--architecture)
   1. [Key Features](#key-features)
   2. [Design Patterns](#design-patterns)
5. [Implementation Process](#implementation-process)
   1. [The Role of Infatica](#the-role-of-infatica)
   2. [Processing, Enrichment & Output](#processing-enrichment--output)
   3. [Business-Engineering Interplay](#businessengineering-interplay)
      1. [Business constraints shaped engineering](#business-constraints-shaped-engineering)
      2. [Engineering shaped business](#engineering-shaped-business)
6. [Growth, Monetisation, and Shutdown](#growth-monetisation-and-shutdown)
7. [Lessons](#lessons)
   1. [Technical](#technical)
   2. [Startup](#startup)
8. [Conclusion](#conclusion)
9. [Appendix: Source Code](#appendix-source-code)

---

## The Business

At UNSW in 2023, student groups published events across many platforms. UniMate aggregated, structured, and presented event data in one user-friendly interface. Our product made event discovery easy and thereby improved student engagement with their campus community.

Before UniMate, we spent months exploring ideas. The aggregator idea stood out because we understood the problem firsthand. We'd both experienced social disengagement at university, and a big part of that was the sheer difficulty in discovering events. Solving this felt genuinely impactful for 60,000+ students at UNSW. Our market research backed up both the problem and our proposed solution. The idea was also scalable to other universities in Sydney - all facing the same problem - and so presenting good options for growth.

We spent three months validating the idea and then building the MVP. I picked and learned the tech stack. Then we launched our public alpha, during which we built, researched, tested, and iterated constantly. I was still learning new design lessons and improving the backend, working towards a pipeline robust enough for future growth. Our product was live for two months, serving over 1500 users. Then a university-backed competitor came onto the market. This presented a few challenges - chiefly that the university owned the intellectual property we were publishing. We decided we'd learned enough and wound the business down.

---

## System Design & Architecture

The backend implemented a linear pipeline pattern:

1. Ingest raw HTML;
2. Extract structured event data;
3. Semantically enrich it (through summarisation and tagging); and
4. Serialise for storage and output.

### Key Features

- **Pipeline architecture:** Cleanly separated stages: scraping → processing → output, each with its own Python module.
- **CLI interface:** Allowed manual overrides, human-in-the-loop for some failure states, and partial restart of the pipeline on cached data.
- **Retry logic:** Exponential backoff capped at 5 retries improved reliability against flaky sources.
- **Infatica integration:** Proxies routed requests through mobile/residential IPs, avoiding rate limits and bot detection.
- **Regex- and index-based substring parsing:** Made scraper resilient to dynamic DOMs.
- **HTML dump logging:** Enabled quicker, reproducible debugging with saved response bodies and error states.
- **GPT-based classification:** Multi-label classification via binary GPT prompts to create new event metadata for better querying.
- **Versioned output and backups:** Supported safe concurrent runs and partial recomputation.

### Design Patterns

Several design patterns emerged while I was building and refining the system:

- **Pipeline Pattern:** Data passed through modular stages with segregated interfaces and serialisation between stages.
- **CLI Controller:** The CLI orchestrated the system like a controller in the model-view-controller pattern, selecting subroutines at runtime.
- **Strategy Pattern:** Event taggers were encapsulated as independent binary classifier strategies.
- **Factory Pattern (Lightweight):** IO and utility modules abstracted path/filename construction and output writing to ensure consistency across modules.
- **Observer-Like Logging:** Though not a full observer system, the system uses a log- and dump-driven architecture to allow decoupled debugging after execution terminates.

---

## Implementation Process

We discovered early that no student clubs published APIs. I began scraping, using Pandas to handle data and BeautifulSoup to parse static HTML. Dynamic sites presented a challenge: JavaScript rendering created inconsistent document object models (DOMs) which broke our parser. I considered Selenium, but analysis of scrape dumps showed that the structure we needed was somewhat consistent across page renders. I wrote custom parsing functions instead. This avoided learning and integrating another tool and kept our stack lean. It only broke once - an afternoon fix.

### The Role of Infatica

Blocking was a real concern. We considered the legal and ethical implications of scraping and operated well within those boundaries. Nonetheless, scraping from home IPs was unreliable. At some point, our program would trigger cybersecurity protections and encounter scraper-breaking captchas.

Traditional datacenter proxies were unusable - most were blacklisted as bots. I researched and found Infatica: a distributed proxy service with access to millions of residential and mobile IPs. Their network routed requests through legitimate user devices across the globe. Infatica solved:

- IP-based rate limits;
- Bot detection systems; and
- Session-based blocking.

Our scraper appeared indistinguishable from normal users. With session persistence and geographic rotation, we scraped without faults.

### Processing, Enrichment & Output

The pipeline cleaned, enriched, and serialised data. It:

- Deduplicated events across platforms;
- Normalised date/time formats;
- Applied GPT-based tagging and summarisation; and
- Exported the data in plaintext, CSV, and binary formats.

I introduced automation only when manual work became a bottleneck. This delayed complexity while building scalability in at a natural rate. The versioned filesystem supported reproducibility, speeding up fixes. As the system matured, my workload shifted from maintenance to feature delivery, which I took as a sign of healthy design.

### Business-Engineering Interplay

#### Business constraints shaped engineering

- **No web backend:** We used manual CSV uploads to our website to validate demand, instead of a web backend;
- **Proxy choice:** Cost and reliability constraints made Infatica the only feasible choice; and
- **No mobile app:** We delayed the mobile app to prioritise the pipeline and start work on the web backend.

#### Engineering shaped business

- **Lack of a web backend:**
  - We had to do time-consuming manual uploads, taking time away from other business activities and product development;
  - We couldn't ingest human submissions automatically, limiting the breadth of events we could host on our site;
- **Limited engineering team:**
  - I had no real-world experience, let alone on customer-facing products or robust data systems, which slowed our product development;
  - A bad experience with an early addition to the team made us hesitant to bring on new people, though we were recruiting developers again shortly before the university competitor came onto the market;
- **No-code frontend:** Neither of us in the founding team had web experience, so I used a no-code website builder (Wix) for our MVP site. This limited our product flexibility, but saved time in engineering.

This interplay taught me to justify engineering decisions in business terms, and vice versa.

---

## Growth, Monetisation, and Shutdown

We grew organically via Facebook groups and posters we put up around campus. We quickly validated our product-market fit, serving 30-50 daily users after our product launch despite an underdeveloped user interface and limited features.

Our monetisation plan was to sell affiliate marketing to bars, nightclubs, and other student-focused businesses, and later to sell a "premium" service with extra features.

Unfortunately, the university soon released a competitor, backed by official club support and with similar features. Recognising our overwhelming disadvantage, and interested in pursuing other ambitions, we shut down and moved on - satisfied and grateful for what we had learned.

---

## Lessons

### Technical

- Full automation is essential for scale;
- To build systems, think in systems;
- Logs and backups are worth it for reproducible debugging alone; and
- Modularity pays off over time.

### Startup

- Premature optimisation kills business momentum;
- Fast product validation is everything. We spent too long researching pre-MVP; and
- External competition can render strategy irrelevant overnight.

---

## Conclusion

UniMate was my first exposure to real-world software engineering under real-world constraints. I engineered a working system which collected, processed, and delivered useful data to over a thousand students. I learned to design minimal systems, structure for growth, and deliver incrementally under constantly changing business needs. Most importantly, I learned what kind of engineer I wanted to become - one who builds scalable, robust systems, and makes every decision with deliberation and care. Though UniMate shut down, its lessons have stayed with me as I have moved on to more advanced projects.

---

## Appendix: Source Code

You can view the full source code of the UniMate backend on GitHub [here](https://github.com/one-2/unimate-mvp).

This MVP is not elegant or perfect, but it served 1500+ users for our business.

Highlights include:

- `scraper/Scripts.py` - Dynamic HTML parsing and modular data extraction;
- `scraper/InfaticaRequests.py` - Resilient request logic using distributed proxies;
- `processor/Tagger.py` - GPT-based multi-label classification pipeline; and
- `io/Filesystem.py` - Versioned filesystem structure for reproducibility and scalability.

---