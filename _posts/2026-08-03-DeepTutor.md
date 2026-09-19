---
title: My Deep Tutor Anecdotal Experience
description: How I use Deep Tutor as a college student Part I
author: Zinko
date: 2026-08-03
categories: [AI]
media_subpath: '/assets/img/posts/DeepTutor'
---

No AI was used in the writing of this article.

Note: This is Part 1 of a 2 part series. The 2nd part will be released in the future once I spend more time actually using DeepTutor instead of debugging it.

## Overview

I got sick of trying to find anecdotal experiences with DeepTutor so I decided to write my own blog post about my experiences. Also note that this post was written over the span of 4 months and some of the content within will be out of date as currently DeepTutor is doing nearly daily releases.

I'm going to assume you already know what DeepTutor is (since you found your way to this page). If not, here's the github: https://github.com/HKUDS/DeepTutor.

The goal of this project was to test how effective AI learning tools, specifically DeepTutor, are for college students. 

Am I riding the AI band wagon? Perhaps...

![The Internet is a passing fad](InternetFad.png)


## Setup

I originally set up Deeptutor just on localhost on my laptop but I later moved it to my homelab to have better uptime. I'm very fortunate to have some hardware capable enough to run AI models locally. For reference, I'm running a locally hosted Gemma 4 31b as my model of choice for all my testing. Gemma 4 should be conceivable to run for those who don't have hardware to locally host ($.14-.25/M tokens or even free). I'm accessing my model just by using the ollama api.

## Knowledge

This is arguably the most important feature of DeepTutor. You can create Knowledge Bases (KBs) in which you can upload your own sources for DeepTutor to call via Retrival Augmented Generation (RAG). 

The current best competitor that does this is [Google's NotebookLM](https://notebooklm.google.com). I used NotebookLM extensively before coming to DeepTutor. While NotebookLM is more fleshed out and feature rich, DeepTutor gives you full access to do whatever you want with your KBs (including custom tool calls).

The DeepTutor KBs UI is also more responsive then NotebookLM's. They also actually let you redownload stuff after you upload it (I learned the hard way that NotebookLM doesn't when I was trying to download from it last week). There's also the fact that you don't need a google account to use it.

### Personal Knowledge Vaults

Since all my stuff is locally hosted I don't need to worry about my data getting trained on. I immediately uploaded my entire obsidian knowledgebase that is essentially just my offboard brain. This lets me do AI querying and lets me connect multiple notes/thoughts together for synthesis rather than just a key word search. 

### Textbook KBs

Since you can upload your own KB articles, one of the best student usage's is to upload your textbook as KB. At the time of writing, the pdf file size limit is 200Mb. Granted, this is conditional on having a digital format of a textbook which can be a bit rough.

For one of my classes, all of the course content was externally linked through canvas. It was a bit of work to get it into DeepTutor but by having Gemini help me with a tamper monkey script I managed to download all the course content. Once that was finished, it's just a upload away to have a fully functioning kb that my AI can teach me info on.

## TutorBots

Note: Since the writing of this section, TutorBots have been replaced with Partners. I haven't had the chance to play around with Partners much but I imagine that all of the same stuff that TutorBots can do, Partners can. I'm sure they also have new fun things they can do aswell.

### Bots on bots on bots

One of my favorite features of DeepTutor is the TutorBot feature. It's a fairly unique concept.

