+++
date = '2026-09-17T11:15:30+10:00'
draft = false
title = 'AI Without the Mystery'
tags = ['Artificial Intelligence', 'Digital Safety', 'Privacy', 'Soft Skills']
summary = "A practical introduction to using AI wisely."
+++

## Introduction:

- **Artificial intelligence (AI)** is capability of a system to perform tasks typically associated with human intelligence. Few examples:
  - recognising patterns
  - comprehending text 
  - generating language
  - making predictions
  - decisions based on reasoning
- Broadly speaking, AI falls into two main categories:
  - **Generative AI**: Generats new content such as text, images, music or code from a prompt. e.g. Chatbots, Image generation.
  - **Predictive AI**: Analyses patterns in data to estimate what is likely to happen next. Spam filters, Recommendation systems and House price Forecasting.
- What most of us call AI in everyday life refers to **Generative AI**: systems like ChatGPT, Claude or Gemini that can produce words, pictures, sound or computer code from a prompt. 
- It's not important to understand categories of AI in detail - Only thing necessary to know is that AI is more than just ChatGPT, Claude, Gemini etc. though that may be what we most use on a day to day basis.
- To understand how this kind of AI works
  - In its simplest form - Think of it like your mobile-phone keyboard autocomplete. It would **recommend** the next set of most **probable** set of **alphabets or words** most **suited** to **complete the sentence** - one small piece of a word at a time.
- These pieces of words are called **tokens**. 

## Tokens
- Many AI providers charge you by how many tokens a prompt and reply use. Different Model providers have different tokenization algorithms but You can approximate it as 4 token for every 3 english words. E.g. 1,000-word message might use roughly 1,300 to 1,500 tokens. Some plans include a monthly token allowance, while others charge extra once you pass the limit. 
- The point is simple: long prompts, long answers and many generations can use up a monthly allocation quickly.
- https://platform.openai.com/tokenizer

<img src="/img/tokenizer.png" alt="How a chatbot breaks text into tokens" width="700">

## The stages of an AI model: from learning to answering

<pre class="mermaid">
flowchart LR
    A(📚 Prepare data) --> B(🧠 Train model) --> C(🎯 Fine-tune) --> D(🚀 Deploy) --> E(💬 Inference: answer)

    classDef stage1 fill:#dff3ff,stroke:#39a9db,color:#163b50,stroke-width:2px
    classDef stage2 fill:#e8e1ff,stroke:#8064d8,color:#30245a,stroke-width:2px
    classDef stage3 fill:#ffe5ef,stroke:#e66b99,color:#54253a,stroke-width:2px
    classDef stage4 fill:#fff0cf,stroke:#e2a72e,color:#513c12,stroke-width:2px
    classDef stage5 fill:#dff5e8,stroke:#48a66b,color:#19462b,stroke-width:2px

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

An AI assistant is not created in one step. A useful way to picture its life is: prepare examples, train a model to find patterns, tune how it responds, then run it each time someone asks a question.

### 1. Gather and prepare data
- The responsible people collect data or create examples suited to the task, such as text or labelled pictures for an image classifier. They filter and organise this material so it can be processed by computers.
- Common sources include:
  - web pages gathered by large crawls such as Common Crawl 
  - books and news articles (often licensed from publishers)
  - public code from sites such as GitHub
  - reference works such as Wikipedia and conversations collected from people using the tool.
