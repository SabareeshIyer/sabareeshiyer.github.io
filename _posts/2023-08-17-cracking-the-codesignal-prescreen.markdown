---
layout: single
title:  "Cracking the CodeSignal prescreen"
canonical_url: 'https://sabareeshiyer.substack.com/p/cracking-the-codesignal-pre-screen'
date:   2023-08-17 19:54:09 -0400
categories: software software-engineering interviews interview-preparation technology
---

Much has been said about the inefficacy and inaccuracy of the hiring process for software engineers. It is not just the interviewees who bemoan having to slug through hundreds of obtuse coding problems on LeetCode to have a shot at landing a top job - the companies doing the hiring are equally displeased with a process that lets false positives abound and creates mis-hires aplenty. Companies, like Amazon, which are notorious for their hire-to-fire culture can hardly be held fully culpable when the industry standard process, for the lack of more appropriately cathartic words, sucks donkey balls.

Into this yawning chasm of interviewing incompetence steps CodeSignal’s _Industry-Standard Coding Framework_ evaluations. These evaluations are quickly becoming the pre-screen of choice for ambitious tech-forward companies big and small alike. They combine the scalability of LeetCode-style algorithmic challenges with the utility and relevance of testing on skills one is actually likely to use on the job. Fat lot of good a thorough knowledge of dynamic programming will do if an engineer is unable to produce modular, bug-free, extensible software. And it is for this reason that the CodeSignal assessments are here to stay. 

In this article, we will go over some techniques, thought patterns and tips a budding software engineer can use to get through these assessments.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/epmw61482wzmylwi8xln.jpg)

## 1. Understand the assessment

Your assessment will ask you to build a fairly simple system to perform some business logic on representations of real-life entities. For example, you might be asked to build a mock banking system or an employee management system. The question is usually structured in 4 levels with each successive level unlocking only upon the successful completion of the previous level. 

The prompts are deceptively simple. For someone coming from the background of taxing LeetCode interviewing which depend on determining the exact right algorithm, optimization or insight to apply to the question, these prompts might even look trivial. But as one of my favorite YouTubers says, _this is just an illusion_: the devil is in the details. The assessment is fairly demanding in terms of technical complexity, so solving the whole thing is no cake walk. The key to solving multiple levels of the assessment is extensibility.

> The key to solving multiple levels of the assessment is extensibility.

Below we’ll look at how to approach the problem in such a way that these concerns can be adequately addressed.

## 2. Be classy

Although a certain sense of style can never hurt your chances, I’m referring here to the core premise of all long-term maintainable, extensible code: a generous usage of classes. Object-oriented programming is critical to maintaining state, depicting real-life entities and code-extensibility. Embrace it.

As a general rule, you should represent each real-life entity with an object - $10 is not an object, but a payment of $10 is; Carl Sagan is not an object, but an astronomer named Carl Sagan is; employment is not an object, but an employee is. During the assessment, you should take time to think about which entities (and hence, objects) you’ll be working with and which operations go on which objects. A good rule of thumb is to put each operation on the class of the actor who performs the actions that the operation denotes. An obvious example might be: if an employee enters the office, that is an action s/he is taking - so `enter_office()` should be on the `Employee` class. By contrast, if an employee gets paid, even though it might sound like something he did, the actor is the manager, so we should be partial to a `pay_employee()` method on the manager over a `get_paid()` on the employee.

## 3. Be mindful of state – modularization is your friend

This is never explicitly specified at any point by the platform, but the major thing that CodeSignal assessments actually test you on is your ability to maintain state. If you try to get by Level 1 with a bare-bones architecture, you will quickly find yourself in a state of befuddlement as you try to juggle all the objects you work with in one central entity that maintains state. The assessment challenges you to find a way to extend your classes in such a way that the objects can maintain their state in the right way without compromising data integrity. For example, you might have a function on your `BankAccount` class to record when money goes out of the account. In that function, you deduct the withdrawn amount from the balance and maintain a total of all withdrawals and you’re feeling pretty good about yourself. However, the next Level might throw a curveball asking you to maintain a list of all outgoing payments and you find yourself scrambling to cram more logic into the function which is growing out of control faster than you expected. Here, modularization can be your friend. Put any discrete action you can think of in a separate function. 

> Put any discrete action you can think of in a separate function. 

At the time of writing, this can be a little annoying since CodeSignal gives you just one file to work with and makes you scroll up and down, but hopefully this will get a little less cumbersome.

**Why is this important?**

In a production environment when you’re working at a company, _everything_ you touch is to perform a business action. What do actions do? They move entities from one state to another. Any company, from the smallest to the largest, tech or otherwise, is basically a state machine. This applies to your local mom-and-pop store just as much as it does to Google or Amazon. It is critical to maintain the state of the objects that we touch. To illustrate the impact of this, can you imagine the consequences if we put out some code into production for an e-commerce website which refunds customers for returns but does not maintain that state in the database? We would never know if the customer was refunded based on the object state.

You might rightly ask at this point, seeking a less abstract answer, what exactly do we mean by state? When an employee gets paid, we want to store that information somewhere. When a bank account gets money deposited into it or withdrawn from it, we want to store that information somewhere. Whenever something happens in our system that affects its entities, we need to have a way to store it. This can be as simple as an attribute on the Employee class to store `TotalWagesReceived`, for instance, but always store state.

## 4. Slow is smooth, Smooth is fast

When I take a CodeSignal assessment, I try to plan my time beforehand so that I don’t fall behind unawares. Since there are 4 levels and each level gets successively harder, I try to plan it as 10 minutes for Level 1, 20 minutes for Level 2, and 30 minutes each for Levels 3 and 4. Without exception, my estimation has been way off the mark every single time. And when you find yourself having taken 20 minutes for level 1, it is natural to find yourself trying to rush it for the next level. Don’t. The challenge is not to write as many lines of code as possible. The challenge is to get as much of the functionality as you can working. 

> You’d be much better served slowing down to deliberate on design considerations rather than ploughing head-first into the problem trying to outrun the clock with your fingers.

No matter how far behind you find yourself, take a minute in between levels to think about your approach. Make a quick plan in your head of how you’re going to implement everything that level asks you to do before proceeding, lest you might find yourself on the second half of the level wishing you had spent a few more seconds designing the first half better. Knowing the requirements and addressing them properly beforehand allows you to produce the best possible code.

## 5. Fret not

Unlike LeetCode challenges, your success in a CodeSignal assessment is not predicated on your ability to knock the whole problem out of the park. Do your best to solve each stage of the problem with the best code you can produce. I have gotten past the pre-screen sometimes without even finishing Level 3. Also, don’t concern yourself with time or space complexity. For example, if you have some functionality you’re working on where the easiest solution is to sort a list, do it. From my experience, you are not penalized for sub-optimal performance of your code. I don’t mean to imply you should brute-force using exponential algorithms, but usually, you do not have to worry about optimizing something from O(n logn) to O(n) if that requires you writing your own algorithm to solve the problem instead of in-built sort. The evaluation is not algorithmic – keep that in mind. All that matters is the test cases. 

If you have any additional tips or questions, leave it in the comments!
