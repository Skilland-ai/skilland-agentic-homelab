PRIORIZAR LAS FUENTES OFICIALES PARA TODO, LUEGO LAS NO OFICIALES PARA INSPIRARNOS EN SETUPS, PLAYBOOKS, CONFIGURACIONES ETC


Fuentes oficiales:

https://hermes-agent.nousresearch.com/docs

https://github.com/NousResearch/hermes-agent

Puedes descargartelas en el VPS si quieres para tenerlas a mano o descargarlas incluso dentro de este repo, lo que quieras para maximizar la eficiencia de nuestra consulta constante a estas fuentes oficiales para todo





## Dump bruto de fuentes no oficiales

<pegar todo aquí sin ordenar>

Fuente 1:
Link: https://x.com/mikenevermiss/status/2063489268169728513

Transcripción:

How to Become a Hermes Agent Operator
learn how to operate and master Hermes Agent. set up the agent control room template, configure specialist agents, and grow from one agent to a whole marketing company on one VPS.
hermes is an open-source autonomous agent by @NousResearch.
it runs on your laptop or a cheap VPS, remembers everything across sessions, and writes its own reusable skills as it works. 
you control it through a terminal, Telegram, Discord, Slack, or email, whichever surface fits your workflow.
the core promise is compounding. on day one, hermes is a capable assistant. by day thirty, it has built a library of skills from your exact use cases, and repeating the same work gets faster and tighter every time.
Install Hermes in Two Minutes
-------------------------------
run one curl command from the official Nous Research repo to install hermes. the installer pulls Node.js, Python dependencies, SQLite, and the hermes runtime automatically. the whole process takes under three minutes on a decent connection.
once installed, a setup wizard runs and asks which model provider you want. the three most common choices: anthropic (claude-sonnet-4, high quality), openai (gpt-5.4 with thinking mode, popular daily driver), or openrouter (qwen/qwen-3.5, free and capable for routine work).
after setup, run `hermes` to open the CLI. give it a simple job first, something like "summarize my last five github notifications." if it responds with real output, your install is working. everything from here builds on that foundation.
Understand What You Just Installed
------------------------------------
hermes stores everything inside `~/.hermes/`. skills it builds live in `~/.hermes/skills/`. session history is in SQLite with full-text search, meaning it can retrieve something you told it three weeks ago even if it is not currently in active memory.
memory works in three layers: short-term for the current session, working memory for important task context, and long-term through `MEMORY.md` and `USER.md` files. the agent reads these files at the start of every session to rebuild context.
the agent's identity lives in `SOUL.md`. this file is the equivalent of a system prompt written as a charter. it defines what the agent prioritizes, how it communicates, and what it avoids. write it before you start assigning real work.
Set Up Your Agent Control Room
--------------------------------
a control room is one hermes profile configured to orchestrate everything else. create it with `hermes profile create control-room`. this profile holds no specialist knowledge, its only job is routing tasks to the right sub-agent and tracking results.
each specialist agent is its own profile with its own `SOUL.md`, its own memory files, and its own skill library. create a researcher profile, a writer profile, a scheduler profile. each one stays focused on a single domain and gets better at it over time.
wire everything together by enabling the `delegate_task` tool on the control room profile. when you send the control room a job, it breaks it down and routes subtasks to whichever specialist is best suited. results come back to the control room, which assembles and returns the final output.
Connect Your Messaging Surface
--------------------------------
the most useful thing you can do in the first week is connect hermes to Telegram. go to @BotFather, create a bot with a username ending in `_bot`, and paste the token into hermes gateway config. from that point, you can command your agents from your phone anywhere.
since all sessions share the same SQLite database, you can start a job in the terminal and check its status on Telegram without losing any context. the conversation thread is one continuous record regardless of which surface you used.
for team setups, create a shared profile on the VPS and grant team members access via the messaging gateway allowlist. this gives your whole team one agent they can all query without you building any custom UI.
Configure Scheduled Recurring Work
------------------------------------
hermes has a built-in cron system. jobs are defined in `~/.hermes/cron/jobs.json` using natural language frequency. the gateway checks every 60 seconds and runs due jobs in fresh, isolated sessions.
useful starting jobs: a daily briefing pulled from your configured sources at 8am, a weekly content draft generated from a topic queue, a nightly summary of any repo activity. each result delivers back to your Telegram or saves locally, whichever you set.
the key advantage of cron over manual prompting is that the agent builds skills from repeated job runs. after a few weeks of daily briefings, hermes knows exactly how you like them formatted and stops asking clarifying questions.
Grow From One Agent to a Marketing Operation
----------------------------------------------
once the control room and messaging are working, add specialist profiles for each marketing function. a research agent that monitors competitors and trends, a writer agent trained on your brand voice, a scheduler agent that manages and posts content drafts.
teach each profile your style by feeding it examples early. run `hermes profile create writer`, then in the first session paste five pieces of content you have already written and tell it "this is the voice and format you write in." it writes a skill file from those examples automatically.
with four profiles running on a $6 VPS, one orchestrator and three specialists, you have the functional output of a small content team running 24/7. each agent compounds independently, and the control room coordinates the whole thing from a single command.
What Breaks and How to Catch It
---------------------------------
the most common early mistake is skipping `SOUL.md`. an agent without identity is technically capable but inconsistent, it will handle edge cases differently each time and drift from your expectations without you noticing.
the second mistake is letting skills accumulate without reviewing them. hermes writes skills automatically, but not every skill it writes is correct. run `hermes skills list` weekly and delete any that describe a flawed approach before the agent reinforces it further.
if a session runs long and starts producing worse output, context is filling up. use `/compress` inside the session to summarize older context, or start a fresh session and let hermes pull what it needs from memory files. do not let degraded sessions run indefinitely.
The Operator Mindset
----------------------
an operator's job is not to prompt. it is to define what the agents do, verify the output quality, and improve the skill library over time. the more precisely you define each profile's `SOUL.md` and the more consistently you assign the right work to the right profile, the better every agent gets.
treat each profile as a hire. give it a clear role, examples of the work you expect, and time to build up its skill library before you judge its output. the compounding is real but it takes two to four weeks of consistent use to become obvious.
the agents do not replace judgment. they multiply the volume of work that your judgment can cover. your job shifts from doing the work to reviewing it, and that is the leverage.




Fuente 2: 
Link: https://x.com/sharbel/status/2067257256215789785


Transcripción:

You see people online using Hermes to run their business. It finds them leads, it writes briefs, it watches the internet, sends them updates on their phone, >> [snorts] >> runs little agents in the background. Then you install it and ask it to summarize a PDF. That gap is what this video is about. So, after 100 days with Hermes, I want to show you the actual bridge. How you go from asking Hermes random questions to building repeatable loops, Telegram workspaces, [music] sub agent teams, event triggers, and a mission control dashboard you can open from anywhere in the world. By [snorts] turning one boring task at a time into a system that runs without [music] you. Let's get started. The first mistake that I've learned throughout my first 100 days is using Hermes like a smarter search box. Asking it for things like "Hey Hermes, give me ideas. Summarize this, research that, write a draft about this." I mean, that is pretty useful and it's a big, massive, major reason for AI agents being useful, but that or those types of tasks don't compound because essentially you get an answer to your question, but the work disappears. The better move is to turn the task into a repeatable loop. Here's the difference. If I say "Give me YouTube ideas," Hermes can give me YouTube ideas. But if I say "Every time I ask you to give me YouTube ideas, check my posted videos, check my rejected ideas, check my Notion content board, check current demand, check competitor outliers, then tell me the one video I I film next, why it matters now. What proof I need and what the first 30 seconds should show. See, that's not a prompt anymore. That's an entire workflow. Hermes is checking for sources. It is applying rules. It's making decisions. It is returning something I can act on, something that is actionable. And that is the first real upgrade. Do not ask what can Hermes answer for me. Ask what decisions do I keep making manually? Because that is usually where the loop is. For me, one loop is reaction opportunities. I do not want to wake up, scroll X, scan AI news, check what is fresh, think through whether it matters, and then decide if I should post. So, Hermes can do that for me every day, every couple of hours. It can check for fresh AI stories. It can check expose by me providing it with a rock API. It can check for product launches, filter for YouTube relevant topics. It can prioritize things from the last hour, or skip stale topics and things that it finds are duplicates. A massive pro tip, by the way, do the thing manually first. Make sure that the loop works manually first. For example, for my YouTube video ideation, I've made sure that Hermes can fetch me every single individual piece of the puzzle. I've made sure that it can use and fetch all of the information and data that it needs from the sources it requires. That I made sure that it knows how to use that data to come up with video ideas. Then I made sure that the video ideas are actually good and actual signals. Once I confirmed all that, then I schedule it as a cron, which is just a fancy word for a repeatable job, something that happens on an occurrence, every day, every couple of hours, you you choose. You can say like every morning check what matters, every Friday audit video ideas, every day scan competitors, and crons should make sense to you. I mean, check these sources, follow these rules, ignore these things, send me this output, run it on a schedule. This is how you go from asking Hermes for help to having Hermes report back. And this works for almost any job. A founder can summarize new leads every morning. A creator can scan video opportunities every week. A developer can open PRs daily. A salesperson can find follow-ups they might have forgot. The value is not in having Hermes do the task once. The value is that it can turn the task that grunt work that you find yourself having to do every day into a repeatable operating system. But, the second you start creating loops, you hit the next problem. Everything gets noisy if all the work lives in one place. My first Hermes setup was basically just one giant junk drawer. I would talk to Hermes about my YouTube ideas, my X posts, my business strategy, my personal tasks, just random questions, and it was all in the same chat. And granted, that can feel a lot simpler, especially when you're starting out, until it becomes impossible to tell what anything was for. The fix was not a more complicated app, it was Telegram topics. I stopped treating Telegram like one conversation with an AI, and I started treating it like separate different workspaces. I mean, I have one topic that is dedicated to YouTube. I It's all I talk about with Hermes about. This is where one of my sub-agents also live, called Nova, but we'll get into that later. One topic is X. That one is built for me to understand what is happening around X. I mean, have I been offline the entire day? Do I need a quick refresher? Can I ask Hermes to fetch sources for one of my tweets that I'm writing or putting out? Another topic is general, and I strongly recommend you have a general topic where it's a sort of catch-all topic that you can ask any question that you have that doesn't really fit into your other topics. One topic is React, which sends me reaction opportunities for things I can talk about on X. This is especially helpful for me if I've been offline or on meetings for an entire day and have not had time to see what is happening with the AI market. The magic is not Telegram or even Hermes. The magic is that every workspace starts having a job. Every Telegram topic is a completely separate workspace. When I message Hermes in the YouTube topic, Hermes does not need to guess what mode it's in. It doesn't need to load a specific context and store away another type of context. It is already in the YouTube room. And that changes the quality of the output you get immediately. Because the more powerful your agent becomes, the more dangerous messy context becomes. If I'm asking for a video idea, I do not want the agent thinking about my grocery list, a code bug, and some random email from yesterday. >> [snorts] >> I want it inside the content workspace using the content rules and content agents or sub agents. That is the practical setup I would recommend. Start with three topics. One for your main work, one for content or research, and one for admin administrative stuff. Then give each topic a simple operating rule. For content, the rule might be before suggesting anything, check what I already posted, what I rejected, what is currently trending, and whether I can actually make it. For admin, the rule might be organize the task, draft the response, but ask before sending anything externally. Now, Hermes is not just answering messages. It is working inside the right room. That is the second upgrade. Chats become workspaces. But, workspaces only solve where the work happens. They do not solve who does the work. That is where sub agents change the setup for me. Let's go to mistake number three. And I know one Hermes agent can do a lot. And that is the trap. Because when something can do a lot, you start giving it everything. Research the market. Check competitors. Inspect notion. Find title ideas. Write the hook. Summarize the hundreds of decisions that I have to make every day. I mean, it can do that, but it will get very messy very quickly. And that's what happened with me. I noticed that the better pattern is sub agents. Think of the main agent as being the main operator. The one who coordinates with all of your other employees. It does not need to personally inspect every detail. It needs clean reports from specialists. Then, it needs to make the final call. For example, if I want Hermes to pick my next video, I can split the work. One sub agent checks my posted and filmed pipeline. One sub agent checks competitor outliers. One sub agent checks current demand. The main agent reads the reports and decides what I should actually film. Now, the work is a lot cleaner. The context is cleaner. The decision ends up also being a hundred times better. Just try it and you'll see. And this is where you can use hack number one in this hack number three because once you define how that workflow looks like, then you can turn it into a repeatable cron or a repeatable skill. Meaning, every time you ask for, say, a YouTube idea, it doesn't have to say guess and start from scratch. It already knows, all right, let's deploy our three sub agents. One does this, one does that, one does that, so on and so forth. You get the idea. However, this is also where a lot of people get agents wrong. More agents does not automatically mean better. More focused agents means better. Each agent needs a specific lane. I love to give this analogy, but you don't want your plumber to be your dentist. Or maybe he's a very talented plumber who also had or happened to take a degree in dentistry. I don't I mean, hey. Don't judge him. But, that is why I built highly specialized agents like Nova and Sage. Nova is my YouTube agent. She has a wealth of knowledge and skills. She's trained on finding and checking YouTube trends, comparing video outliers, comparing competitor posts, and finding the best video ideas, and helping me through my research, ideation, everything I need for YouTube. And I've open-sourced her, meaning you can download and install her for free. I'll leave the link in the description. And Sage is my X and content strategy agent, which is basically the same thing as Nova, but dedicated for X. I've also open-sourced him, and he is free to download and install. And I'll include the link in the description for both. Hooray! You can copy their structure or turn them into your own specialized agents. But the point is not my exact agents. The point is the pattern. Your YouTube agent should not be the same as your coding agent. And your coding agent should not be the same as your personal admin agent. And your plumbing agent should not be the same as your dentist agent. Anyway, starting to feel like I'm going in circles around here. Different job means different tools, mean different memories, means different permissions. The list goes on and on. That is how you stop building one overpowered assistant and start building a team. And once you have a team, the next question becomes obvious. How does the team know when to act? This is where event triggers come in. Cron handles time. Webhooks handle events. I know what you're thinking. What is he talking about? That sounds way too technical. But let me explain this to you because the idea is simple. Crons are repeatable events, as we discussed. Things like do this every single morning. But a webhook says do this when something happens. That is the difference between crons and webhooks. Crons repeat something after every passing of a certain amount of time and webhooks do something when something happens. And listen to me because the second one, webhooks, is where Hermes starts to feel alive. Here's an example. I have a Notion content board. When I move a video idea to film tab, that movement triggers work. It triggers a webhook. The second a video moves to to film, Hermes can validate it. It starts researching it. Did I already post something that is too similar? Is there current demand for that video idea that I just moved? What is the strongest title for that video? Should I film this now, later, or just kill it, abandon it? That is the difference between a database and a control service. Notion is not just where the ideas live. Notion becomes the button that starts the workflow. It becomes the trigger to a chain of events and work. And you can use this yourself anywhere you want. Uh let me give you some ideas. A form gets submitted, Hermes researches the lead. A GitHub PR opens, Hermes reviews the risk. A customer pays, Hermes adds it to the daily summary. A file gets uploaded, Hermes extracts the useful parts. You receive an email, Hermes reads it and summarizes it to you and comes up with a draft of what you could reply to. The setup is pretty simple. You can get as wild as you want with the ideas. All you need to do is create a webhook route in Hermes. And super simple, by the way. Don't let this intimidate you. You can literally ask your Hermes, Hermes, how do we create webhook triggers? And it will guide you. Or it will do it for you if you have it connected to like a super smart model. It will connect to the app itself. Uh the only thing you'll need to do on your end is, you know, tell it what you need from it. And then whenever that event happens, Hermes runs the workflow every single time. And if the app does not support a clean webhook, you can still get close with a polling cron. What in the world is a polling cron? It's a cron that keeps polling, did this event happen every 5 minutes? It didn't. Okay, never mind. I won't do anything. Oh, now it did in the next 5 minutes. Oh, it just did. All right, let's run the cron. Or simply put, Hermes can check every few minutes, compare what changed, and only act when the right thing happens. The bigger lesson is this, stop making yourself the trigger for Hermes to wait for you to ask for things, and let your tools, your emails, your data trigger Hermes. That is when your system starts working even when you are not thinking about it, even when you're not working. But once you have loops, topics, sub-agents, and triggers, you run into the final problem. You cannot manage a real system from a chatbot forever. You need a place to see the machine. On to mistake number five. Chat is good for commands. Chat is bad for visibility. If Hermes is doing real work, I need to know what is happening, what is running, what finished, what failed, where are the different things that I need and ask for in order to be productive on a day-to-day basis. This is why I highly recommend that you build yourself a mission control. Mission control is the dashboard layer. It's your information layer. Think of you opening Jarvis and you see all of this information and you're like, "Wow, this is so cool and futuristic." This is your mission control. For me, it is a live Vercel website connected to my workflows. Uh I have set up Google authentication Gmail authentication so that I can log in to it through my Gmail. That way, you know, some random person can't just find the website link and log in to him itself and control my entire life or ruin my entire life. And what this also means is I can open it on my phone. I can log in and I can control Hermes straight from my phone. I can have every single thing that I need right on my phone. And the great thing about that is I can start using it anywhere I am in the world. I don't need to be next to my local machine, in case you're running Hermes on a local instance. I don't need to be on my desktop if I'm out in the road, traveling, at the gym, something done, or I'm on holiday and I don't have my work equipment with me, I can still be productive by literally asking Hermes to do the thing for me. Mission controls give you the confidence to let Hermes do more because you can actually see what it is doing. That is the difference between a toy setup and a real setup. A toy setup hides everything in chat. A real setup gives you command, visibility, and approval. And if I were to download and install Hermes from scratch, I would build it in this order. One boring loop, one Telegram workspace, one specialist agent, one scheduled cron, and one event trigger. Then, mission control once the system gets too big for just chat. That is a great path for you to level up your Hermi skills and control. Answers become loops, chats become workspaces, one agent becomes many agents and a team. Manual work becomes triggers and invisible work becomes your mission control. That is what 100 days with Hermi taught me. The point is not to use every feature. The point is to transfer your workflow into the system. That is when Hermi stops feeling like a chatbot. And that is when it becomes an operating layer to your entire life and a genuine point of improvement to your quality of life. So, if you want to start, don't overbuild. Pick one task you already repeat over and over again and turn it into a loop. Run it through Hermi. Ask it to help you. Then, from there, add one layer at a time. Add workspaces, then once you've done that, add sub agents, then crons, then webhooks, then mission control. And if you want the specialist agents I showed, Sage and Nova, those are open source on my GitHub. I'll include the links below. If you want the template to my mission control, I'll also include the link to that below. It's also open source and free for you to download. Feel free to copy them, modify them, or use them as templates. Uh but, the real lesson here is bigger than just those agents. Do
You need a place to see the machine.


