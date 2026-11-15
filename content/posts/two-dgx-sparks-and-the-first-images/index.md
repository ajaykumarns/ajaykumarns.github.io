---
title: "I can haz private intelligence?"
subtitle: "Me gets them runnings, then aks them to draws my work in pictures"
date: 2026-10-25T18:00:00+05:30
lastmod: 2026-11-15T12:00:00+05:30
draft: false
type: standard-view
featured: true
sidebar: true
toc: true
math:
  enable: false
lightgallery: false
hiddenFromHomePage: false
hiddenFromSearch: false
author: Ajay Nadathur
description: "I finally got two NVIDIA DGX Sparks. A short account of the initial setup and the image experiments that turned my work into two illustrated galleries."
tags:
  - DGX Spark
  - Local AI
  - Image Generation
  - ComfyUI
categories:
  - blog
  - tech
resources:
  - name: featured-image
    src: featured-private-intelligence.webp
---

## The good old days

Who remembers the good old days when [I can has cheeseburger](https://en.wikipedia.org/wiki/I_Can_Has_Cheezburger%3F) was all rage? I spent so many of my waking hours going through all the funny memes the internet had to offer. The world has changed so much since then — now you can generate your own images of cats, cities, and whatever one can imagine, just by describing it to a machine. And we are spoiled for choice: head to [openrouter.ai](https://openrouter.ai) or any other service provider, try new models pay-per-usage, and pick from plenty of image and video tools on tap, including [gpt-image](https://openai.com/index/introducing-4o-image-generation/), [Google Nano Banana](https://developers.googleblog.com/introducing-gemini-2-5-flash-image) and much, much more.

## The dark side of public inference

However, the main problem with all of these services is that any data you send to them is no longer private, in spite of whatever assurances they give. Take what happened at Cloudflare recently: [**a bug in the KV cache on their Workers AI stack leaked data across user sessions**](https://blog.cloudflare.com/kv-cache-exposure-remediation) — 155 responses containing pieces of other customers' sessions, over a couple of weeks in late August and early September, and no sophisticated hacker involved, just an engineering mistake! Imagine uploading your financial statements to a hosted model and a stranger's session getting served your private financial details.

Or take the [Cursor incident](https://cursor.com/blog/security-incident-update) from October 2026 — an attacker got into a bucket of coding agent traces through an access key leaked by its inference vendor, stole credentials from it, and from there pushed a trojanized Claude Code extension into Cursor's VS Code marketplace for about 11 hours, reaching at most 5,000 users. Prompts, support data, and customer details were all in the mix.

And it isn't just the hosted services either — it's also what AI-generated apps ship with. [Crissy Field analyzed 159,041 Lovable projects](https://www.crissyfield.de/research/lovable-en/) and found 24,664 sending database records to the browser with no login required; 30% of those they inspected had tables full of email addresses. Some exposed passport numbers and payment details, others 200,000 chat messages. The pitch is "describe the app, we'll build it" — the fine print is that somebody still has to check who can read the database afterwards. How much control do you really have once your data is inside someone else's pipeline?

Not much, if any — which is exactly why I've always hesitated to upload any sort of private information such as credit card bills or personal images, even for something harmless like a trend. Like ChatGPT's viral [Ghibli effect](https://www.reuters.com/technology/artificial-intelligence/ghibli-effect-chatgpt-usage-hits-record-after-rollout-viral-feature-2025-04-01/) — everyone was doing it, and I sat it out. The ['80s photo trend](https://economictimes.indiatimes.com/news/new-updates/piyush-goyal-joins-viral-chatgpt-80s-photo-trend-with-a-retro-ai-generated-picture-vibing-to-the-80s-trend/articleshow/133973486.cms?from=mdr) that was fashionable in India until recently, same story. I'm not pasting credit card bills or personal photos into a stranger's server just to get a cute avatar out of it. So for a while I just... waited for the version of this that didn't demand so much.

## The machine I was waiting for

What I was waiting for was a machine that I owned 100% myself, one that could let me use some of this "artificial" intelligence without having to give up my privacy or my family's data. Fortunately, NVIDIA launched the [DGX Spark](https://www.nvidia.com/en-us/products/workstations/dgx-spark/) — a compact computer for local AI, with 128 GB of unified memory per box, shared between the processor and the graphics processor.

If you are curious about these devices, check out these videos:

<style>
.dgx-videos{display:flex;gap:1rem;align-items:flex-start;background:#f7f7f7;border:1px solid rgba(0,0,0,.1);border-radius:14px;padding:1rem;margin:1.75rem auto}
.dgx-video{flex:1;min-width:0}
.dgx-video p{margin:.6rem 0 0;font-size:.85rem;color:#666;text-align:center}
.dgx-video iframe{border-radius:10px;overflow:hidden}
@media (max-width:640px){.dgx-videos{flex-direction:column}}
</style>
<div class="dgx-videos">
<div class="dgx-video">
{{< youtube 82SyOtc9flA >}}
<p>DGX intro</p>
</div>
<div class="dgx-video">
{{< youtube 0LaUiu-xTVc >}}
<p>Connecting two DGX devices</p>
</div>
</div>


And for the longest time, I've been watching DGX Spark videos non-stop but never quite pulled the trigger on the purchase. Finally, on a pleasant day when I felt brave and adventurous, I gave in and ordered 2 of these beauties via naddod.com's [listing](https://www.naddod.com/products/103030.html) (I was lucky enough to snag these just a week or two before the prices went up).

<style>
.dgx-carousel{position:relative;max-width:340px;margin:2rem auto 2.25rem;border:1px solid rgba(0,0,0,.1);border-radius:14px;overflow:hidden;background:#111}
.dgx-track{display:flex;transition:transform .35s ease}
.dgx-slide{min-width:100%;margin:0}
.dgx-slide a{display:block;line-height:0}
.dgx-slide-img{display:block;width:100%;height:auto;cursor:zoom-in}
.dgx-nav{position:absolute;top:50%;transform:translateY(-50%);width:38px;height:38px;border:0;border-radius:50%;background:rgba(0,0,0,.55);color:#fff;display:flex;align-items:center;justify-content:center;cursor:pointer;z-index:10}
.dgx-nav:hover{background:rgba(0,0,0,.8)}
.dgx-nav svg{width:18px;height:18px;fill:none;stroke:#fff;stroke-width:2.4;stroke-linecap:round;stroke-linejoin:round}
.dgx-prev{left:10px}.dgx-next{right:10px}
.dgx-dots{position:absolute;bottom:12px;left:0;right:0;display:flex;gap:8px;justify-content:center;z-index:10}
.dgx-dot{width:9px;height:9px;border-radius:50%;border:0;background:#fff;opacity:.45;cursor:pointer;padding:0}
.dgx-dot.active{opacity:.95;transform:scale(1.25)}
.dgx-carousel-caption{text-align:center;font-size:.85rem;color:#666;margin-top:-.5rem;margin-bottom:1.5rem}
@media (min-width: 760px){
  .dgx-carousel{max-width:700px}
  .dgx-track{transform:none !important}
  .dgx-slide{min-width:50%}
  .dgx-slide + .dgx-slide{border-left:3px solid #111}
  .dgx-slide-img{cursor:zoom-in}
  .dgx-nav,.dgx-dots{display:none}
}
.dgx-figures{display:grid;grid-template-columns:1fr;gap:1rem;margin:1.5rem auto}
@media (min-width:720px){.dgx-figures{grid-template-columns:repeat(2,1fr)}}
.dgx-figure{margin:0;text-align:center}
.dgx-figure a{display:block;line-height:0;border:1px solid rgba(0,0,0,.08);border-radius:14px;overflow:hidden;max-width:340px;margin:0 auto}
.dgx-figure img{display:block;width:100%;height:auto;cursor:zoom-in;transition:transform .2s ease}
.dgx-figure a:hover img{transform:scale(1.02)}
.dgx-figure figcaption{margin-top:.6rem;font-size:.9rem;line-height:1.55;color:#444}
.dgx-figure-wide{margin:2rem auto;text-align:center}
.dgx-figure-wide a{max-width:none}
</style>
<link rel="stylesheet" href="/lib/glightbox/css/glightbox.min.css">

<div class="dgx-carousel" id="dgx-unboxing" role="region" aria-label="Photos of the DGX Spark delivery">
  <div class="dgx-track">
    <figure class="dgx-slide">
      <a class="glightbox" href="/dgx-spark/unboxing/DGX_Spark_box.jpg" data-gallery="dgx-unboxing" data-title="Sealed box, as it arrived">
        <img class="dgx-slide-img" src="/dgx-spark/unboxing/DGX_Spark_box.jpg" alt="The sealed DGX Spark box on my desk" width="960" height="1280" loading="lazy">
      </a>
    </figure>
    <figure class="dgx-slide">
      <a class="glightbox" href="/dgx-spark/unboxing/IMG_1017.jpg" data-gallery="dgx-unboxing" data-title="Two DGX Sparks, fresh out of the box">
        <img class="dgx-slide-img" src="/dgx-spark/unboxing/IMG_1017.jpg" alt="Open box revealing two DGX Spark units" width="960" height="1280" loading="lazy">
      </a>
    </figure>
  </div>
  <button class="dgx-nav dgx-prev" type="button" aria-label="Previous photo"><svg viewBox="0 0 24 24" aria-hidden="true"><polyline points="15 18 9 12 15 6"></polyline></svg></button>
  <button class="dgx-nav dgx-next" type="button" aria-label="Next photo"><svg viewBox="0 0 24 24" aria-hidden="true"><polyline points="9 18 15 12 9 6"></polyline></svg></button>
  <div class="dgx-dots">
    <button class="dgx-dot active" type="button" aria-label="Photo 1"></button>
    <button class="dgx-dot" type="button" aria-label="Photo 2"></button>
  </div>
</div>
<div class="dgx-carousel-caption"><em>Clicked a few photos after delivery</em></div>

It is a great device and fits the bill in every way that matters to me:

1. **Private by default.** Credit card bills, personal photos, anything with my name on it — it all stays on the machine. No logs on someone else's server, no terms-of-service roulette, no "your data may be used to improve our models."
2. **Multimodal, not just text.** The same hardware that holds a big language model also runs image generation entirely locally — which is how this whole post started — and it keeps getting better across audio, video, and whatever ships next.
3. **Always on, always mine.** No usage caps, no rate limits, no "model retired, please migrate."

<figure class="dgx-figure dgx-figure-wide">
  <a class="glightbox" href="/dgx-spark/gollum-dgx-spark.jpg" data-gallery="gollum" data-title="My precious"><img src="/dgx-spark/gollum-dgx-spark.jpg" alt="Gollum cradling a DGX Spark and calling it his precious" loading="lazy" decoding="async" width="1024" height="1024"></a>
</figure>

<script src="/lib/glightbox/js/glightbox.min.js"></script>
<script>
(function () {
  var root = document.getElementById('dgx-unboxing');
  var track = root.querySelector('.dgx-track');
  var dots = Array.prototype.slice.call(root.querySelectorAll('.dgx-dot'));
  var count = track.children.length;
  var index = 0;
  function go(n) {
    index = ((n % count) + count) % count;
    track.style.transform = 'translateX(-' + index * 100 + '%)';
    dots.forEach(function (dot, i) { dot.classList.toggle('active', i === index); });
  }
  root.querySelector('.dgx-prev').addEventListener('click', function () { go(index - 1); });
  root.querySelector('.dgx-next').addEventListener('click', function () { go(index + 1); });
  dots.forEach(function (dot, i) { dot.addEventListener('click', function () { go(i); }); });
  root.addEventListener('keydown', function (event) {
    if (event.key === 'ArrowLeft') { go(index - 1); }
    if (event.key === 'ArrowRight') { go(index + 1); }
  });
  if (window.GLightbox) {
    var initLightbox = function () {
      GLightbox({ selector: '.glightbox', loop: true, touchNavigation: true, keyboardNavigation: true });
    };
    if (document.readyState === 'loading') {
      document.addEventListener('DOMContentLoaded', initLightbox);
    } else {
      initLightbox();
    }
  }
})();
</script>


## The joy of owning intelligence

After setting these up and making sure the devices were working, the first thing I wanted to try out was image generation. With the help of Codex, I downloaded and installed the following image generation models: Qwen-Image-2.1-Turbo, FLUX.2 Klein 4B, and Z-Image-Turbo. I ran a bunch of tests, and when the images finally came out, it blew my mind. Quite thrilling to own intelligence running on your own private device and have fun with it.

Being a heavy Codex user for the past couple of months, I wanted to visualize Codex's impression of my working style so far.

### Enter ComfyUI

Codex first wrote up a rough outline of its impression of my work. Then, with the help of ComfyUI, it generated the images from that outline. The first result was *Ajay in images*: a cover and twelve scenes. It opens with this:

> You build systems, test what they do, protect work that is live, and still make room for wonder.

A generous description. I'll take it.

<div class="dgx-figures">
<figure class="dgx-figure">
  <a class="glightbox" href="/dgx-spark/portrait-of-ajay/01-systems-gardener.png" data-gallery="portrait-of-ajay" data-title="The Systems Gardener · Qwen"><img src="/dgx-spark/portrait-of-ajay/01-systems-gardener.png" alt="A maker tends an illuminated garden of small connected systems" loading="lazy" decoding="async" width="1024" height="1024"></a>
  <figcaption><strong>The Systems Gardener</strong> · Qwen<br>You build tools and care for them after they start to run.</figcaption>
</figure>
<figure class="dgx-figure">
  <a class="glightbox" href="/dgx-spark/portrait-of-ajay/09-precise-repair.png" data-gallery="portrait-of-ajay" data-title="The Precise Repair · FLUX"><img src="/dgx-spark/portrait-of-ajay/09-precise-repair.png" alt="A gloved hand repairs one small part of a working machine" loading="lazy" decoding="async" width="1024" height="1024"></a>
  <figcaption><strong>The Precise Repair</strong> · FLUX<br>You fix the part that failed and keep the rest safe.</figcaption>
</figure>
</div>

These two capture things I care about: maintaining what you build, and fixing a failure without disturbing everything around it.

**[See the complete gallery: Ajay in images →](/dgx-spark/portrait-of-ajay/)**

## Naturally, I asked for another set

I liked the first gallery enough to ask for a second one with different images. *The Second Atlas* has eleven images. The style changes from dark scenes and gold light to bright colours and paper worlds.

<div class="dgx-figures">
<figure class="dgx-figure">
  <a class="glightbox" href="/dgx-spark/ajay-second-atlas/00-book-of-possible-work.png" data-gallery="ajay-second-atlas" data-title="The book of possible work · Qwen"><img src="/dgx-spark/ajay-second-atlas/00-book-of-possible-work.png" alt="An open book becomes a set of colorful handmade worlds" loading="lazy" decoding="async" width="1024" height="1024"></a>
  <figcaption><strong>The book of possible work</strong> · Qwen<br>Each page opens into a place to explore. The same care guides the search, the plan, the repair, and the result.</figcaption>
</figure>
<figure class="dgx-figure">
  <a class="glightbox" href="/dgx-spark/ajay-second-atlas/04-proof-relay.png" data-gallery="ajay-second-atlas" data-title="The Proof Relay · FLUX"><img src="/dgx-spark/ajay-second-atlas/04-proof-relay.png" alt="A small gold marble moves through a physical model toward a lit lamp" loading="lazy" decoding="async" width="1024" height="1024"></a>
  <figcaption><strong>The Proof Relay</strong> · FLUX<br>You check that one result reaches real use.</figcaption>
</figure>
</div>

**[See the complete gallery: The Second Atlas →](/dgx-spark/ajay-second-atlas/)**


## For now

I've done more with the Sparks since then, but I'll stop this first post here. This was a very satisfying start for me personally. In the next blog post, I will explain the current setup and what's running on these two Spark devices. Until then: **may your models stay loaded.**

---

*This article was written with the help of an AI agent, based on the work we did together. The opinions, edits, and final responsibility are mine.*

## References

- [NVIDIA DGX Spark](https://www.nvidia.com/en-us/products/workstations/dgx-spark/) - NVIDIA's compact computer for local AI
- [DGX Spark Playbooks: ComfyUI](https://github.com/NVIDIA/dgx-spark-playbooks/blob/main/nvidia/comfy-ui/README.md) - Setting up ComfyUI on DGX Spark
- [Running CrewAI with Local Models: Observations and Insights](/running-crewai-with-local-models-observations-and-insights/) - My earlier local-model experiments on a MacBook Air
- [Ajay in images](/dgx-spark/portrait-of-ajay/) - The first gallery
- [The Second Atlas](/dgx-spark/ajay-second-atlas/) - The second gallery
