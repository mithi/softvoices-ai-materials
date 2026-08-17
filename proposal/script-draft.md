# SoftVoicesAI — spoken script

1049 words ≈ 7.0 min at a calm pace, leaving 60–90 s for the live demo on slide 7 — roughly 9 minutes in total. Same text sits in each slide's speaker notes.

---

**1 · Title — 0:00–0:23**

Good afternoon. I'm Shulamith Rivera Sevilla. Please call me Mithi. I'm a software engineer, and I work on user interfaces. My proposal is SoftVoicesAI. It's an interface that helps people think a little harder about the takes they see on social media. I'll spend most of my time on the design, a quick demo, and the study.

**2 · Related work — 0:23–0:55**

First, where this comes from. A few groups have shown that AI can help us think, instead of thinking for us. One idea: have the AI ask questions rather than give answers. People catch bad logic better that way. Another: use several agents instead of one voice, so you compare views instead of trusting one. And a third: let the AI push back, like a debate partner. All promising. Almost none of it tried on social media, where people react fastest.

**3 · Objective — 0:55–1:27**

So here is my goal. Build an interface where several AI agents help you think more critically about a post you just read. Not to move you to any side. We don't push a view. You stay the judge. By more critically I mean three things. You see more than one side. You notice where those sides pull against each other. And you can put them together into something new. That last part is what I want to measure.

**4 · Challenges — 1:27–2:00**

Why is this hard? Two reasons. The place: feeds put us with people who already agree, and ranking pushes the angriest posts to the top. The mind: we decide fast, then look for reasons afterwards. And if you tell someone they are wrong, they dig in. In one study, people were paid to follow the other side for a month. They came out slightly more extreme. So there are two problems. What do you even say to someone. And how do you say it.

**5 · Roles — 2:00–2:43**

First, what to say. Each agent has one job — one angle you probably would not take on your own. One says your point back to you fairly, so you feel heard. One argues the other side as well as it can be argued. One asks who else this affects. One reminds us we have feared this before: Plato worried about writing. One points at the jump from the evidence to the conclusion. One asks if a single small study is enough. One notices loaded words like terrifying. And one asks what a vague word actually means. Not every angle fits every post, so the system picks.

**6 · Dialogue — 2:43–3:22**

Second, how to say it. This part comes from research on good listening. Speak like a thoughtful friend, not a debate opponent. Keep it short and plain. Say what is fair in their view first. Give them something to think about instead of a verdict. Say maybe, not definitely. Ask instead of tell. And never make it about the person. Here is the difference. Instead of “those screen time studies are oversold” — “those numbers do look alarming, I get the worry. Though doomscrolling and calling a friend aren't really the same screen time, are they?”

**7 · Pipeline & demo — 3:22–3:58**

Here is how one session runs. You get a real post that people argued about. One question: what is this claiming, and what do you think. You write your take. Then the agents comment — on the post, and on what you wrote. Two at a time. You can tag any comment privately: raised something new, worth sitting with, shifted my view, didn't land. Or flag it if it looks false. The counts stay private, so nothing becomes a winning side. Then you write your answer again. Let me show you.

**8 · Study design — 3:58–4:27**

The study. A small pilot first, three to five people: fix the prompts, train the scorers, see how long a session takes. Then the main study, about twenty-four people who use social media daily and say they want to think more critically. Session zero is consent and a practice run. Sessions one to six are one post each, on different days, in rotated order. Session seven is a questionnaire and an interview.

**9 · Research questions — 4:27–4:53**

Three questions. First: is the second answer deeper than the first? Two people score every answer without knowing which is which. Second: how does it feel to use — is the effort useful or just confusing, is it enjoyable, would they keep using it. Third: what do people actually do — which agents get reactions, which get flagged, and what comes up in the interviews.

**10 · RQ1 analysis — 4:53–5:22**

This is the first question. The numbers on screen are simulated. I wrote the analysis code and ran it on fake data, to check the pipeline works. What I would report is this: the raw difference; then the same difference after controlling for length, because second answers are simply longer; and then a version that treats the six posts as fixed. If it only held in the first row, I would say so.

**11 · RQ2 analysis — 5:22–5:42**

For the second question, three pictures. One dot per person, so you see the spread and not just an average. The trend over six sessions, to see if the novelty wears off. And useful effort against wasted effort — I want people in the bottom right corner: useful, not confusing.

**12 · RQ3 analysis — 5:42–6:01**

The third question is descriptive. Which agents got which reactions. Whether shifted my view fades as people get used to them. And which roles people found useful at the end. Every flagged comment gets checked afterwards and sorted: a real error, a fair debate, or just disagreement.

**13 · Limitations — 6:01–6:32**

Now the honest part. There is only one version of the system, so I cannot tell you which piece did the work — the angles, the tone, or simply writing twice. That needs a follow-up study. The agents always appear in the same order, so role and position are mixed together. The per-session questions are single items. Everyone here already wants to think better. And I left out the most heated topics, which are the hardest ones.

**14 · Summary — 6:32–6:60**

To sum up. I am building an interface where several AI agents help people take a second look at what they read. Each one has its own angle, and each one speaks like a thoughtful friend. And I am testing whether that second look is actually deeper, how it feels to use, and what people do with it. Everything will be public. Thank you. I am happy to take questions.

---

## Cuts if you run long

- Slide 2: name one line of related work instead of three.
- Slide 5: describe four agents, let the slide carry the rest.
- Slide 12: drop the flag-checking sentence.
- Slide 13: give two limitations, keep the rest for Q&A.
