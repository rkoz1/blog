---
title: Practical guide to setting up a Home Lab
meta_title: Home Lab on Mac Mini M4 with automation, LLMs and more
description: Home Lab on Mac Mini M4 with automation, LLMs and more
date: 2025-04-17T05:00:00Z
image: /images/posts/cursor_interview/main_image_cursor.png
categories:
  - Automation
  - Server
author: Rafal Koziarz
tags:
  - server
  - cloudflare
  - domain
  - ollama
  - n8n
  - homelab
draft: false
---
Home Lab is a fun way to learn and experiment, but it can also be a powerful tool for automating some of the daily tasks, without the need for 3rd party cloud or expensive SaaS licenses. **For anyone, regardless of your technical background, it can be a gateway to managing your own (free!) AI/LLMs and creating automation using no-code tools like n8n *(see 'Automate Everything!')***

For anyone working in software development, it is also a chance to **be your own IT department** - handling everything yourself - infrastructure, identity, scripting, DevOps process, development and much more. It also gives you the opportunity to experiment with new technology without the walls of enterprise proxies, policies and politics. 

For those of you interested in Solution and Enterprise Architecture, I believe it gives you the opportunity to shape an opinion about each layer in the stack. A simple hello world can be enough to build empathy for what developers have to go through when using certain technologies.

In my **[introduction post](/blog/blog_made)** I mentioned the concept of a Second Brain - the role of my Home Lab will also be to help me manage the tremendous amount of information I come across each day and condense it into manageable content that I can digest while having my morning breakfast. More on that in the *'Compressing my day into a PDF'* section. 

Let's start with a little bit of context

## What is a Home Lab?

Home Lab is essentially a server that runs your "home" development, services and experiments. Whether it's just a server, depends on what you are doing. Claude describes the difference between the two as this:

>A server is a single computer dedicated to providing specific services on a network, while a home lab is a broader experimental environment containing multiple devices (which may include servers) used for learning, testing, and skill development in a risk-free setting.

## My Setup

Although technically anything can be a server and your existing laptop or PC can serve as a Home Lab / server, having a separate device that will run 24/7 was the reason why I opted for buying a Mac Mini.

### The Hardware

I went for the absolute basic model with a M4 chip and 16GB ram - more than plenty for the type of things I will talk about in this post

The system consumes **4w of power when idle**, which is incredible

### The Software

After going through the standard MacOS setup, I made a list of things I wanted to have installed:

{{< notice "tip" >}}

NixOS is an example of a fully declarative operating system - meaning if I passed you the configuration, you could fully reproduce everything I have done to the smallest detail, with a single run command. Unfortunately not a MacOS feature!

{{</ notice >}}
## Local (free) LLMs / AI
## Automate Everything!
## Compressing my day into a PDF

## Accessing your services from the internet

