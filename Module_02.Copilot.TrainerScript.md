# Module 02 - Documentation With GitHub Copilot (2h) - Trainer Script (Light, Simple English)

This is a read-aloud script for the transitions and the first/last minutes.

You will jump to `info/lab_2.dotNet/Module_02.DotNet.md` for the actual step-by-step instructions and prompts.

## Timing (Suggested - ~2 hours)

- 00:00-00:05 Courtesy wait
- 00:05-00:12 Intro + how we will work
- 00:12-00:20 Environment check
- 00:20-00:32 Exercise 1 (12 min)
- 00:32-00:45 Exercise 2 (13 min)
- 00:45-01:00 Exercise 3 (15 min)
- 01:00-01:10 Break (10 min if on time, otherwise 5 min)
- 01:10-01:25 Exercise 4 (15 min)
- 01:25-01:40 Exercise 5 (15 min)
- 01:40-01:55 Exercise 6 (15 min)
- 01:55-02:00 Wrap-up + survey + goodbye

## 00:00-00:05 Courtesy Wait

Say:

"Hi everyone, we'll start in about five minutes to give people time to join. While we wait, please open VS Code, open the `Exercise 1` folder, and make sure GitHub Copilot Chat is working."

**IMPORTANT: Start recording now.**

Say:

"Quick reminder: this session is being recorded."

### After 5 minutes, say:

"Good afternoon everyone. Thank you for joining today's lab."

"Let's get started."

## 00:05-00:12 Short Intro (What We Will Do)

Say:

"Today is a 2-hour hands-on lab focused on documentation with GitHub Copilot in a .NET Claims Management API."

"In this lab, you will use GitHub Copilot's documentation features to generate, improve, and maintain professional documentation for the Claims Management ASP.NET Core API. You'll master Chat modes (Ask, Edit, Agent, Plan), Smart Actions, Custom Instructions, chat participants, and autonomous documentation workflows."

**What You'll Learn:**
- Use Smart Actions and Chat modes to understand and document existing code
- Generate comprehensive XML documentation comments with consistent formatting
- Establish and enforce repository-wide documentation standards
- Create specialized documentation workflows with custom agents
- Automate complete documentation suites using Agent Mode

**What You'll Build:**
- Complete XML documentation comments across the Claims API codebase
- Repository documentation standards (`.github/copilot-instructions.md`)
- Custom documentation specialist agent
- Comprehensive documentation suite (API.md, ARCHITECTURE.md, CONTRIBUTING.md)

"The structure is simple: I will demonstrate each exercise on screen, and you will replicate it. If you fall behind, don't panic: finish the step you're on, then re-join us on the next exercise."

"During each exercise, I'll read the instructions, and I'll copy/paste the prompts into the meeting chat so you can copy them easily. I'll also paste them into Copilot Chat on my side so you can see the workflow end-to-end."

"You have three helper files: `Requirements.md` for setup, `Lab_Script.md` for the exercises, and `Prompts.md` as a copy/paste reference."

"Interaction: please stay muted by default and ask questions in the meeting chat. I will pause briefly after each exercise."

"We will take a short break halfway through: 10 minutes if we're on time, otherwise 5 minutes."

"Two quick Copilot tips before we start: context and model selection."

"First, context: Copilot is only as good as what it can see. You can add context in a few ways:"

"1) Select code in the editor and ask your question; Copilot uses the selection as context."

"2) Use `@workspace` in the prompt when you want project-wide answers, like 'find all controllers' or 'audit documentation coverage'."

"3) Attach files/folders to the chat context using the Add/plus button in the chat panel, or by dragging a file into the chat."

"4) If you are asking about a specific file, name it explicitly, like `src/ClaimsApi/Controllers/ClaimsController.cs`."

"Second, model selection: in the chat panel you can usually pick a model, or leave it on Auto. Here is a good rule of thumb:"

"- Use Auto for day-to-day work."

"- Use a faster/lighter model for quick Q&A, summaries, or small edits where latency matters."

"- Switch to a stronger model for multi-step reasoning, Agent mode work, or when the first answer is shallow or inconsistent."

"If you switch models and the answer changes a lot, treat that as a signal to add more context or tighten your prompt."

While people open the lab (optional filler):

"Please keep the lab script open on the side. It has the exact prompts."

"I will show each prompt on screen and paste it into chat."

"If Copilot is slow, please wait. It is reading your project context."

## 00:12-00:20 Environment Check

Say:

"Before we start Exercise 1: please confirm Copilot Chat responds on your machine. If it doesn't, restart VS Code and verify you're logged in with the correct GitHub account."

"Also, make sure you opened the whole `Exercise 1` folder, not a single file. Workspace context matters."

Common issues and quick fixes:

"- If you see 'Sign in required', click and authenticate with your GitHub account."

"- If you see 'No subscription' or 'Not authorized', contact your admin or check your license."

"- If Copilot Chat does not appear, restart VS Code."

If someone is blocked and you are spending too long troubleshooting, say:

