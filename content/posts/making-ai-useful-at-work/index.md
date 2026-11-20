---
title: "Making AI Useful at Work"
subtitle: "What our first developer bootcamp taught me about building a shared foundation for AI-assisted development"
date: 2026-11-20T12:00:00+05:30
lastmod: 2026-11-20T12:00:00+05:30
draft: false
type: standard-view
url: /making-ai-useful-at-work/
featured: true
sidebar: true
toc: true
math:
  enable: false
lightgallery: false
hiddenFromHomePage: false
hiddenFromSearch: false
author: Ajay Nadathur
description: "Why we ran an AI bootcamp at Dkatalis, how it gave engineers a shared foundation, and what custom MCP tools and Temporal taught us about useful, reliable AI."
tags:
  - AI
  - Software Engineering
  - Developer Productivity
  - Engineering Leadership
  - MCP
  - Temporal
categories:
  - blog
  - tech
resources:
  - name: featured-image
    src: featured.webp
---

Sundar Pichai once described AI as ["something more profound than electricity or fire"](https://www.weforum.org/stories/all/google-ceo-ai-will-be-bigger-than-electricity-or-fire/), and I struggled with that comparison for a long time. The internal AI course material I saw at Google mostly covered linear regression and predictive models, which I found useful, but hardly profound. My interest only really developed when I started exploring large language models, or LLMs, in early 2024.

As someone who occasionally fancies himself a theoretical physicist and enjoys reading about black holes and subatomic particles, I kept asking myself: what could be more profound than electricity itself? I would picture a turbine driving a generator, with current flowing through wires into our devices and back through the circuit, and find the comparison difficult to accept. It began to make more sense when I thought about the scale of AI's impact on how every one of us works, something that has become especially visible in software development over the past year or so.

## Why we ran a bootcamp

With that scale of change, I understand why people worry about AI taking their jobs. I think the more useful response is to help people learn how to use it effectively and become better at their work, which takes time, practice, and support from leadership. Simply giving engineers access to a tool and hoping they figure out the rest leaves too much to chance.

The noise around AI makes this harder. Open YouTube or X and there is another model release, an impressive demo, or someone explaining why every engineer should use a particular tool. It is easy to come away feeling anxious about what you might be missing, even though a one-off demo tells us little about how the same approach fits into an existing team's daily work. There is a considerable difference between building a new app for a demonstration and making a useful change inside a repository with existing behaviour, team standards, and checks that the change must pass.

Companies and their leadership have a responsibility to evaluate those claims and identify what helps their teams, while giving engineers the time and support to try these methods properly. When everyone has to work out an approach independently, teams can end up repeating the same experiments and using different standards for what good work looks like. That makes it harder to share what works and improve productivity across the company.

That was the intent behind our first AI bootcamp for developers at Dkatalis. We focused on an engineering team's daily needs and built the course from first principles, covering one building block at a time and following it with working sessions where people could experiment, ask questions, and build.

## A shared foundation to build on

One of the most useful things the bootcamp helped us do was establish a common language and standardise the basics of working with agents. Engineers could start from a shared understanding of how to provide context, set boundaries, define completion, and verify the result. Those practices give teams something they can improve together as the tools change.

This also leaves room for engineers to choose the models and harnesses that fit their needs. A harness is the software that manages an agent's execution, context, and tools. We explored options including [OpenCode](https://opencode.ai/docs/) and [pi](https://pi.dev/) because I wanted people to understand how the pieces work together and feel comfortable trying different approaches. Much of the attention goes to [Claude Code](https://code.claude.com/docs/en/overview), but understanding the underlying components makes it easier to evaluate other tools on their own merits.

The model and harness are parts of a development toolchain that also needs useful repository context, access to the right systems, and checks around the work. [Repository instructions](https://agents.md/), [reusable skills](https://agentskills.io/home), and [guardrails](/guardrails-against-ai-slop/) help make team expectations explicit. Once engineers share that foundation, they have a better starting point for their own experiments, and useful results become easier for another team to understand and reuse.

## The week in brief

- **Day 1:** AI fundamentals, harnesses such as OpenCode and pi, repository instructions, reusable skills, and guardrails.
- **Day 2:** Using [MCP](https://modelcontextprotocol.io/docs/getting-started/intro) to connect agents to tools and data, taking a [Jira](https://www.atlassian.com/software/jira) ticket to a tested [draft merge request in GitLab](https://docs.gitlab.com/user/project/merge_requests/drafts/).
- **Day 3:** Splitting suitable tasks across agents, keeping changes separate, and independently checking the combined result.
- **Day 4:** Local and cloud agents, including building custom MCP servers and connecting them to Wayang.
- **Day 5:** Reliable execution with the [Temporal](https://temporal.io/) team, including preserving workflow progress, retrying failed calls, and resuming after interruptions.

## The custom MCP work impressed me

MCP, the Model Context Protocol, connects agents to tools and data. We used Jira and GitLab workflows to make this concrete, so participants could work through the steps from understanding a ticket to implementing and testing a change. I believe custom MCP servers built around company workflows deserve far more attention, because they can connect agents to the systems and processes our teams already use.

On day four, we explored the difference between working with an agent in a developer's local environment and delegating work to a remote workspace. Wayang, our internal cloud-agent platform, gave us a way to explore remote work, including reviews and investigations supported by evidence.

What really impressed me was seeing participants build custom MCP servers and connect them to the cloud agent. Their ideas and demos blew me away. Once people understood the building blocks and had the tools to connect them, they could start applying their own knowledge of the company to what they built. For me, that showed how the right training and tools can give people room to apply their creativity and improve productivity within the company.

This is also why the shared foundation matters. A useful tool or workflow developed by one engineer becomes much more valuable when other teams can understand it, check it, and build on it.

## Reliable execution with Temporal

On day five, the Temporal team connected our work with agents to the engineering needed around longer-running tasks. Through order-management examples, we explored how workflows manage state, preserve progress, retry failed calls, and resume after interruptions. The session covered reliable applications as well as agent workflows, giving the week a useful connection to familiar software-engineering concerns.

As agents take on more work, a model call or tool request becomes one step in a larger process that can still fail halfway through. Understanding what has already happened and how to continue safely matters just as much as deciding what the agent should do next. That made [durable execution](https://docs.temporal.io/durable-execution), where the system preserves workflow progress across interruptions, a fitting topic for the final day.

Temporal's [open-source durable execution platform](https://github.com/temporalio) is used by companies including Netflix, Stripe, and Coinbase, and it was useful to connect those reliability ideas with the workflows we had been exploring during the week.

## Taking it back to the teams

The company's [bootcamp recap on LinkedIn](https://www.linkedin.com/posts/dkatalis_dkatalis-ai-bootcamp-2026-activity-7525392202441805824-YBzi) has a few moments from the week.

The work continues as people take these methods back to their teams, where they will need opportunities to practise and support when things do not go as expected. The aim is for those lessons to become shared instructions, reusable skills, and workflows that other teams can use and improve. That continued investment matters as much as giving people access to the tools in the first place.

If you're helping teams adopt AI, what has helped your engineers turn experiments into regular practice, and how are you supporting them once the training ends?