For each TutorBot (which I'll refer to as TB from now on) you create a soul. This is one of my first souls, based on the default template

```md
# Soul

I am a coding assistant focused on helping developers write better software by providing deep, actionable code comprehension.

## Personality

- **Explanatory:** Articulates the *function* and *design rationale* of every code section.
- **Concise:** Gets straight to the point; avoids unnecessary verbosity.
- **Pragmatic:** Focuses on understanding existing code structure over suggesting abstract improvements.

## Approach

- **Context First:** Reads and understands the entire code block before offering analysis.
- **Deep Dive:** For every section, explains *what* it does and *why* it is designed that way (the underlying intent).
- **Efficiency:** Prefers direct, point-by-point explanations that maximize comprehension with minimal reading effort.
```

For each of these bots you can specify things that they do. You set the soul, the user profile (details about YOU), tools it can use, agend instructions, and heartbeat tasks (checked every 30 minutes). 

The best part? You never have to touch these after you set the soul.

The AI is able to adjust each of these for you however you like.

It also can modify its own instructions...

![This is fine...](ThisIsFine.jpg)



### Discord integration
Each TB has this nifty thing called channels. You are able to setup your bot with loads of communication platforms (discord, telegram, slack, even email!)

I use discord as my primary communication and so a few prompts later I now know how to setup a discord bot. Yet a few more prompts and now it's connected! 

I made a TB specifically for discord communication. Currently, it's a general purpose TB but it focuses on speed and quering stuff from my general Obsidian KB.

It's sooo nice not have to open my laptop to talk with it, I just DM it and we're set.

I also don't have to do anymore funky networking stuff... thank goodness.


### Usage

How helpful are these TutorBots really?

The answer is... very*.

#### Personal Example of TutorBotts

This past term I've been taking a psych class. It's a bit crazy since we're compressing a semester of content into 7 weeks.

Since this is a 3 credit class they say we're supposed to spend 12-18 hours a week working on it. I don't know about everyone else but I don't have time for that.

So how long did I spend on class a week?

About 3 hours...

![Turbo](snail.jpg)

Now before you go crazy and start preaching the good word of DeepTutor there are some things to keep in mind...

##### Pros

It is fantastic at connecting things within a topic to things you already know. This helps create connections in your brain by anchoring it to a familiar concept. For example, I once got something along the lines of "The amygdala is the SOC of the brain." 

It speeds up reading a TON. It's recommended that each of the lessons take 80-130 minutes. On average it took me about 15-20 minutes to read, do the mini activities, and take a 5 question quiz.

##### Cons

My accuracy on lesson quizes was very spotty. Sometimes the AI would get the content on the quiz spot on, other times it completely missed and I did poorly on the quiz because of that.

If the course has stupid questions that check for reading memorization instead of conceptual understanding (i.e. "The author said _". Really stupid questions). If that's the case, you're just kinda cooked.

It's also not a complete all in one solution. I still recommend doing any mini quizzes/practice before taking a quiz with it. In order for it to be effective at studying for the test it needs to know what's on the test.

It also forgets its own context within TutorBots a lot. I'm not sure if this is just because Gemma 4 only has a 262k context window or if it's DeepTutor's fault but it is quite annoying.

I have encounted quite a number of issues with it not loading my latest chats whenever I'm running it. 


## Troubleshooting

Feel free to skip this section as most of these issues will probably be fixed in future versions.

I was running into issues on the TutorBot page where I couldn't create a bot. I initially thought this was something weird to do with CORS because of the error message. However, after doing some poking around I found a import error in the logs. 

![CORS/500 error](TutorBotError.png)

This was remedied by `pip install -r requirements.txt`

Why did this happen? I have no idea.

The setup wizard imported a lot of things whenever it ran but I guess it didn't do it all?

### Migration

Once I got further into it I wanted to have DeepTutor running constantly so that I didn't have to constantly be restarting it on my laptop. I did this by moving it to my homelab.

This was full of a mirad of issues from venvs being broken, node not installing correctly, etc...

I also had an interesting error where none of my data was showing up on the webui.

In order to fix it I had to add this in /web/next.config.js

```js
const nextConfig = {
    \\ other things
    allowedDevOrigins: ["192.168.1.2", "localhost"], \\added this line
    \\ more other things
```

For some reason the frontend couldn't talk to the backend even though they're both on local host?


![All Modern Infrastructure](AllModernInfra.jpg)

It's definately 1.0 software that's not a easy setup for the average student.

### Restarting

I eventually got tired of having to do weird git stash stuff every time I updated it to get the new features and so I migrated to using their offical docker container. After I got all the docker kinks worked out, it runs fine. I did change their docker run command into a docker compose file (just threw it into chat) and started migrating all of my data to that.


## Conclusion

Long story long, if you're reading this post then you're probably tech savy enough to get it setup and working. If this is the case, go ahead and set it up. Overall, I'd judge it as giving me a 3x boost to my learning speed while helping me to have greater retention and comprehension compared to reading a textbook (although I hate textbook learning and the vast majority of the time never bother to read it).