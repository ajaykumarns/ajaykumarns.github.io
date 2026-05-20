---
title: "AI slop? What about human slop?"
subtitle: "Sloppy code was never just an AI problem"
tags: [AI, LLM, Development, Software Engineering, Code Quality]
categories: [blog, tech]
date: 2026-05-20T14:05:00+05:30
lastmod: 2026-05-21T00:39:54+05:30
draft: true
type: standard-view
weight: 1

featured: true
sidebar: true
toc: true
math:
  enable: false
lightgallery: false

hiddenFromHomePage: false
hiddenFromSearch: false

author: Ajay Nadathur
description: "AI slop is real, but sloppy code has always had a human version: rushed, under-reviewed, inconsistent, and protected by excuses."

resources:
  - name: featured-image
    src: featured.png
---

## The AI slop panic

You cannot talk to developers these days without the conversation somehow becoming about AI. Talk to any curious engineer and the conversation almost always takes the same turn: "AI slop", how AI is still bad at writing code, how our jobs are perfectly safe because reading AI-generated code during a production outage will be a nightmare, and so on.

To be fair, the complaint is not imaginary. AI can produce nonsense with excellent indentation. But the panic feels overblown when it pretends that sloppy code was invented sometime after ChatGPT got a login page.

Developers read Hacker News, Twitter, newsletters, conference hot takes, and every other imaginable channel, then repeat the same points like a distributed tape recorder. Every time this topic comes up, I want to shout:

> **What about human slop?**

Was every human developer writing perfect code before LLMs entered the chat? How many of us can honestly say:

> Across all the projects I have seen, I have never encountered bad code, horrible code, sloppy code, or a giant pile of tech debt wearing a trench coat.

My honest answer would be: all the time.

To be clear, I am not saying sloppy code is acceptable. Projects that tolerate growing slop will eventually slow down, fail, or blow up at the worst possible time. **The problem is not that AI invented slop. The problem is that many teams have no reliable way to stop slop from landing.**

Anyway, are you asking how we fix this problem? Excellent question. We will get there. But first, story time.

To explain why I am allergic to "AI invented bad code" discourse, let me briefly ruin Steve Yegge's classic title.

## Get that job at an Indian MNC

_A humble remix of Steve Yegge's classic [_Get that job at Google_](https://steve-yegge.blogspot.com/2008/03/get-that-job-at-google.html), for the clueless._

If you are one of those truly fortunate souls who has never worked on a sloppy project, I have a tip for you: try joining an Indian MNC. You will be blessed with firsthand experience.

By the way, MNC stands for multinational company. Western companies outsource IT work to these firms for cheaper labor, then sometimes act shocked when the discount software arrives with discount maintainability. Many of these places do not really reward excellence or innovation. Employees get no stock options, no RSUs, and very little bonus, if any.

Among the perks:

1. Sit in an air-conditioned room all day staring at a monitor.
2. Enjoy unlimited "tea" breaks.
3. Take the free company bus.
4. Sit in traffic for two hours each way.
5. Experience enough office politics to question every choice you made in this life as well as the previous ones.

The ultimate reward for "talented individuals" is the famous "onsite opportunity". You ship some important features, pay your dues, kiss the appropriate ring, then go abroad and perform liaison work for the client. From onsite, you "manage" junior team members, complain about how untalented the freshers are, and wonder why nobody can debug the excellent piece of code you wrote in 2009. What a pain in the arse.

One of the early proud moments of my parents' lives was when I got a job offer during a campus recruitment event held by one of these companies, often treated as a national treasure of India. After the first few months of "training", I ended up working for a European client whose software we had to learn and modify.

Needless to say, the code was of excellent quality. Thousands of lines inside single functions and methods. The only reliable way to debug a feature was to scatter `alert('file.xyz line no=1234')` everywhere, guess what might work, and hope JavaScript was in a forgiving mood. If that failed, you waited until the "expert" became available from onsite and asked them to rescue you.

There were no real standards or guidelines within the project. If the fix worked, you committed the changes.

> No unit tests? No integration tests? Perfectly fine, just check it in and move on with your blessed life.

The code eventually got so bad that an architect from the client side demanded static checkers, unit tests, code coverage, and anything else that could be thrown at the problem without requiring a complete rewrite. Some of these tools include [Simian](https://simian.quandarypeak.com/), [PMD](https://pmd.github.io/), and many others. The client had to babysit us constantly, asking for these reports with every release.

The hope was that things would improve every cycle. But hey, we had deadlines. And "more important stuff" to work on. Still, once the reports existed, the client could at least track the quality of the product and demand improvements.

**This immediately clicked for me: quality stopped being a vague moral preference and became something that could be measured.**

## When quality becomes infrastructure

Before joining Google, I had never read or heard about google3 or how the development lifecycle worked there. But when you see how things are done at Google and other large engineering organizations, you realize how much effort goes into software development, quality improvement, and long-term maintenance.

For starters:

1. Code cannot be checked in without approvals, including review from the owners of the project.
2. Formatting and style rules are enforced consistently across the company.
3. A bunch of checks need to pass before your change can even show up properly for review. Basically, your change has to survive checks before a reviewer wastes time on it.
4. There are controls around which library dependencies you can import or use. This feels even more sensible now, considering recent supply-chain attacks like [Shai-Hulud 2.0](https://www.microsoft.com/en-us/security/blog/2025/12/09/shai-hulud-2-0-guidance-for-detecting-investigating-and-defending-against-the-supply-chain-attack/) against package ecosystems.
5. Unit testing and code coverage requirements are taken seriously.

And much, much more.

The contrast could not be more obvious.

> In one environment, quality depended on whoever happened to care enough that day.

In the other, **quality was built into the path to submit code.**

## Is Code Review enough?

Looking at those two environments, you might conclude that the answer is strict code review. Code review matters, of course. A thoughtful reviewer can catch design mistakes, unclear abstractions, missing tests, security issues, and the occasional:

> Why is this variable named `temp2_final_really_final`?

Code review alone is not enough. Humans get tired. Large diffs blur together. If the standard lives only in the reviewer's head, it will be applied inconsistently.

This is where guardrails matter. **Guardrails make quality harder to accidentally ignore.** They do not replace engineering judgment, but they reduce the number of things humans have to remember manually every single time.

## What are guardrails?

Guardrails are the checks around the repo: formatters, linters, tests, ownership rules, dependency checks, CI gates, and whatever else stops obviously bad changes from entering the codebase.

**The exact tools matter less than the principle: decide what "acceptable" means, then enforce it.**

A coding standard in a wiki or a checklist to do a "pull request" is more of a suggestion than an actual enforcement. **A check that blocks the merge is an actual standard that would prevent slop growth.**

## What does this have to do with AI slop? 

If the repository accepts a sloppy change, the process failed. The author being human or AI is secondary.

**The cure for both is not nostalgia; it is standards, guardrails, and enforcement.** Without those, slop will grow whether it's written by humans or AI.

I will go deeper into practical guardrails in a follow-up post. Until then, may your CI be stricter than your optimism.
