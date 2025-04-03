---
title: "Running CrewAI with Local Models: Observations and Insights"
tags: [CrewAI, AI Agents, Local LLMs, Python]
categories: [blog, tech]
date: 2025-04-03T10:30:00+05:30
draft: false
---

# Introduction

While exploring CrewAI and running agents locally, I came across a [post on Twitter](https://x.com/_avichawla/status/1900434449797701942) claiming it’s possible to run CrewAI with Gemma and use it to generate a small book. I replicated most of the code and tried running it locally. Initially, it didn’t work, but with some minor modifications, I managed to get it running successfully.

## My Experiment: Book Writer with Local Models

For those unfamiliar with the tweet, the idea is to use an agentic framework and a locally running LLM to generate a few pages of a book based on a given topic or theme. This can be achieved in two ways:

1. Directly prompting an LLM to write about a topic.
2. Breaking the goal into multiple sub-goals and having a set of agents solve one step at a time. The output of each sub-goal is then fed into the next step, and so on.

The second approach, also known as chain-of-thought (CoT), helps the LLM solve the problem more reliably. The system consists of multiple agents:

- **Book Researcher**: Gathers information about the topic.
- **Book Outline Writer**: Creates a structured outline for the book.
- **Chapter Researcher**: Researches specific chapter topics.
- **Senior Writer**: Writes individual chapters based on the research.

Each agent runs sequentially, and the output is passed to the next agent. The working script and instructions for running it are available on [GitHub](https://github.com/ajaykumarns/snippets/blob/main/crewai_bookwriter/book_writer.py). I recommend checking out the README and trying it yourself. If running locally isn’t feasible, OpenAI or Gemini API calls are suggested (and are likely much faster).

## Local Model Performance

I ran the experiment with the following specifications:

- **Device**: MacBook Air M3
- **Memory**: 24GB
- **CPU**: 8-core
- **GPU**: 10-core

Here are my observations on how the models performed:

### Gemma3:4b

Google’s Gemma model delivered mixed results (at least for me, running locally):

1. It frequently failed to follow instructions and made errors when calling the web search tool. The tool required a string as an argument, but Gemma kept calling it with a dictionary. (I didn’t attempt fine-tuning or modifying the instructions.)
2. Ollama timed out a couple of times, even though I had plenty of memory. While running `ollama ps`, it showed 100% GPU usage, but I’m unsure why.

These issues caused multiple intermediate failures, and the book generation process often didn’t complete. Overall, it took around 20–30 minutes to run the experiment with Gemma, making it unreliable.

### Deepseek-r1:7b

This model was quite slow on my laptop. After some testing, I discovered it didn’t support tool-calling, so any instructions requiring research were ignored.

### Llama3.2

Similar to Gemma, this model struggled with tool usage and frequently made errors when invoking the web search tool.

### Qwen2.5:3b

This model worked flawlessly. It followed instructions correctly, used tools effectively, and conducted proper research. I ended up using Qwen2.5:3b for experimenting with multiple topics.

### Qwen2.5:7b

This model performed similarly to the 3b variant but was slightly slower on my device.

### Summary

| **Model**       | **Performance**                                                                 | **Issues**                                                                                     | **Remarks**                                                                 |
|------------------|---------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| **Gemma3:4b**    | Mixed performance; failed to follow instructions and caused errors in tool use | Frequent failures due to incorrect argument types; GPU timeouts despite sufficient memory     | Took 20–30 minutes to complete; unreliable for consistent book generation  |
| **Deepseek-r1:7b** | Slow performance; lacked tool-calling support                                | Unable to perform research tasks due to missing tool-calling capability                       | Not suitable for tasks requiring external research                          |
| **Llama3.2**     | Similar issues as Gemma; struggled with tool usage                             | Errors in invoking the web search tool                                                        | Unreliable for tasks involving external tools                               |
| **Qwen2.5:3b**   | Excellent performance; followed instructions and used tools effectively        | None observed                                                                                 | Best choice for local book generation; reliable and efficient              |
| **Qwen2.5:7b**   | Similar to Qwen2.5:3b but slightly slower                                     | None observed                                                                                 | Reliable but slower than the 3b variant                                    |

Your mileage may vary depending on your local memory and CPU capacity. I suggest starting with smaller models and gradually trying larger ones to avoid wasting time, as I did.

## Conclusion

Overall, experimenting with CrewAI and running these models locally was an enjoyable experience. For my specific use case of automated book writing, Qwen2.5:3b provided the best balance of quality and performance among the local models tested. CrewAI’s flow-based system proved robust for managing complex, multi-stage content creation.

If you’re interested in experimenting with CrewAI and local models, check out my [implementation on GitHub](https://github.com/ajaykumarns/snippets/blob/main/crewai_bookwriter/book_writer.py) and adapt it to your needs.

---

*Have you experimented with CrewAI or similar agent frameworks? Share your experiences!*