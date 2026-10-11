+++
date = '2026-10-10T09:00:00+10:00'
draft = false
title = 'AI Without the Mystery - The Full Article'
tags = ['Artificial Intelligence', 'Digital Safety', 'Privacy', 'Soft Skills']
summary = "A guide on to how AI works, where it can help and how to check its answers, protect your privacy and use it safely."

+++

## Introduction

Artificial intelligence (AI) is the ability of a computer system to perform tasks we usually associate with human thinking: recognising patterns, understanding language, generating text, making predictions and reasoning towards decisions. In daily life, however, most of us meet a narrower kind of AI.

Broadly, AI falls into two families. **Generative AI** creates new content, whether text, images, music or computer code, from a prompt. Chatbots and image generators are the obvious examples. **Predictive AI** analyses patterns in existing data to estimate what is likely to happen next, as spam filters, recommendation systems and house-price forecasts do.

What most of us call AI, and what this guide focuses on, is generative AI: systems such as ChatGPT, Claude or Gemini that can produce words, pictures, sound or computer code from a prompt. It is not important to master these categories. The one point worth holding on to is that AI is broader than the few chatbots we happen to use each day.

To understand how this kind of AI works, start with the autocomplete on a phone keyboard. It recommends the next most probable set of letters or words that would complete the sentence, one small piece at a time. Generative AI does something similar on a far larger scale, and the small pieces of words it works with are called **tokens**.

## Tokens

