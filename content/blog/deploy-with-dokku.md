---
date: '2025-07-08T13:19:04+03:00'
draft: false
title: 'Deploy With Dokku'
categories: ["deployment", "tutorials"]
tags: ["deployment", "dokku"]
---

Today I want to share why Dokku changed how I think about deployments. This isn't a tutorial—you can find those anywhere. This is about **why** you should consider it.

## What is Dokku?

Dokku is a Platform-as-a-Service (PaaS) that runs on a single server. Think of it as your own personal Heroku, but self-hosted, open source, and lightweight.

It started as a collection of bash scripts. Now it uses Go too, but the philosophy remains the same: **keep deployment simple**.

## My Experience

I've deployed these with Dokku:
- WordPress sites, Moodle instances, Ruby applications, Node.js projects, Kanboard, Grafana

All running on one small server. No complexity, no container orchestration nightmares.

The Dokku team puts it perfectly: *"Use it on inexpensive cloud providers. Use the extra cash to buy a pony or feed kittens. You'll save tens of dollars a year on your dog photo sharing website."*

## Why Dokku Over Competitors?

Simple answer: **Dokku is the simplest one**.

It gives you more control than other platforms. The documentation is excellent and AI tools understand Dokku well. 

Personally, Dokku feels like home. I'm still new to the deployment world—maybe I should try other options too. But Dokku abstracts less than its competitors, which means I can interact with the server and Docker directly when needed. 

Since Dokku is simple and built with bash and Go, I can read the source code directly to understand what's happening under the hood.

## Ready to Get Started?

If you're convinced and want to try Dokku yourself, check out my [deployment guides](/deployment-guides/) where I share step-by-step instructions for deploying various applications.