---
title: "Said and Done: an agent to track promises"
date: 2026-06-24
type: post
categories: [Projects]
tags: [agents, ai, claude-code, openspec, python, railway]
---

For a long time I've been bothered by how cheap it is to make a public promise. Nobody ever goes back to check whether politicians, company executives or self-proclaimed experts actually followed through on what they said. AI seemed like the perfect tool to automate that tracking, and after sitting on the idea for a while I finally decided to give it a shot.

## 🏗️ The system

"Said and Done" was a system that tracks promises and predictions in the media: it extracts the content, the author and the expiry date, and then monitors whether they were fulfilled. The architecture has three layers — data and business logic, public website, and background agents — designed to evolve independently and easily deployable on [Railway](https://railway.app). **One agent scans RSS feeds looking for new promises; another monitors expired ones searching for evidence of fulfilment via web search.** Both propose changes to a centralised review queue: nothing is published directly, everything goes through a human review first.

{{< figure src="/img/posts/said-and-done-architecture.svg" alt="Said and Done Architecture" caption="Said and Done Architecture" width="70%" >}}

For development I used Claude Code from the start, in vibe coding mode: I let the AI propose the architecture in Python and built on top of it without worrying too much about the internals. Midway through I integrated **[OpenSpec](https://openspec.dev)**, which I found very useful for refining ideas, identifying edge cases and inconsistencies, and reviewing implementation plans in detail before executing them. Since I didn't have a strong opinion on the implementation, I probably didn't explore everything OpenSpec could offer — but it still changed the way I worked considerably.

## 🎓 Things I learned

The system ran for about four or five weeks. From that time I take away four things:

**Agent cost depends heavily on the model.** Processing dozens of news items per day with Sonnet via API has a significant monthly cost for a personal project. Haiku makes it economically viable, but the results are somewhat worse. The conclusion is clear: either you pay for the best possible outcome, or you accept that someone will need to review the work.

**False positives were the most persistent problem.** Event announcements, predictions without a concrete date, ambiguous statements. With Haiku there was too much noise; with Sonnet, less, but still enough. I revised the prompt several times and it kept improving, but never enough to avoid having to check the queue every day. The analysis task requires a significant comprehension effort that a simpler model can't handle consistently today.

**I underestimated duplicate detection.** The same story in different outlets or picked up on different days would appear multiple times as separate promises. At the cost of increasing expenses, I ended up integrating AI to detect duplicates among pending proposals too. It worked much better than the purely syntactic approach I tried initially.

**AI-generated tests don't always cover every case.** The system suffered runtime errors due to API responses inconsistent with the expected data structure, especially around field lengths. Things that the tests — also generated with AI assistance — hadn't anticipated, and that only appeared once the system had been running in production for a while. Something that should have been easily identifiable slipped through to "production" due to gaps in the AI's default test generation.

## 📊 Results

In the end, as I said, I only had the system running for a few weeks. The reality is that it required a daily review of the queue — new proposals and expired promises — and I ended up abandoning and uninstalling it shortly after. Not because it didn't work technically, but because the attention cost it required wasn't sustainable for me.

> AI has largely removed the technical barrier to building something, but if the result isn't fully automated, it still requires a maintenance effort that many personal projects can't sustain.

That shift from "I don't have time to build it" to "I don't have time to keep it alive" is a real one. A cost that was always there, but one that now stands out as the main barrier.

That said, I personally consider the project a success. As a PoC, it delivered what it needed to: I learned to put together a complete system with several AI agents working in parallel, I better understood the need for and challenges of including human-in-the-loop in that kind of pipeline, and I saw first-hand the advantages — and limits — of using tools like Claude Code and [OpenSpec](https://openspec.dev) in development. For a few weeks of occasional work, not bad at all. I suspect if you're reading this, the story sounds familiar — doesn't it?