Many providers charge by the number of tokens that a prompt and its reply use. Different providers split text differently, but a useful approximation is four tokens for every three English words, so a 1,000-word message may use about 1,300 to 1,500 tokens. Some plans include a monthly token allowance while others charge extra once you pass the limit. The practical consequence is simple: long prompts, long answers and many generations can use up a monthly allocation quickly. You can see how a given sentence is split using the [OpenAI tokenizer](https://platform.openai.com/tokenizer).

<img src="/img/tokenizer.png" alt="How a chatbot breaks text into tokens" width="700">

## The stages of an AI model: from learning to answering

An AI assistant is not created in one step. A useful way to picture its life is to prepare examples, train a model to find patterns, tune how it responds, and then run it each time someone asks a question.

<pre class="mermaid">
flowchart LR
    A(📚 Prepare data) --> B(🧠 Train model) --> C(🎯 Fine-tune) --> D(🚀 Deploy) --> E(💬 Inference: answer)

    classDef stage1 fill:#dff3ff,stroke:#39a9db,color:#163b50,stroke-width:2px
    classDef stage2 fill:#e8e1ff,stroke:#8068d8,color:#30245a,stroke-width:2px
    classDef stage3 fill:#ffe5ef,stroke:#e66b99,stroke:#54235a,stroke-width:2px
    classDef stage4 fill:#fff0d0,stroke:#e2a72e,stroke:#513c12,stroke-width:2px
    classDef stage5 fill:#dff5e8,stroke:#48a66b,stroke:#19462b,stroke-width:2px

    class A stage1
    class B stage2
    class C stage3
    class D stage4
    class E stage5
</pre>

<script type="module">
  import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@11.12.0/dist/mermaid.esm.min.mjs';
  mermaid.initialize({ startOnLoad: false, theme: 'base', flowchart: { curve: 'basis', htmlLabels: true } });
  await mermaid.run({ querySelector: '.mermaid' });
</script>

### 1. Gather and prepare data

The people building a model first collect data or create examples suited to the task, such as text or labelled pictures for an image classifier, and then filter and organise that material so computers can process it. Common sources include web pages gathered by large crawls such as Common Crawl, books and news articles often licensed from publishers, public code from sites such as GitHub, reference works such as Wikipedia and conversations collected from people using the tool. The data shapes what a model can learn, and it carries the flaws of its sources, so more data does not automatically mean better answers.

There is also a growing question about running out of good data. The research group Epoch AI estimates that the world holds roughly 300 trillion tokens of useful public human text, and that models could exhaust that pool somewhere between 2026 and 2032, or sooner if the same material is reused heavily. Providers are already paying for access to books, archives and other private collections to secure an edge. The estimate is explained in [Epoch AI's study on the data ceiling](https://epochai.org/blog/will-we-run-out-of-data) and covered in plain language by [PBS NewsHour](https://www.pbs.org/newshour/science/will-ai-run-out-of-data-an-expert-explains-what-to-know-about-the-ai-data-crunch).

### 2. Train the model

During **training**, the algorithm adjusts the model's internal numbers so that it learns to produce results similar to the data it is trained on. A model, for example, practises predicting missing or next pieces of text across a very large number of examples. This takes enormous computing power and specialised chips working together in data centres. To get a feel for the scale, an early model such as GPT-3 is estimated to have consumed about 1,287 megawatt-hours of electricity, roughly the annual use of more than 100 average American homes. Modern models are far larger again. The figures come from [a widely cited research estimate](https://arxiv.org/abs/2104.10350), with household comparisons from the [US Energy Information Administration](https://www.eia.gov/tools/faqs/faq.php?id=97&t=4).

### 3. Tune its behaviour

A trained model is often **fine-tuned** with more focused examples drawn from the way it will be used, such as question-and-answer pairs, and with feedback from people who judge its output. This stage shapes how the model responds, although it does not guarantee that every answer is correct, fair or safe.

Tuning changes several things at once. It teaches a model to refuse harmful requests, such as instructions for making a weapon or a virus, yet the same training can overshoot and cause an assistant to decline harmless requests, for example when a nurse asks a genuine medical question. It sets the model's tone and house style, so one tool sounds warm and chatty while another is blunt and brief, and a support bot can be tuned on a company's own question-and-answer pairs so that it replies in the company's wording and follows its rules. Much of this happens through learning from ratings: in reinforcement learning from human feedback, people compare pairs of answers and pick the better one, and over time the model leans towards the style people reward.

That reliance on approval has a side effect known as the flattery problem, because models learn to agree with the user. [Anthropic's 2023 research](https://www.anthropic.com/research/towards-understanding-sycophancy-in-language-models) found that when a person states a mistaken belief, both people and the scoring models often prefer a confident answer that agrees with them over the correct one. This is why an assistant may open with "You're absolutely right!" even when you are wrong. Some providers also tune against a written set of principles, such as "be helpful and avoid harm", and then have the model critique and rewrite its own answers against those rules.

### 4. Test before release

Developers evaluate the model with a range of tasks and safety checks. They look for accuracy, harmful responses, privacy risks and the way the model behaves when a question is unclear, and they compare its output against known answers and known failures.

### 5. Run it: inference

**Inference** is the name for using a trained model. When you send a prompt, the model processes it and generates an answer. For a chatbot, that means predicting a response one small piece at a time, token by token.

### 6. Keep it running

After release, providers continue to monitor the model, fix problems and adjust its behaviour through updates to its instructions or, less often, to the model itself. A major new version is usually trained again from a newer and larger body of data, which is one reason the tools change so quickly from year to year.

<img src="/img/inference.gif" alt="How an AI model generates an answer token by token" width="700">

## How can you ask a right prompt

The quality of an answer depends heavily on the question. A short, vague request gives the model little to work with, so it falls back on the assumptions of its training data. A few deliberate details change the answer out of all proportion to the effort they take.

### Improve a weak prompt

A weak prompt asks, "Help me make a shopping list." A better one says, "Help me make a shopping list for three easy vegetarian dinners for one person, avoid nuts and keep the ingredients inexpensive." The second version supplies the audience, the limits and the context. State those three things and the model stops guessing. Say who the answer is for, what you want covered and what should be left out.

### Five questions to sharpen any request

Before you send a prompt, answer five questions. What are you asking for: a draft, a summary, a comparison or a set of questions? Who is it for, so that the language and level fit: for example, "explain this to someone new to the topic". What are the limits, such as length, number of options or budget? What should it show, such as its sources or its reasoning? And what should it avoid, such as invented facts, jargon or advice it cannot support?

### A prompt that works

> Help me plan three easy vegetarian dinners for one person using ingredients I already have. Avoid nuts, keep the cost low and give me a short shopping list for anything missing.

### Let the AI interview you

Sometimes the best prompt is no prompt at all. Ask the AI to interview you instead.

> I am planning a trip. Ask me the questions you need so you can give me a good plan.

This turns the model into an interviewer, so it gathers the details before it answers. It is especially useful when you do not yet know what information matters, whether you are booking travel, choosing a product or preparing for an appointment. If you try it, add a small limit, such as asking for no more than five questions, one at a time.

## Ways of saving money

The cheapest way to use AI is often to use it less than you think you need to. Start with the free version of a tool. Free chatbots are good enough for everyday questions, and a paid plan is worth considering only when you have a specific job the free tier cannot handle, such as very long documents, heavy image work or daily use. Know how you are billed, because a monthly subscription costs the same however much you type whereas usage-based apps and developer tools charge by the word, so a long conversation becomes a larger bill.

You can cut the cost of a single request in several easy ways. Words such as "please" and "thank you" do not improve the answer, but on usage-based tools every extra word is a cost. Ask for short answers, for instance "answer in three bullet points" or "keep it under 100 words". Remember that output usually costs more than input, so a request that invites a very long reply is the expensive part. Start a fresh chat for a new topic, because a long thread is resent with every message. Paste only the paragraph you want answered rather than the whole document, and use the smallest model that can do the job, since a quick rewrite does not need the most powerful and costly one.

It also helps to be specific about the change you want. Asking to "show me just the corrected paragraph" is cheaper than regenerating an entire document. Turn off optional features you are not using, such as web search or image tools, if your plan charges for them, and take a free trial only when you need a short burst of heavy use, remembering to cancel before it renews. Watch tools that charge by credits or by the minute, because image, video and audio generation cost more per use, and set the size, length and number of outputs you actually need. Finally, keep an eye on your usage: set a spending limit on any account that bills per use, check the usage page each month and cancel subscriptions you have stopped using.

## Where AI helps and where it does not

It is tempting to treat AI as either a marvel or a menace. In practice it suits some jobs well, some jobs only with care, and a few jobs not at all.

### Good for everyday, low-stakes tasks

For tasks where a mistake is easy to spot and cheap to fix, AI is a genuine time-saver. It can brainstorm meal ideas from ingredients you already have, turn rough notes into a polite email or a club newsletter, and explain a familiar topic in simpler words. It can assemble a packing checklist once you give it the destination and dates, suggest questions to take to a doctor or a mechanic, or hold a rehearsal conversation, such as pretending to be a receptionist while you practise booking an appointment. It can summarise a public article you paste in, provided you check the original before passing it on, and it can generate a quiz for a family gathering or ideas for a hobby project.

### Useful, but only with checking

Other tasks sit in the middle. AI can help, but the result needs a review before you rely on it. These include travel plans, product comparisons, recipes involving allergies, local services and historical facts. When drafting a complaint letter, let the AI organise the language, then replace every placeholder and check every claim. When translating a simple message, ask a fluent speaker to check anything important. When working out a budget, use the AI to suggest categories or questions, then verify the numbers with a calculator and your own bills. When reading about a medical term, use the AI to prepare questions for a qualified professional, not to diagnose yourself.

### Do not hand over the decision

Some decisions should never rest on an AI answer. These include emergencies and symptoms that need urgent care, changes to medicine, and the interpretation of test results. They include deciding whether to invest, borrow money, buy cryptocurrency or make any major financial move, and matters such as legal deadlines, contracts, wills, immigration and tax. They include sharing a private family dispute, another person's health details or confidential work information, and sending money, passwords or identification because a message, image or voice recording seems persuasive. AI can help you prepare a question for an expert. It is not the expert who accepts responsibility for the answer.

## AI scams

Scams have always relied on pressure and a plausible story. AI makes the story more convincing, which is why a simple routine helps.

**Pause.** Ask whether the answer is pushing you to act quickly, spend money, share data or make a health or legal decision. If it is, slow down. **Prove.** Find the original source. For Australian government information, look for an official `gov.au` website. For a medicine, check with a pharmacist, a doctor or the official product information. For a bank, use the number printed on your card or statement. **Proceed** only once the important point agrees with a trustworthy, independent source.

### Fact-checking habits worth building

A few habits cover most situations. Ask the model, "What are your sources? Give direct links, not just names," and then open them, since a link can be wrong or invented and the page must actually support the claim. Search the key claim in your own words and compare at least two reliable sources for anything important. Check the date, because rules, prices, opening hours and public figures change. Look for the original source, since a hospital, government department, bank, manufacturer or recognised professional body is usually more dependable than a copied social-media post. If the answer involves numbers, redo the arithmetic yourself. If you cannot verify a claim, say so and ask a person or an organisation that can.

### Tools that can help spot AI-made content

A number of free tools can flag material that may have been generated by AI, though none is conclusive. For pictures and video, [Hive AI Detector](https://hivemoderation.com) and [AI or Not](https://www.aiornot.com) give a quick verdict, [Illuminarty](https://illuminarty.ai) highlights the parts of an image that influenced its answer, [Sightengine](https://sightengine.com) is built for bulk checks, and [Content Credentials](https://contentcredentials.org/verify) reads a built-in provenance record when an image carries one. For writing, [GPTZero](https://gptzero.me) and [Originality.ai](https://originality.ai) estimate how likely text is to be machine-generated, but treat them as weak signals because they are easily fooled by short or edited passages. For voice and deepfake video, [Reality Defender](https://www.realitydefender.com) examines audio, images and video for synthetic media.

A detector should support your judgement, not replace it. The most useful single step is often to find the original: reverse-image searches on [Google Lens](https://lens.google) or [TinEye](https://tineye.com) can reveal an earlier, unedited copy of a picture that has been given a misleading caption. Look too at the small details that generators frequently get wrong, such as hands, text, jewellery, reflections and shadows. And remember the underlying rule: a polished image is not proof that an event happened.

### The new voice is not proof

Scammers now have access to the same audio and image tools as everyone else, and a short clip of a person's voice is often enough for a convincing imitation. A frightening call might sound exactly like a grandchild in trouble, urging you not to tell anyone and to send money at once. The [US Federal Trade Commission](https://consumer.ftc.gov/comment/180311) warns that even a brief recording can be turned into a clone, and its advice is straightforward: never trust the voice on its own. Hang up and call the relative back on a number you already know, rather than the one the caller provides. Agree on a family safe word or a question only your family could answer, and never let urgency make the decision for you. A genuine organisation will let you verify things independently, while a scammer tries to keep you inside their call, message or link.

### Scam signs worth memorising

The warning signs repeat across many scams: a surprise prize, inheritance, refund or romance that comes with a request for money; a message claiming your account will close today unless you click a link; a caller who wants remote access to your computer or phone; a photo or video of a public figure promoting an investment that cannot be found on their official website; and a request for a code that has just been sent to your phone, which is often the key to your account. When in doubt, stop and talk to someone. A second pair of eyes is a powerful security tool.

### Pictures, videos and "too good to be true" evidence

A photograph used to feel like strong evidence. Now it may be real, edited, generated or taken from somewhere else and given a false caption. Staring at every eyelash or shadow is not a dependable test on its own. Instead, check the context: who first posted it, whether there is a date and location, whether reputable news outlets report the same event, whether the account has a long history or was created recently, and whether the material is designed to make you angry, frightened or eager to invest before you can think. A video of a politician, a celebrity or a doctor may be a deepfake, so treat an extraordinary claim as unproven until it appears through that person's official channels or through reliable reporting. Seeing something "with your own eyes" is no longer the end of the question. It is the beginning of it. AI-generated images can still be a delight, used for an invitation, a story illustration or an idea for a garden; simply label them honestly if another person might mistake them for a real event.

## Popular AI subscriptions compared, including free plans (prices in US dollars per month, checked October 2026)

The same assistant is rarely the best at everything, so it helps to start from the job you want done. In each table below the free options come first, followed by the paid ones from cheapest to most expensive. Prices are US dollars per month, checked October 2026.

### Where to find them

| Assistant | Website |
|---|---|
| Claude (Anthropic) | [claude.ai](https://claude.ai) |
| ChatGPT (OpenAI) | [chatgpt.com](https://chatgpt.com) |
| Gemini (Google) | [gemini.google.com](https://gemini.google.com) |
| Copilot (Microsoft) | [copilot.microsoft.com](https://copilot.microsoft.com) |
| Perplexity | [perplexity.ai](https://www.perplexity.ai) |
| Grok (xAI) | [grok.com](https://grok.com) |
| Brave Leo (built into the Brave browser) | [brave.com/leo](https://brave.com/leo/) |
| Comet (Perplexity's AI browser) | [perplexity.ai/comet](https://www.perplexity.ai/comet) |
| Leonardo.Ai (images and video) | [leonardo.ai](https://leonardo.ai) |

### 1. Everyday questions, writing and brainstorming

Good for drafting a message, explaining a topic, planning a trip or sorting out ideas.

| Option | Cost as of Oct 2026 | What you get | Link |
|---|---|---|---|
| Claude Free | Free | Sonnet and Haiku models, web search, file creation, memory | [claude.com/pricing](https://claude.com/pricing) |
| ChatGPT Free | Free | Unlimited text chats on GPT-6 Luna (fair-use rules apply), limited images and voice. May show ads | [chatgpt.com/pricing](https://chatgpt.com/pricing) |
| Gemini Free | Free | Gemini 3.5 Flash-Lite, image generation, Gemini Live voice chat | [gemini.google/subscriptions](https://gemini.google/subscriptions/) |
| Copilot Free | Free | Copilot in the browser and Windows, with usage limits | [copilot.microsoft.com](https://copilot.microsoft.com) |
| Grok Free | Free | Limited access on grok.com and inside X | [grok.com/plans](https://grok.com/plans) |
| Google AI Plus | $4.99 | 2x the free usage, Gemini 3.6 Flash and 3.1 Pro | [gemini.google/subscriptions](https://gemini.google/subscriptions/) |
| ChatGPT Go | $8 | More messages, uploads and images than Free. May show ads | [chatgpt.com/pricing](https://chatgpt.com/pricing) |
| Google AI Pro | $19.99 | 4x the free usage, Gemini 3.1 Pro and more | [gemini.google/subscriptions](https://gemini.google/subscriptions/) |
| ChatGPT Plus | $20 | Full access to the top models and higher limits | [chatgpt.com/pricing](https://chatgpt.com/pricing) |
| Claude Pro | $20 | Higher limits and access to the strongest Claude models | [claude.com/pricing](https://claude.com/pricing) |
| Perplexity Pro | $20 | Higher limits and a choice of models | [perplexity.ai](https://www.perplexity.ai/hub/pricing) |

### 2. Working with files and documents

Unlike a plain chatbot, these tools work directly with the documents you upload.

| Option | Cost as of Oct 2026 | What you get | Link |
|---|---|---|---|
| Any free chatbot above | Free | Paste or upload a short document (with private details removed) and ask for help | |
| Claude Pro | $20 | Long documents, file creation and memory | [claude.com/pricing](https://claude.com/pricing) |
| ChatGPT Plus | $20 | File uploads, image understanding and code interpreter | [chatgpt.com/pricing](https://chatgpt.com/pricing) |
| Google AI Pro | $19.99 | Large context windows for long documents | [gemini.google/subscriptions](https://gemini.google/subscriptions/) |

### 3. Images, video and audio

Good for invitations, story illustrations, garden ideas and short clips. Label AI-made media honestly, and expect quality to vary with the task.

| Option | Cost as of Oct 2026 | What you get | Link |
|---|---|---|---|
| Gemini Free | Free | Image generation and editing | [gemini.google/subscriptions](https://gemini.google/subscriptions/) |
| ChatGPT Free | Free | Limited image generation | [chatgpt.com/pricing](https://chatgpt.com/pricing) |
| Leonardo.Ai | Free to start | Image and video generation with a daily credit allowance | [leonardo.ai](https://leonardo.ai) |
| Google AI Pro | $19.99 | Image and some video generation features | [gemini.google/subscriptions](https://gemini.google/subscriptions/) |
| ChatGPT Plus | $20 | More images and faster generation | [chatgpt.com/pricing](https://chatgpt.com/pricing) |

### 4. Research with sources

Good for comparing products, background reading and questions where you want links you can open and check yourself. Always open the sources, because a model can cite a page that does not say what it claims.

| Option | Cost as of Oct 2026 | What you get | Link |
|---|---|---|---|
| Perplexity Free | Free | Answers with linked sources, with a small daily number of advanced searches | [perplexity.ai](https://www.perplexity.ai) |
| Gemini Free | Free | Web search with links | [gemini.google.com](https://gemini.google.com) |
| ChatGPT Free | Free | Web browsing on request | [chatgpt.com](https://chatgpt.com) |
| Perplexity Pro | $20 | Higher research limits, more file uploads and a choice of models | [perplexity.ai](https://www.perplexity.ai/hub/pricing) |
| Claude Pro | $20 | Research features and projects for organising sources | [claude.com/pricing](https://claude.com/pricing) |

### 5. Coding help

Useful for explaining code, fixing small bugs and writing short scripts, always with a review before you run anything.

| Option | Cost as of Oct 2026 | What you get | Link |
|---|---|---|---|
| Any free chatbot above | Free | Explain code, suggest fixes and write short snippets | |
| Claude Pro | $20 | Strong coding help and longer context | [claude.com/pricing](https://claude.com/pricing) |
| ChatGPT Plus | $20 | Advanced code reasoning and tools | [chatgpt.com/pricing](https://chatgpt.com/pricing) |

*Features and prices change often. Confirm the current details on the provider's own page before you pay.*

## Closing thought

AI is neither magic nor useless. It is a tool. A calculator does not decide whether you can afford a holiday, and a map does not decide whether it is safe to travel. In the same way, AI does not decide what is true, wise or right for you. Use it for ideas, drafts and explanations. Protect your private information. Check important facts, and slow down when money, health or urgency enters the conversation. Curiosity plus caution is not fear of technology. It is confidence with technology.
