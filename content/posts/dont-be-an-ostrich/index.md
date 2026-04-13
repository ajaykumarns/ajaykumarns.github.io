---
title: "Don't Be an Ostrich"
subtitle: "Why AI-assisted development is not an option"
tags: [AI, Android, Development, Productivity, LLM]
categories: [blog, tech]
date: 2026-04-13T12:00:00+08:00
lastmod: 2026-04-13T12:00:00+08:00
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

## The Conversation That Started It All

Walking back to the office today, I was reminded of a conversation with a Google teammate over 10 years ago. We were discussing Ruby's guiding principle — making programming languages easier for humans.

Yukihiro Matsumoto, the creator of Ruby, put it best: *"Often people, especially computer engineers, focus on the machines... But in fact we need to focus on humans, on how humans care about doing programming or operating the application of the machines. We are the masters. They are the slaves."*

He advocated for a shift *"from a machine-centered paradigm to a human-centered one."* And in 1993, he noted: *"I felt scripting to be the way future programming should be — human-oriented."*

XML isn't something a human should have to edit.

## The Makefile Era

When I started working on the Android platform at Google, there was no Android Studio. Everything was a simple makefile-style repository — you couldn't even import it into IntelliJ. For someone coming from a Java world used to IntelliJ, this was painful.

Even if I manually added project sources to the IDE, everything would show up as errors because none of the libraries would be available in the classpath. Most folks ended up using Vim, Emacs, or their own personal editor, running commands manually with make, figuring out how to run a particular test.

During my time on the Android Pixel team building the Setup Wizard, I remember commenting how absurd it was that humans were expected to manually edit XML files to fix Android layer bugs.

## Before Robolectric

This was also before Robolectric existed. If you've worked on the Android source code before Robolectric, you know exactly how painful it was to test applications.

Imagine having to:
1. Manually edit an XML layer file
2. Run the make command to rebuild the entire app
3. Push it into the emulator or install it on the phone
4. Wait for it to load
5. Go through your feature again

No visual editors. No hot reload. This was the state of the art back then.

## More Human-Centric Development

Looking back now, that primitive system was just a stepping stone. Every painful make command, every manual XML edit, every long rebuild cycle — it all led us here.

We finally have development that's truly human-centric. We no longer have to do these stupid things. We can just tell the AI what we want, and it will build it for us.

The future of development isn't about memorizing build systems or wrestling with XML files. It's about describing what you want and letting the machine handle the rest.

What great times to be alive.

---

## Don't Stick Your Head in the Sand

I am still surprised to see people who refuse to even try out the new development methodology using LLMs. I guess these people have never gone through pain developing applications in their lives. It almost feels like sticking your head in the sand, refusing to at least try out the new way of development.

If budget is a factor, try out free tools such as OpenCode. Give it a genuine shot. You might be surprised by what you're capable of building when the machines actually work for you.

## References

- **Yukihiro Matsumoto (Matz), Ruby Creator — Human-Centric Philosophy**
   - *"We are the masters. They are the slaves."* — [Ruby Lang Archives](https://ruby-lang.org)
   - *"From a machine-centered paradigm to a human-centered one"* — Pearson/Artima Interview
   - *"I felt scripting to be the way future programming should be — human-oriented"* (1993) — [Structured Programming and Object Oriented Programming](https://ptgmedia.pearsoncmg.com/images/9780321714633/samplepages/9780321714633.pdf)

- **Android Development Tools**
   - Android Studio — [https://developer.android.com/studio](https://developer.android.com/studio)
   - Robolectric (unit testing for Android) — [https://robolectric.org/](https://robolectric.org/)
   - IntelliJ IDEA — [https://www.jetbrains.com/idea/](https://www.jetbrains.com/idea/)

- **AI Development Tools**
   - OpenCode — [https://opencode.ai](https://opencode.ai)
   - LLM Agents in Software Development

- **Programming Language**
   - Ruby — [https://www.ruby-lang.org/en/](https://www.ruby-lang.org/en/)
