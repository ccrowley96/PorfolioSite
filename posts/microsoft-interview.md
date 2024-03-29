---
title: Interviewing @ Microsoft
subtitle: My experience interviewing at Microsoft
date: 2018-10-24
images:
  - /img/ms_square.jpg
  - /img/food_bois.jpg
  - /img/game_room.jpg
  - /img/office.jpg
tags:
  - interviews
  - microsoft
layout: layouts/post.njk
eleventyExcludeFromCollections: true # <--draft
---
>Holy hot damn salami. I had ten days before the biggest interview in my life.

### How I ended up at Microsoft.
In my first year of University, I submitted my 30 font resume with 0 relevant experience to a Microsoft recruiter at a campus event.  This somehow turned into an on campus interview several weeks later.  I was under the impression that I was applying for the *Explorer Program*, an internship tailored for new University students with little technical experience, but unbeknownst to me, I was applying for the full software engineering internship.  

I made several **yuuuge** mistakes during this interview.  First, I started coding out a solution without thinking about the problem or how to approach it.  Second, I chose to dive into the syntactic nightmare of a full Java class instead of pseudo coding or writing out a general algorithmic approach.  And lastly, I didn't ask for any clarification, such as: How is this data input to my function?  What should the function return? Etc...  I was wildy unprepared, sweating profusely, and extremely nervous given the weight of the internship.

> **pro·fuse·ly** - adverb - 
to a great degree; in large amounts.

Needless to say, I didn't get any exciting calls.

_Fast forward 2 years later._

I get an email from a Microsoft recruiter asking to set up another on campus interview.  

> Ok, keep it cool Cory, deep breaths, you got this.  Time to show MS that you're dat coding boi.

I show up to the interview slightly more confident than the last time.

This time, I had some content on my resume.  Freelance web development work, involvement with the tech scene at Queen's, and my biggest project yet, a prototype for a [Queen's Rideshare platform](/projects/qshare), which I had been working on in the last few months.  The recruiter was very interested in the projects I was working on.  **Score**.  After stumbling through a recursive tree traversal questions, pointer heavy and written in pure C, I completed the interview, convinced I had done just as poorly as the first time.  

> Learn Python, omg OMG learn Python - street smart software interview tips with detective J. J. Bittenbinder

A couple of weeks later, I received another email from Microsoft, I made it to the final round interviews, they were going to fly me out to Vancouver for a full software engineering interview.  Holy hot damn salami.  I had **ten** days before the biggest interview in my life.

### Preparing for the interviews
![Interview Prep](/img/MicrosoftPrep.png)

It was midterm week of the hardest year in my University career, but I decided my time was better spent learning algorithms and preparing for this interview. I skipped the week of school, spent every day in the library, and made many study sheets like the image above.

**What I Studied**
* Linked Lists
* Stacks & Queues
* Heaps
* ArrayLists
* **HashMaps** (most useful) 
* Breadth & Depth First Search
* Sorting
* Recursion (scary)
* Big O Time Complexity
* Trees
* C++, C, Java
* String Manipulation

**How I Studied**
* PRAMP Practice Interviews
* Hackerrank & Leetcode
* **Cracking the Coding Interview**
* Algorithms & Data Structs. in C
* Practice interview questions on paper / whiteboard

### The interview in Vancouver
After exploring Vancouver for a day with my brother and friend Jake (who came up to visit me in Vancouver for the weekend), I walked just down the street from my hotel to the Microsoft office.  I sat in the waiting room with about 20 other nervous candidates flown in from all around Canada.  To this day, I still find the hardest thing about interviewing is getting control of your nerves.  Go easy on the caffeine, and do whatever calms your mind.

**De-stress walk on Vancouver Seawall.  October 22nd, 2017.**
![Vancouver Seawall](/img/seawall.jpg)

After what seemed like an eternity of distracted conversation, we were ushered into a large board room with free food and comfy chairs.  Then, one at a time, full-time engineers came into the room and called our names.  I had four 45-minute-long technical interviews.

The first question was a trick question.  C'mon dude.  I'm so nervous, give ya boi a break. It was a math logic puzzle with no obvious answer (to me anyway).  If the test was to see how I reacted under problem solving pressure -- I failed.

The question was to write a function that swapped the value of two variables using no extra memory i.e. know additional variables.  I was so nervous that I couldn't get my thoughts together to come up with, the, or any, solution.  After 30 minutes of confusion, the first interview finally ended.  By the end of the first interview, I was sure that I had failed the whole interview process.

If you're interested, the answer to that question goes something like this.

```
a = -2
b = 5

a = b - a // 7
b = b - a // -2
a = b + a // 5

a // 5
b // -2
```

Using simple addition / subtraction, you can swap the value of two variables with no extra memory.  This seems obvious once you see it, but under pressure, it seemed near impossible.  **It's hard to problem solve under pressure**.

The next two interviews went well.  They covered algorithms that I had prepared for and I was able to write out efficient solutions (_linear big O time complexity in computer manz talk_).

My final interview was with the lead developer of one of the most popular Xbox games.  Basically this guy was really, really smart.  He plunged to the depths of each area of my technical knowledge within minutes.  Every topic I mentioned was a new test of my knowledge.  He had an intimidating beard, wise, squinting eyes, and filled the room with his presence.  He recognized that my weakest area of algorithmic knowledge was recursion, so he asked a recursive questions.  Classic.  I managed to get 90% of the way to a solution before getting lost in the _'base cases'_ and infinite recursive calls.  He finally stepped in with a few pointers, and I finished the question.  He then asked a string manipulation question.  I approached the problem using a HashMap as the data structure for constant lookup time, thinking this would impress the video game genius.  Instead, he asked me to implement the hashing function for my HashMap instead of the original question.  

> *Uh oh.  Keep it high level Cory, you don't know how to do this.*

I gave the engineer an _are you smarter than a fifth grader_ level lesson on Hash functions and the magical insides of HashMaps.  And just as he was about to dive deeper, our time ran out.  I was going for the confident: _**I might know what I'm talking about**_ kind of vibe.

I thanked all of the interviewers, packed my stuff up, and walked out of the building, thinking about all of the little mistakes I had made and what I should have done differently.  Thinking about the first question that I couldn't get, and how my nerves had taken over.  Thinking about the candidate  sitting next to me who was talking about how he had gone out last night, and about how easy all of the questions they were asking were (he didn't get the job).  I was **sure** I didn't get the job.

Seven days later I found out that I was going to be living and working in Vancouver for the four summer months.  I'd been hired for the Microsoft Garage Internship, working on experimental Microsoft projects with some of the brightest technical minds across Canada.  I found out three days before my birthday.  This opportunity has changed my career and life.

### What I learned in the process
1. Technical interviews are like finals.  You'll fail them unless you study.
2. Practice, practice, practice.  Use LeetCode, study algorithm & data structure fundamentals, learn a language really well (I think I'll study Python for my next interview), and practice with friends - out loud and on whiteboards.
3. Breathe.  During the interviews, do anything you can to control your nerves, talk through your process out loud, and never give up on a question.  When I interviewed, I felt so sure that I had failed the interviews, but I was hired all the same.  You often are doing better than you give yourself credit for.

**Pics of the 725 Granville St. Office**