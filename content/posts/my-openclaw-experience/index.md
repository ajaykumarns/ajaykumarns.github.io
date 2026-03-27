---
title: "My OpenClaw Experience"
subtitle: "Building an AI assistant that actually works"
tags: [OpenClaw, AI, Self-hosting, Productivity, Telegram, Tailscale]
categories: [blog, tech]
date: 2026-03-25T09:47:00+08:00
lastmod: 2026-03-25T09:47:00+08:00
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
description: "My curiosity got the best of me, and I gave into the temptation of setting up OpenClaw"

resources:
  - name: featured-image
    src: feature.png
---

## What's OpenClaw?

In the unlikely scenario that you've been living under a rock, OpenClaw is a self-hosted AI agent framework with integrations for email, chat, and more. It promises to be your best personal assistant.

## Installing and Configuring OpenClaw

Let me be honest: it's not newbie friendly. The install command looks simple, but trust me, that's misleading. After installation, you need to configure tokens and settings to get the agent running. Needless to say, I'm not writing a tutorial for it.

The overall experience needs to be smoother for democratization. No wonder companies are jumping on the hype train with "one click" installations—just Google it. However, you're better off trying it locally via Docker or using a VPS to limit potential damage.

## My Current Setup

Here's my current stack:

- **VPS Server** – Pick your poison.
- **OpenClaw** – Installed via npm script.
- **Telegram** – Fantastic and works out of the box.
- **OpenRouter** – My LLM provider. Easy to onboard and start using, no issues so far.
- **LLM Model** – `MiniMax-2.7`. Decent overall, though sometimes you have to correct the agent.
- **Tailscale** – How did I not know about this until recently? Thank you to this tweet:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">When I set up a new Hetzner VPS first thing I do install Tailscale and once I'm in via Tailscale lock down the firewall to only accept web traffic on HTTPS 443 for Cloudflare IPs and SSH 22 for Tailscale IP<br><br>That way nobody can get in<br><br>I know I keep repeating this but it should… <a href="https://t.co/v1LU34l5Bv">https://t.co/v1LU34l5Bv</a></p>&mdash; @levelsio (@levelsio) <a href="https://twitter.com/levelsio/status/2033546675063554213?ref_src=twsrc%5Etfw">March 16, 2026</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

### Model Experiments

I tried several models:

- **Claude** – Super expensive. Burns through money like nothing. Hard pass.
- **Gemini Flash** – Runs quickly and cheaper than Claude, but reasoning can be problematic. It broke my OpenClaw instance a couple of times by corrupting `~/.openclaw/config.json`.
- **MiniMax** – My default model. Pricing is economical and it works most of the time. I've noticed it's lazier than other models and tends to take shortcuts when there's too much work. For regular chats though, it works very well.
- **Kimi** – No success with this one, even though it scores high on leaderboards. 🤷

## Tips

Here are a few things I learned the hard way.

First up: turn on verbose mode (`/verbose`) for the first few days. You can catch the agent early if it's doing something unexpected or burning tokens unnecessarily. The bot has full system access—it can edit its own configuration and restart services. It still feels unreal that it can modify itself. Unfortunately, it's not foolproof; you can brick the installation quite easily.

When it comes to personas, experiment and see what sticks. I started with a genderless bot, then made it female with a nice Indian name. I had it generate a self-portrait for its Telegram profile pic! One feature request for Telegram: I wish bots could update their own profile pics and descriptions—it would make them feel more lively. As for WhatsApp setup, I skipped it since it requires a separate phone number.

If you code, install `opencode` or `claude` and ask OpenClaw to invoke these CLI tools. It works surprisingly well. But be careful with Google account access—I haven't and won't trust an agent without hard guardrails. I'm considering setting up a shadow account for email forwarding, giving the agent full access only to that.

A few other things: use Tailscale to set up an alias for your VPS and enable Tailscale SSH. It's safe and super easy to log in. Lock down your Telegram settings—make sure your bot isn't open to random strangers messaging it. And don't upgrade OpenClaw impulsively. It's still rough around the edges. I did and paid dearly with hours of debugging. See [here](https://github.com/openclaw/openclaw/issues/53099) and this:

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">I missed a release step last night with the web control UI assets, current release doesn't load that correctly, you can update to beta where it's fixed, or wait for the updated release later.<br><br>Just working on automating the whole release pipeline, and adding e2e tests for web.</p>&mdash; Peter Steinberger 🦞 (@steipete) <a href="https://twitter.com/steipete/status/2036218803001114779?ref_src=twsrc%5Etfw">March 23, 2026</a></blockquote> <script async="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

## References

- [OpenClaw](https://openclaw.ai) | [GitHub](https://github.com/openclaw/openclaw)
- [OpenRouter](https://openrouter.ai)
- [Tailscale](https://tailscale.com)
- LLM Models: MiniMax, [Claude](https://www.anthropic.com) by Anthropic, Gemini Flash by Google, [Kimi](https://www.moonshot.cn) by Moonshot
- [OpenClaw Issue #53099](https://github.com/openclaw/openclaw/issues/53099)

## Summary

I'm still playing with my personal assistant, mostly via Telegram, and learning every day. Not sure where this will go or what it will evolve into. But one thing's for sure: the world will never be the same.