- The data shapes what a model can learn. It may contain gaps, old information, mistakes or unfair patterns, so more data does not automatically mean better answers.
- **Are we running out of clean data?** Broadly, yes, as a forecast. Researchers at Epoch AI estimate the useful stock of public human-written text at around 300 trillion tokens and project that language models could use it all up at some point between 2026 and 2032, or sooner if models are trained heavily on the same data. 
- As clean text grows scarce, companies are already paying for it, for example through deals to use forum posts and news archives.
  - [Will we run out of data to train large language models? (Epoch AI, 2024)](https://epoch.ai/publications/will-we-run-out-of-data-limits-of-llm-scaling-based-on-human-generated-data)
  - [AI “gold rush” for training data could run out of human-written text (PBS NewsHour, 2024)](https://www.pbs.org/newshour/economy/ai-gold-rush-for-chatbot-training-data-could-run-out-of-human-written-text-as-early-as-2026)

### 2. Train the model
- During **training**, the algorithm adjust a model’s internal numbers so it learns to produce similar results to the data it is trained on. A model, for example, practises predicting missing or next pieces of text across a very large number of examples.
- But it takes a lot of computation power and specialised chips working together in data centres.
- To get a feel of it currently we are on GPT 6 model but training of one of the earlier OpenAI’s GPT-3 used about **1,287 megawatt-hours (MWh)** of electricity or enough to power **119 homes in US for an entire year**. - References
  - [Research estimate for GPT-3](https://arxiv.org/abs/2104.10350)
  - [US household electricity figures](https://www.eia.gov/tools/faqs/faq.php?id=97&t=4)

### 3. Tune its behaviour
- A trained model may then be **fine-tuned** with more focused examples based on the usecase it is going to be used for - such as question-and-answer pairs. 
- This is done with model learning based on human feedback on the output.
- This stage shapes how the model responds. It does not guarantee that every answer is correct, fair or safe.
- **Examples of what tuning changes:**
  - **Refusals and safety.** Tuning teaches a model to decline harmful requests, such as instructions for making a weapon or a virus. The same tuning can overshoot: assistants sometimes refuse harmless requests, such as a nurse asking a genuine medical question.
  - **Tone, personality and house style.** Providers tune the assistant’s voice, so one tool sounds warm and chatty while another is blunt and brief. A support bot can be tuned on a company’s own question-and-answer pairs so it replies using the company’s wording and rules.
  - **Learning from ratings.** In “reinforcement learning from human feedback”, people compare pairs of answers and pick the better one. Over time the model leans toward the style people reward, which is part of why today’s answers are more polite and better formatted than the earliest ones.
  - **The flattery problem.** Training on human approval has a side effect: models learn to agree with you. [Anthropic’s 2023 research](https://www.anthropic.com/research/towards-understanding-sycophancy-in-language-models) found that when a person states a mistaken belief, both people and the scoring models often prefer a confident answer that agrees with them over the correct one. This is why an assistant may open with “You’re absolutely right!” even when you are wrong.
  - **Written rules.** Some providers tune with a written set of principles, such as “be helpful and avoid harm”, then have the model critique and rewrite its own answers against those rules.

### 4. Test before release
- Developers evaluate the model with tasks and safety checks. They look for things such as accuracy, harmful responses, privacy risks and how it behaves when a question is unclear.

### 5. Run it: inference
- **Inference** is the name for using a trained model. When you send a prompt, the model processes it and generates an answer. For a chatbot, it predicts a response in small pieces called tokens.

### 6. Monitor and improve
- After release, providers monitor performance, fix problems and may update the software, its instructions or the model itself. A major new model can require another training process.
- A lot of models use the information we give and our usage pattern to further train the model. We will later go through what information is safe and not safe to share with an AI Chatbot.

<img src="/img/inference.gif" alt="Inference: a chatbot generating an answer token by token" width="700">

### Can I trust what AI tells me?

- **Where its knowledge comes from.** An AI assistant is trained on an enormous collection of text and code gathered from the open internet, books, news articles, social media and public code repositories. It is not fed one trusted encyclopedia, so its sources are a mix of accurate, outdated and simply wrong material, and nobody checks every sentence before training.
- **A simple picture in your mind.** Imagine a keen apprentice who has learnt from millions of books, code, social media feeds, news and conversations.
  - **Ask for a first draft of a speech:** excellent task.
  -** Ask whether your chest pain is dangerous:** wrong task. The apprentice cannot examine you, take responsibility or call an ambulance.
  - **Ask for the opening hours of a local shop:** most of the mordern model uses tools (e.g. a web browser) to search through a shop’s own website.
- it could answer your question in a very convincingly confident answer but wrong or irrelevant to your question. This is called a “confabulation”, or **hallucination**. It can invent names, dates, quotes, statistics, laws, references and even whole web pages, and it presents them with total confidence. 
- With the earlier models if you ask it questions like "what is todays date" it would answer a date in the past probably when it was trained on. Now-a-days models are trained to use the right tools it has access to, to do appropriate operation like - fetch the date or do calculation etc.
- **An example with real consequences.** In 2023 a New York lawyer asked ChatGPT to find earlier cases that supported his argument. It produced six cases that did not exist, complete with convincing names, judges and quotes. The lawyer filed them in court without checking, and the judge later fined the lawyers and their firm $5,000 for relying on fake citations.
- **A small error, an enormous cost.** In February 2023 Google showed off its chatbot Bard with an advert that claimed the James Webb Space Telescope had taken the first picture of a planet outside our solar system. That was wrong: the first such image came in 2004 from the European Southern Observatory’s Very Large Telescope. Astronomers spotted the mistake within hours, and Alphabet’s share price fell sharply that day, at one point wiping about US$100 billion from the company’s value.
- **How to check before you trust.** 
  - Treat every answer as a first draft, not a fact.
  - Ask: “What are your sources? Give direct links, not just names.” Then open each link and confirm it exists and supports the claim.
  - Search the key claim in your own words and compare at least two reliable sources.
  - Prefer the original source: a government department, hospital, bank, manufacturer or recognised professional body.
  - Check the date. Rules, prices, opening hours and public figures can change.
  - When it involves math - ask for formula used, Redo any arithmetic with a calculator. 
  - If the answer affects your health, money, safety or rights, confirm it with a real person before you act.
- References:
  - The United States National Institute of Standards and Technology notes that generative systems can confidently generate false material and even false citations. [NIST’s Generative AI Profile](https://tsapps.nist.gov/publication/get_pdf.cfm?pub_id=958388) explains why this is a known risk.
  - Do not argue with it as though it is hiding the truth. Ask for sources, then check the sources yourself.

## How can you ask a right prompt

### Five questions that make AI answers better

- **What is the job?** “Write”, “summarise”, “compare”, “make a checklist” or “help me practise” gives it a clear role.
- **Who is it for?** “Use plain Australian English for a 75-year-old beginner.”
- **What limits matter?** “Keep it under 150 words” or “give only three options.”
- **What should it show?** “State your assumptions and link to official sources.”
- **What must it avoid?** “Do not invent facts. If you are unsure, say so.”

### A prompt you can copy

> Explain **[topic]** in plain language for a beginner. Give me three key points, one everyday example and three questions I can use to check the information with an official source. If a fact may have changed recently, say that clearly.

### Let the AI interview you

> I need to plan a trip. Ask me a series of relevant questions to get me a recommendation.

- This puts the AI in the role of an interviewer. It gathers the details that matter before it answers.
- Add a limit so it does not run away: “Ask me up to five questions, one at a time, and wait for my answers before you reply.”
- This works well whenever you are not sure which facts matter, such as planning a trip, choosing a product or preparing for an appointment.

### Improve a weak prompt

- Weak: “Help me make a shopping list.”
- Better: “Help me make a shopping list for three easy vegetarian dinners for one person, avoid nuts and keep the ingredients inexpensive.”
- Identifying the good parts of the prompt: you supplied the **audience**, **limits** and **context**. Note if you do not provide the full context it will fill it with the information it was trained on. so Summary set your -audience, purpose and boundaries.

## What information can you share and not share in your prompts

- Before pasting anything into an AI service, imagine it printed on a postcard. Would you be comfortable if a stranger read it?

<figure>
  <img src="/img/lorentz-postcard-1911.jpg" alt="A handwritten 1911 postcard by the physicist Hendrik Lorentz" width="460">
  <figcaption>Physicist Hendrik Lorentz wrote this postcard in February 1911 to J.F. Hulk, a curator at the Teylers Museum in Haarlem, to arrange a planned visit by Albert Einstein and his wife. Public domain image, via Wikimedia Commons.</figcaption>
</figure>

- Share **general and made-up details** wherever they will do the job. For example: “Write a kind message to a family member about helping an older neighbour who has memory difficulties.”
  - This asks for the same helpful wording without naming a real person or sharing private health details.
- Remove names, addresses, dates of birth, account numbers, customer numbers and licence or passport details.
- Never enter passwords, one-time codes, PINs, security-question answers or recovery codes. A genuine bank or government agency will not need these in a chatbot.
- Do not upload a photograph of a passport, Medicare card, bank statement, tax document, medical report or legal document to a public AI tool.
- Treat health information, finances, location history, family photos, voice recordings and private messages as especially sensitive.
- Ask before entering information about another person. Their privacy belongs to them too.
- The Office of the Australian Information Commissioner explains that personal information can include names, contact details, identifiable images and information that can reasonably be linked back to a person. [Read the OAIC guidance on AI and privacy](https://www.oaic.gov.au/privacy/privacy-guidance-for-organisations-and-government-agencies/guidance-on-privacy-and-developing-and-training-generative-ai-models).

### A safer way to ask

- Say what outcome you want without supplying the identifying detail.
- “Help me make a list of questions for a specialist about a knee replacement.”
- “Give me a calm script for asking a bank to explain an unfamiliar charge.”
- “Create a simple household budget template with rent, food, transport and medicines.”
- Then put your real details into your own private document, not the chatbot.


## Ways of saving money.

- Use the free version first. Free chatbots are good enough for everyday questions, and you only need to pay when you have a specific job the free tier cannot do, such as very long documents, heavy image work or a tool you use every day.
- Know how you are billed. A monthly subscription costs the same however much you type, but usage-based apps and developer tools charge by the word, so a long conversation is a bigger bill.
- Drop the padding. Words like “please” and “thank you” do not make the answer better, and on usage-based tools every extra word is a cost.
- Ask for short answers. “Answer in three bullet points” or “keep it under 100 words” costs less and is easier to read.
- Remember that output costs more than input. Most paid services charge more for what the AI writes than for what you send, so a request that invites a huge answer is the expensive part.
- Start a fresh chat for a new topic. A long, rambling thread is re-sent with every message, which uses up your allowance and can confuse the model.
- Paste only what is needed. Send the paragraph you want answered, not the whole document, unless the task really is the whole document.
- Use the smallest model that can do the job. A quick rewrite or a simple list does not need the most powerful and most expensive model.
- Ask for the change, not the whole thing. “Show me just the corrected paragraph” is cheaper than regenerating the entire document.
- Turn off extras you are not using, such as web search or image tools, if your plan charges for them.
- Take a free trial only when you need a short burst of heavy use, and cancel before it renews. Students, teachers and some community groups can get the same tools at a lower price.
- Watch tools that charge by credits or by the minute. Image, video and audio generation often cost more per use, so set the size, length and number you need instead of asking for many versions.
- Keep an eye on your usage. Set a spending limit on any account that bills per use, and check the usage page each month. Cancel subscriptions you have stopped using.

## 3. The traffic-light rule: where AI fits

### Green light: useful, low-stakes jobs

- Brainstorming meal ideas from ingredients you already have.
- Turning rough notes into a polite email, birthday message or club newsletter.
- Explaining a familiar topic in simpler words: “Explain superannuation as if I am new to it.”
- Making a packing checklist for a trip after you supply the destination and dates.
- Suggesting questions to take to a doctor, lawyer, mechanic or financial adviser.
- Practising a conversation: “Pretend you are the receptionist. Help me rehearse booking an appointment.”
- Summarising a public article that you paste in, while checking the original before passing it on.
- Generating a quiz for a family gathering or ideas for a hobby project.

### Amber light: useful only with checking

- Travel plans, product comparisons, recipes involving allergies, local services and historical facts.
- Drafting a complaint letter: let AI organise the language, but replace every placeholder and check every claim.
- Translating a simple message: ask a fluent speaker to check anything important.
- Working out a budget: use it to suggest categories or questions, then check calculations with a calculator and the original bills.
- Understanding a medical term: use it to prepare questions for a qualified health professional, not to diagnose yourself.

### Red light: do not hand the decision to AI

- Emergencies, symptoms that need urgent care, changing or stopping medicine and interpreting test results.
- Deciding whether to invest, borrow money, buy cryptocurrency or make a major financial move.
- Legal deadlines, signing contracts, wills, immigration matters or tax lodgements.
- Sharing a private family dispute, someone else’s health details or confidential work information.
- Sending money, passwords or identification because a message, image or voice recording seems persuasive.
- **Aha moment:** AI can help you prepare a question for an expert. It is not the expert who accepts responsibility for the answer.

## 4. The “pause, prove, proceed” check

- **Pause.** Is the answer asking you to act quickly, spend money, share data or make a health or legal decision? If so, slow down.
- **Prove.** Find the original source. For Australian government information, look for an official `gov.au` website. For a medicine, check the pharmacist, doctor or official medicine information. For a bank, use the number printed on your card or statement.
- **Proceed.** Only act after the important point agrees with a trustworthy independent source.

### Three easy fact-checking habits

- Ask: “What are your sources? Give direct links, not just names.” Then open them. A link can be wrong or made up, so check that the page exists and actually supports the claim.
- Search for the key claim in your own words. Compare at least two reliable sources for important matters.
- Check the date. Rules, prices, opening hours, travel conditions and public figures can change.
- Look for the **original** source. A hospital, government department, bank, manufacturer or recognised professional body is usually better than a copied social-media post.
- If the answer uses numbers, redo the arithmetic with a calculator. A chatbot can make basic calculation errors.
- If you cannot verify it, say “I do not know yet” and ask a person or organisation that does.

### A smart example: the miracle rebate

- A chatbot says: “You can claim a new $2,000 energy rebate this month.” It sounds specific and helpful.
- Do not fill in a form from the answer or share your utility account number.
- Search the relevant state or federal government website yourself. Check the programme name, eligibility, closing date and application method.
- If the offer is genuine, an official page will explain it. If it is not, you have saved yourself money and worry.

## 5. AI scams: the new voice is not proof

- Scammers use the same tools we do, including tools that can imitate a voice, create a picture or write an urgent message with excellent grammar.
- A frightening call may say: “Grandma, I have had an accident. Please do not tell Mum. Send money now.” It may sound exactly like a loved one.
- The United States Federal Trade Commission warns that a short clip posted online can be enough for a criminal to attempt a voice clone. Its advice is simple: do not trust the voice alone. [Read the FTC warning](https://consumer.ftc.gov/comment/180311).
- Hang up. Call your relative using a number you already know, or contact another trusted family member. Do not use the number supplied by the caller.
- Agree on a family **safe word** or a simple question only your family can answer. It should not be a fact easily found on social media.
- Never let urgency make the decision for you. “Act now”, “keep this secret” and “pay by gift card, cryptocurrency or instant transfer” are danger signs.
- A real organisation will let you verify independently. A scammer tries to keep you in their message, call or link.

### Scam signs worth memorising

- A surprising prize, inheritance, refund or romance paired with a request for money.
- A message that claims your account will close today unless you click a link.
- A caller who asks for remote access to your computer or phone.
- A photo or video of a public figure promoting an investment that cannot be found on their official website.
- A request for a code that was sent to your phone. That code is often the key to your account.
- When in doubt, stop and talk to someone. A second pair of eyes is a powerful security tool.

## 6. Practical device safety, without the jargon

- Use a different, long password for each important account. A password manager can remember them for you.
- Turn on two-factor authentication where available. It means a password alone is not enough to enter your account.
- Keep your phone, tablet, browser and apps updated. Updates often fix security problems, not just add features.
- Download AI apps only from the official Apple App Store, Google Play store or the provider’s real website. Check the developer name and reviews, but do not rely on reviews alone.
- Read the privacy settings before using a new service. Look for options about chat history, training and data controls, then choose what you are comfortable with.
- Log out of important accounts on a shared computer. Lock your own device with a PIN, passcode or biometric lock.
- Be careful with browser extensions that promise “free AI”. An extension may be able to read what you see or type in the browser.
- Australia’s cyber security guidance emphasises that security supports the safety, privacy and reliability of AI systems. [Cyber.gov.au’s AI security guidance](https://www.cyber.gov.au/business-government/secure-design/artificial-intelligence/guidelines-for-secure-ai-system-development) is a useful reminder that convenience and safety should travel together.

## 7. Keep your human skills in the picture

- AI is strong at speed, first drafts and finding patterns in a large amount of text.
- People are strong at values, relationships, context, compassion and deciding what is worth doing.
- Ask yourself: “What would a sensible friend ask before believing this?”
- Use AI to create options, not to choose your values.
- Do not be embarrassed to ask the same question in a simpler way. “Explain that without jargon” is an excellent instruction.
- Do not be embarrassed to walk away. You do not owe a chatbot, an advert or a caller an immediate reply.
- **Aha moment:** the most valuable skill in the age of AI may be the old-fashioned one: knowing when to pause and ask a good question.

## 8. Pictures, videos and “too good to be true” evidence

- A photograph used to feel like strong evidence. Now it may be real, edited, generated or taken from somewhere else and given a false caption.
- Do not try to become a detective by staring at every eyelash or shadow. Image quality is not a dependable test on its own.
- Instead, check the **context**:
  - Who first posted it?
  - Is there a date and location?
  - Do reputable news outlets or official organisations report the same event?
  - Does the account have a long, credible history or was it created recently?
  - Is the picture being used to make you angry, frightened or eager to invest before you can think?
- A video of a politician, celebrity or doctor may be a deepfake: a convincing artificial imitation. Treat an extraordinary claim as unproven until it appears through that person’s official channels or reliable reporting.
- **Aha moment:** “I can see it with my own eyes” is no longer the end of the enquiry. It is the beginning of it.
- AI-generated pictures can still be delightful. Use them for an invitation, a story illustration or an idea for a garden. Just label them honestly if another person might mistake them for a real event.

### Example: the celebrity investment advertisement

- You see a video of a famous television presenter recommending a new investment opportunity.
- The video looks polished. The caption says places are limited. A link asks for your phone number.
- Do not use the link. Search for the presenter’s verified account and their official website. Search the investment name plus the word “scam”.
- Discuss any investment with a licensed financial professional you have contacted independently. A familiar face in a video is marketing, not proof.

## 9. How to use AI alongside people, not instead of them

- Use a chatbot before an appointment to organise your thoughts. Take a printed list of questions to the real person.
- Use it after an appointment to turn **your own non-sensitive notes** into plain-language reminders. Do not treat the result as a clinical record.
- Ask a librarian to show you good research sources. Libraries are one of the best places to practise digital confidence without pressure.
- Compare an AI suggestion with the experience of a local group, a trusted friend or a professional. Different perspectives uncover blind spots.
- If English is not your first language, AI can help you prepare a short message. For a legal, medical or financial document, use a qualified interpreter or adviser for the final meaning.
- If you are helping a friend with technology, do the verification together. The goal is not to take over their device. It is to leave them with a skill they can use next time.

### Helpful phrases for asking a real person

- “An AI tool told me this. Could you help me check whether it applies to my situation?”
- “I do not understand this term. Could you explain it without jargon?”
- “Before I click or pay, what is the official way to verify this?”
- “What information should I never enter into this service?”
- These questions are not silly. They are exactly the questions careful people ask.

## 10. Common mistakes and easy replacements

- **Mistake:** asking, “Can I trust AI?”
  - **Better question:** “Can I trust this particular answer for this particular decision after checking it?”
- **Mistake:** pasting a whole letter, report or email to get a summary.
  - **Better approach:** remove names and numbers, summarise only the general parts or ask the sender for a plain-language explanation.
- **Mistake:** treating a chatbot’s friendly tone as a relationship.
  - **Better approach:** enjoy the conversation if you wish, but seek human support for loneliness, grief, danger or a major personal choice.
- **Mistake:** using the first answer as the final answer.
  - **Better approach:** ask it to show assumptions, give alternatives and state what it cannot know.
- **Mistake:** clicking the first link in an AI answer.
  - **Better approach:** type the organisation’s address yourself or use a bookmark you already trust.
- **Mistake:** feeling embarrassed after nearly falling for a scam.
  - **Better approach:** tell someone promptly. Scams are designed to rush and manipulate capable people. Fast reporting can protect you and others.

## 11. A short group activity for a talk or community class

- Read this request aloud: “Write a warm invitation to a neighbourhood afternoon tea.”
- Ask the group what could safely be included: the public venue, date, time and a request to RSVP.
- Ask what should not be included: anyone’s private phone number, medical information or a list of people who live alone.
- Generate a draft, then improve it together: make it friendlier, shorter and clearer.
- Next, read this request: “My bank has texted a link. Is it real?”
- Ask the group what the AI can do safely: list scam warning signs and help write a script for calling the bank.
- Ask what it must not do: decide the text is genuine, open the link, access the bank account or tell someone to share a code.
- Finish with the sentence everyone can remember: **“I verify through the official channel I find myself.”**

## 12. A gentle 10-minute practice session

- Choose a low-risk task. For example: “Help me make a shopping list for three easy vegetarian dinners.”
- Read the answer and improve the request: “Make it suitable for one person. Avoid nuts. Keep the ingredients inexpensive.”
- Notice what happened: the result improved because **you** supplied judgement and context.
- Ask it for a fact: “What is the opening time of my nearest library?”
- Now practise checking: find the library’s official website or call it. Notice that the chatbot’s answer is only a starting point.
- Finish by writing one rule on paper: “I will not enter passwords, codes, bank details or private documents into a chatbot.” Put it near your device.

## 13. A pocket checklist for every AI interaction

- What am I trying to achieve?
- Is this a low-stakes task or a decision that could affect health, money, safety or rights?
- Have I removed private information?
- Does the answer ask me to hurry, pay or keep a secret?
- Can I verify the important claim through an official, independent source?
- Would I be comfortable explaining this decision to a trusted friend?
- If the answer is “no” or “I am not sure”, pause and get human help.


## **Popular AI subscriptions compared, including free plans (prices in US dollars per month, checked October 2026)**

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
| SuperGrok Lite | $10 | Entry-level paid Grok | [grok.com/plans](https://grok.com/plans) |
| Google AI Pro | $19.99 | 4x the free usage and 5 TB of storage | [gemini.google/subscriptions](https://gemini.google/subscriptions/) |
| Claude Pro | $20 | Opus, Sonnet and Haiku with at least 5x the free usage | [claude.com/pricing](https://claude.com/pricing) |
| ChatGPT Plus | $20 | The newest GPT-6 models with expanded limits | [chatgpt.com/pricing](https://chatgpt.com/pricing) |
| SuperGrok | $30 | Newest Grok models with higher limits | [grok.com/plans](https://grok.com/plans) |

### 2. Asking questions about the web page you are reading

A browser assistant sits in a side panel, reads the page (or your open tabs) and answers questions about it. Typical uses are summarising a long article, explaining jargon in a contract, comparing two products or translating a page.

| Option | Cost as of Oct 2026 | What you get | Link |
|---|---|---|---|
| Brave Leo | Free | Built into the Brave browser. Summarises pages and videos and answers questions using open models. Rate-limited, and no account is needed | [brave.com/leo](https://brave.com/leo/) |
| Gemini in Chrome | Free (where available) | Side panel in Chrome that summarises the page, compares tabs and explains anything you point at. Rollout started in the US, so it may not be in your country yet | [gemini.google/overview/gemini-in-chrome](https://gemini.google/overview/gemini-in-chrome/) |
| Copilot Mode in Edge | Free (limits apply) | Opt-in mode in Microsoft Edge on Windows and Mac that can see your open tabs and answer questions about them. Microsoft launched it as free "for a limited time", so check the current terms | [microsoft.com/edge](https://www.microsoft.com/en-us/edge/ai-powered/copilot-mode/faqs) |
| Comet (Perplexity) | Free | A whole browser with an assistant on every page that summarises, chats with your tabs and does basic tasks | [perplexity.ai/comet](https://www.perplexity.ai/comet) |
| Brave Leo Premium | $14.99 (or $149.99 a year) | Adds Claude and DeepSeek models and higher limits | [brave.com/leo](https://brave.com/leo/) |
| Claude in Chrome | $20 (Claude Pro) | Reads the page you are signed in to and answers questions about it | [claude.com/claude-in-chrome](https://claude.com/claude-in-chrome) |

### 3. Letting the AI click, fill in forms and run errands in the browser

These "agent" features go further than answering questions. They can click, type and move between pages for you. They are also the riskiest: a web page can hide instructions that try to trick the AI. Avoid banking, health records and anything involving passwords, and check each step before approving it.

| Option | Cost as of Oct 2026 | What you get | Link |
|---|---|---|---|
| Comet (Perplexity) | Free | The free assistant can handle basic tasks. The more advanced Background Assistant is reserved for paid plans | [perplexity.ai/comet](https://www.perplexity.ai/comet) |
| Brave Leo | Free | "Agentic browsing" has been in early testing since May 2026, so expect rough edges | [brave.com/leo](https://brave.com/leo/) |
| Google AI Pro | $19.99 | Includes Chrome's "auto browse" feature that works through tasks for you | [gemini.google/subscriptions](https://gemini.google/subscriptions/) |
| Claude in Chrome | $20 (Claude Pro) | Clicks, types and fills forms. Stops before purchases and other sensitive actions | [claude.com/claude-in-chrome](https://claude.com/claude-in-chrome) |
| Perplexity Max | $200 | Comet's Background Assistant and Email Assistant | [perplexity.ai](https://www.perplexity.ai/hub/pricing) |

### 4. Working inside Word, Excel and PowerPoint

Instead of copying text out of a chatbot, these add-ins work inside your open file: explaining a cell, building formulas, rewriting a paragraph, turning notes into slides.

| Option | Cost as of Oct 2026 | What you get | Link |
|---|---|---|---|
| ChatGPT Free | Free | Limited use of ChatGPT's Excel, Word and PowerPoint add-ins | [chatgpt.com/pricing](https://chatgpt.com/pricing) |
| ChatGPT Go | $8 | Same add-ins, still limited | [chatgpt.com/pricing](https://chatgpt.com/pricing) |
| Microsoft 365 Personal | $9.99 | Copilot inside Word, Excel, PowerPoint and Outlook for the subscriber | [microsoft.com](https://www.microsoft.com/en-au/microsoft-365/p/microsoft-365-personal/cfq7ttc0k5bf) |
| Google AI Pro | $19.99 | Gemini inside Gmail, Docs and Vids for Google's own apps | [gemini.google/subscriptions](https://gemini.google/subscriptions/) |
| Microsoft 365 Premium | $19.99 | Highest Copilot usage in the Office apps | [microsoft.com](https://www.microsoft.com/en-au/microsoft-365/p/microsoft-365-premium/cfq7ttc11z3q) |
| Claude Pro | $20 | Claude for Excel, PowerPoint and Word: edits with tracked changes, formulas that keep working, slides in your own template | [claude.com/claude-for-microsoft-365](https://claude.com/claude-for-microsoft-365) |
| ChatGPT Plus | $20 | Full access to the Excel, Word, PowerPoint and Google Sheets add-ins | [chatgpt.com/pricing](https://chatgpt.com/pricing) |

### 5. Email and calendar

Useful for summarising a long thread, drafting a reply, sorting your inbox or finding a meeting time. Check every draft before sending, because the AI does not know your relationships or what you left out.

| Option | Cost as of Oct 2026 | What you get | Link |
|---|---|---|---|
| Gemini in Chrome | Free (where available) | Can draft an email or a post from the page you have open | [gemini.google/overview/gemini-in-chrome](https://gemini.google/overview/gemini-in-chrome/) |
| Any free chatbot above | Free | Paste in the thread (with names and private details removed) and ask for a draft reply | |
| Google AI Plus | $4.99 | Gemini inside Gmail | [gemini.google/subscriptions](https://gemini.google/subscriptions/) |
| Microsoft 365 Personal | $9.99 | Copilot inside Outlook | [microsoft.com](https://www.microsoft.com/en-au/microsoft-365/p/microsoft-365-personal/cfq7ttc0k5bf) |
| Google AI Pro | $19.99 | Gemini inside Gmail and Docs | [gemini.google/subscriptions](https://gemini.google/subscriptions/) |
| Claude Pro | $20 | Claude for Outlook (beta): sorts your inbox, writes replies that wait for you to press send, finds meeting times | [claude.com/claude-for-microsoft-365](https://claude.com/claude-for-microsoft-365) |
| Perplexity Max | $200 | Email Assistant in the Comet browser | [perplexity.ai](https://www.perplexity.ai/hub/pricing) |

### 6. Research with sources

Good for comparing products, background reading and questions where you want links you can check yourself. Always open the sources, because an AI can cite a page that does not say what it claims.

| Option | Cost as of Oct 2026 | What you get | Link |
|---|---|---|---|
| Perplexity Free | Free | Answers with linked sources, with a small daily number of advanced searches | [perplexity.ai](https://www.perplexity.ai) |
| Gemini Free | Free | Deep Research reports | [gemini.google.com](https://gemini.google.com) |
| ChatGPT Free | Free | Limited deep research and web search | [chatgpt.com](https://chatgpt.com) |
| Claude Free | Free | Web search (the full Research mode needs a paid plan) | [claude.ai](https://claude.ai) |
| ChatGPT Go | $8 | Limited deep research with more usage than Free | [chatgpt.com/pricing](https://chatgpt.com/pricing) |
| Google AI Pro | $19.99 | Higher Deep Research limits and a 1M-token context window for long documents | [gemini.google/subscriptions](https://gemini.google/subscriptions/) |
| Claude Pro | $20 | Research mode and projects for organising your sources | [claude.com/pricing](https://claude.com/pricing) |
| ChatGPT Plus | $20 | Expanded deep research | [chatgpt.com/pricing](https://chatgpt.com/pricing) |
| Perplexity Pro | $20 | Higher research limits, more file uploads and a choice of models | [perplexity.ai](https://www.perplexity.ai/hub/pricing) |

### 7. Coding help

Includes explaining code, fixing bugs, writing small scripts and building simple websites.

| Option | Cost as of Oct 2026 | What you get | Link |
|---|---|---|---|
| Google AI Studio | Free | Experiment with Gemini models, with no cost to start | [aistudio.google.com](https://aistudio.google.com) |
| Google Antigravity | Free | Coding agents with basic weekly limits | [antigravity.google](https://antigravity.google/pricing) |
| ChatGPT Free | Free | Limited Codex access | [chatgpt.com/codex](https://chatgpt.com/codex/) |
| Claude Free | Free | Chat-based coding help (Claude Code needs a paid plan) | [claude.ai](https://claude.ai) |
| Google AI Pro | $19.99 | Higher limits in Jules and Antigravity | [gemini.google/subscriptions](https://gemini.google/subscriptions/) |
| Claude Pro | $20 | Claude Code included, sharing your plan's usage | [claude.com/product/claude-code](https://claude.com/product/claude-code) |
| ChatGPT Plus | $20 | Expanded Codex usage | [chatgpt.com/codex](https://chatgpt.com/codex/) |

### 8. Pictures and video

For invitations, story illustrations, garden ideas and short clips. Label AI-made images honestly if someone could mistake them for a real photo.

| Option | Cost as of Oct 2026 | What you get | Link |
|---|---|---|---|
| Gemini Free | Free | Image generation and editing | [gemini.google.com](https://gemini.google.com) |
| ChatGPT Free | Free | Limited image creation | [chatgpt.com](https://chatgpt.com) |
| Copilot Free | Free | Simple image requests, with usage limits | [copilot.microsoft.com](https://copilot.microsoft.com) |
| Leonardo.Ai Free | Free | 150 tokens a day. Your creations are public, so avoid private photos, and check the terms before commercial use | [leonardo.ai](https://leonardo.ai) |
| Google AI Plus | $4.99 | Video generation and 200 Flow credits | [gemini.google/subscriptions](https://gemini.google/subscriptions/) |
| ChatGPT Go | $8 | More image creation than Free | [chatgpt.com/pricing](https://chatgpt.com/pricing) |
| SuperGrok Lite | $10 | Grok Imagine at 480p | [grok.com/plans](https://grok.com/plans) |
| Leonardo.Ai Essential | $12 | 8,500 tokens a month, private creations, more control over style | [leonardo.ai](https://leonardo.ai) |
| Google AI Pro | $19.99 | 1,000 Flow credits and a limited trial of Veo video generation | [gemini.google/subscriptions](https://gemini.google/subscriptions/) |
| ChatGPT Plus | $20 | Image creation with reasoning | [chatgpt.com/pricing](https://chatgpt.com/pricing) |
| Leonardo.Ai Premium | $30 | 25,000 tokens a month, unlimited relaxed-speed images on Leonardo's own models | [leonardo.ai](https://leonardo.ai) |
| Leonardo.Ai Ultimate | $60 | 60,000 tokens a month, unlimited relaxed-speed video | [leonardo.ai](https://leonardo.ai) |

### 9. Heavy, all-day use

Worth considering only if you hit the limits of the $20 plans most days.

| Option | Cost as of Oct 2026 | What you get | Link |
|---|---|---|---|
| Google AI Ultra | $99.99 or $199.99 | 5x or 20x the AI Pro usage, 20 TB of storage | [gemini.google/subscriptions](https://gemini.google/subscriptions/) |
| Claude Max 5x | $100 | 5x Pro usage, Fable model included, $100 a month of API credits | [claude.com/pricing](https://claude.com/pricing) |
| ChatGPT Pro 100 | $100 | Pro-level reasoning and much higher limits | [chatgpt.com/pricing](https://chatgpt.com/pricing) |
| Claude Max 20x | $200 | 20x Pro usage, $200 a month of API credits | [claude.com/pricing](https://claude.com/pricing) |
| ChatGPT Pro 200 | $200 | More usage than Pro 100 | [chatgpt.com/pricing](https://chatgpt.com/pricing) |
| Perplexity Max | $200 | Highest limits and 10,000 agent credits a month | [perplexity.ai](https://www.perplexity.ai/hub/pricing) |
| SuperGrok Heavy | $300 | Highest Grok limits and the multi-agent Grok 4 Heavy | [grok.com/plans](https://grok.com/plans) |
| ChatGPT Pro 500 | $500 | Highest ChatGPT usage and Ultrafast mode | [chatgpt.com/pricing](https://chatgpt.com/pricing) |

*Features and prices change often. Browser assistants in particular are rolling out country by country, so confirm on the provider's page that a feature is available where you live before you pay.*



## Closing thought

- AI is neither magic nor useless. It is a tool.
- A calculator does not decide whether you can afford a holiday. A map does not decide whether it is safe to travel. AI does not decide what is true, wise or right for you.
- Use it for ideas, drafts and explanations. Protect your private information. Check important facts. Slow down when money, health or urgency enters the conversation.
- Curiosity plus caution is not fear of technology. It is confidence with technology.

