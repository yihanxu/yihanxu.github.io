---
layout: post
comments: true
title: "A product requirement documentation I drafted 8 years ago"
tags: product_requirement, writing, PhD_days, peer_review, cornwall
category: SnapshotOfTheDay
---

I know life is dramatic and unpredictable. But not in my wildest dreams could I have imagined that one day, while sipping cider, with the misty wind from Carbis Bay in Cornwall caressing my hair and face, I'd be helping my former colleague revise a paper that I drafted eight years ago.

As the first author, I was supposed to carry it through and get it published. However, I was soon consumed by my thesis and gave it up.

But the professor who oversaw it apparently didn't. Not after so many years, and not after it was desk-rejected by a few journals. Last month, we got a minor revision decision, so perhaps it might finally see the light of day? That is, if we address the reviewers' comments properly and timely.

While reading the reviewers' report, memories flooded back from the distant past, when I was still in the third year of my PhD. I was keen to design an embodied conversational agent that could gain investors' trust through thick and thin (as few investors can hold on when experiencing stock market turbulence). It was very much a predecessor of the AI agents we see today. But back then, the agent was far less advanced or fluent. I had to draft all the conversational scripts myself. I also had to draft a tremendous amount of documentation to make the experimental web application I envisioned a reality. 

I had almost forgotten all of it until I had to sift through the old files to draft a response to one reviewer's comment. And then I came across a note I had written to the software engineer to articulate what I wanted.

I was strangely touched by how thorough and dedicated I once was. Some bits of that still live with me, of course, but perhaps they don’t grip me in quite the same way anymore, now that I routinely use AI to help me draft documentation and notes.

I just wanted to share one piece from that era, as a sample of my writing and of the thought that went into it when I was trying very hard to express my requirements clearly.

# A note on block randomisation

I wrote this note with two goals in mind.
 
- To explain what block randomisation is.
- To illustrate its implications for our experimental design and logistics.

*Last updated:  2 Nov 2018*

---

We're all familiar with the idea of randomisation. In our online pilot, we randomly assign participants to different conditions. Except for the conditional variables, we try to hold everything else as the same. We do this to test whether the factors that we’re interested in (e.g. communication style / bot personality) make a difference. 

The idea is simple enough, but the implementation is not necessarily so. It's incredibly hard to *isolate* and *quantify* the effects of the experimental factor. You know people used to believe objects fall at speed proportional to their mass. That is, until Galileo used a vacuum chamber to remove the effects of air resistance in his famous Leaning Tower of Pisa experiment. Unfortunately, social science doesn't have such luxurious, neat tools that physics has, so social scientists have to come up with other ways to build something similar to the vacuum chamber.

Block randomisation could be seen as a "vacuum chamber", it aims to make the effects of an experimental factor cleaner and more noticeable. 

For example, suppose we found that Max was participants' favourite, but we're still not sure whether this preference is true for both men and women. What if the following extreme scenario happened? 

| |Condition 1 (Max) | Condition 2 (Linus) |   
|---|---|---|
| Participant Pool| 99 men + 1 woman | 99 women + 1 man |
| Men's preference| 8 | 6 |
| Women's preference| 6 | 8 |
| Preference by condition| (99x8+6)/100 = 7.98 | (99x6+8)/100 = 6.02 |

If the gender ratio of the participants is skewed, and if the preference differs between men and women, then we may mis-interpret the experimental results. One solution to address the above problem is to divide participants into subgroups called blocks before they visit the lab. For example, we could have men block and women block, each block having the same No. of participants. Then we can randomly assign participants into different conditions within each block -- this is the idea of block randomisation. Compared to a completely randomized design, this approach reduces variability (noise) within each condition, giving us a better estimate of the effects caused by condition variables.

Now, for my study 1 lab session, the ideal participant pool will be as follows: 

| Participant Pool | Condition 1 (Dominant Max) | Condition 2 (Submissive Linus) | No. of participants by participantPersonality | 
|---|---|---|---|
| Participants with dominant personality | 15 men + 15 women | 15 men + 15 women | 60 |
| Participants with submissive personality  | 15 men + 15 women| 15 men + 15 women| 60 |
| No. of participants by botPersonality | 60 | 60 | Total: 120|

Likewise, for my study 2 lab session, the ideal participant pool will be as follows: 

| Participant Pool | Condition 1 (Max + Improve) | Condition 2 (Max + Deteriorate) | Condition 3 (Linus + Improve) | Condition 4 (Linus + Deteriorate) |No. of participants by participantPersonality | 
|---|---|---|---|---|---|
| Participants with dominant personality | 15 men + 15 women | 15 men + 15 women | 15 men + 15 women | 15 men + 15 women | 120|
| Participants with submissive personality  | 15 men + 15 women| 15 men + 15 women | 15 men + 15 women | 15 men + 15 women | 120|
| No. of participants by condition | 60 | 60 | 60 | 60 | Total: 240|
 
For the online session, since we couldn't screen participants based on their gender and personality, we can only rely on luck and wish the participant pool will be similar across conditions. If not, perhaps we could do some ad hoc statistical adjustment, but that's not good practice. 

But for lab session, we don't want to leave things to chances, we want to take control while we can. That's why we design the *manual configuration* mechanism in the beginning. Now as you already know, lab participants take a pre-test questionnaire before visiting the lab. Thus by the time they visit the lab, we  already know their gender and personality type. 

My original plan to implement block randomisation is to make a huge spreadsheet of prospective participants, arrange them by date, time slot, gender, and personality. Something like this (for study 1):

| Date | Time slot | Matric Number | Personality | Gender | Condition |
|---|---|---|---|---|---|
| 2018-11-12 | 10-11am | g3423452a | dominant | female | X |
| 2018-11-12 | 10-11am | g3423233a | dominant | male | X |
| 2018-11-12 | 11-12am | u3234252b | submissive | male | X |
| 2018-11-12 | 11-12am | u1452452b | submissive | female | X |
| 2018-11-12 | 13-14pm | g2423452c | dominant | male | X |
| 2018-11-12 | 13-14pm | u6423452c | submissive | female | X |

With this spreadsheet, I'll just rely on lab assistants to help me balance the proportion of gender and personality. However, now I think I'll probably get into trouble using this approach. My plan will fail in the following scenarios:

- 	Some participants don't show up (the non-show-up rate is about 20%), and lab assistants cannot decide quickly how to re-arrange conditions for the missing slots 
- 	A lot of participants with same gender and personality show up together, and lab assistants are simply over-whelmed 
- 	Lab assistants mistakenly assign participants to the wrong conditions 
- 	Lab assistants don't realise that some conditions have already got 30 participants, thus no need to assign participants to that condition further
- 	Other unpredictable situations, you name it

So what do I want? I need a simple algorithm that implements block randomisation.

- Inputs from lab admin: participant gender, personality
- Inputs inferred from experimental design: No. of participant for each cell (30 in my case), No. of conditions, etc.
- Output: The ideal participant pool that I illustrated above

Could you think of a way of achieving so? It'll be great if you could help us with this. The idea of block randomisation will also be applicable for the chat-bot project. Actually, I think it will be useful to a lot of field experiments and commercial projects.

**Note:** Integrating this algorithm to the conditionPage may be risky. If you think that's the case, then just let this algorithm be independent from the current web application. As long as it helps lab admin quickly assign conditions for prospective participants in the unpredictable real world scenarios.

P.S. I know this is doable because I once visited a lab that does block randomisation even for online experiments. The workflow looks like this. It's a black box for me, hopefully not for you.


 

