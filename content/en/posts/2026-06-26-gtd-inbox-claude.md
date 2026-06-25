---
title: "How I taught Claude to process my GTD inbox"
date: 2026-06-26
type: post
draft: true
categories: [Productivity]
tags: [GTD, Notion, Claude, Skills, MCP]
---

## 🧠 The problem

My memory is pretty mediocre. Not in the dramatic sense of forgetting important things, but in that everyday sense of permanently feeling like something is slipping through the cracks: a task I wanted to get done this week, a deadline creeping up without me noticing. That feeling generates a low-grade stress I really don't like.

A while back I discovered [GTD](https://gettingthingsdone.com) — Getting Things Done, David Allen's system — and used it for a while to manage professional tasks. About a year ago I decided to bring it back for my personal life, using [Notion](https://notion.so) as the backbone. I started from [this template](https://app.notion.com/marketplace/templates/task-management-gtd-work-flow), simplified it a bit, and the result works well: projects, individual tasks, and an inbox where I jot down everything that comes in to process later.

{{< figure src="/img/posts/gtd-notion-inbox.png" alt="My GTD system in Notion" caption="My GTD system in Notion" width="70%" >}}

The problem was right there, in the "later". **The process of reviewing the inbox and turning each note into a properly labelled task, assigned to a context, with the right dates and status... felt tedious**: not because it was hard, but because it involved enough manual steps — creating, editing, deleting items — to keep pushing that processing moment off. And when you postpone processing your GTD inbox, the inbox stops being an inbox and becomes just another container of chaos, which is exactly what you were trying to avoid.

## 🤝 The solution

I found the solution with the [**Notion connector for Claude**](https://developers.notion.com/guides/mcp/overview) and its MCP. What I did was teach it the databases I use, explain my workflow and the usual property values, and run a couple of tests until it could process the inbox the way I expected. Once the results were consistent, I asked it to turn everything into a [skill](https://docs.anthropic.com/en/docs/claude-code/skills) where it recorded everything it needs: database IDs, JSON templates for creating or editing pages, the workflow, default values, and so on.[^1]

{{< figure src="/img/posts/gtd-notion-architecture.svg" alt="GTD architecture with Claude and Notion MCP" width="60%" >}}

The process now goes like this: I ask it to process the inbox, it shows me all the pending entries and for each one asks what I want to do. Most become individual tasks. Some become projects, and then it asks me to describe the subtasks. For any task, it knows what default values to use and only asks me to confirm the location — at home, out of the house, at the computer, on the phone — because that depends on the specific task and there's no way to infer it.

There's one detail I find interesting: for projects, Claude knows that the first task must be left in "Ready" status — because it can already be executed — but the rest have to be "Blocked", because they normally depend on that first one being done. That's the kind of contextual logic I used to apply manually every time.

[^1]: The Notion integration in Claude has some limitations — among them, it can't delete pages. I wanted it to remove each inbox entry after processing to keep things clean. The solution was to add the Zapier integration, which does have that capability. A bit of a hack, but it works.

## ✅ The result

What's actually changed? That I genuinely process the inbox now, regularly. Before I'd put it off because it felt like a chore; now it's a five-minute conversation where I'm basically just answering concrete questions. The system does what it promised to do when I first read about it — get things out of your head and into a trusted place. It's just that now Claude does almost all the work of putting them there correctly.