"If troubleshooting is taking too long, please disconnect and register for another session later. There are also support calls available. I'll paste the official message at the end."

You can copy/paste this text in the chat:

```text
If you experience issues with requirements and setup of lab environment, please consider to register again in another date and join our Support Calls available every Monday and Friday. Please write an email to TechnicalExcellenceSchools@generali.com and inform us about this.
```

## Exercise Transitions

Use this pattern for every exercise:

- Say what the exercise is about (1-2 sentences)
- Say: "And now we'll start Exercise X."
- Jump to `info/lab_2.dotNet/Module_02.DotNet.md` and run the exercise as written
- While Copilot runs, use the suggested filler lines (optional)

## Exercise 1 (Intro)

Say:

"Exercise 1 is about orientation: Copilot Chat modes, Smart Actions, and using Copilot safely to understand code before changing anything."

"And now we'll start Exercise 1."

While Copilot is generating/explaining (optional filler):

"While Copilot is working, notice how much the answer depends on context: the selected method, the current file, and the overall workspace."

"Remember: Ask mode is non-destructive. Use it aggressively to understand code before you modify documentation."

After finishing Exercise 1 (quick check):

"Quick check: did everyone manage to get an explanation from the Smart Action and ask one follow-up question?"

Q&A micro-pause (30-60 seconds):

"Please type `OK` in the meeting chat if you're done, `1` if you're stuck, or `2` if Copilot isn't responding. We'll wait 30 seconds and then move on."

## Exercise 2 (Intro)

Say:

"Exercise 2 is where we start writing docs: we will generate XML documentation comments and verify them via IntelliSense."

"And now we'll start Exercise 2."

Safety mantra:

"Before we accept any edits: preview the diff, verify it against the code, reject if you're unsure, and iterate with a tighter prompt."

While Copilot proposes changes (optional filler):

"When you are in a mode that edits code, always review the diff. Copilot is fast, but you are responsible for correctness."

"Reject and re-run if you see wrong parameter names, wrong return types, or made-up status codes."

After finishing Exercise 2:

"Please hover one method and confirm the XML docs show up in the tooltip. That is our quick verification."

Q&A micro-pause (30-60 seconds):

"Type `OK` if you're done, `1` if you're stuck, `2` if Copilot isn't responding. We'll wait 30 seconds and then continue."

## Exercise 3 (Intro)

Say:

"Exercise 3 is about consistency at scale: we will create repository custom instructions so Copilot automatically follows our documentation standards."

"And now we'll start Exercise 3."

While Copilot generates `.github/copilot-instructions.md` (optional filler):

"This file is a force multiplier: instead of repeating standards in every prompt, we define them once and Copilot applies them everywhere in this repository."

"If you want better outputs, make your standards specific and testable, not generic."

Q&A micro-pause (30-60 seconds):

"Type `OK` if the file was created, `1` if you're stuck, `2` if Copilot isn't responding. We'll wait 30 seconds and then take a short break."

Break decision:

"We are roughly at the halfway point. If we are on time, we'll take a 10-minute break. If we're running late, we'll do 5 minutes."

## Break (5-10 min)

Say:

"We'll take a short break now. Please be back at a specific time: I'll post the return time in the meeting chat."

"When we return, we'll apply the standards across more files, create a documentation specialist agent, and finish with an Agent-mode documentation suite."

"If you're behind after the break, use the `Exercise X/` folders as checkpoints to re-join us quickly."

### Message to post in chat BEFORE the break:

```text
Break time! We'll return at [TIME].
Example: "Break time! We'll return at 14:15" (or "2:15 PM")
Please be back on time so we can finish the lab together.
```

### When the break time is over, post in chat:

```text
We are starting again now. Please join us for Exercise 4.
```

### When you return from break, say:

"Welcome back everyone."

"We will now continue with Exercise 4."

## Exercise 4 (Intro)

Say:

"Exercise 4 applies what we just set up: we audit documentation coverage across the workspace and then apply standards across multiple files."

"And now we'll start Exercise 4."

While Copilot audits the workspace (optional filler):

"A useful workflow is: audit first, then fix highest priority files first, then re-audit."

"If the workspace answer is too broad, narrow it to one folder or one controller at a time."

Q&A micro-pause (30-60 seconds):

"Type `OK` if you're done, `1` if you're stuck, `2` if Copilot isn't responding. We'll wait 30 seconds and then move on."

## Exercise 5 (Intro)

Say:

"Exercise 5 creates a specialized helper: a custom documentation specialist agent to review and enforce standards more consistently."

"And now we'll start Exercise 5."

While Copilot creates the agent file (optional filler - say some of these while it runs):

"This prompt is intentionally long. It's not just asking Copilot to write text; it's defining a specialist that you can reuse."

"Notice the structure of the prompt:"

"- The YAML header defines the agent metadata: a description and which tools it can use. Think of tools as permissions: what the assistant is allowed to do."

"- The body defines three things: a persona, domain knowledge, and a quality checklist. That's how we make behavior consistent across conversations."