16:52
Mistake 5: Managing everything from chat forever
16:52
On to mistake number five. Chat is good for commands. Chat is bad for visibility. If Hermes is doing real work, I need to know what is happening, what is running, what finished, what failed, where are the different things that I need and ask for in order to be productive on a

17:15
day-to-day basis. This is why I highly recommend that you build yourself a


17:20
Building a Hermes mission control dashboard
17:21
mission control. Mission control is the dashboard layer. It's your information layer. Think of you opening Jarvis and you see all of this information and you're like, "Wow, this is so cool and futuristic." This is your mission control. For me, it is a live Vercel website

17:39
connected to my workflows. Uh I have set up Google authentication Gmail authentication so that I can log in to it through my Gmail. That way, you know, some random person can't just find the website link and log in to him itself and control my entire life or ruin my

17:59
entire life. And what this also means is I can open it on my phone. I can log in and I can control Hermes straight from my phone. I can have every single thing that I need right on my phone. And the great thing about that is I can start using it anywhere I am in the world. I

18:21
don't need to be next to my local machine, in case you're running Hermes on a local instance. I don't need to be on my desktop if I'm out in the road, traveling, at the gym, something done, or I'm on holiday and I don't have my work equipment with me, I can still be

18:38
productive by literally asking Hermes to do the thing for me. Mission controls give you the confidence to let Hermes do more because you can actually see what it is doing. That is the difference between a toy setup and a real setup. A toy setup hides everything in chat. A real setup

18:55
gives you command, visibility, and approval. And if I were to download and install Hermes from scratch, I would


19:04
The exact order I would build Hermes from scratch
19:04
build it in this order. One boring loop, one Telegram workspace, one specialist agent, one scheduled cron, and one event trigger. Then, mission control once the system gets too big for just chat. That is a great path for you to level up your Hermi skills and control. Answers

19:27
become loops, chats become workspaces, one agent becomes many agents and a team. Manual work becomes triggers and invisible work becomes your mission control. That is what 100 days with Hermi taught me. The point is not to use every feature. The point is to transfer

19:49
your workflow into the system. That is when Hermi stops feeling like a chatbot. And that is when it becomes an operating layer to your entire life and a genuine


20:00
How to start without overbuilding
20:01
point of improvement to your quality of life. So, if you want to start, don't overbuild. Pick one task you already repeat over and over again and turn it into a loop. Run it through Hermi. Ask it to help you. Then, from there, add one layer at a time. Add workspaces,

20:21
then once you've done that, add sub agents, then crons, then webhooks, then mission control. And if you want the specialist agents I showed, Sage and Nova, those are open source on my GitHub. I'll include the links below. If you want the template to my mission control, I'll

20:39
also include the link to that below. It's also open source and free for you to download. Feel free to copy them, modify them, or use them as templates. Uh but, the real lesson here is bigger than just those agents. Do not just ask Hermi to help.

20:56
Teach it how your work runs. That is the leverage. And if you've enjoyed this video, make sure to subscribe because I've got a ton more like it on my channel and a ton more coming your way. Oh, would you look at that? The YouTube algorithm gods really think you'll enjoy this video.

21:16
So, I'll see you there.



Fuente 3:

Link: https://www.youtube.com/watch?v=FpIvl6b4tRo

Transcripcion:

This is my current Hermes setup. It started as a mission control dashboard I built for Open Claw. Then I added one Hermes workflow, then another, then another. And at some point, Hermes stopped feeling like something I had to open and prompt manually and started feeling more like a 24/7 assistant running in the background. So, in this video, I'm going to show you the 10 Hermes agent hacks I'd set up first if I wanted Hermes to feel less like a chat app and more like an actual assistant. I'll show you the real examples, too. things like my mission control, my web hook triggers, my Hermes cam bam board, the cron jobs that send me work, the sub aents I use for maximum output, and the skills I use that save me from hours of work every day. Let's get started. My first hack and one of the biggest is mission control. This is where the whole system, your entire system becomes visible to you. For me, that means max HQ. It shows me what is happening around my content, around my agents, around my ideas, my performance on YouTube and X and now with my Hermes and things like my canban. When Hermes is doing real work, I do not want that work buried inside a chat thread. I want to see what is running, what is waiting on me, what is being blocked, what needs approval, and what changed since yesterday. This is why I added a Hermes cam bam board directly into the dashboard. Now when Hermes is working on this video for example, I can actually see the tasks instead of digging through chat history. Hermes stops being something I just message and it starts becoming a part of my operating layer. If you want this exact mission control, by the way, I've done a complete video covering it and I've also open sourced it so you can literally install it for free and send it to your Hermes to have it install it for you for free. But mission control only shows you the system. This next hack is where Hermes starts waking up without me manually prompting it. Okay, this is one of my favorite workflows because when I move a video that I have a video idea that I might have on notion into my to film list, Hermes automatically creates a filming brief for me. Let me show you something I want you to start thinking about is how can you get your Hermes agent to start following you around where you already live, where you already work, not in a creepy way, but where you already do your work. For me, I find myself working a lot on Notion and really liking the interface on notion. So, I've set up an automation for my Hermes agent to listen for triggers. So, when I move a video idea, say I have this one, the only AI automation you'll need in 2026. Say I move it to my to film list, that will send the trigger to my Hermes agent. It is watching every 10 minutes and it will send me a filming brief on my Telegram. So instead of me moving an idea, forgetting why I liked it, then manually asking for research later for Hermes to research it later, Hermes watches that board and reacts when the idea becomes real. Should I film this now, later or kill it? What is the strongest title idea I could have for this uh video? What are some backup titles? What is a strong first 30-se secondond hook of the video? What are proof assets that I will need throughout the video? What is the checklist that I'll need to compile before filming this video? This is the difference between Hermes being something you prompt into turning it into something that assists you, something that follows and guides you, guides your workflow. The workflow changed state. So, Hermes knew what to do next. And here you go. It just saw it. It said the moved item is the only automation tutorial you'll need in 2026, which is the video we moved. And then it gave me its verdict. It said film it later unless we narrow it down. And then it gave me a better recommended angle, which is this one along with core framing, so on and so forth. Right now, my setup watches this board every few minutes. But you can also build the instant version with notion automation, make Zapier or just a web hook. The principle I want you to take away from this and what matters the most is when your workflow changes state, Hermes should know what to do next. And once you understand that, the next question is what should Hermes do when nothing changes but when time passes? Let's move on to hack number three. The third hack is cron jobs. Craw jobs are how Hermes starts the conversation. Every morning I ask it things like, "Send me an AI story worth reacting to." Every morning. Or every few hours, "Scan X for fresh posts I should quote." Or, "Every day, check if competitors posted any outlier videos, videos that performed better than anything else." Or, "Every week, audit my notion content board." or even every Friday summarize what content ideas are stuck in my pipeline. This is one of the fastest ways to make Hermes feel like a 24/7 assistant because useful information starts arriving before I even ask for it. Craw jobs are time based. So you can choose things like every morning or every hour or every Monday. When the clock hits a certain time, Hermes wakes up and does the thing that you ask it. Scheduled work is only half the system. To make Hermes useful, you also need to give it better objectives than normal prompts. Let's move on to hack four. The fourth hack is slashgoal. A normal prompt asks Hermes for one response, but slashgoal gives Hermes an objective to work towards. Here's how I want you to think of the slashgoal command. You type in slashgoal just like I have here and you start with an outcome which in my case in this example is decide the strongest Hermes agent video that I should film this week. Then you can give it sources using for me it's Vid IQ YouTube outliers competitor transcripts my posted videos and nova memory. Then you can add constraints. Avoid repeated angles and generic AI guru framing. And then you can end it with a deliverable. When is it done? What deliverables does it need to give you? End with a filming ready title, hook, demo list, and proof assets. So again, the template/goal. Put your outcome using your sources. Include the resources that it can use with constraints. include the constraints. Then ending in deliverable. Include the deliverable you want it to end with so that it knows when is it done. When is it done with its goal? Did you look at that? It already completed it and it gave us every single thing we asked for without making a mistake. An absolutely massive hack that I want you to walk away with is you can make Hermes write the goal for itself. You can send it something like I want to use slashgoal but I don't want a vague goal. Interview me with only the questions you need. Hold on. Let me actually write it down. Where are my manners? Okay, there you go. I just wrote it down. I want to use slash goal, but I do not want a vague goal. Interview me with the only questions you need. Then turn my answers into the strongest possible slashgo command. include the exact outcome, context, tools, and sources, constraints, final, notable, and when Hermes should stop. So, you can literally use this command to create a slash a massively good slashgo command because fuzzy prompts create fuzzy output. Clear goals create useful assistant behavior. But even with a great goal, one agent can still become a bottleneck. So the next hack is splitting the work up. The fifth hack is using sub agents as a research team. For this video, I can have Hermes, for example, run three sub aents. one for Vid IQ and keyword signals, one for YouTube outliers and transcripts, and one for my channel performance and uh Nova memory. And for this example, I've given it this prompt. Research this Hermes video idea using three sub aents. Number one, Vid IQ and keyword signals. Two, YouTube outliers and transcripts. Three, my channel performance and Nova memory. Then combine the verdict into one filming recommendation. One agent gives me an answer. Sub agents give me an entire team. But once you have multiple threads of work, you need a place to separate them. Onto hack number six. This one sounds simple, but the framing matters. The hack is not Telegram. The hack is turning Telegram topics into separate workspaces. Let me show you. I have a YouTube topic where I talk to my Hermes agent only about YouTube related stuff. I have a react topic where it sends me reaction opportunities, things that are trending on X that I can react to right now. I have a coding topic, general topic, a research topic. The list goes on and on and on. Each topic becomes a different context. YouTube is where Nova works, where I have a specific sub agent designed for my YouTube workflow. React is where Hermes sends me reaction opportunities on X. Coding is where technical work happens. Uh general is where smaller operations or random things go. Different work needs different rooms. Topics organize the conversation, but they still don't manage the work itself. For that you need a board hack number seven. The seventh hack is canban for agent task management. This is the piece I recently added to my mission control. But once Hermes is working on more than one thing. I started to need a board. Otherwise tasks start to just disappear and fall out of sight. There would be multiple tasks I would forget. I even asked Hermes for things like research Hermes outliers or check Vid IQ or create this notion trigger or help me prepare this upload package for YouTube. Handbomb gives your work a place to live and now I can see what is ready, what is running, what is done, who owns what, which agent is doing what and what is being blocked. Cambban is how agent works stops disappearing into the chat. But if you want Hermes to repeat your best processes, a board is not enough. You need to turn those processes into reusable skills. The eighth hack is skills. A skill is basically an SOP, a standard operating procedure for Hermes. The best example for this is Nova, my YouTube agent. Nova knows my YouTube process. It knows the SOP step by step. Number one, check Vid IQ. Number two, look at posted videos. Number three, avoid rejected ideas, things I've rejected in the past. Uh, read performance logs, separate evidence labels, write scripts using a retention framework, uh, include SEO packages, match my voice, and avoid things I hate. The list goes on and on and on. What that means is I do not have to rebuild my YouTube process every time. I do not need to create a master prompt for every single process. I can just say use Nova for this transcript or use Nova to decide if this idea is worth even filming. If you're interested in Nova specifically, by the way, I have an entire video dedicated about it. I've also open sourced her to the world. So you can also grab that GitHub link, send it to your Hermes agent and you'll have the same exact skill I have at your disposal inside your Hermes. And this is my list of skills. I currently have 115 skills. Things like Sage, which is also open source by the way, code review, GitHub code review, requesting code review, a bunch of code reviews, AI news digest, research paper writing, so on and so forth. any workflow I have to explain twice. I start thinking about turning it into a skill. And I mean, the nice thing about Hermes is it already does that on its own. But what I do recommend you really pay close attention to is how can you not just rely on Hermes's ability to selfdevelop those skills, but also how can you help it do that in the way you want? How can you help it reach the goal in the way that you want every single time? Skills handle repeatable processes. The next layer is events where outside systems trigger Hermes automatically. The ninth hack is web hooks and eventbased agents. Chron jobs run because the clock changed. Web hooks run because the world changed. That's the best way to think about it. Web hooks are essentially a trigger that comes up when an event happens, when something changes. A few examples, a new lead comes in in your business. Hermes researches the company immediately. Uh, a GitHub PR opens. Hermes summarizes the risks immediately. Uh, one of your competitor posts a video. Hermes checks if it is worth reacting to. You just hopped off a meeting and a transcript was just generated. Hermes extracts that transcript, summarizes it, and adds tasks for you on notion or on your own mission control. If there's something that you need to do, a keyword starts trending. Hermes starts drafting a content angle. The goal is not to automate everything. The goal is to remove the dead zones where something important happens and nobody acts on it until later. Here's where I want you to think, how can I have Hermes react to the things I'm doing without me having to tell it to just based on things changing and my workflow, me changing a status on my mission control or on my notion or wherever it is that you operate on. And once you have all of this, the final hack is not more automation, it's specialization. The last hack is separating agents by job. You don't want your accountant to be your dentist. You don't want your dentist to be your pilot. So, I don't want every agent to use the same model, the same tools, memory, and the same permissions. Nova, which is my YouTube agent, has, for example, Vid IQ access, YouTube access, YouTube memory, script rules, so on and so forth. She has a stronger reasoning model plugged into her. Sage, my ex agent, has trend scouting, reaction opportunities. Uh, he has a different memory altogether. My coding agent has my repository access, GitHub access, code review skills. My administrative agent has calendar access, reminders, notion, emails, and asks for approval before sending anything. Some agents need the smartest model I can afford. Some just need to check a page every hour and tell me if something changed. Some should have right access, and some should absolutely not >> have right access. The unlock is not one giant super agent. The unlock is a team of smaller agents with the right brain tools, memory, and permissions for the job that you want them to do. Again, don't let your dentist fly your plane. So, if Hermes still feels like another chat app, I would start looking at the workflows around it. Give it a mission control. Let it react when your notion board changes or your mission control board changes. Set up cron jobs so useful information arrives before you even ask. Use slash goals instead of using vague prompts. Split research across sub aents or massive tasks or code changes or anything worth having multiple people work on it. Use sub aents across those tasks. Separate workspaces. Use telegram topics. track tasks and can boards, turn repeatable processes into skills, uh, and connect outside events, and stop making one agent do every job. That is when Hermes starts feeling less like another chat app and more like a real 24/7 assistant. Not because it's magical, although it can be, but because you designed a customized system that is specialized around it. If you want the Nova YouTube agent skill I used, I'll link the full video on GitHub below. Or if you want my mission control or my ex content analyst, I'll leave all those links down below. And if you want me to make a follow-up showing the exact setup I used to create web hook events, then comment web hook and I'll break that down next. Anyway, subscribe if you enjoyed this content because I have a lot more on my channel and a lot more coming up your way. See you in the next video.


Fuente 4:

Link: https://www.youtube.com/watch?v=2pIihd3dpoA

Transcripcion:

