# Wes Bos - Coding and AI

https://wesbos.com/
https://syntax.fm/

https://www.crowdcast.io/c/webu23/PocVC 

## Coding with AI, Building with AI

- AI gives boost in productivity, code quality, range of what you can build
- Copilot will produce what is called "ghost code"
- Type something in english, it will let you translate it into a bash script

Ghost Code

![](./D1S1i01.png)

CLI

![](./D1S1i02.png)

- Chatbots
- Automatically write pull requests!
- Text to UI: v0.dev, Visual Copilot, openv0
  - Iterative: can take english commands to generate and revise front end code based on appearance

- Good for generating boilerplate

## Why AI?

- Faster than Google
- Context Aware
- Solves your problem, not somebody else's problem (like Stack Overflow)

## Using AI to Code

- Dummy Data

![](./D1S1i03.png)

- "Add types to this code"

![](./D1S1i04.png)

- Good for scaffolding out 

![](./D1S1i05.png)

- Make Reusable

![](./D1S1i06.png)

- Generate CSS

![](./D1S1i07.png)

- Write a Regex

![](./D1S1i08.png)

-Test driven development: if you don't know what the function is, you can write the tests and tell AI to generate the function

![](./D1S1i09.png)

- ffmpeg

![](./D1S1i10.png)

- assistance with npm install

![](./D1S1i11.png)

Should we be trusting a robot? Probably not, but what we can do is ask the robot to explain it and to generate input for tests

Give feedback on errors

Not perfect! 

## How to integrate AI Into apps

- Wes uses an AI service to transcribe the syntax podcast. It spits out data for each episode at the word level in a huge file.
- "Utterances" can be generated for transcript (data about each word)
- What we want is a nice JSON summary of an episode with topics, tweets, data/stats, etc

![](./D1S1i12.png)

- Prompts for this (extremely simplified)

![](./D1S1i13.png)

- There's an idea in AI called "tokens."
- Token limit: how much text can you send an AI before it's not able to generate something?
- Every word is a token, periods are tokens, new lines are tokens.
- A transcript of a 1 hour podcast is roughly 15,000 tokens.
- Need to save space for the output (how much text you want back counts towards tokens)

![](./D1S1i14.png)

- There are dozens of models out there. Always a tradeoff between quality, speed, and price.
- Most common one used right now is GPT 3.5 turbo 16k, meaning you can put 16,000 tokens into the model
- It is possible to condense text using AI to reduce token input size.

![](./D1S1i15.png)

- Take all the utterances and craft your detailed prompt

![](./D1S1i16.png)

- Craft the request

![](./D1S1i17.png)

- Out the other end we get very good title, description, and topics, detailed summary, tweets, speaker times, links, but somehow it's not good at math

![](./D1S1i18.png)
![](./D1S1i19.png)
![](./D1S1i20.png)



## Embeddings

- Wes built an AI tool demo that allows users to ask about DIY tools that were mentioned on the podcast.
- The tool was able to figure out both episodes where an oscillating tool was mentioned and successfully figured out that it was categorized as a DIY tool!
- How does it know about 600+ hours of transcripts??? (It doesn't)
- Embeddings are the answer.
- Can convert utterances into embeddings, which ended up costing $3 for 680+ episodes of the podcast

![](./D1S1i22.png)

- Simpler example of embeddings: tweeted "what did you do today?"
- Can take the text of the answers and convert them into numbers with some function
- Can give the AI both of these sets of numbers (embeddings) and it will be able to figure out why they are similar!

![](./D1S1i23.png)
![](./D1S1i24.png)
![](./D1S1i25.png)

- Useful for search, classification / Tagging, Grouping Items, Anomaly detection, Similar Items / Images
- We start with our utterances and convert them to embeddings. Each embedding is an array of 1,536 numbers (vector elements).

![](./D1S1i26.png)

- Can now convert a question into an embedding and find similar utterances, grab sentences before and after, and then make context and prompt

![](./D1S1i27.png)


## Are we screwed

- No. Gives us a boost with what we can do.


## What can we make with our new superpowers?

- Increases the amount of stuff we can make.
- Less about centering divs and more about pushing boundaries.
- Don't ignore this. Stay sharp!


## Q+A with Jason Lengstorf

- New developers using AI to code? Good. Use it. We can't stop it. But pause and understand what you are doing. 
- Is there a type of developer that shoudl worry about AI? Tech sector constantly changes, you have to go with the flow and embrace it. 
- Raycast is Wes' day to day (GPT 3.5) and Github CoPilot 
- Speak what you want and a React component pops out! Versailles v0.dev?? (early access only)
- When shouldn't we be using AI? Don't paste secrets in there.
- New Anthropic: with 100,000 tokens, you can paste in an entire codebase and use it as context!
- Play with it to get better
- Learn how to write good prompts
- AI will replace mass-produced low quality websites
