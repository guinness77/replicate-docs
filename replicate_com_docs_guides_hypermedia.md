Docs

Search documentation`⌘K`

Get started

Collapse sidebar

[Run a model from Node.js](https://replicate.com/docs/get-started/nodejs) [Run a model from Google Colab](https://replicate.com/docs/get-started/google-colab) [Run a model from Python](https://replicate.com/docs/get-started/python) [Fine-tune an image model](https://replicate.com/docs/get-started/fine-tune-with-flux)

Guides

[Build a website with Next.js](https://replicate.com/docs/guides/nextjs) [Build a Discord bot with Python](https://replicate.com/docs/guides/discord-bot) [Build an app with SwiftUI](https://replicate.com/docs/guides/swiftui) [Cache images with Cloudflare](https://replicate.com/docs/guides/cloudflare-image-cache) [Use realtime speech with OpenAI](https://replicate.com/docs/guides/openai-realtime) [Push your own model](https://replicate.com/docs/guides/push-a-model) [Push a Diffusers model](https://replicate.com/docs/guides/push-a-diffusers-model) [Push a Transformers model](https://replicate.com/docs/guides/push-a-transformers-model) [Handle webhooks with Val Town](https://replicate.com/docs/guides/build-a-webhook-notifier-with-val-town) [Deploy a custom model](https://replicate.com/docs/guides/deploy-a-custom-model) [Push a model using GitHub Actions](https://replicate.com/docs/guides/push-a-model-using-github-actions) [Set up a CI/CD pipeline](https://replicate.com/docs/guides/continuous-model-deployment) [Get a GPU on Brev](https://replicate.com/docs/guides/get-a-gpu-on-brev) [Get a GPU on Lambda Labs](https://replicate.com/docs/guides/get-a-gpu-on-lambda-labs) [Working with LoRAs](https://replicate.com/docs/guides/working-with-loras)

ComfyUI

Hypermedia

[Build AI apps fast with hypermedia](https://replicate.com/docs/guides/hypermedia) [What is hypermedia, and why use it for AI apps?](https://replicate.com/docs/guides/hypermedia/what-is-hypermedia) [Building a face swapping app with Val Town, HTMX, and Replicate](https://replicate.com/docs/guides/hypermedia/build-hypermedia-app)

Instant ID

Language models

Llava

Model best practices

Photomaker

Stable Diffusion

Upscaling images

Whisper

Topics

Models

Predictions

Deployments

Webhooks

Organizations

Billing

Site policy

Reference

[How does Replicate work?](https://replicate.com/docs/reference/how-does-replicate-work) [Client libraries](https://replicate.com/docs/reference/client-libraries) [HTTP API](https://replicate.com/docs/reference/http) [OpenAPI schema](https://replicate.com/docs/reference/openapi) [Open source](https://replicate.com/docs/reference/open-source)

In the age of generative AI it can feel like everything is moving too fast. There are so many fun generative models to play with, and new ones released every day. It's hard to keep up.

Especially when combining different models, the workflows get complex and hard to manage. But you don't want to spin up a new production app with frontend, backend, and GPU every time you try something new.

What if you could quickly glue a few models together to suit your workflow? What if you could do this without leaving your browser? Even... from your phone? We're not talking about "no-code" interfaces here. What if you could build and deploy a custom AI app with just a few lines of code?

This guide will walk you through the basics of hypermedia and how to use it to build AI powered apps. We'll combine several models to build a custom AI web app and deploy it to the web as a single serverless function. You can follow along in the browser and fork the app to create your own custom AI workflows.

Our example app is Movie Real, a face swapping app that puts you on the big screen:

Movie Real: Creating Hypermedia Apps

![](https://cdn.loom.com/avatars/27000210_d78c15cb0d8a4ed3a6395110e27869aa_192.jpg)

[Movie Real: Creating Hypermedia Apps](https://www.loom.com/share/b2ca8d61cef744daa3388754efa667dd?source=embed_watch_on_loom_cta&t=0 "Movie Real: Creating Hypermedia Apps")

2 min

807 views

4

[Open video in Loom](https://www.loom.com/share/b2ca8d61cef744daa3388754efa667dd?source=embed_watch_on_loom_cta&t=0 "Open video in Loom")

1.2×

1 min 36 sec⚡️2 min 1 sec1 min 36 sec1 min 20 sec1 min 4 sec57 sec48 sec38 sec

😍

Anonymous

😂

Anonymous

😂

Anonymous

🥺

Anonymous

👍

Peng Zhang

😍

Zeke Sikelianos

A

this video is busted on Chrome on Android mobile jsyk I had to get out of bed and get on my PC to watch this

3

A

Why is the guy who's talking better looking than the guy who gets inserted into the photos?
+2 other comments

Introduction

Your user agent does not support the HTML5 Video element.

![](https://cdn.loom.com/avatars/27000210_d78c15cb0d8a4ed3a6395110e27869aa_192.jpg)

[Movie Real: Creating Hypermedia Apps](https://www.loom.com/share/b2ca8d61cef744daa3388754efa667dd?source=embed_watch_on_loom_cta&t=0 "Movie Real: Creating Hypermedia Apps")

2 min

807 views

4

[Open video in Loom](https://www.loom.com/share/b2ca8d61cef744daa3388754efa667dd?source=embed_watch_on_loom_cta&t=0 "Open video in Loom")

1.2×

1 min 36 sec⚡️2 min 1 sec1 min 36 sec1 min 20 sec1 min 4 sec57 sec48 sec38 sec

😍

Anonymous

😂

Anonymous

😂

Anonymous

🥺

Anonymous

👍

Peng Zhang

😍

Zeke Sikelianos

A

this video is busted on Chrome on Android mobile jsyk I had to get out of bed and get on my PC to watch this

3

A

Why is the guy who's talking better looking than the guy who gets inserted into the photos?
+2 other comments

Introduction

## [Anchor for who-is-this-guide-for](https://replicate.com/docs/guides/hypermedia\#who-is-this-guide-for) Who is this guide for?

This guide is for developers who want to rapidly prototype AI powered apps. You're familiar with HTML, CSS, and JavaScript, and you've used AI models before.

Maybe you've heard about hypermedia and are curious to test it out. Or maybe you're a full-stack veteran looking for a way to quickly iterate AI projects. Whatever your background, this guide will help you build AI apps fast.
We'll walk through everything step by step and you can follow along in the browser.

[Next:What is hypermedia, and why use it for AI apps?](https://replicate.com/docs/guides/hypermedia/what-is-hypermedia)