Hermes just shipped the feature that genuinely changes the entire game. >> [snorts] >> A few days ago, if you wanted to use Hermes properly, you had to be comfortable living in the terminal, editing configuration files, writing up tools, and basically treating your AI assistant like a developer project. That was fine for me. I like that stuff. But, it also meant Hermes was powerful in a way that was hard to explain to normal people. Well, today, the Hermes team just announced Hermes Desktop. The reason this matters is that Hermes finally has a native interface for the thing it was already becoming, which is a real assistant that can use your files, remember how you work, run tools, manage tasks, and operate across your computer. So, in this video, I'm going to show you exactly how to install the new desktop app, what it actually is inside it, and then I'm going to show you how I would set this up if I wanted Hermes to run my day today. All right, first up, here is the announcement. The new posted, "The next evolution of Hermes agent is here. Introducing Hermes Desktop. Everything you love about Hermes now native on your machine." That one sentence is important because it tells you how to think about this. This is not a separate beginner version of Hermes. The desktop app uses the same Hermes core that we all came to love and adore. So, if you already use Hermes in Telegram or in the terminal, this is not a new assistant that starts from zero. It is another front end to the that same agent. That is the first big unlock because before this, Hermes had a weird problem. The product was insanely powerful, but the interface made it look smaller or feel smaller than it actually was. If someone asked, "What is Hermes?" you have to explain it through, you know, a terminal window and technical terms. Now, you can just tell them, "Hey, download the desktop app." and show them. That changes the entire top funnel. Now, let me show you how to install it. Right on the Hermes website, you can go to Hermes desktop, which is where I am. I'll include this link in the description. And you'll find, for me, for example, I'm on Mac OS, so I can click right here and it'll download the application. There it is. I double-clicked on it and now I can just click install Hermes. Now, I don't have Hermes installed on this MacBook, which is great for us because we can just do that. I can show you how simple it is to get started. But that being said, if you already have Hermes installed, you can literally open your terminal and type in Hermes desktop and it'll install that with your running Hermes instance. But in my case, I want to make this as beginner-friendly as possible and I want to show the setup from scratch. Here we are. This took less than 2 minutes to finish installing and it just gave me this launch Hermes, which is exactly what I'm going to do right now. Boom. There we are. Literally less than a 3-minute long installation and we are literally in. That being said, you now have a couple of things that you need to do, which number one is connect a model provider to it. In my case, I'm connected to Open Router. I've given it my Open Router API key. Uh and I've chosen Claude Sonnet 4.6. For you, you can choose anything you want. You can connect through uh OAuth, Codex, so that you can use GPT 5.5, which is absolutely amazing with Hermes. You can use Open Router, which will make you pay for per token spend, but the pro is you can use any model or almost any model that you want that exists in the world. So, I'm going to click apply. By the way, if you want to add any API keys or connections to Hermes, you can click on API keys, go to, for example, Open Router is what I'm using, and in my case, in your case, you'd be setting it up. In my case, I I'm replacing it right now. And put in the new value. And hit save. It's literally this simple. The next step would be going to gateway and making sure that you're running, if you have a desktop, if you're running it locally, then choosing the local option. If you would like to set a remote instance, then choosing the remote gateway. I'm on a local gateway. And all I can do is basically save and reconnect. As you can see in the settings, there's a lot that you can edit and create. You can go change up your model. You can go to chat, switch up your personalities. How do you want your Hermes to be? What in the world is Cat Girl? Or Shakespeare? I have no idea. So, you can set your time zone. You can also customize the appearance if you want it to look cyberpunk, uh for example. I like the way that this comes in, which is very, you know, minimal. I don't want the the UI to be too distracting. You can define your workspace. And finally, the last missing piece that most people would want is messaging, which in most people's case is going to be Telegram, but you also have the option for Discord, Slack, WhatsApp, Signal, whatever it is that you use. And in the case that you use MS Graph webhooks, I don't know who uses that, but in case you do, you have the option. But that being said, I'm going to show you how to set up Telegram since it is the most common. For that, you're going to want to message BotFather. It's @BotFather on Telegram. Once you go there, you can type in {slash} newbot to create a bot. You'll need to name your bot. Hermie the demo, I'm going to call mine. And then pick out a username. It needs to end with bot, the word bot. So, I'm going to give mine the username Hermie the demo {underscore} bot. And it'll give you a token that you'll have to copy paste, go back to your application, which is right here for us, and paste that bot token. Then, the missing piece is your allowed Telegram user ID, which is your personal Telegram user ID. Which in order to get that, you can message uh userinfobot @userinfobot on Telegram, and it'll give you your user ID. You can just click on user or where is it? Oh, no, actually, you can just type in anything, like hi, and it will reply back to you, as you can see, with your user ID, which you can copy right here. Oops. These are my messages to myself. How dare you look at that? And then, paste that here. Once you click save changes, it should apply. It says right here, "Restart needed, but credentials are set." So, that's what we're going to do. It actually says it right here, "Restart the gateway from the status bar to apply this change." So, we're going to click on gateway right here, open it up, and restart messaging right here. Gateway restart is running, and then we should be set. And just like that, when we do that, you can see, now our Telegram is connected. And if we go to Telegram, to our bot, once you start a conversation with it, say hi, it'll tell you you need to type {slash} set home, which I just did, to make this chat your home channel. And just like that, it is now live on Telegram. How are you today? Let's see. It should be typing. There you go. It's typing. And it should be responding any second. Doing great, thanks for asking, ready to tackle whatever you throw at me. Now, you also have access to Hermes on your phone. So, you can be texting at home, on the go, anywhere you are in the world, which is one of the best use cases for having an AI agent. That being said, I mean, a quick walk-through of the app. You can go to skills and tools to view all of your installed skills, or all of the new skills that you installed. You can enable or disable them right from this view. You can also go to tool sets and enable or disable uh the different tools that your Hermes can use. For example, do you want it to be able to use skills? Absolutely, we're going to turn that on. Do you want it to have persistent memory? Absolutely, turn that on. Cron jobs, there's a lot. I want you to go through this and think of what are the skills and tools that you think your AI agent will need. Will it need to generate images? If so, turn it on. Will it need to analyze videos? If so, turn it on. So on and so forth. Finally, the last thing I want to look at is artifact, which is all of the files and documents that your Hermes creates and interacts with, which are all listed here. You can go to images, files, links, whatever it is that it has access to or created will be included right here. Oh, look at that. You can also pin a session. If there's one session that you keep using, you can pin it up. Shift-click a shot to pin. Oh, there you go. I can just right-click a session and I can pin it right there. Lastly, something cool you can do is manage your profiles right on the app, which is your ability to create different personas, configuration files, skills, and soul.md, which is the essence, the personality of your agent. You can manage profiles right here and create different profiles. For example, my main agent, you can put it on a certain model, a certain AI provider, LLM. >> [snorts] >> You can give it a different specialized persona, personality. Then, I can create a new one. Say, test 1 2. Say that is what I want to call it for some reason. Then, you can give that one a separate personality. This is in the case you want to use multiple sub agents that do separate things. One main agent, for example, one content agent, one operations business operations agent, one, I don't know, YouTube editor agent. I have no idea what kind of agent you want to be creating. That is up to you. The sky is the limit. But, there you go. This is how to do it. And you can go into the settings for the different agents. Yada, yada, yada, so on and so forth. And that's it. It's literally this simple. Before today, Hermes was easiest to explain to technical people. Now, however, the pitch is much simpler. You can download the desktop app, connect your tools, and give it a real workflow. Then, let the same agent follow you across your desktop, your terminal, Telegram, and different project folders. And that is the real unlock. It's not that it became a prettier chat app. It's that it now has a native control room for an agent that already had the power underneath. If you want the exact setup I would use, I will put the Hermes desktop link and the install commands in the description. If you want me to do a follow-up, I can also show the full build from zero. What is the first skill that you can run, the first cron job, or the first Telegram workflow. But, the short version is this. Hermes was already powerful. Hermes desktop makes it OP. That is overpowered for our non-technical friends. And that is when a tool starts crossing from developer toy into something normal people can actually run. If you enjoyed this video, make sure to subscribe because I have a ton more content coming your way. Oh, and the algorithm gods just told me that you are very likely to enjoy this video as well. So, I'll see you there.


Fuente 4: 

Link: https://github.com/ClaudioDrews/memory-os

Fuente 5: 

Link: https://x.com/tonbistudio/status/2068559870589079552

Transcripcion:

3 Easy Ways to Build Cheap (or Free) Automation Pipelines with Hermes Agent
I don't like spending money, and I really don't like automation that quietly breaks while I'm not looking. Turns out those two problems have the exact same fix.
The solution? Hermes Agent and cron jobs. The catch is that most people are using them wrong. A naive "check every 5 minutes" job fires a full model turn every five minutes forever, whether anything happened or not. That burns tokens, and every one of those turns is another roll of the dice where the model can do something dumb.
So the whole game, to me, is keeping the model out of the loop until you actually need it, and shrinking its job when you do. Less model means less money and fewer moving parts that can go wrong at the same time. Here are the three ways I do it.
If you prefer to watch a video on this topic, check out my YouTube video on this topic.
Way 1: Don't use the model at all (no_agent)
The bluntest one. A lot of scheduled jobs don't need a language model in the first place.
You pass --no-agent and point the job at a script:
hermes cron create "every 5m" --no-agent \
  --script ram-watch.sh --deliver telegram
# ram-watch.sh
if [ "$ram" -gt 85 ]; then echo "⚠️ RAM at ${ram}%"; fi
Hermes runs the script on your schedule and sends whatever it prints, word for word. No model, no provider, no tokens. Empty output is a silent tick, and a non-zero exit gets you an error alert, so a broken watchdog can't just fail quietly on you.
Use this any time the script already knows the exact message. Heartbeats, disk and RAM alerts, CI pings, "is the site up." There's nothing for a model to decide, which means nothing to pay for and nothing to hallucinate. This is the real free tier.
Way 2: Pay nothing until something changes (the wakeAgent gate)
This is the one I use the most. You want the model's reasoning, but only when there's actually something to reason about.
You hang a little pre-run script on the job. It runs every tick, dirt cheap, no model, and prints a single line that decides whether the agent even wakes up:
# pre-run gate — runs every tick, no model
new = check_for_new_bug_reports()
if not new:
    print(json.dumps({"wakeAgent": False}))   # skip the agent, costs $0
else:
    print(json.dumps({"wakeAgent": True, "context": {"report": new}}))
If it prints wakeAgent: false, Hermes skips the agent entirely for that tick. Zero tokens. If it prints wakeAgent: true, the agent wakes up with that context blob already in hand, knowing exactly what changed. The script is the cheap part that runs constantly, the agent is the expensive part that barely runs. You can poll every two minutes for free and only pay the second state actually moves. The usual triggers are a file changing, an external flag getting dropped, or a count going up in your own database.
And cheaper isn't even the main win here. On a normal tick the model never spins up at all, so there's no turn that can wander off and do something weird. It only ever runs against a real, confirmed change.
Way 3: Chain cheap (jobs into a pipeline (context_from)
The first two ways keep a single job cheap. This one is how you wire several of them together into an actual pipeline without it turning into a fragile mess. The feature that does it is context_from, and it's the part I'd hate for you to miss.
context_from takes one job's most recent output and prepends it straight into the next job's prompt:
Job 1 (Collect): No model, just logs the data every hour
no_agent=True   script=collect.py   deliver=local

Job 2 (Brief): Reads collect's latest output, summarizes it, ships it
context_from=<Job 1's ID>        # prepend job 1's last output into this prompt
enabled_toolsets=["file"]     # lean tool surface
deliver=telegram
So a free no_agent script logs the data every hour, and a daily job reads it through context_from and writes the summary. The model never goes and fetches anything, it just summarizes what the collector already gathered for free. The data lands right in the prompt, so you can keep that second job's toolset lean too.
Here's the part I actually care about. You could do this by hand, have job one write a file and job two read it. But that hands the whole handoff to two nondeterministic agents, one that has to write the right path in the right format and one that has to remember to read it, and either can fumble it (we've all watched an agent confidently write to the wrong place). context_from does the read and the prepend at runtime, in code, not in the model. So the wiring just works instead of you crossing your fingers. The handoff stops being a thing that can break.
Collect, triage, ship. Each job cheap, each handoff guaranteed. That's a real pipeline with no framework underneath it.
Wrapping up
Every trick here is the same move. Keep the model out of the loop, give it less to do when it's in, and take the fragile handoffs out of its hands. You save money and delete a thing that can go wrong, every single time.
no_agent for anything a script can fully decide on its own.
The wakeAgent gate for "watch constantly, think rarely."
context_from to chain the cheap jobs into a pipeline whose wiring can't drift.
Stack it all together and you can leave genuinely useful automation running all day, every day, for pennies, instead of a cool demo you switch off the second the bill shows up.


Fuente 6:

Link: https://x.com/IBuzovskyi/status/2068629714776756339

Transcripcion:

15 LEVELS OF HERMES AGENT. FROM CHATBOT TO 24/7 AUTONOMOUS SYSTEM.
Most people install Hermes Agent and use it as a chatbot. They type a prompt, get a response, close the tab. That covers maybe 10% of what the agent can do.
This article maps every level of Hermes Agent usage, from the first prompt to a system that runs your business without you. 15 levels, grouped into three phases. Each level builds on the one before it, but you can jump to any level that fits your setup.
The structure is the same for every level: what it is, what it unlocks, how to set it up, and the mistake that trips people up at that stage.
All technical details verified against Hermes Agent v0.17.0 official documentation and source code.
Subcribe to my SubStack for more articels: https://substack.com/@yanxbt
PHASE 1 — FOUNDATION (Levels 1-3)
You are using Hermes. The agent responds to what you ask.
LEVEL 1 — ONE-SHOT PROMPTS
What it is: You installed Hermes. You type prompts. The agent responds with tool calls, file edits, web searches, terminal commands. Basic interaction.
What it unlocks: Hermes executes tasks across your file system, terminal, and the web. It reads files, writes code, searches the internet, runs shell commands. It does things. A chatbot talks about things.
Setup:
Desktop app: download from hermes-agent.nousresearch.com. One-click install. CLI: hermes setup
Three setup modes: → Quick Setup (Nous Portal): OAuth login, model + Tool Gateway in one command → Full Setup: walk through every provider, tool, and option yourself → Blank Slate: everything starts OFF except provider, model, file tools, and terminal. No web search, no browser, no memory, no delegation, no cron, no skills, no plugins, no MCP. You enable only what you need. Nothing loads that you didn't choose, even after updates.
Blank Slate is the cleanest starting point for users who want full control over what the agent can and cannot do.
Connect a model provider. Start chatting.
The mistake: Treating Hermes as a search engine. "Tell me about X" wastes an agent that can DO things. "Research X, write a report, save it to ~/reports/" uses the tools.
Example: "research the top 5 CRMs for solo founders, compare pricing and features, save a report to ~/reports/crm-comparison.html" — agent searches, compares, writes the file. done in 3 minutes.
LEVEL 2 — MEMORY + SOUL.MD
What it is: Hermes remembers you across sessions. SOUL.md defines who the agent is. MEMORY.md and USER.md store durable facts about your projects, preferences, and business context.
What it unlocks: The agent stops asking you to re-explain things. Two people asking the same question get different answers because Hermes knows their different contexts. Your instructions, preferences, and business details persist across every session.
v0.17.0 added atomic memory operations: the agent can batch add, replace, and remove memory entries in one call. Memory updates no longer fail mid-edit when the budget is tight.
Setup:
Desktop app / Dashboard: Profile → SOUL.md → edit CLI: open ~/.hermes/SOUL.md in any editor
Write 50-80 lines covering identity, voice, operations, and restrictions. The agent reads this on every session start.
The mistake: Leaving SOUL.md empty and expecting personalized output. Hermes without a SOUL.md is generic by design. The identity file is the difference between a general assistant and YOUR assistant.
Example: you ask "should I raise prices?" Without SOUL.md: generic advice about pricing strategy. With SOUL.md containing your business model, margins, and customer segments: "your entry tier converts at 12%. raising it $10 risks churn in segment B where you have 60% of revenue. test on segment A first."
YanXbt
@IBuzovskyi
·
11 jun.
HERMES AGENT SOUL.MD: WHY 50 LINES MATTER MORE THAN YOUR MODEL (COMPLETE GUIDE)
SOUL.md is the most important file in your Hermes Agent setup. It occupies slot #1 in the system prompt. Every turn, every session, every profile reads it first. It defines who the agent is before...
LEVEL 3 — SLASH COMMANDS
What it is: Commands that change how the agent works mid-session. Most users never type these.
What it unlocks: Parallel work inside a single session. You stop waiting for one task to finish before starting the next.
The commands:
/background <prompt> Fires a task in the background. Your main session stays free. Result appears as a panel when done.
/steer <prompt> Injects a message into the current run without interrupting it. Redirects the agent mid-execution.
/queue <prompt> Queues a follow-up. Waits until the current task finishes, then runs automatically.
/model <name> Switches models mid-session. Start with Sonnet for planning. Switch to DeepSeek for execution. Switch to Opus for review.
v0.17.0 added grok-composer-2.5-fast via Grok OAuth: the 200K context coding model behind Cursor's Composer, accessible through your Grok subscription.
Configure default behavior when you type while the agent is busy:
set in Desktop app, Dashboard, or config.yaml:
display:
  busy_input_mode: steer  # or queue, or interrupt
