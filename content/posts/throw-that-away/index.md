---
title: "Throw That Shit Away"
subtitle: "Why AI-assisted development is not an option"
tags: [AI, Android, Development, Productivity, LLM]
categories: [blog, tech]
date: 2026-04-25T12:00:00+08:00
lastmod: 2026-04-25T12:00:00+08:00
draft: false
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
description: "A reflection on how far we've come in development — and why AI agents are the natural conclusion of decades of painful progress."

resources:
  - name: featured-image
    src: featured.jpg
---

## The Spark

Recently, I was listening to Boris Cherny on [Lenny's Podcast](https://www.youtube.com/watch?v=We7BZVKbCVw) — the head of [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview) at [Anthropic](https://www.anthropic.com/). Among many things discussed, one statement caught my attention: he talked about how cheap it's become to throw away code without any emotional attachment.

That took me aback.

I initially struggled with the idea of being so nonchalant about things built with hard work by humans. How can you throw things away without a second thought? Take my hard disk — it's still littered with thousands of files from pet projects I never completed. A graveyard of ambitions, as they say. Even with recent advances in code generation using [Codex](https://openai.com/index/introducing-codex/) or [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview), I still can't bring myself to delete these files or archive those hobby projects from my [GitHub](https://github.com/) repo.

*'They're precious! Nobody can have them! I will not delete it!'*

Yes, Gollum.

But jokes aside, it took me a while to process Boris's statement. I wanted to understand why this fact of life is becoming increasingly true.

---

## The Reluctance to Let Go

I've worked at several companies across different locations — the Bay Area, Bangalore, and most recently Singapore — each with its own work culture. In almost all these workplaces, you end up meeting challenging personalities who have strong opinions on what you built and how they conduct code reviews.

It used to happen all the time: I'd create a change and send it out for review. Then the review would take weeks. If I followed up, the answer was always, "Go find something else to work on. I'll get back to it soon." But you never knew when!

Feedback was sporadic. Sometimes painfully slow — two weeks of silence. Sometimes fast — within 30 minutes. But sometimes the feedback was just... bad.

> "You shouldn't have done it this way. Rewrite it in a completely different approach."

Some of these reviews had no justification — no links, no pointers, no reading material explaining why one approach is better than another. It was more personal taste than reasoned argument.

Fortunately, this wasn't the case at Google. I loved that every review needed a pointer back to agreed-upon standards. Why should a class be marked `final`? There would always be a link to [*Effective Java*](https://www.amazon.com/Effective-Java-Joshua-Bloch/dp/0134685997/) explaining why. At Google, we also had clear agreements on how long a change request could wait for reviews. In many other companies, this was left to the whims of leadership and individual engineers.

There were times when I felt frustrated with bad reviews — I'd put so much effort into a change, tested it end-to-end, and seen it work. Then all of it had to be thrown away. Every line of code typed, every logical discussion you had with yourself about the approach — your own blood and sweat transmuted into living, breathing code! (lol)

There were so many emotions behind it, and frankly, zero learnings.

I'm sure I'm not the only person who felt this way, nor the first to go through similar situations. Looking back now, it's crazy to think I agonized over this — even though I was getting paid. There's no deduction from my pay just because a change didn't land on master. There's no deduction just because it didn't get pushed to production.

But the fact remained: my work amounted to nothing. That's what was frustrating.

---

## The Shift: Code Is Cheap

Now with coding tools like Codex or Claude Code, I no longer code every line myself. Instead, I have a discussion with the coding agent, ask it to do a deep dive, and collect the basic facts. Once that is there, I ask it to implement a particular feature — but I never allow it to run amok. I always want to see the plan, the approach it is planning to take. Then, based on my own personal taste as well as minor adjustments here and there, I ask the agent to code.

This changes the entire relationship you have with code. Instead of each line being a product of your own fingers and your own reasoning, it's now a collaborative output — one that can be iterated on, revised, or discarded without the same emotional weight.

That brings us back to Boris's point: if code is cheap to generate, it's cheap to throw away. And that's actually liberating.

---

## But There's a Catch

Some folks find this way of working quite intense. You have to be constantly engaged — tracking what the agent is doing, going through the diffs, agreeing or disagreeing with every decision. It's like micromanaging a junior employee.

In fact, I've been asked this question: *With coding agents, aren't humans spending more time multitasking?*

Here's the deal. You have a thing to do. You ask the agent to do it, and the agent takes its own time to implement the changes. You have two options:

1. Sit there, share it on the screen, and watch a streaming line of updates from the agent about what it is doing.
2. Open a new tab and ask the agent to work on something else.

Once you have the second agent going, you have another choice:

1. Open a third tab and ask the agent to do something else, or
2. Go back to the first tab and review the changes the first agent made?

The more tabs you have open, the more multitasking you'll end up doing. Honestly, this is quite stressful. We, as humans — at least me — cannot stretch ourselves across so many different topics and executions all at once. It is mentally draining.

This is an approach I would **not** recommend to anybody.

## A Better Way

So how do we solve this problem? We have coding agents that can do a pretty good job of making changes with a little bit of guidance — but we don't want to stress ourselves into forced multitasking. Here's what I ended up doing.

I came across a cookbook that Codex shared — a guide on how to ask Codex to come up with a plan and then execute it completely. You can find it [here](https://developers.openai.com/cookbook/articles/codex_exec_plans). I suggest you make a copy of this plan and put it inside your `.agents` folder in your project. When you prompt the agent to work on something or a longer feature, what you ask is: *"Make an executable plan and then review it carefully."*

This is where most of your attention goes. Once the plan is ready, you go through it carefully, make minor adjustments here and there, and then kick it off by saying *"Execute it till the end."* Then you focus on something else — open a new tab, or do some other work. You don't revisit the tab until later.

Make this a practice — kick-start a bunch of executable plans at once. Block a good enough chunk of your time so that you can focus without getting distracted by agents humming away in the background. When you've exhausted the current chunk of work, go back and check which agent has completed.

For the agents that have finished, go into their workspace, play with the changes, and see if there are any problems. If you notice something, prompt the agent again with a list of changes, ask it to plan it again, and then execute it. That's it. Don't revisit the same tab until later. This way, you create concrete time windows where you can focus without trying to juggle too many things at once.

And if you don't like the work the agent did? You can always choose to throw it away — because the original request wasn't good enough, or the approach was wrong. This is what I think Boris means by prototyping multiple versions, playing with them, and then deciding which one to finally pick up.

## The Mixed Feelings

Overall, I feel very productive using coding agents — multitasking and implementing so many features all at once. But at the same time, there's a lingering fear: perhaps my coding skills will eventually fade away. Or if there's some sort of outage in Codex or Claude Code, I really don't have the energy or the patience to manually code anything ever again.

It's a brand new world. But at the same time, I am afraid of the dependence this new world is enforcing on these really smart tools. What do you think? Do you feel the same? Please feel free to share your thoughts.

---

## Throw That Shit Away

So here's the thing I've been circling back to.

For most of my career, throwing away code felt like I was *losing* something. Every function I wrote, every clever abstraction — I treated them like possessions. My hard disk is full of abandoned pet projects. My GitHub is a graveyard of half-formed ideas. Every single one of them, I was convinced, was going to be the one.

Now ask yourself: did I ever get paid less because a change didn't make it to production? Did anyone send me an invoice for all those hours spent debugging something that got scrapped?

No. And yet it *felt* like I was losing money every time.

Boris Cherny's point finally made this click for me: throwing code away isn't failure. It's the system working. You try something, you look at it, and if it doesn't meet the bar — you throw it away and try again. No Gollum clutching his precious. No "but I spent two weeks on this."

"Throw That Shit Away" is an operating philosophy. It means: stop treating every prototype like it's sacred. Stop defending code that doesn't deserve to live. Stop shipping things that are "good enough" instead of things that are actually good.

Because the beautiful thing about where we are now? The code that gets to production is the code that *deserves* to be there. Everything else? It was always meant to be temporary — a prototype that taught you what not to do!

Happy coding!

---

## References

- [Boris Cherny on Lenny's Podcast – Building Claude Code](https://www.youtube.com/watch?v=We7BZVKbCVw)
- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code/overview)
- [OpenAI Codex](https://openai.com/index/introducing-codex/)
- [Effective Java by Joshua Bloch](https://www.amazon.com/Effective-Java-Joshua-Bloch/dp/0134685997/)
