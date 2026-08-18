SoftVoicesAI - Final Spoken Script

# Slide 1

Good afternoon. I'm Shulamith Rivera Sevilla. Please call me Mithi. I'm a software engineer focused on user interfaces and experiences.

My proposal is SoftVoicesAI. It is an interface that aims to help people think more critically about posts they see on social media.

Today, I'll focus on three things. I'll talk about the ideas behind its design, show you a quick demo of how it works, and then present the research questions and study plan.

# Slide 2

The proposal is inspired by research exploring how AI can be used as a thinking partner, rather than simply as an answering machine. The papers on this slide explore that idea in different settings, including research-paper reading, research ideation, and group decision-making. Some have also shown the value of using multiple agents to introduce different perspectives.

These studies led me to wonder: could we bring the idea of an AI thinking partner into something more ordinary - the social-media posts?

# Slide 3

The goal of SoftVoicesAI is to help users think more critically about the social-media posts they read. And it does so by using multiple AI agents. It is important to note that SoftVoicesAI doesn't push any specific viewpoint; it doesn't try to make you think a certain way. The goal is to encourage users to think more critically.

What I mean by "thinking more critically" is  not treating an issue as simply good or bad. It means recognizing that there may be both harms and benefits, and those are case to case and depend on different factors, like the specific contexts and situations.

# Slide 4

Thinking critically on social media is difficult.

First, platforms are incentivized to keep us engaged. As a result, our feeds prioritize posts that provoke a reaction and repeatedly show us views similar to our own.

Second, people often decide by gut feel and find reasons afterward, rather than reasoning before deciding. And hearing, "You're wrong, and here's why," can also make us cling even more tightly to what we already believe.

So SoftVoicesAI has to address two design problems: what to say - things that the user might not have thought about - and how to say them so that the user actually considers them and not shut them down.

# Slide 5

SoftVoicesAI has eight agents, each offering a specific thing the user may have overlooked. They consider questions such as: What is strongest in the user's own point? What would a well-argued opposing view look like? Whose perspective is missing? What does the evidence actually show? And is the language making the claim sound stronger than the evidence supports?

# Slide 6

The agents should sound less like someone trying to win an argument and more like a thoughtful friend.

A friend does not try to sound smart or begin by telling you that you are wrong. They try to understand how you reached your view, acknowledge what is reasonable in it, and then offer something you may not have considered.

That means avoiding language that leaves the user feeling judged, corrected, or pushed.

Reflection cannot be forced; the best the system can do is make it easier.

# Slide 7

Demo
https://claude.ai/code/artifact/021464f8-a783-4565-9d27-e3f65febfffb

# Slide 8

First, we will run a small pilot to refine the procedure and train the raters. For the main study, we will analyze about twenty-four active social-media users, using six carefully selected real posts.

The study consists of eight short sessions, each lasting around ten to twenty minutes. Session zero covers consent, a background questionnaire, and a practice run.

In sessions one through six, participants complete the full SoftVoicesAI pipeline with one post per session. Everyone sees all six posts, but in a counterbalanced order.

Session seven consists of an end-of-study questionnaire and an interview.

# Slide 9

First, does integrative complexity (a measure of critical reflection) increase from the initial response to the revisited response? Two blind raters will score each response from one to seven.

Second, how do users experience the system? Does the effort feel productive or wasted? Is it effective and enjoyable, and would they use a system like this?

Third, what patterns appear across the six sessions and eight roles? I will examine reactions, flags, response length, and interview themes.

I have one hypothesis-testing question, followed by two descriptive and exploratory questions.

# Slide 10

The numbers here are simulated, not study results.

The three models ask three versions of the same question.

First: does a participant's revisited response score higher than their own initial response? The model also accounts for the fact that some posts naturally produce more complex responses than others.

Second: does that difference remain after accounting for response length? If it becomes smaller, longer answers may explain part of the increase.

Third: does the conclusion change if we treat these six posts as six specific cases, rather than as a random sample of social-media posts?

We would show all three results so it is clear how robust - or sensitive - the finding is.

# Slide 11

The second question is about how it feels to use the system. Again, this is fake data.

Chart 1 compares productive effort with wasted effort: ideally, using the system requires thought without creating unnecessary confusion.

Chart 2 shows the variation between participants' ratings.

Chart 3 follows each measure across six sessions, so we can see whether the experience changes with repeated use - for example, whether the novelty wears off or the system becomes easier to use.

# Slide 12

The third question is exploratory. It asks what people actually do with the system across repeated sessions.

We will examine how often participants react, which reactions each role receives, whether revisited responses become longer, and how these patterns change over time.

We will compare that behavior with what participants say in the final questionnaire and interview.

Flagged comments will also be checked afterward and classified as a factual error, a debatable claim, or simple disagreement.

# Slide 13

This study evaluates SoftVoicesAI as a whole. If responses improve, we cannot tell whether that is because of the agent roles, the communication style, or simply writing a second response. That will require a controlled follow-up.

Because the agents always appear in the same order, we also cannot separate the effect of the role from its position.

The short questionnaires reduce participant burden but may be less reliable, and some inaccurate agent comments may go unnoticed. Also, we include only participants who report that they want to think more critically.

Finally, this first study leaves out highly charged topics, especially those involving identity.

# Slide 14

To summarize, this research contributes the SoftVoicesAI interface; an evaluation of its association with integrative complexity, user experience, and behavior; and public design and study materials.

The larger question behind the project is whether we can design human-AI interfaces that do not think for people, but help people do more of their own thinking.

Thank you. I am happy to take questions.