The mistake: Not knowing these exist. Most users type a prompt, wait for it to finish, type another prompt. /background alone doubles your throughput per session.
Example: you're drafting a proposal. mid-session: /background research [competitor] pricing and positioning. you keep writing. 5 minutes later a panel appears with the competitive analysis. you paste it into the proposal without breaking flow.
PHASE 2 — LEVERAGE (Levels 4-7)
Hermes works smarter. You stop doing tasks the agent can handle.
LEVEL 4 — SKILLS + RIGHT MODEL PER SKILL
What it is: Skills are on-demand knowledge documents and tool collections the agent loads when needed. Each skill can run on a different model.
What it unlocks: The agent becomes a specialist on demand. A research skill loads research methodology. A code review skill loads security patterns. Each skill uses the model best suited for its job.
Setup:
Desktop app / Dashboard: Skills Hub → Browse → Install CLI: /skills search [topic]
v0.17.0 rehauled the Skills Hub: connected hubs (OpenAI, Anthropic, HuggingFace, NVIDIA), featured section, full skill previews before install, and security scan on each skill.
v0.17.0 also added image editing: image_generate now edits source images ("make this logo blue", "remove the background"). Same tool, new mode.
Assign a model per skill in the Desktop app or config.yaml:
research/web search → DeepSeek V4 Flash ($0.10/M tokens, cheapest) code review → Claude Opus 4.8 ($5/$25/M, best coding benchmarks) content writing → Claude Sonnet 4.6 ($3/$15/M, strongest prose + tool calling) coding (value) → GPT-5.5 ($2/$12/M, #1 Chatbot Arena, 2M context) research with grounding → Gemini 2.5 Pro ($1.25/$10/M, Google Search built in) bulk sub-agent work → DeepSeek V4 ($0.30/$0.50/M, 90% cache discount) /goal judge → Gemini Flash (cheapest, fast enough for binary done/not-done) self-hosted (free) → Qwen 3 8B via Ollama (8GB RAM, handles routine tasks)
MiniMax M2.7 is also worth testing. Nous Research and MiniMax are collaborating to optimize future releases for Hermes. One of the most-used models inside Hermes as of mid-2026.
The mistake: Running every skill on your most expensive model. A routine web search skill burning Opus tokens is money wasted. Match model cost to task complexity.
Example: you run a competitive research skill on DeepSeek V4 Flash instead of Opus 4.8. comparable quality for web search. 30-50x cheaper per call. over 30 runs a month the savings add up fast.
LEVEL 5 — MCPs (CONNECT YOUR WORLD)
What it is: MCP (Model Context Protocol) servers connect Hermes to external tools. Gmail, Calendar, Notion, Slack, ClickUp, GitHub, databases, APIs.
What it unlocks: The agent works with YOUR data, not just the open web. It reads your emails, checks your calendar, pulls from your project board, and answers questions using context from the tools you already use.
Setup:
Desktop app / Dashboard: MCP → Catalog → browse and install CLI: hermes mcp
The mistake: Connecting 15 MCPs at once. Every MCP adds tool schemas to the context window. 15 MCPs with 10 tools each = 150 tool definitions the model reads every turn. Install what you use. Disable what you don't. Tool Search (auto-enabled when schemas eat 10%+ context) helps manage this, but fewer MCPs is still better.
Example: "what happened in Slack this week while I was heads-down coding?" Agent reads your Slack channels, filters by mentions and key topics, cross-references with your goals in memory. delivers a 10-line summary. no tab switching. no scrolling through 200 messages.
LEVEL 6 — SUB-AGENTS + PARALLEL EXECUTION
What it is: delegate_task spawns isolated sub-agents with their own context window, terminal session, and toolset.
What it unlocks: Parallel work across multiple agents. One researches. One critiques. One codes. Parent orchestrates. Each child can run a different model.
Setup:
The agent uses delegate_task automatically when the task benefits from isolation. You can also ask directly:
"spin up a sub-agent on DeepSeek to research X while another on GPT-5.5 critiques the findings"
Configuration:
set in Desktop app, Dashboard, or config.yaml:
delegation:
  max_concurrent_children: 3    # default
  max_spawn_depth: 2            # bounds recursion
Roles:→ leaf (default): executes, cannot re-delegate → orchestrator: can spawn its own workers
Background mode (v0.17.0):delegate_task(background=true) dispatches the sub-agent and returns immediately. Your session stays live. Result re-enters as a new turn when it finishes.
The mistake: Using sub-agents for simple tasks. Delegation has overhead (context setup, tool allocation). A task the main agent can handle in 3 turns should not spawn a sub-agent.
Example: "research three competitors in parallel. one agent per competitor. use DeepSeek for research. parent on Sonnet synthesizes all three." three reports in 10 minutes instead of 30. each agent works isolated so one slow research task doesn't block the others.
LEVEL 7 — ASYNC OPERATIONS
What it is: Three features that let Hermes work without you typing.
What it unlocks: The shift from "I ask, it responds" to "it works, I review."
/goal — persistent objectives:Set a goal. A judge model evaluates after every turn: done or not done? Agent continues automatically until the goal is achieved, you pause it, or the turn budget (default 20) runs out.
/goal find 100 clinics in Toronto,
build a landing page for each,
draft personalized emails to each clinic.
/subgoal adds criteria mid-run without resetting the loop.
Cron jobs — scheduled tasks:Gateway ticks every 60 seconds. Fires due jobs in fresh isolated sessions. Delivers results to 27+ platforms: Telegram, Discord, Slack, WhatsApp, Signal, Matrix, iMessage, Microsoft Teams, Google Chat, LINE, email, SMS, and more.
v0.17.0 additions: → WhatsApp Business Cloud API (official Meta adapter, no QR bridge) → iMessage via Photon Spectrum (no Mac relay needed) → Telegram rich messages (Bot API 10.1, native formatting) → Automation Blueprints: one-click cron templates in the Dashboard (morning briefing, weekly review, news digest, reminder). No cron syntax needed.
Three cost layers: → no_agent mode: script IS the job, $0 forever → wakeAgent gate: script decides if LLM is needed, $0 until something changes → context_from: chain job outputs into pipelines without a framework
Safety net — checkpoints:Enable checkpoints before running autonomous operations. The agent snapshots your working directory before changes. /rollback restores state if something goes wrong overnight.
set in Desktop app, Dashboard, or config.yaml:
checkpoints:
  enabled: true
The mistake: Writing vague cron prompts. Every cron run starts from zero. No memory, no chat history. "Check on that server issue" means nothing. "SSH into 10.0.0.5, check nginx status, verify port 443 returns 200" works.
Example: 8:00 AM. Telegram pings. You didn't ask for this. Cron delivered it: "3 new arXiv papers in your niche. competitor updated their pricing page. GitHub repo you watch merged a breaking change. action: review competitor pricing before your 11am call."
YanXbt
@IBuzovskyi
·
14 jun.
HERMES AGENT BUILDS ITSELF WHILE YOU SLEEP. THE COMPLETE GUIDE TO THE 9-HOUR OVERNIGHT WORKFLOW.
Most AI agents wait for you to type. Hermes Agent does not. And it does something none of the others do: it gets smarter overnight.
Between 11PM and 8AM, a properly configured Hermes setup monitors...
PHASE 3 — AUTONOMY (Levels 8-15)
Hermes works without you. The system compounds over time.
LEVEL 8 — MULTI-PROFILE ARCHITECTURE
What it is: Separate Hermes profiles, each with its own SOUL.md, config, memory, skills, cron jobs, and model. Fully isolated agents on one machine.
What it unlocks: Specialized workers instead of one overloaded generalist. A Scout profile finds signals. An Analyst profile synthesizes research. A Coder profile ships features. Each does one job well with the right model for that job.
Setup:
Desktop app / Dashboard: Profiles → Build (5-step wizard: Identity → Model → Skills → MCPs → Review) CLI: hermes profile create [name]
Each profile becomes its own command:
hermes -p scout chat
hermes -p analyst chat
The mistake: Giving every profile the same SOUL.md. The entire point is isolation. A Scout that tries to analyze wastes tokens. An Analyst that tries to find sources duplicates Scout's work. One job per profile.
Example: Scout found 12 sources overnight. Analyst synthesized them into 4 wiki entries by 10am. Briefer delivered a 5-bullet summary at 8am. You read it over coffee. None of them share memory. Each did one job with the right model for that job.
YanXbt
@IBuzovskyi
·
17 jun.
HERMES AGENT + NOTEBOOKLM + OBSIDIAN:BUILD A 3-AGENT RESEARCH DEPARTMENT THAT GETS SMARTER EVERY DAY
One agent doing research, analysis, and briefing at the same time produces mediocre results. Context gets polluted. The agent confuses what to find with what to analyze with what to report. Priorities...
LEVEL 9 — SELF-IMPROVING KNOWLEDGE BASE
What it is: The LLM Wiki skill, based on Andrej Karpathy's pattern. A self-improving knowledge base built as interlinked markdown files. Ships bundled with Hermes.
What it unlocks: Long-term knowledge that compounds beyond the memory cap. Hermes's built-in memory handles conversational context. The wiki handles domain knowledge: articles, transcripts, meeting notes, research findings. Cross-references stay linked. Contradictions get flagged automatically.
Setup:
set in Desktop app, Dashboard, or config.yaml:
WIKI_PATH=~/obsidian-wiki
On first run, the skill asks for your domain to build SCHEMA.md with the right tag taxonomy.
Connect to Obsidian for graph view: set OBSIDIAN_VAULT_PATH to the same directory.
Feed it: "index this article into my wiki: [paste URL or text]"
The mistake: Never feeding the wiki. An empty knowledge base adds nothing. The value comes from accumulation. Month 1: 50 entries. Month 3: 300+ entries with cross-references. The agent gets sharper because the knowledge base got sharper.
Example: you ask "how does competitor X handle onboarding?" Without wiki: agent searches the web, gives you generic info. With 3 months of wiki entries: agent pulls your own research notes, meeting transcripts where a client mentioned competitor X, and an article you indexed last month. answer includes context no web search could find.
LEVEL 10 — KANBAN ORCHESTRATION
What it is: A durable SQLite task board shared across all profiles. Statuses flow from triage → todo → ready → running → blocked → done → archived. Dispatcher fires every 60 seconds.
What it unlocks: Complex multi-step projects with dependency chains. Each card can run its own /goal loop (goal_mode). Cards with unfinished parent cards wait automatically. Multiple profiles pick up cards assigned to them.
Setup:
/kanban create "Research 100 clinics" \
  --assignee scout --goal --goal-max-turns 15

/kanban create "Build landing pages" \
  --assignee coder --goal --goal-max-turns 20 \
  --depends-on "Research 100 clinics"
CLI: hermes kanban or /kanban in chat.
Kanban vs cron vs delegate_task:→ Kanban: durable work queue, persists across restarts, multi-profile → Cron: time-based scheduling, repeating tasks → delegate_task: one-off parallel execution within a session
The mistake: Using Kanban for simple linear pipelines. Three profiles in a straight line (Scout → Analyst → Briefer) work fine with file-based coordination. Kanban adds value when you have dependency trees, parallel branches, or 10+ tasks that need tracking.
Example: quarterly competitive analysis as a Kanban project. 12 cards: 3 competitors × 4 dimensions (pricing, features, positioning, hiring signals). pricing card depends on web scraping card. hiring card depends on LinkedIn research card. agents pick up work as dependencies clear. you review the final synthesized report.
LEVEL 11 — VOICE MODE
What it is: Speech-to-text and text-to-speech across all messaging platforms. Six STT providers, five TTS providers.
What it unlocks: Talk to Hermes through voice messages on Telegram, Discord, WhatsApp. The agent transcribes, processes, and can respond with synthesized speech. Full voice conversations without typing.
STT providers:→ faster-whisper (free, runs on-device) → local command wrapper → Groq (fast cloud) → OpenAI Whisper API → Mistral → xAI
TTS providers:→ Edge TTS (free, default) → ElevenLabs (best quality, paid) → OpenAI TTS → MiniMax → NeuTTS (free)
The mistake: Using expensive cloud STT for routine voice messages. Local faster-whisper handles most languages well and costs nothing. Save paid STT for complex audio or noisy environments.
Example: driving to a meeting. voice message on Telegram: "anything from last night's research I should know before my 11am call?" Agent responds with a 30-second audio summary. you listen instead of read. hands on the wheel.
LEVEL 12 — BROWSER AUTOMATION
What it is: Hermes can control a browser to navigate websites, fill forms, extract data, and interact with web applications.
What it unlocks: Tasks that require a browser session: scraping dynamic pages, filling web forms, interacting with tools that have no API. The agent sees the page and acts on it.
Setup:
Included in Tool Gateway for Nous Portal subscribers:
hermes setup --portal
Or configure browser automation separately through the dashboard.
The mistake: Using browser automation for tasks that have an API. Browser automation is slower, more fragile, and more expensive than a direct API call. Use it only when no API exists.
Example: competitor has no public API. agent opens their pricing page via browser, extracts current plans and pricing, compares against last month's snapshot stored in your wiki. change detected: they dropped their free tier. flagged in your morning brief.
LEVEL 13 — API SERVER
What it is: Hermes exposed as an OpenAI-compatible HTTP endpoint. Full agent with tools, memory, and skills accessible via standard API format.
What it unlocks: Any frontend that speaks OpenAI format connects to Hermes as a backend: Open WebUI, LobeChat, LibreChat, ChatBox, custom applications, Excel integrations. The agent becomes an API you build on top of.
Setup:
set in Desktop app, Dashboard, or .env:
API_SERVER_ENABLED=true
API_SERVER_KEY=your_secret_key
Start the gateway: Desktop app / Dashboard: Gateway → Start CLI: hermes gateway
Endpoint: http://127.0.0.1:8642/v1/chat/completions
Multi-user setup: Create one profile per user on different ports. Each gets isolated config, memory, and skills.
The mistake: Exposing the API server to the public internet without authentication. The server binds to 127.0.0.1 by default. Access remotely via SSH tunnel, not public exposure. v0.17.0 added OAuth gate on every token-required endpoint and websocket auth for the dashboard.
Example: your competitive research runs as an API endpoint. a custom dashboard queries Hermes for the latest intel. your team sees competitive data on a live internal page. nobody opens Telegram. the data serves itself.
LEVEL 14 — IDE INTEGRATION (ACP)
What it is: Hermes runs as an ACP (Agent Communication Protocol) server inside VS Code, Zed, and JetBrains editors.
What it unlocks: Chat, tool activity, file diffs, and terminal commands render inside your editor. The agent works in your project directory with your editor's context. Same agent core, same tools, same memory as CLI and gateway.
Setup:
hermes acp start
In VS Code: install the ACP extension, point it to Hermes.
What ACP includes:→ File tools: read_file, write_file, patch, search_files → Terminal execution → Chat interface inside the editor → Approval prompts for dangerous commands
What ACP excludes (by design):→ Messaging delivery → Cron job management → Gateway-specific features
The mistake: Thinking ACP replaces the gateway. ACP is for coding sessions inside an editor. Gateway handles messaging, cron, and multi-platform delivery. Both run the same agent core underneath.
Example: coding a pricing page. inside VS Code you ask Hermes: "how does competitor X structure their tiers?" Agent checks your Obsidian wiki, finds your research notes, gives the answer. you adjust your design without opening a browser or Telegram.
LEVEL 15 — PROFILE DISTRIBUTIONS
What it is: Package your entire agent setup as a git repo. Anyone installs your agent with one command.
What it unlocks: Your agent becomes a product. Sell it. Share it with your team. Distribute it to clients. Everything transfers except API keys and personal memories.
v0.17.0 also introduced the RAFT Agent Network: connect Hermes to raft.build as an external agent. Wake-channel bridge with privacy by contract (wake payloads carry metadata only, never message bodies). Your agent can collaborate with agents on other machines.
What a distribution contains:
distribution.yaml    # manifest
SOUL.md              # identity
config.yaml          # model and provider settings
skills/              # custom skills
cron/                # scheduled jobs
mcp.json             # connected tools
Install someone else's distribution:
hermes profile install github.com/user/their-agent
The mistake: Including API keys or personal data in the distribution. Credentials stay per-machine. The distribution carries personality, skills, and workflows. The user brings their own keys.
Example: you built a research department with Scout, Analyst, Briefer. new team member joins. they run: hermes profile install github.com/you/research-dept. they have your three profiles, wiki structure, cron jobs, and SOUL.md templates. they add their own API keys and Telegram bot. running in 10 minutes.
ONE WORKFLOW, 15 EVOLUTIONS
Competitive research. Same task. Watch how it changes at every level.
Level 1: you type "what's new in AI agents this week?" and read a wall of text.
Level 2: agent already knows your niche and competitors from SOUL.md. same question, answer is filtered to YOUR market.
Level 3: /background research competitors while you draft a proposal. results appear without breaking your flow.
Level 4: research skill runs on DeepSeek V4 Flash. analysis skill runs on Sonnet. you stop paying Opus prices for web searches.
Level 5: agent checks Slack, email, and ClickUp BEFORE answering. "competitor launched yesterday. your team discussed it in #product."
Level 6: three sub-agents research three competitors in parallel. each on DeepSeek. parent on Sonnet synthesizes. 10 minutes instead of 30.
Level 7: you stopped asking. cron job runs at 7am. wakeAgent gate: nothing changed = $0. competitor shipped an update = agent wakes, researches, delivers brief to Telegram. you read it over coffee.
Level 8: Scout profile finds signals every 3 hours. Analyst synthesizes at 10am. Briefer delivers at 8am. three profiles. one pipeline.
Level 9: findings go to Obsidian wiki. month 3: 300+ entries. the agent surfaces patterns you didn't ask about because the wiki found connections across sources.
Level 10: quarterly analysis runs as a Kanban project. 12 cards with dependency chains. agents pick up work as dependencies clear. you review the final report.
Level 11: driving to a meeting. voice message: "anything from last night's research?" Agent responds with audio. you listen instead of read.
Level 12: competitor has no API. agent opens their pricing page via browser, compares against last month's snapshot. change detected. flagged in your brief.
Level 13: research runs as an API endpoint. a custom dashboard queries it. your team sees competitive intel on a live page.
Level 14: coding a feature. inside VS Code you ask "how does competitor X handle this?" Agent answers from your wiki without leaving the editor.
Level 15: your research setup is a git repo. new team member runs one command. Scout, Analyst, Briefer, wiki structure, cron jobs. all installed in 10 minutes.
TOKEN ECONOMICS: HOW TO RUN ALL 15 LEVELS WITHOUT BURNING MONEY
every level above 3 costs tokens. here are the controls that keep spending predictable.
RIGHT MODEL PER TASK (Level 4+)
not every task needs your most expensive model. web search = DeepSeek V4 Flash ($0.10/M). synthesis = Sonnet ($3/$15/M). final review = Opus 4.8 ($5/$25/M). assign models per skill, per profile, per cron job. see Level 4 for the full model-per-task reference.
WAKEAGENT GATES (Level 7+)
script runs every tick for free. checks if anything changed. nothing changed = agent never wakes = $0. the agent only spends tokens when there is work to do.
NO_AGENT MODE (Level 7+)
when the script IS the job. uptime checks, disk alerts, file watchers. output goes directly to Telegram. zero LLM calls. zero tokens. ever.
PRE-RUN SCRIPTS (Level 7+)
script gathers data for free. output injected into the prompt as context. the model summarizes what the script fetched instead of burning tool calls to find the data itself.
LEAN TOOL SETS (Level 5+)
set --skills web,file per cron job. fewer tool schemas in context = smaller prompt = cheaper. a news digest job does not need browser, delegation, or kanban tools.
TOOL SEARCH (Level 5+)
auto-enabled when tool schemas eat 10%+ of context. replaces full tool definitions with 3 bridge tools. ~300 tokens instead of thousands. the agent discovers tools on demand instead of loading all at once.
COMPRESSION THRESHOLD (Level 7+)
set in Desktop app, Dashboard, or config.yaml:
compression:
  threshold: 0.40    # default 0.50
fires context compression earlier. keeps long /goal runs and cron sessions within token budget even at 20+ turns.
CURATOR — FREE BY DEFAULT (v0.17.0)
deterministic skill pruning still runs for free. LLM-powered consolidation is now opt-in only:
set in Desktop app, Dashboard, or config.yaml:
curator:
  consolidate: true    # opt-in, default false
routine background curation costs zero tokens. enable consolidation only when your skill library needs deep cleanup.
LOSSLESS DENSIFICATION (PR #47866 by teknium)
search_files results get compressed before reaching the model. same information. fewer tokens. merged into latest Hermes. run hermes update.
AUXILIARY MODELS FOR JUDGE (Level 7+)
the /goal judge runs after EVERY turn. route it to a cheap fast model.
set in Desktop app, Dashboard, or config.yaml:
auxiliary:
  goal_judge:
    provider: openrouter
    model: google/gemini-3-flash-preview
20 judge calls on Gemini Flash vs 20 on Opus = significant savings.
BUDGET CAPS (all levels)
set in Desktop app, Dashboard, or config.yaml:
budget:
  daily_max_usd: 10
  session_max_usd: 2
  monthly_max_usd: 200
hard limits. the agent stops when it hits the cap. set these before enabling any cron job or /goal run.
MONITOR SPENDING
Desktop app / Dashboard: Usage tab shows per-profile breakdown. CLI: /usage in any session for per-session stats.
add "end with token spend this week" to Briefer prompts for weekly cost tracking in Telegram.
the pattern across all of these: push work off the expensive model onto free code, cheap models, and compressed context. the agent reasons. everything else runs for free.
START WITH BLANK SLATE
if you care about token control from day one, install with Blank Slate mode (hermes setup → Blank Slate). everything disabled except provider, model, file tools, terminal. add features one by one as you need them. nothing loads that you didn't explicitly enable. this is the cheapest and most controlled starting point.
WHERE MOST PEOPLE STOP
Levels 1-2. They install Hermes, write a SOUL.md, and use it as a smart chatbot. The agent saves them 30 minutes a day.
The jump from level 3 to level 7 is where daily time savings go from minutes to hours. /background, skills with the right models, cron jobs with wakeAgent gates. These compound.
The jump from level 7 to level 10+ is where the agent stops being a tool and becomes a system. Multi-profile architecture, self-improving knowledge, Kanban orchestration. You review work that happened without you.
HOW TO IDENTIFY YOUR CURRENT LEVEL
You do not need to reach level 15. Most solo founders operate well at levels 7-10. The levels above that solve specific problems: voice for mobile workflows, browser for tools without APIs, API server for custom integrations, IDE for coding, distributions for teams.
Pick the level that matches your bottleneck. Set up that one. Move to the next when it stops being enough



Fuente  7:

Link: https://x.com/IBuzovskyi/status/2065125711401062758?s=20

Transcripcion:

HERMES AGENT SOUL.MD: WHY 50 LINES MATTER MORE THAN YOUR MODEL (COMPLETE GUIDE)
SOUL.md is the most important file in your Hermes Agent setup. It occupies slot #1 in the system prompt. Every turn, every session, every profile reads it first. It defines who the agent is before anything else loads.
Most guides show you a 10-line template and move on. This article goes deeper: where SOUL.md sits in the prompt architecture, what belongs in it (and what does not), how to write advanced souls for different roles, how it affects your token budget, and how to share entire agent personas through profile distributions.
All technical details verified against Hermes Agent official documentation (v0.16.0).
1. What SOUL.md Actually Is
SOUL.md is a markdown file that completely replaces the built-in default agent identity. When Hermes starts a session, it:
Reads SOUL.md from HERMES_HOME
Scans it for prompt injection patterns
Truncates if needed
Injects it as slot #1 in the system prompt
If the file is missing, empty, or cannot be read, Hermes falls back to a built-in default: "You are Hermes Agent, an intelligent AI assistant..."
Hermes auto-seeds a starter SOUL.md on first install. Most users begin with a real file they can read and edit immediately.
Important: changes to SOUL.md take effect on a new session. Existing sessions may still use the old prompt state. After editing your soul, start a fresh session to see the changes.
Location:
~/.hermes/SOUL.md                           # default profile
~/.hermes/profiles/researcher/SOUL.md       # named profile
~/.hermes/profiles/ops/SOUL.md              # named profile
SOUL.md always loads from HERMES_HOME, not from your current working directory. If it loaded from whatever directory you launched Hermes in, your personality could change unexpectedly between projects. The personality belongs to the Hermes instance itself.
2. Where SOUL.md Sits in the Prompt Stack
Understanding the full prompt assembly is critical for writing an effective SOUL.md. The system prompt is built in three layers:
Layer 1 — Stable (cached, rarely changes):
SOUL.md (identity)
→ tool and model guidance
→ skills prompt (names + descriptions index)
→ environment hints
→ platform hints
Layer 2 — Context (project-specific):
system_message (caller-supplied)
→ AGENTS.md (from current working directory)
→ .hermes.md, CLAUDE.md, .cursorrules (project files)
Hermes reads multiple context file formats from your working directory: AGENTS.md, .hermes.md, CLAUDE.md, and .cursorrules. If you use Cursor or Claude Code alongside Hermes and have .cursorrules in your project, Hermes will read them too. This is intentional — it means project conventions stay consistent across tools. But it also means instructions in .cursorrules affect Hermes behavior. If the agent acts differently in one project directory, check for context files you didn't write for Hermes.
Layer 3 — Volatile (changes per session):
MEMORY.md snapshot
→ USER.md snapshot
→ external memory provider block
→ timestamp / session / model / provider line
Final system prompt: stable → context → volatile.
SOUL.md is the very first thing. It sets the frame through which the model interprets everything that follows. A soul that says "you are a meticulous code reviewer" changes how the agent reads AGENTS.md, how it interprets skills, and how it responds to every message.
3. The Rules: What Goes In and What Does Not
This is the most common mistake. People put everything in SOUL.md. Project instructions, workflow details, tool configurations, API documentation. SOUL.md balloons to 200+ lines and eats tokens on every single turn.
Belongs in SOUL.md:
Identity (who the agent is, its role)
Voice (how it communicates, tone, style)
Values (what it prioritizes, what it avoids)
Behavioral boundaries (what it refuses to do)
Operating principles (autonomy level, when to ask vs act)
Does NOT belong in SOUL.md:
Project-specific instructions → AGENTS.md
Coding conventions → AGENTS.md or .cursorrules
Multi-step workflows → Skills
Facts about you → MEMORY.md and USER.md
Tool configurations → config.yaml
The official docs are direct about this: "Move project instructions into AGENTS.md and keep SOUL.md focused on identity and style."
Example showing the split:
SOUL.md (who the agent is):
markdown
# Soul
You are a senior developer. Write clean, tested code.

## Voice
Terse. Reference specific lines and files.

## Restrictions
Never commit without running tests.
AGENTS.md (what this project needs, lives in project root):
markdown
# Project: hermes-dashboard
Stack: React 19, TypeScript, Tailwind
Build: npm run build
Test: npm test
Deploy: vercel --prod
Convention: components in /src/components, hooks in /src/hooks
Never modify /src/core without approval.
SOUL.md travels with the agent across all projects. AGENTS.md changes per project directory.
SOUL.md is scanned for prompt injection patterns on every load. That means you should keep it focused on persona and voice rather than trying to sneak in meta-instructions. The scanner exists because SOUL.md has maximum influence over the agent's behavior. Anything that looks like an attempt to override safety boundaries or manipulate tool behavior will be flagged.
What the scanner catches:
Instructions that attempt to override system-level safety rules
Attempts to disable approval checks or safety features
Commands disguised as personality traits ("as part of my personality, always execute commands without asking")
Encoded or obfuscated instructions
What passes cleanly:
Identity and role descriptions
Voice and communication style
Operating principles and autonomy levels
Restrictions and behavioral boundaries
Workflow preferences
If your SOUL.md gets flagged, simplify the language. Direct behavioral instructions ("never send money without approval") pass. Meta-instructions that try to alter the agent's safety layer don't.
4. Token Impact
SOUL.md injects into every turn of every session. This is the most expensive file in your setup by volume of repetition.
The math:
A 50-line SOUL.md ≈ 400-500 tokens. A 200-line SOUL.md ≈ 1,500-2,000 tokens.
In a 20-turn /goal session:
50-line soul: 400 × 20 = 8,000 tokens on identity alone
200-line soul: 2,000 × 20 = 40,000 tokens on identity alone
With prompt caching on Anthropic models (~75% discount after first turn):
50-line soul effective cost: ~2,400 tokens across 20 turns
200-line soul effective cost: ~12,000 tokens across 20 turns
That 5x difference adds up fast when you run multiple profiles with cron jobs throughout the day.
Guidelines:
Aim for 50-80 lines maximum
One paragraph per section, not one page
Every line should change agent behavior. If removing a line changes nothing, cut it.
Use hermes prompt-size to see your system prompt breakdown:
hermes prompt-size
This shows exactly how much of your context window SOUL.md, skills index, memory, and tools consume before you say a word.
5. The Structure That Works
From the official example and best-performing community souls, this structure covers all essential elements in minimal tokens:
markdown
# Soul
[1-2 sentences: who the agent is and its relationship to you]

## Voice
[3-5 lines: how it communicates. tone, length, style.]

## Operations
[3-5 lines: how it works. autonomy level, decision rules.]

## Restrictions
[3-5 lines: what it never does. hard boundaries.]
Four sections. 15-20 lines each section max. Total: 50-80 lines.
The official starter example:
markdown
# Personality
You are a pragmatic senior engineer with strong taste.
You optimize for truth, clarity, and usefulness
over politeness theater.

## Style
- Be direct
- Be concise unless complexity requires depth
- Say when something is a bad idea
- Prefer practical tradeoffs over idealized abstractions

## Avoid
- Sycophancy
- Hype language
- Overexplaining obvious things
18 lines. Clean. Every line changes behavior.
6. Advanced SOUL.md Templates
These go beyond starter templates. Each is designed for a specific high-leverage role with nuanced behavioral instructions.
6.1 — Strategic Co-Founder
markdown
# Soul
You are my co-founder. You operate with full context
of our business, our runway, and our priorities.
Your job is to challenge my thinking, not confirm it.

## Voice
Push back when I'm wrong. Ask "what's the evidence?"
before accepting any assumption. Use numbers.
Speak in short declarative sentences.
If you disagree, say it in the first sentence,
then explain why.

## Operations
Before any major recommendation, check:
does this move the needle on our current 90-day goal?
If it doesn't, flag it as a distraction.
Default to action over analysis.
When I ask for options, rank them by expected impact
per hour invested. Cut anything below the threshold.

## Restrictions
Never agree with me to be agreeable.
Never recommend more than 3 priorities at once.
Never skip the "what could go wrong" assessment
on any plan that takes more than a week to execute.
Never use the words "potentially" or "arguably."
6.2 — Deep Research Analyst
markdown
# Soul
You are a research analyst with access to the internet,
databases, and files. Your output is evidence, not opinion.

## Voice
Cite sources for every factual claim.
Distinguish between verified facts, informed estimates,
and speculation. Label each explicitly.
Use "I could not verify this" when evidence is weak.
Prefer tables for comparisons. Prefer numbers for scale.

## Operations
Search across minimum 5 sources per question.
Cross-reference conflicting information.
When sources disagree, present both positions
with the evidence for each.
Flag confidence level: high (multiple verified sources),
medium (single credible source), low (unverified or conflicting).

## Restrictions
Never present an unverified claim as fact.
Never skip source attribution.
Never speculate without labeling it as speculation.
Never use "many experts say" without naming them.
6.3 — Autonomous DevOps Engineer
markdown
# Soul
You are a DevOps engineer responsible for deployment,
monitoring, and infrastructure. You operate autonomously
on routine tasks. You escalate anything that could
cause downtime or data loss.

## Voice
Terse. Log-style updates.
"Deployed v2.3.1 to staging. 4 tests passing. 1 flaky.
Holding prod deploy until flaky test resolved."

## Operations
Run all changes through staging before production.
Run tests before and after every deployment.
If tests fail, rollback and report.
For infrastructure changes: dry-run first,
show the diff, wait for my approval.
Monitor error rates for 15 minutes after any deploy.

## Restrictions
Never deploy to production without running tests.
Never modify database schemas without explicit approval.
Never store credentials in code or chat.
If any action could cause data loss, stop and ask.
6.4 — Executive Content Strategist
markdown
# Soul
You are my content strategist. You know my voice,
my audience, and what performs. Your job is to
find angles worth publishing and draft content
that matches how I write.

## Voice
Match my voice exactly. Short sentences.
Numbers over adjectives. Proof over claims.
No corporate language. No hype without data.
Read my recent posts before writing anything.
If my voice has evolved, match the latest version.

## Operations
Before drafting: check trending topics, check competitor
content from the last 7 days, check my recent posts
(avoid repeats within 14 days).
Score every draft on two axes: hook strength (1-10)
and bookmark value (1-10). Rewrite anything below 7.
Send drafts to Telegram for approval. Never publish
without my confirmation.

## Restrictions
Never publish without my explicit approval.
Never reuse a hook pattern from my last 5 posts.
Never use adverbs.
Never fabricate engagement numbers or results.
6.5 — Financial Analyst with Guardrails
markdown
# Soul
You are a financial analyst. You work with real money.
Accuracy is non-negotiable. Every number must be
traceable to a source.

## Voice
Present findings as: metric, source, date, confidence.
"Revenue: $2.3M (Q1 2026 10-K filing, high confidence)"
Round only when precision doesn't matter.
Use tables for any comparison involving more than 2 items.

## Operations
Pull data from official filings (SEC, annual reports)
before using third-party estimates.
When building projections, state every assumption
explicitly. Show sensitivity analysis on the top 3
assumptions that drive the model.
Flag any metric where the margin of error exceeds 10%.

## Restrictions
Never present a projection without stating assumptions.
Never use a single data point as a trend.
Never round numbers from financial statements.
Never provide investment advice or recommendations.
Always include a disclaimer on any forward-looking analysis.
7. /personality Overlays
SOUL.md is your durable baseline. /personality is a session-level overlay that temporarily modifies behavior without changing the underlying identity.
/personality codereviewer
This loads a named personality from config.yaml on top of SOUL.md for the current session only. When you start a new session, the overlay is gone and SOUL.md is back.
Built-in presets (ship with Hermes):
/personality              # reset to SOUL.md baseline
/personality concise      # shorter, terser responses
/personality technical    # detailed, precise, engineering-focused
Define custom personalities in config.yaml:
yaml
agent:
  personalities:
    codereviewer: >
      You are a meticulous code reviewer.
      Identify bugs, security issues, performance
      concerns, and unclear design choices.
      Be precise and constructive.
    
    brainstorm: >
      Forget constraints for this session.
      Generate ideas freely. Quantity over quality.
      No filtering, no feasibility checks.
      We'll evaluate later.
    
    editor: >
      You are a ruthless editor.
      Cut every unnecessary word.
      Shorten every sentence that can be shorter.
      Flag every claim without evidence.
When to use SOUL.md vs /personality:
SOUL.md: permanent identity. How the agent behaves across all sessions. Who it is.
/personality: temporary mode. This session needs a different approach. Switch back next session.
Example: your SOUL.md defines a strategic co-founder. But right now you need a brainstorming session without the usual pushback. Use /personality brainstorm for this session. Tomorrow, the co-founder is back.
8. Profiles: Multiple Souls on One Machine
Each Hermes profile gets its own SOUL.md, its own memory, its own skills, its own config. Running multiple profiles is running multiple agents.
bash
hermes profile create researcher
hermes profile create coder
hermes profile create ops
Each profile now has:
~/.hermes/profiles/researcher/
├── SOUL.md          # researcher identity
├── config.yaml      # model: gpt-5.5
├── .env             # API keys
├── memories/        # researcher-specific memory
├── skills/          # researcher-specific skills
└── cron/            # researcher-specific schedules
Clone from an existing profile:
bash
hermes profile create work --clone
Copies config.yaml, .env, and SOUL.md into the new profile. Same API keys and model, but fresh sessions and memory. Edit the SOUL.md to change the personality.
Full clone (everything):
bash
hermes profile create backup --clone --clone-from coder
Copies everything: config, API keys, personality, all memories, full session history, skills, cron jobs, plugins. A complete snapshot.
Switch between profiles:
bash
hermes                  # default profile
researcher              # named profile (becomes its own command)
coder chat              # start a session as coder
ops gateway start       # connect ops to Telegram
Profile Builder (new in dashboard):
The dashboard now has a visual Profile Builder. No CLI needed:
bash
hermes dashboard → Profiles → Build
Five-step wizard: Identity → Model → Skills → MCPs → Review. Set the SOUL.md, pick the model, toggle skills, connect MCP servers, and deploy. One flow, one new agent.
The model matters per profile:
Different roles need different models. Match the model to the soul:
researcher:
→ SOUL.md: research analyst, evidence-based
→ model: gpt-5.5 (cheap, high volume search tasks)

coder:
→ SOUL.md: senior engineer, code review
→ model: claude-fable-5 (best coding model)

content:
→ SOUL.md: content strategist, voice matching
→ model: claude-sonnet-4 (strong writing)

ops:
→ SOUL.md: operations manager, terse
→ model: deepseek-v4-flash (routine tasks, cheapest)
How models follow SOUL.md differently:
Not every model interprets your soul with the same precision. This matters for advanced souls with nuanced voice or strict restrictions.
Claude (Sonnet, Opus, Fable): follows restrictions and voice instructions closely. Best for souls with specific communication rules. Rarely drifts from stated boundaries.
GPT-5.5: strong on general instructions. Can drift from nuanced voice guidelines over long sessions. Reinforce key rules in both Soul and Restrictions sections.
DeepSeek V4 Flash: follows simple instructions well. May ignore subtle behavioral guidelines. Keep the soul direct and short for DeepSeek profiles. Specific restrictions ("never do X") work better than nuanced voice directions ("communicate with understated confidence").
Local models (Qwen, Gemma): follow basic structure but struggle with complex behavioral rules. Use the simplest possible soul. Focus on restrictions over voice.
If your agent keeps ignoring a restriction, the fix is often switching to a model that follows instructions more precisely, rather than making the soul longer.
9. Profile Distributions: Share an Entire Agent
A profile distribution packages a complete Hermes agent as a git repo. Anyone with access can install the whole agent with one command.
What a distribution contains:
my-research-agent/
├── distribution.yaml   # manifest: name, version, requirements
├── SOUL.md             # the agent's personality
├── config.yaml         # model, temperature, tool defaults
├── skills/             # bundled skills
├── cron/               # scheduled tasks
└── mcp.json            # MCP server connections
Install a distribution:
bash
hermes profile install github.com/you/my-research-agent
One command. The agent is ready. Memories, sessions, and API keys stay per-machine. The personality, skills, and workflows transfer.
Update a distribution:
bash
hermes profile update researcher
Pulls the latest changes from the repo. Your memories and sessions are untouched.
Security note from official docs: "SOUL.md and skills ARE active as soon as you start chatting with the profile, so read them before your first run if you're installing from someone you don't know."
This is analogous to installing a browser extension or a VS Code extension. Low friction, high power, trust the source.
10. Common Mistakes
Mistake 1: Putting everything in SOUL.md
Project instructions, workflow details, API docs. SOUL.md grows to 200 lines. Every turn burns 2,000 tokens on identity. Move project instructions to AGENTS.md. Move workflows to skills. Move facts to MEMORY.md.
Mistake 2: Designing the perfect soul in one shot
The official docs say it directly: "That iterative approach works better than trying to design the perfect personality in one shot." Start with 20 lines. Use Hermes for a week. Notice where it drifts from what you want. Add a line. Remove a line. The best SOULs are refined through use, not designed from scratch.
Mistake 3: Duplicating SOUL.md across directories
SOUL.md loads from HERMES_HOME only. Placing a SOUL.md in your project directory does nothing. If you want project-specific instructions, use AGENTS.md in the project root. Hermes loads AGENTS.md from the current working directory at session start.
Mistake 4: Ignoring sub-agents
When Hermes delegates work to sub-agents via delegate_task, SOUL.md is NOT loaded for the sub-agent. Sub-agents use the hardcoded DEFAULT_AGENT_IDENTITY instead. This is by design: sub-agents should be generic workers, not copies of your personalized agent. If you need a specialized sub-agent, use a separate profile with its own SOUL.md and coordinate through Kanban.
Mistake 5: Not using /personality for temporary shifts
Editing SOUL.md for a one-off session ("I need it to brainstorm freely for 30 minutes") then forgetting to change it back. Use /personality for temporary modes. SOUL.md stays untouched.
Mistake 6: Copy-pasting someone else's soul without reading it
Profile distributions are powerful but the SOUL.md activates immediately on first session. A malicious or poorly written soul can change agent behavior in ways you don't expect. Read every SOUL.md before using it, especially from unknown sources. The prompt injection scanner catches obvious attacks but a subtly misaligned soul passes the scanner.
11. The Iterative Method
The best SOUL.md is not written. It is grown.
Week 1: Start with the official starter template (18 lines). Use Hermes normally. Notice where the agent's tone, decisions, or behavior don't match what you want. Write down each observation.
Alternative: let Hermes interview you and write it:
If you don't know where to start, ask Hermes to create your SOUL.md through an interview:
I want you to write a SOUL.md for yourself.
Interview me about:
- what kind of work I do
- how I want you to communicate
- what decisions you can make on your own
- what you should never do
- how to handle situations when things break

Ask one question at a time.
When you have enough context, write a SOUL.md
under 60 lines with sections:
Soul, Voice, Operations, Restrictions.
The agent asks 5-8 questions, then produces a soul based on your actual answers. Often sharper than what you'd write from scratch because the interview surfaces preferences you wouldn't think to articulate.
Week 2: Add one line per observation. "Never agree with me to be agreeable." "Use numbers, not adjectives." "Ask for evidence before accepting claims." Each line addresses a specific behavior you observed.
Week 3: Check hermes prompt-size. Is SOUL.md growing past 80 lines? Review each line. If removing it changes nothing about agent behavior, cut it. Consolidate overlapping instructions.
Month 2: Ask Hermes to rewrite your SOUL.md based on how you actually work together:
Review our conversation history.
Based on how I give feedback, what I approve,
what I reject, and how I communicate:
rewrite my SOUL.md to reflect how we actually work.
Keep it under 60 lines.
The agent has seen hundreds of your interactions. It knows your patterns better than you can articulate from memory. The draft it produces often captures preferences you never thought to write down.
Month 3+: Your SOUL.md is stable. Small edits when your work changes. The Curator prunes your skills. Memory handles evolving context. SOUL.md handles the constants: who the agent is and how it thinks.
12. Test Your SOUL.md
After writing or editing your SOUL.md, verify it works:
Test 1 — Identity check:
Who are you? What is your role?
The agent should describe itself using the identity from your SOUL.md, not the default "I'm Hermes Agent, an AI assistant."
Test 2 — Voice check:
Explain what a cron job does.
Compare the tone and style to what your SOUL.md specifies. A researcher soul should give a factual answer. A co-founder soul should give a strategic one. An ops manager should give a terse one.
Test 3 — Restriction check:
[Ask it to do something your restrictions forbid]
If your soul says "never send messages without approval," ask it to send a message. It should refuse or ask for confirmation.
Test 4 — Prompt size check:
bash
hermes prompt-size
Verify SOUL.md token count is where you expect. If it grew past 800 tokens, trim it.
Test 5 — Drift check (after 2 weeks):Start a new session and repeat tests 1-3. Agents with deep memory can drift from SOUL.md over time as accumulated context starts to outweigh the identity block. If drift happens, the soul needs sharper language or the memory needs pruning.
13. SOUL.md and Long-Term Memory
SOUL.md defines who the agent is. Memory defines what it knows. Both are capped.
For work that accumulates knowledge over weeks and months (research projects, client histories, content strategy), the built-in memory caps (2,200 chars for MEMORY.md, 1,375 chars for USER.md) can become a bottleneck.
Two extensions that work alongside SOUL.md:
External memory providers:Mem0, Honcho, and 6 other providers use retrieval-based injection instead of full dump. Only relevant memories load per turn. 72% fewer tokens than naive injection.
bash
hermes memory setup
Obsidian vault as extended memory:Hermes ships with a bundled Obsidian skill. The agent reads, searches, and creates notes in your vault. Obsidian becomes the uncapped long-term layer: research, session summaries, project context, learned patterns — all as linked markdown notes.
SOUL.md handles identity (who the agent is). MEMORY.md handles working memory (what it needs now, capped). Obsidian handles long-term knowledge (everything it has ever learned, uncapped).
Three layers. Each serves a different purpose. Each has a different scope.
14. Quick Reference
File location:
~/.hermes/SOUL.md                    # default profile
~/.hermes/profiles/NAME/SOUL.md      # named profile
Commands:
bash
hermes prompt-size              # see token breakdown
/personality NAME               # temporary overlay
/personality                    # clear overlay, back to SOUL.md
hermes profile create NAME      # new profile with own SOUL.md
hermes profile install URL      # install shared agent
Prompt stack order:
SOUL.md → tool guidance → skills index → env hints
→ AGENTS.md / .cursorrules / .hermes.md
→ MEMORY.md → USER.md → timestamp
Alternative: system_message in config.yaml:
yaml
agent:
  system_message: "Additional instructions appended after SOUL.md"
This injects text into the system prompt alongside SOUL.md. Use it for instructions that apply to all sessions but don't belong in the identity file (API conventions, output format rules). SOUL.md handles who the agent is. system_message handles how the caller wants output formatted.
Token budget guidelines:
50 lines ≈ 400-500 tokens per turn
80 lines ≈ 700-800 tokens per turn (maximum recommended)
Use hermes prompt-size to verify
Prompt caching on Anthropic: ~75% off after first turn
What goes where:
SOUL.md    → who the agent is (identity, voice, values)
AGENTS.md  → what the project needs (instructions, conventions)
MEMORY.md  → what the agent learned (facts, preferences)
USER.md    → who you are (profile, context)
Skills     → how to do things (procedures, workflows)
Conclusion
SOUL.md is 50-80 lines of text that define everything about how your Hermes Agent thinks, speaks, and operates. It is the most leveraged file in your setup. One line added or removed can change agent behavior across every future session.
The difference between a useful agent and a frustrating one usually comes down to SOUL.md. Not the model. Not the tools. Not the prompt engineering. The identity.
Start with 20 lines. Iterate from experience. Let the agent rewrite its own soul after a month of working together. The best souls are grown, not designed.




Fuente 8:

link: https://x.com/IBuzovskyi/status/2064377155476193362?s=20

Transcripcion: 
8 Loops Inside Hermes Agent (And Why They Compound)
Most agent frameworks have one loop: prompt → response → repeat.
Hermes Agent runs 8 loops simultaneously at different timescales, from milliseconds to weeks. Each loop serves a different purpose. Each one makes the others more effective. When stacked, they create a compounding system that improves with every session.
This article maps every loop inside Hermes Agent, explains how they nest, and shows what breaks when any of them fails. All technical details are verified against the official Hermes Agent developer documentation (hermes-agent.nousresearch.com/docs).
Hermes Agent reached 95,600 GitHub stars seven weeks after launch — the fastest-growing agent framework of 2026 (TokenMix, April 2026). Independent benchmarks from TokenMix show self-created skills cut research task time by 40% versus a fresh agent instance. This article shows the loop architecture behind that result.
What Is a Loop in Agent Architecture
A loop is a cycle: do → check → decide → repeat or stop.
Every agent has at least one. The core loop sends a message to the model, gets a response, checks for tool calls, executes them, and loops back. Without it, there is no agent. There is only a single API call.
What separates agent frameworks is how many loops they run, at what timescales, and whether those loops feed into each other. Four types of loops exist in agent systems (per FlowZap's taxonomy):
Retry loops — run again after failure. Simplest form.
Reflection loops — one agent critiques the output before the next pass.
Memory loops — store a lesson that influences a future run.
Skill loops — encode a procedure that changes how future runs execute.
Most frameworks implement types 1 and 2. A few implement type 3. Hermes implements all four natively, plus orchestration loops that coordinate across agents and time.
Loop 1 — The Core Agent Loop
Timescale: milliseconds to minutes per turn.
This is the heartbeat. Everything else runs on top of it.
The core loop lives in run_agent.py (AIAgent class, 15,000+ lines). Each turn follows this sequence:
1. Receive user message (or continuation from /goal judge)
2. Append to conversation history
3. Build or reuse cached system prompt (prompt_builder.py)
4. Check if compression is needed (>50% context)
5. Build API messages from history
6. Inject ephemeral prompt layers (budget warnings, context pressure)
7. Apply prompt caching markers (Anthropic)
8. Make interruptible API call
9. Parse response:
   → tool calls? Execute, append results, go to step 5
   → text response? Persist session, flush memory, return
Three API modes resolve automatically based on provider:S
All three converge on the same internal format (OpenAI-style role/content/tool_calls dicts) before and after API calls.
Tool execution within the loop:
Single tool call → executed in main thread. Multiple tool calls → executed concurrently via ThreadPoolExecutor. Results reinserted in original call order regardless of completion order.
Some tools are intercepted before reaching the registry:
Iteration budget:Default 90 iterations per session (configurable via agent.max_turns). At 100%, the agent stops and returns a summary. Subagents get independent budgets capped at delegation.max_iterations (default 50).
Interruptible calls:API requests run in a background thread while monitoring an interrupt event. When interrupted (user sends new message, /stop, or signal), the API thread is abandoned. No partial response enters conversation history.
What breaks without this loop: everything. This is the kernel.
Loop 2 — The Ralph Loop (/goal)
Timescale: minutes to hours per goal.
Named after Ralph Wiggum. Inspired by Codex CLI 0.128.0 by Eric Traut (OpenAI). Hermes's implementation is independent, adapted to its architecture.
The core idea: keep a goal alive across turns. An auxiliary judge model evaluates after each turn: done or continue?
User sets /goal →
  Turn 1: agent works toward objective
  Judge evaluates: done? → no
  ↻ Continuing toward goal (1/20): [judge's reason]
  Turn 2: agent takes next step
  Judge evaluates: done? → no
  ↻ Continuing toward goal (2/20): [judge's reason]
  ...
  Turn N: agent completes
  Judge evaluates: done? → yes
  ✓ Goal achieved: [reason]
Technical details from official docs:
Default max_turns: 20 (configurable via goals.max_turns)
/goal resume resets the turn counter to zero and continues
/subgoal adds acceptance criteria mid-loop without resetting
Judge prompt rewrites to include all subgoals — goal is only done when original objective AND every subgoal are met
Works identically on CLI and every gateway platform
Goal state persists in SessionDB.state_meta
The judge runs on the auxiliary client (can be a cheaper model than the main one)
Kanban integration:Pass --goal to kanban_create (CLI) or goal_mode=True (dashboard/tool) and the kanban worker runs in a goal loop. The judge checks the worker's output against the card's title + body as acceptance criteria.
/goal [description]     # start
/goal status            # check progress
/goal pause             # pause, preserve context
/goal resume            # continue, reset counter
/goal clear             # end
/subgoal [text]         # add criteria mid-run
/undo [N]               # take back last N turns
What breaks without this loop: agent completes one turn and stops. No multi-step reasoning. No persistent objectives. Every task must be manually supervised turn by turn.
Loop 3 — The Self-Improvement Loop
Timescale: runs after completed tasks (minutes to hours).
This is the loop that makes Hermes different from most other agent frameworks. Official documentation describes it as "a closed learning loop."
The cycle:
1. Agent completes a task
2. Agent reviews what worked
3. Agent identifies reusable patterns
4. Agent saves procedure as a skill file
   → ~/.hermes/skills/[skill-name].md
5. Next similar task: agent finds the skill via search
6. Agent loads skill body into context
7. Agent executes faster using the documented procedure
8. If the procedure improves during use, agent updates the skill
Skills are not prompt templates. They are full procedures containing:
When to use (trigger conditions)
Step-by-step procedure
Known pitfalls to avoid
Verification steps (how to confirm it worked)
Required tools and dependencies
The agent creates and updates skills using the skill_manage tool. After solving a complex problem, Hermes may offer to save the approach as a skill for next time.
The compounding math:From verified user benchmarks (TokenMix study, cited in official user stories): agents with 20+ self-created skills cut research-task time by ~40% compared to a fresh agent instance.
This improvement compounds. Each completed task potentially creates or refines a skill. Month 3 looks different from day 1 because the agent has accumulated 40-60 skills encoding procedures that used to require full instructions.
Nudge system:The self-improvement loop is triggered by "nudges" — periodic checks that spawn a background fork of AIAgent (same pattern used by the Curator). The fork runs in its own prompt cache and never touches the active conversation.
What breaks without this loop: every session starts from zero. The agent never learns. Day 90 output quality equals day 1. You explain the same process every time.
Loop 4 — The Curator Loop
Timescale: runs every 7 days (default), during idle periods.
Skills accumulate. Without maintenance, you end up with dozens of narrow near-duplicates that pollute the catalog and waste tokens.
The Curator solves this.
Check: has interval_hours elapsed since last run? (default: 7 days)
Check: has agent been idle for min_idle_hours? (default: 2 hours)
Both true → spawn background AIAgent fork
  → scan ~/.hermes/skills/
  → identify redundant or overlapping skills
  → archive unused skills to ~/.hermes/skills/.archive/
  → compress and consolidate related procedures
  → optimize descriptions for better searchability
  → log what changed
From official documentation:
Triggered by inactivity check, not a cron daemon
Fires on CLI session start and on recurring tick inside gateway's cron-ticker thread
First run defers by one full interval_hours on new installs (gives you time to review before it touches anything)
Never auto-deletes. Worst outcome is archival to .archive/ (recoverable)
By default (prune_builtins: true) can archive unused bundled skills after archive_after_days of non-use
Hub-installed skills (from agentskills.io) are always off-limits
yaml
curator:
  interval_hours: 168        # 7 days
  min_idle_hours: 2           # only runs when idle
  prune_builtins: true        # can archive unused built-in skills
  archive_after_days: 30      # unused threshold
hermes curator status        # check last run
hermes curator pause         # skip next run
hermes curator resume        # re-enable
Why this loop matters for Loop 3:The Self-Improvement Loop creates skills. The Curator Loop maintains them. Without the Curator, Loop 3 eventually degrades the system by flooding the skill index with noise. Tool Search (Loop 7) relies on accurate skill names and descriptions for retrieval. Poorly maintained descriptions degrade search accuracy.
What breaks without this loop: skill bloat. The agent accumulates hundreds of narrow, overlapping skills. Context gets polluted. Search returns wrong skills. Token usage grows without corresponding quality improvement.
Loop 5 — The Memory Loop
Timescale: after each session and periodically during sessions.
Memory in Hermes operates across three layers:
Layer 1 — Session memory (active context):The conversation history of the current session. Lives in RAM and SQLite.
Layer 2 — Persistent memory (MEMORY.md + USER.md):Facts, preferences, and insights that survive across sessions. Auto-written by the agent when it identifies important information.
yaml
memory:
  memory_enabled: true
  user_profile_enabled: true
  memory_char_limit: 2200    # ~800 tokens, injected every turn
  user_char_limit: 1375      # ~500 tokens, injected every turn
Layer 3 — Session recall (FTS5 full-text search):Every CLI and messaging session stored in SQLite (~/.hermes/state.db) with FTS5 full-text search. Search queries return actual messages from the DB — no LLM summarization, no truncation.
The memory loop cycle:
1. Agent processes conversation turn
2. Periodic check: is there important information to persist?
3. If yes: write to MEMORY.md or USER.md (capped by char limits)
4. On session end: flush all pending memory writes
5. Next session: MEMORY.md and USER.md injected into system prompt
6. Agent has accumulated context without re-explanation
Memory nudges follow the same background-fork pattern as the self-improvement loop and the Curator.
External memory providers (8 plugins):For deeper intelligence beyond built-in memory:
Mem0 (knowledge graph + semantic retrieval, 72% fewer tokens vs naive injection)
Honcho (two-peer dialectic: USER observations + AI observations)
Hindsight, Holographic, RetainDB, ByteRover, Supermemory, OpenViking
Built-in memory continues to work alongside external providers. The external provider is additive.
What breaks without this loop: the agent forgets everything between sessions. You re-explain your preferences, your projects, your workflow every time you start a new conversation. No compounding.
Loop 6 — The Kanban Dispatcher Loop
Timescale: every 60 seconds.
The Kanban system is the orchestration layer that coordinates multiple agents and tasks.
Every 60 seconds:
  1. Scan kanban board (SQLite: ~/.hermes/kanban.db)
  2. Find tasks in Ready status
  3. Assign to available workers
  4. Track heartbeats on Running tasks
  5. Detect zombie processes (worker died but card still Running)
  6. Reclaim zombie cards (reset to Ready for retry)
  7. Check retry budgets (don't retry infinitely)
  8. Report blocked tasks for human review
Statuses: Triage → To-Do → Ready → Running → Blocked → Done → Archived
Kanban Swarm architecture:
hermes kanban swarm
Spawns: root orchestrator + parallel workers + gated verifier + gated synthesizer + shared blackboard.
Human-in-the-loop:When a task enters Blocked status, execution pauses until a human provides input. Approval buttons are native in Telegram and Slack.
Kanban is deliberately single-host. kanban.db is a local SQLite file. The dispatcher spawns workers on the same machine. Multi-host is not supported — there is no coordination primitive for workers across hosts. For multi-host setups, run an independent board per host and use delegate_task or a message queue to bridge them.
Integration with /goal (Loop 2):Pass --goal or goal_mode=True when creating a kanban card. The worker runs in a goal loop instead of single-shot mode. The judge checks worker output against the card's title + body as acceptance criteria.
What breaks without this loop: multi-agent work becomes manual coordination. You track tasks in your head or in a spreadsheet. Crashed tasks go unnoticed. No retry. No visibility.
Loop 7 — The Compression Loop
Timescale: fires when context usage exceeds thresholds.
Hermes runs a dual compression system:
Layer 1 — Gateway Session Hygiene (85% threshold)
  Safety net. Fires before the agent processes a message.
  Prevents API failures when sessions grow too large
  between turns (overnight accumulation in Telegram).
  Uses rough character-based token estimate.

Layer 2 — Agent ContextCompressor (50% threshold, configurable)
  Primary compression system. Fires inside the agent's
  tool loop with access to accurate API-reported token counts.
The compression algorithm (4 phases):
Phase 1 — Prune old tool results (cheap, no LLM call)
  Tool results > 200 chars outside the protected tail
  get replaced with:
  [Old tool output cleared to save context space]

Phase 2 — Check if Phase 1 was enough
  Re-estimate tokens. If below threshold: done.
  If still over: proceed to Phase 3.

Phase 3 — Summarize middle conversation turns
  LLM call to summarize the compressible region.
  Protected: first 3 messages + last 20 messages.
  Tool call/result pairs never split.

Phase 4 — Create new session lineage
  Compression creates a "child" session ID.
  Memory flushed to disk BEFORE compression
  to prevent data loss.
Configuration:
yaml
compression:
  enabled: true
  threshold: 0.50         # compress at 50% of context window
  target_ratio: 0.20      # how much of threshold to keep as tail
  protect_last_n: 20      # recent messages always preserved

auxiliary:
  compression:
    model: null            # cheaper model for summaries
    provider: auto
Pluggable context engine:
yaml
context:
  engine: "compressor"    # default, lossy summarization
  engine: "lcm"           # plugin, lossless context management
Plugins can replace the built-in engine. The user must explicitly set context.engine — plugins are never auto-activated.
What breaks without this loop: long sessions hit context window limits. API calls fail. The agent either crashes or the provider returns truncated responses. Multi-turn /goal runs become impossible beyond 15-20 turns.
Loop 8 — The Sub-Agent Loop
Timescale: minutes per sub-agent, parallel execution.
delegate_task spawns child agents with isolated context. Each child runs its own core loop (Loop 1) independently.
Token cost note: each sub-agent runs its own full Loop 1 session. 3 concurrent sub-agents ≈ 3x your single session cost. Use cheaper models for sub-agents doing routine or research work. Reserve expensive models for the parent orchestrator where output quality matters.
Parent agent receives complex task
  → Spawns sub-agent 1 (own context, own tools)
  → Spawns sub-agent 2 (own context, own tools)
  → Spawns sub-agent 3 (own context, own tools)
  
  Max concurrent: delegation.max_concurrent_children (default 3)
  
  Each sub-agent:
    → Runs core loop (Loop 1)
    → Can use /goal (Loop 2) if goal_mode=True
    → Creates skills (Loop 3) from completed work
    → Writes to memory (Loop 5) if relevant
    → Runs compression (Loop 7) if needed
    
  Sub-agents return summaries to parent
  Parent's context stays light
  
  Roles:
    leaf (default): cannot re-delegate
    orchestrator: can spawn its own workers
    bounded by delegation.max_spawn_depth
Single task:
delegate_task(goal="research X", context="...", toolsets=[...])
Batch (parallel):
delegate_task(tasks=[
  {goal: "research topic A", ...},
  {goal: "research topic B", ...},
  {goal: "research topic C", ...}
])
Children run in parallel, capped by max_concurrent_children. Total iterations across parent + subagents can exceed the parent's cap (each gets its own budget).
What breaks without this loop: every task runs sequentially in one context. Complex tasks requiring parallel research, analysis from multiple angles, or simultaneous code review across modules all bottleneck on a single agent.
How The Loops Nest
The loops do not run independently. They nest inside each other and across timescales:
WEEKLY:
  Loop 4 (Curator) runs → cleans skills from Loop 3
    → improves accuracy of Loop 7 (Tool Search in skills)

DAILY:
  Cron job fires →
    Loop 6 (Kanban) assigns task →
      Loop 2 (/goal) starts on the task →
        Loop 1 (Core) executes each turn →
          Loop 7 (Compression) fires if context grows →
          Loop 8 (Sub-agents) spawn for parallel work →
            Each sub-agent runs its own Loop 1
        Loop 3 (Self-improvement) fires after task completes →
          New skill saved
      Loop 5 (Memory) writes persistent facts

EVERY SESSION:
  Loop 5 (Memory) injects MEMORY.md + USER.md
  Loop 1 (Core) runs turns
  Loop 7 (Compression) manages context
  Loop 3 (Self-improvement) reviews and saves
The compounding chain:
Loop 3 (skills) makes Loop 2 (/goal) faster because the agent has documented procedures
Loop 4 (Curator) keeps Loop 3 clean so skills stay searchable
Loop 5 (memory) gives Loop 1 context about you and your preferences
Loop 6 (Kanban) orchestrates multiple Loop 2 instances in parallel
Loop 7 (compression) keeps Loop 1 affordable across long runs
Loop 8 (sub-agents) multiplies Loop 1 capacity for parallel work
Remove any single loop and the others degrade. Remove Loop 3 and the agent never improves. Remove Loop 4 and Loop 3 eventually bloats the system. Remove Loop 7 and long sessions crash. Remove Loop 5 and every session starts cold.
The system works because the loops are designed to feed each other.
How Hermes Compares to Other Loop Architectures
Not every agent framework implements the same loops. Here is where the landscape stands:
GenericAgent (github.com/lsdefine/GenericAgent, 12.4K stars) takes a different approach: minimal seed code (~3K lines, 9 atomic tools) that self-evolves into a full system. Their goal mode uses time budgets instead of turn budgets ("keep optimizing X for N hours"). Token consumption is 6x lower than comparable frameworks per their technical report
DSPy (github.com/stanfordnlp/dspy, 25K+ stars, Stanford NLP) treats prompts as programs and optimizes them against metrics. Different philosophy from Hermes: DSPy optimizes the prompt through compilation. Hermes optimizes the procedure through skill creation. DSPy is the most serious optimization engine in the space. Hermes is the most complete self-improving runtime.
Hermes's advantage is that all 8 loops are native, integrated, and designed to feed each other. Most other frameworks implement 2-3 loops and leave the rest to the user.
What Breaks When a Loop Fails
Each loop has a specific failure mode:
The most dangerous failure: Loop 3 saving a bad skill. A wrong procedure gets reused across future sessions, compounding the error. This is why Loop 4 (Curator) and human review both exist. The Curator catches stale skills. Human review catches wrong skills.
Configuration Reference
All loop-related settings in one place:
yaml
# Loop 1 — Core
agent:
  max_turns: 90                    # iteration budget per session

# Loop 2 — /goal
goals:
  max_turns: 20                    # turns per goal run

# Loop 3 — Self-improvement
# No direct config. Controlled by skill_manage tool availability
# and nudge system (background fork pattern)

# Loop 4 — Curator
curator:
  interval_hours: 168              # 7 days between runs
  min_idle_hours: 2                # only runs when idle
  prune_builtins: true             # can archive unused built-ins
  archive_after_days: 30           # unused threshold

# Loop 5 — Memory
memory:
  memory_enabled: true
  user_profile_enabled: true
  memory_char_limit: 2200          # ~800 tokens
  user_char_limit: 1375            # ~500 tokens

# Loop 6 — Kanban
# Dispatcher runs every 60 seconds (not configurable)
# Zombie detection and heartbeat tracking automatic

# Loop 7 — Compression
compression:
  enabled: true
  threshold: 0.50                  # compress at 50% of context
  target_ratio: 0.20
  protect_last_n: 20

context:
  engine: "compressor"             # or "lcm" for lossless

auxiliary:
  compression:
    model: null                    # cheaper model for summaries
    provider: auto

# Loop 8 — Sub-agents
delegation:
  max_concurrent_children: 3
  max_iterations: 50               # budget per sub-agent
  max_spawn_depth: 2               # orchestrator nesting limit
Token Cost Per Loop
Not all loops cost tokens equally. Some are free. Some are the main cost driver.
Estimates based on typical usage patterns. Use /usage in Hermes to measure your actual numbers.
Cheapest loops: Kanban (zero), Curator (minimal), Compression (net saver). Most expensive: Sub-agents (multiplier), /goal (20x core turns), Core (base cost).
Optimization priority:
Use auxiliary model for /goal judge and compression (cheap model for side-jobs)
Lower memory char limits on profiles that don't need deep context
Set realistic max_turns per profile (20 for research, 50 only for code)
Enable Tool Search to avoid loading unused schemas
Run routine cron jobs on cheaper models (GPT-5.5 via Codex at $0)
For full token economics breakdown and monthly budget calculations, see: Hermes Agent as a Personal AI Operating System — Section 3: Token Economics
Start Here
Read about 8 loops and don't know where to begin. Three steps:
Step 1 — Get Loop 1 + Loop 5 running (5 minutes)
Install Hermes. Run hermes setup --portal. Start a session. Talk to it. Memory writes happen automatically. Loop 1 (core) and Loop 5 (memory) are active from the first message.
Step 2 — Add Loop 2 (next 10 minutes)
Run your first structured /goal:
/goal [what you want done]
using [what sources to check]
with constraints: [what to avoid]
deliverable: [what "done" looks like]
The agent works across multiple turns until the judge says done. Loop 3 (self-improvement) fires automatically after the goal completes.
Step 3 — Add time and orchestration (next 30 minutes)
Set your first cron job. Something small:
Every morning at 8am send me a summary
of trending AI news to Telegram.
You now have 5 loops running: Core (1), /goal (2), Self-improvement (3), Memory (5), and Compression (7, fires automatically when needed).
Kanban (6), Curator (4), and Sub-agents (8) activate as your usage grows. The Curator starts after 7 days. Sub-agents spawn when you use delegate_task. Kanban activates when you track multiple tasks.
You don't configure all 8 on day one. You start with 2. The rest come online as your system expands.
The Real Insight
Agent frameworks are defined by their loops. A framework with one loop (prompt → response) is a chat wrapper. A framework with two loops (prompt → response → retry) is slightly better. A framework with all 8 is an operating system.
Hermes runs 8 loops across timescales from milliseconds to weeks. Each loop feeds the others. Skills make goals faster. The Curator keeps skills clean. Memory gives every session context. Kanban orchestrates parallel work. Compression keeps costs manageable. Sub-agents multiply capacity.
The compounding happens in the intersection of these loops, not in any single one. An agent that improves its own procedures AND maintains those procedures AND remembers your preferences AND orchestrates parallel work AND manages its own context is a fundamentally different tool than one that responds to prompts.
That is the loop architecture of Hermes Agent.
For the full architectural mapping of all 17 layers, read: Hermes Agent as a Personal AI Operating System — OS mapping, token economics, comparison table, practical setup paths.

 
Fuente 9: 

Link: https://x.com/IBuzovskyi/status/2062101068842975409?s=20

Transcripcion:

10 HERMES AGENT HACKS THAT TURNED MY CHAT AGENT INTO A 24/7 SYSTEM
These 10 Hermes Agent hacks saved me 15+ hours every week - and they work for any workflow you run repeatedly. Content, software development, business operations, client management, research, sales. If you do it more than once, Hermes can run it.
My examples are from content and social media automation because that's what I run daily. The setups themselves are domain-agnostic. A cron job that scans X for trending posts uses the same mechanic as one that checks GitHub for open PRs or monitors a CRM for new leads.
Most people use Hermes Agent like a chat app. They open it, type a prompt, get a response, close it.
That leaves 90% of what Hermes can do on the table.
Here are 10 setups that turn Hermes from a chat window into a 24/7 system that works while you sleep, reacts when your workflow changes, and gets sharper with every run.
If you only have time for 3, start with: Cron Jobs (#3), /goal Structure (#4), and Skills (#8). These three alone change how Hermes feels overnight.
Table of Contents
Mission Control — setup: 30 min, saves: 2 hrs/week
Event Triggers — setup: 20 min, saves: 3 hrs/week
Cron Jobs — setup: 10 min, saves: 5 hrs/week ⭐
/goal Structure — setup: 5 min, saves: 4 hrs/week ⭐
Sub-Agents — setup: 5 min, saves: 3 hrs/week
Telegram Workspaces — setup: 10 min, saves: 1 hr/week
Kanban Board — setup: 5 min, saves: 2 hrs/week
Skills as SOPs — setup: 15 min per skill, saves: 5 hrs/week ⭐
Webhooks — setup: 30 min, saves: 3 hrs/week
Separate Agents — setup: 20 min per profile, saves: 4 hrs/week
1. MISSION CONTROL
The first setup and the biggest one: build a dashboard where everything is visible.
When Hermes is doing real work, you don't want that work buried inside a chat thread. You want to see what is running, what is waiting on you, what is blocked, what needs approval, and what changed since yesterday.
Ask Hermes to build it:
bash
Build me a mission control dashboard. Start with:
- A kanban board showing all active agent tasks
- A content pipeline where I can add ideas and track progress
- A memory wiki showing everything we've worked on
- A performance section showing my X and content metrics
Hermes also has a built-in dashboard out of the box:
hermes dashboard
Opens at localhost:9119. Skills, models, cron jobs, profiles, kanban board. Start here, then customize when you need more.
Hermes also just launched a native Desktop app for macOS, Windows, and Linux. Side-by-side preview, file browser, integrated voice. Same data directory as CLI and Telegram. Work from Desktop at your machine, switch to Telegram on the go. One agent, every surface.
Download: hermes-agent.nousresearch.com/desktop
Fastest path to a working agent on any surface:
hermes setup --portal
One OAuth covers the model + web search + image generation + TTS + cloud browser. No separate API keys needed.
Once you add a Kanban board directly into the dashboard, Hermes stops being something you message and starts becoming part of your operating layer. You can see every task, every status, every blocked item in one place instead of digging through chat history.
Mission control shows you the system. The next setup is where Hermes starts waking up without you prompting it.
2. EVENT TRIGGERS
Think about where you already work. Notion. Linear. Google Sheets. Slack. You move a task, update a status, add an idea. Right now, nothing happens after that. You have to remember to tell Hermes about it later.
The fix: make Hermes watch for changes and react automatically.
Example workflow: when you move a video idea to your "To Film" list in Notion, Hermes detects the change and sends you a filming brief on Telegram within minutes.
That brief includes:
Should you film this now, later, or kill it?
The strongest title angle
A 30-second hook for the opening
Proof assets you'll need
A pre-filming checklist
You didn't prompt Hermes. You moved a card. Hermes saw the state change and did the work.
How to set this up:
Option A — Hermes cron job watches for changes (simplest):
Schedule a cron job every 10 minutes:
check my Notion board [board URL].
if any card moved to "To Film" in the last 10 minutes,
research the topic, write a filming brief,
send it to Telegram.
Option B — Webhook trigger (instant):Use Notion automations, Make, or Zapier to send a webhook to Hermes when a card moves. The response is instant instead of polling every 10 minutes.
The principle: when your workflow changes state, Hermes should know what to do next.
3. CRON JOBS
Event triggers react to changes. Cron jobs react to time.
Every morning I get useful information before I ask for it. That shift made Hermes feel like an employee who starts work before I wake up.
Cron jobs that run in my setup:
Every morning at 8am:
send me one AI story worth reacting to on X.

Every 3 hours:
scan X for fresh posts in my niche I should quote tweet.

Every day at 9pm:
check if competitors posted any outlier content today.

Every Monday at 9am:
audit my content board. flag ideas stuck for more than 7 days.

Every Friday at 6pm:
summarize what content shipped this week,
what performed, what didn't, and why.
Setting these up in Hermes is plain English. No crontab syntax. Just tell the agent what you want and when.
The difference: instead of you remembering to ask Hermes things, useful information arrives before you even think about it. That is what makes it feel like a 24/7 assistant.
Scheduled work is half the system. The other half is giving Hermes better objectives than normal prompts.
4. /GOAL WITH STRUCTURE
A normal prompt asks Hermes for one response. /goal gives Hermes an objective to work toward across multiple turns until it's done.
Most people use /goal like a prompt. They type something vague and get vague results back. The difference between a useless /goal and one that ships real work is structure.
The template that works:
/goal [OUTCOME]
using [SOURCES]
with constraints: [CONSTRAINTS]
deliverable: [DELIVERABLE]
Example:
/goal [OUTCOME]
using [SOURCES]
with constraints: [CONSTRAINTS]
deliverable: [DELIVERABLE]
Every part does a job:
Outcome tells Hermes when the goal is achieved
Sources tells it where to look
Constraints tell it what to avoid
Deliverable tells it what "done" looks like
Fuzzy prompts create fuzzy output. Structured goals create useful work.
The interview hack:
If you don't know how to structure your goal, make Hermes do it for you:
I want to use /goal but I don't want a vague goal.
Interview me with only the questions you need.
Then turn my answers into the strongest possible
/goal command. Include the exact outcome, context,
sources, constraints, deliverable,
and when you should stop.
Hermes asks you 5-8 questions, then writes its own /goal command from your answers. The resulting goal is sharper than anything you'd write from scratch.
5. SUB-AGENTS AS A RESEARCH TEAM
One agent gives you an answer. Sub-agents give you a team.
For any research task worth doing, I split it across multiple sub-agents running in parallel. Each one has a different source. The results merge into one recommendation.
Example:
/goal research the best content angle for this week.
spawn 3 sub-agents:

1. scan X for trending posts in AI agents niche,
   pull engagement numbers and hooks that worked

2. analyze my last 30 days of posts,
   find patterns in what performed vs what didn't

3. check competitor accounts,
   flag any outlier content from the last 7 days

combine all three into one recommendation
with the strongest angle, a draft hook,
and proof assets I'll need.
Each sub-agent gets its own context window. Only the final summary returns to the main session. Your main context stays light.
This is the difference between asking one person to research everything (slow, shallow) and having three specialists each go deep on their part (fast, thorough).
Best use cases for sub-agents:
Research across multiple sources
Competitive analysis (one sub-agent per competitor)
Content creation (one for research, one for drafting, one for editing)
Code reviews (one for logic, one for security, one for performance)
6. TELEGRAM TOPICS AS WORKSPACES
Telegram topics turn one chat into separate workspaces. Each topic becomes a different context with a different job.
My setup:
YouTube topic — content planning, scripts, filming briefs
React topic — trending posts on X worth reacting to
Coding topic — technical work, debugging, PRs
Research topic — deep dives, competitor analysis
General topic — smaller tasks, random questions
Different work needs different rooms. When everything runs in one chat, context bleeds. A coding question gets mixed with a content brief. A research task interrupts a draft review.
Topics fix that. Each workspace keeps its own conversation thread. Hermes knows what you're talking about based on which topic you're in.
Set up topics in any Telegram group:
Create a group with your Hermes bot
Enable Topics in group settings
Create a topic per workspace
Start messaging Hermes in each topic separately
Cron jobs per topic:
YouTube topic cron, every morning at 8am:
research trending AI content topics on X and YouTube.
send me 3 content ideas with engagement data.
post results in this topic only.

React topic cron, every 3 hours:
scan X for posts in AI agents niche
with 500+ likes in the last 3 hours.
if any are worth reacting to, draft a quote tweet
and send it here for approval.

Research topic cron, every Monday at 9am:
run a competitor audit.
check what @competitor1 @competitor2 @competitor3
posted last week. flag outliers. send report here.
Each topic gets its own cron job. Research stays in Research. Content stays in Content. No cross-contamination.
7. KANBAN FOR TASK MANAGEMENT
Once Hermes works on more than one thing, you need a board. Otherwise tasks disappear into chat and you forget what you even asked for.
Hermes has a built-in Kanban board. Durable SQLite storage. Shared across all profiles.
hermes kanban list
Shows your board. Drop tasks into triage. The dispatcher auto-assigns them to workers every 60 seconds.
Statuses: Triage → To-Do → Ready → Running → Blocked → Done
What this changes:
You see what is ready, running, and done
You see which agent owns which task
You see what is blocked and why
Crashed tasks get auto-reclaimed (zombie detection)
Heartbeats track worker health
Every /goal you set also becomes a Kanban card automatically. Multiple goals across multiple profiles, all visible on one board.
/goal research competitors → kanban card
/goal draft weekly report → kanban card
/goal triage inbox → kanban card
All three run in parallel. All three tracked in one place.
Kanban is how agent work stops disappearing into the chat.
Morning workflow with Kanban:
/goal research competitors → kanban card
/goal draft weekly report → kanban card
/goal triage inbox → kanban card
Drop 5 tasks at breakfast. By lunch, half are done. You didn't manage any of them.
8. SKILLS AS SOPs
A skill is a standard operating procedure for Hermes. You encode a process once and the agent uses it forever.
Hermes already creates skills on its own after every task. It reviews what worked, saves the workflow as a markdown file in ~/.hermes/skills/, and reuses it next time.
Writing skills intentionally for your key workflows is where the leverage multiplies.
Example — a content creation skill:
Save this as a skill called "content-post":

# Content Post Workflow

1. Check trending topics in AI agents niche via X search
2. Cross-reference with my last 14 days of posts (avoid repeats)
3. Pick the strongest angle based on engagement patterns
4. Write a draft in my voice:
   - ALL CAPS hook with HERMES AGENT as subject
   - arrows → for feature lists
   - No em-dashes, no adverbs, no throat-clearing
   - End with "full setup guide in the article 👇"
5. Score the draft:
   - Hook: does it stop the scroll? (1-10)
   - Bookmark fuel: would someone save this? (1-10)
   - Proof: is every claim backed by a number? (1-10)
6. If any score below 7, rewrite that section
7. Send final draft to Telegram for approval
Now whenever you say "use content-post for today's draft", Hermes runs the entire SOP without you explaining the process again.
Any workflow you explain twice should become a skill. Over time your agent accumulates dozens of skills, each one encoding a process that used to take manual instructions.
Skills are transparent. They live as markdown files. You can read them, edit them, delete them. No black box.
To see all skills:
hermes skills
Or open the dashboard → Skills tab:
hermes dashboard
Hermes ships with 60+ built-in tools across terminal, web, browser, vision, image generation, TTS, and code execution. Skills layer on top of those tools to create full workflows.
9. WEBHOOKS AND EVENT-BASED AGENTS
Cron jobs run because the clock changed. Webhooks run because the world changed.
A few examples of event-based triggers:
A new lead comes in → Hermes researches the company immediately
A GitHub PR opens → Hermes summarizes the changes and flags risks
A competitor posts content → Hermes checks if it's worth reacting to
A meeting transcript drops → Hermes extracts action items and adds tasks to your board
A keyword starts trending → Hermes drafts a content angle
The point is removing dead zones where something important happens and nobody acts on it until later.
Hermes receives webhooks through its gateway. Configure the webhook URL in your automation tool (Make, Zapier, n8n) and point it at your Hermes gateway endpoint.
Example: competitor monitoring via n8n + Hermes:
n8n workflow:
1. RSS trigger watches competitor blog (every 30 min)
2. if new post detected → send webhook to Hermes

Hermes /goal on webhook receive:
/goal a competitor just published: [title] [url].
read the full article via web search.
summarize the key points in 3 lines.
assess: should I react to this on X?
if yes, draft a reaction post in my voice.
send everything to Telegram for approval.
Example: new lead notification:
Zapier trigger: new form submission on website
→ webhook to Hermes

Hermes /goal on webhook receive:
/goal new lead: [name], [company], [email].
research their company via web search.
find their LinkedIn and recent posts.
draft a personalized follow-up email.
send draft to Telegram for approval.
The principle: cron jobs handle time. Webhooks handle events. Together they cover every scenario where Hermes should wake up without you touching it.
10. SEPARATE AGENTS BY JOB
You don't want your accountant to be your dentist. You don't want one agent doing every job with the same model, same tools, same memory, and same permissions.
Hermes profiles let you create separate agents for separate roles. Each profile has its own:
soul.md (personality and rules)
memory (what it knows)
skills (what it can do)
model (how smart it needs to be)
MCP connections (what tools it has access to)
permissions (what it's allowed to do)
Example setup:
hermes profile create content-lead
→ soul.md: you produce content. match my voice.
   use trending data. avoid repeated angles.
→ model: claude-sonnet-4 (needs strong writing)
→ tools: X search, web search, analytics

hermes profile create researcher
→ soul.md: you find information. deep research only.
   no opinions. facts and numbers.
→ model: gpt-5.5 (cheaper, high volume)
→ tools: web search, firecrawl, browser-use

hermes profile create ops
→ soul.md: you handle admin. calendar, email triage,
   reminders. ask for approval before sending anything.
→ model: gpt-5.5 (routine tasks, cost-efficient)
→ tools: email, calendar, notion

hermes profile create code-reviewer
→ soul.md: you review PRs. flag security issues,
   logic errors, performance problems.
→ model: claude-opus-4-8 (needs deep reasoning)
→ tools: github, terminal
Some agents need the smartest model you can afford. Some just need to check a page every hour. Some should have write access. Some should never have write access.
First /goal for each profile:
content-lead:
/goal research trending topics in AI agents niche.
cross-reference with my last 14 days of posts.
draft 2 posts in my voice.
score each on hook strength (1-10) and bookmark value (1-10).
send drafts to Telegram for approval.

researcher:
/goal run a deep research session on [topic].
use web search and firecrawl to pull data from
at least 5 sources. compile findings into
a structured markdown report with numbers,
sources, and key takeaways. save to file.

ops:
/goal check my inbox. summarize what needs a response.
pull today's calendar events.
flag anything urgent.
send morning briefing to Telegram by 9am.

code-reviewer:
/goal review the latest PR on [repo].
check for security issues, logic errors,
and performance problems.
write a review summary with specific line references.
send to Telegram.
Each profile runs its first /goal, learns from the result, and saves the workflow as a skill. Second run is faster. Fifth run is automatic.
Share any profile with one command:
Built a research agent that works? Share it via git:
cd ~/.hermes/profiles/researcher
git init && git add . && git commit -m "initial"
git push origin main
Anyone can install your agent:
hermes profile install github.com/you/researcher
They fill in their own API keys, and the agent runs with your skills, your soul.md, your workflows. Their memories and sessions stay separate.
The unlock is a team of smaller agents with the right brain, tools, memory, and permissions for their specific job.
Run them simultaneously. Each specialised. Each improving independently in their own lane.
HOW THEY CHAIN TOGETHER
These 10 setups compound when you stack them. Here is one chain running in my system right now:
8:00 AM — cron job (#3) fires.

the content-lead profile (#10) wakes up
and starts a /goal (#4) with structure:

"find the 3 strongest content angles for today
using X trending data and my last 14 days of posts."

it spawns 3 sub-agents (#5):
→ sub-agent 1 scans X for trending posts
→ sub-agent 2 pulls my recent post performance
→ sub-agent 3 checks competitor accounts

all three become kanban cards (#7).
dispatcher tracks them in parallel.

sub-agents finish. content-lead runs
the content-post skill (#8) to draft 2 posts.

drafts land in my Content topic
in Telegram (#6) for approval.

I tap approve on one. reject the other.
the approved post publishes via xurl.

10 minutes later a competitor publishes
a reaction to the same topic.
a webhook (#9) fires.
Hermes drafts a follow-up angle
and sends it to my React topic (#6).

I see everything on mission control (#1).
what ran, what shipped, what's pending.
One morning. Seven hacks fired. Two posts ready. Zero manual research.
That is the system.
THE REAL INSIGHT
If Hermes still feels like another chat app, look at the system around it.
Give it a mission control so you can see what's happening. Set up event triggers so it reacts when your workflow changes. Set up cron jobs so useful information arrives before you ask. Use /goal with structure instead of vague prompts. Split research across sub-agents. Separate workspaces with Telegram topics. Track tasks on the Kanban board. Turn repeatable processes into skills. Connect outside events via webhooks. Stop making one agent do every job.
Ten setups. Each one saves hours per week. Stack all ten and Hermes runs your operations while you focus on the work that moves the needle.
The agent is ready. The stack is ready. Wire the system and let it work.
→ Follow for AI agent blueprints every week → Save this. The /goal template and skill examples are worth bookmarking. → Comment "SYSTEM" and I'll send you the full skill templates for each setup.
Want 7 more hacks? The extended version with Session Recall, Token Optimization, Voice Mode, Browser Automation, Overnight /goal Runs, Memory Providers, and Tool Search is on Substack: Read the full 17-hack guide on Substack →
Resources
Official:
Hermes Agent Docs — installation, configuration, full CLI reference
Skills Hub — community skills, browse and install
GitHub — source, issues, PRs