"When you create this kind of specialist, make it concrete: include the vocabulary of your system and what 'good' looks like. Otherwise the assistant will drift to generic advice."

"Also notice that we reference `.github/copilot-instructions.md`. This is important: the specialist agent is not a replacement for repository instructions; it's a layer on top that helps enforce them."

Q&A micro-pause (30-60 seconds):

"Type `OK` if the agent file was created and shows up in the selector, `1` if you're stuck, `2` if Copilot isn't responding. We'll wait 30 seconds and then continue."

While Copilot is done and you review the result (optional filler):

"When the file is created, don't just assume it works. We validate in two ways:"

"1) Does it show up in the mode selector? If not, reload VS Code."

"2) Does it behave like a specialist? It should answer with our domain terms, mention our standards, and give actionable review feedback."

"A good specialist answer references the actual codebase, uses consistent terminology, and calls out concrete gaps like missing `<response>` tags or unrealistic examples."

## Exercise 6 (Intro)

Say:

"Exercise 6 is Agent mode: we will ask Copilot to generate multiple documentation files and cross-references. Your job is supervision: review every diff and reject hallucinations."

"And now we'll start Exercise 6."

Safety mantra:

"Agent mode can touch many files. Preview the diff, verify against code, reject if unsure, and tighten the prompt if you see systematic errors."

While Agent is running (optional filler - say some of these while it runs):

"This prompt is a good example of how to work with Agent mode: it is broken into numbered tasks, with explicit outputs and quality gates. That helps the agent plan and keeps it from wandering."

"Pay attention to two parts of the prompt:"

"- The task breakdown: update API docs, create architecture docs, create contributing guidelines, update the README, then cross-reference everything."

"- The quality standards: imperative mood, realistic data, working examples, consistent terminology. These are 'acceptance criteria' you can use when reviewing diffs."

"As the agent runs, you will typically see status messages like 'Analyzing project structure' or 'Generating docs/API.md'. That's normal. What matters is what it proposes to change and whether those changes are correct."

"Agent mode is powerful, but not authoritative. Your role is to supervise: read every diff before accepting. If you're unsure, reject and ask it to revise with a narrower instruction."

"When reviewing documentation, the most common failure modes are:"

"- Invented endpoints or paths: the agent might assume `/api/v1/auth/...` even if the code uses a different route. Always compare to controller attributes."

"- Invented request/response shapes: verify against DTOs and action signatures."

"- Wrong status codes: check what the controller actually returns in success and error cases."

"- Broken links and anchors: markdown links are easy to get wrong; validate them after generation."

"If the agent is slow: that's usually because it is reading many files and generating multiple documents. This is a good time to remind everyone about model choice: a stronger model is often better for multi-file consistency, but it can be slower."

While the agent proposes file changes (optional filler):

"Notice how it requests approval per file change. A safe workflow is: accept one file, skim it quickly for glaring issues, then accept the next."

"If you see a systematic problem, like wrong base URLs, stop accepting and correct the prompt. Otherwise you'll accept the same mistake across multiple files."

After Agent completes (optional filler about the result):

"At the end, you should have a documentation suite, not just one file. The goal is a connected set of docs: API reference, architecture overview, contributing guidelines, and an updated README that links to them."

"Before we consider it 'done', we do a quick sanity check: open each generated file, look for placeholders like TODO, verify examples use realistic data, and run the cross-reference validation prompt."

Q&A micro-pause (30-60 seconds):

"Type `OK` if you're done, `1` if you're stuck, `2` if Copilot isn't responding. We'll wait 30 seconds and then wrap up."

## After The Last Exercise (Closing Script)

Say:

"We just finished the last exercise. Before we wrap up: take 30 seconds and look at the files we touched. The real win is the workflow: understand -> document -> standardize -> scale -> automate -> verify."

"Key takeaways from today:"

- "Choose the right interaction method: Ask for understanding, Edit for controlled changes, Agent for multi-file work, Plan for structuring complex tasks."
- "Context is everything: the better the context, the better the output."
- "Standards are leverage: `.github/copilot-instructions.md` removes repetition and improves consistency."
- "Supervision is mandatory: always review diffs and test examples when you can."

"I'll now paste the survey link. Please fill it in; it's very important for improving the program."

## Labs Reminder and Prerequisites (5 minutes before closing)

Say:

"Now I will paste the survey link. Please fill it in."

### Copy/Paste (Official Text)

LAB feedback survey:

```text
Please fill our LABS feedback survey, it takes a few minutes for you and it is super important for us to improve our School !
Link:
https://welearngenerali.qualtrics.com/jfe/form/SV_6eSxmtUuuvITaMC
```

Environment issues message:

```text
If you experience issues with requirements and setup of lab environment, please consider to register again in another date and join our Support Calls available every Monday and Friday. Please write an email to
TechnicalExcellenceSchools@generali.com and inform us about this.
```

## Goodbye

Say:

"Thanks everyone for joining. Have a great day, and see you in the next module."

**IMPORTANT: Stop recording and end the meeting (do not just leave).**
