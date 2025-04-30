---
title: "How and why did I start a blog?"
meta_title: "Building a blog"
description: "Guide on building blogs with Hugo"
date: 2025-04-28T05:00:00Z
image: "/images/posts/why_blog/blog_made.png"
categories: ["Technology"]
author: "Rafal Koziarz"
tags: ["go", "hugo", "github actions", "github pages", "github"]
draft: false
---

<hr>

## The Reason

For years it has always been on my mind to put some thoughts on 'paper' and start a blog. 

Recently, I was introduced to a book called Building a Second Brain, which explores the benefits of having a system to offload the vast amount of information that bombards our brains daily. In today's fast moving world (new AI 'revolutionary change' every week, [new javascript framework almost every day](https://dayssincelastjsframework.com/) and unbelievable things you see on the news) it's increasingly difficult to step back and reflect on what you have read, what does it mean for you or how would you apply it to your work. 

A blog gives me the chance to reflect, but also to share some ideas with friends and colleagues. Hope it makes a difference to someone (even if its just myself).

{{< notice "note" >}}

The book **Building a Second Brain by Tiago Forte** is about creating a personal knowledge management system that helps you capture, organize, and use the vast amount of information you encounter daily. This system acts as a "Second Brain" — a digital extension of your mind that stores important ideas, insights, and information so you can free up mental space for higher-level thinking, creativity, and productivity

{{< /notice >}}

<hr>

## The Style

With this blog I am not trying to shake the foundations, however I do want to share my experiences (good and bad) building applications, using new tools, as well as, discuss anything I have researched and give my opinion about each. 

I'm not an expert in everything I write about, however I believe one of my key strengths to be solution architecture and being able to quickly evaluate where and when a technology can be used to fulfill a purpose (read: meet business requirements). 

I welcome feedback, so please reach out either directly, or via [LinkedIn](https://www.linkedin.com/in/rafalkoziarz/). 

To keep the blog 'human' I will be avoiding using LLM's to help me write!

<hr>

## The Stack

I'm a big fan of [Fireship](https://www.youtube.com/c/Fireship) and saw one of the 100 second videos about **Hugo**, a static website generator. I've used MKDocs in the past, which conceptually is very similair, but Hugo is a lot faster (compilation/hot reload/built using Go). More importantly, what motivated me to try it was the extensive library of community themes, which enabled me to quickly style the website and add features like image optimization, preloading, and other page loading enhancements.

For deployments I opted for the simplest and most efficient CI/CD I know, which is **GitHub Actions**. I deploy the static files directly to **GitHub Pages** and expose the website using my own domain name. 

{{< notice "tip">}}
Everything is captured below in a diagram I generated using **DiagramGPT**, which I highly recommend. 

For drawing from scratch I usually opt for **draw.io**, which can commit directly to your GitHub repository alongside your code.
{{< /notice>}}
{{< image src="images/posts/why_blog/workflow.png" caption="Workflow for the Blog" alt="alter-text"  command="fill" option="q100" class="img-fluid" title="Blog Workflow" webp="true" zoomable="true"  >}}

<hr>

## Links

* [Fireship](https://www.youtube.com/c/Fireship)
* [Hugo](https://gohugo.io/)
* [Hugo in 100 Seconds](https://www.youtube.com/watch?v=0RKpf3rK57I)
* [MKDocs](https://www.mkdocs.org/)
* [Building a Second Brain](https://www.amazon.com/Building-Second-Brain-Organize-Potential/dp/1982167386)
* [GitHub Pages](https://pages.github.com/)
* [DiagramGPT](https://www.eraser.io/diagramgpt)