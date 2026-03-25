# Module 02 - Documentation With GitHub Copilot (2h) - Trainer Script (Light)

This is a read-aloud script for the transitions and the first/last minutes.

You will jump to `info/lab_2.dotNet/Module_02.DotNet.md` for the actual step-by-step instructions and prompts.

## Timing (Suggested)

- 00:00-00:05 Courtesy wait
- 00:05-00:12 Intro + how we will work
- 00:12-00:20 Environment check
- 00:20-01:00 Exercises 1-3
- 01:00-01:10 Break (10 min if on time, otherwise 5 min)
- 01:10-01:55 Exercises 4-6
- 01:55-02:00 Wrap-up + survey + goodbye

## 00:00-00:05 Courtesy Wait

Say:

"Hi everyone, we'll start in about five minutes to give people time to join. While we wait, please open VS Code, open the `Exercise 1` folder, and make sure GitHub Copilot Chat is working."

If the session is recorded, start recording now and say:

"Quick reminder: this session is being recorded."

## 00:05-00:12 Short Intro (What We Will Do)

Say:

"Today is a 2-hour hands-on lab focused on documentation with GitHub Copilot in a .NET Claims Management API."

"The structure is simple: I will demonstrate each exercise on screen, and you will replicate it. If you fall behind, don't panic: finish the step you're on, then re-join us on the next exercise."

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

## 00:12-00:20 Environment Check

Say:

"Before we start Exercise 1: please confirm Copilot Chat responds on your machine. If it doesn't, restart VS Code and verify you're logged in with the correct GitHub account."

"Also, make sure you opened the whole `Exercise 1` folder, not a single file. Workspace context matters."

If someone is blocked and you are spending too long troubleshooting, say:

"If troubleshooting is taking too long, please disconnect and register for another session later. There are also support calls available. I'll paste the official message at the end."

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

## Exercise 2 (Intro)

Say:

"Exercise 2 is where we start writing docs: we will generate XML documentation comments and verify them via IntelliSense."

"And now we'll start Exercise 2."

While Copilot proposes changes (optional filler):

"When you are in a mode that edits code, always review the diff. Copilot is fast, but you are responsible for correctness."

"Reject and re-run if you see wrong parameter names, wrong return types, or made-up status codes."

After finishing Exercise 2:

"Please hover one method and confirm the XML docs show up in the tooltip. That is our quick verification."

## Exercise 3 (Intro)

Say:

"Exercise 3 is about consistency at scale: we will create repository custom instructions so Copilot automatically follows our documentation standards."

"And now we'll start Exercise 3."

While Copilot generates `.github/copilot-instructions.md` (optional filler):

"This file is a force multiplier: instead of repeating standards in every prompt, we define them once and Copilot applies them everywhere in this repository."

"If you want better outputs, make your standards specific and testable, not generic."

Break decision:

"We are roughly at the halfway point. If we are on time, we'll take a 10-minute break. If we're running late, we'll do 5 minutes."

## Break (5-10 min)

Say:

"Please be back in a few minutes. When we return, we'll apply the standards across more files, create a documentation specialist mode, and finish with an Agent-mode documentation suite."

## Exercise 4 (Intro)

Say:

"Exercise 4 applies what we just set up: we audit documentation coverage across the workspace and then apply standards across multiple files."

"And now we'll start Exercise 4."

While Copilot audits the workspace (optional filler):

"A useful workflow is: audit first, then fix highest priority files first, then re-audit."

"If the workspace answer is too broad, narrow it to one folder or one controller at a time."

## Exercise 5 (Intro)

Say:

"Exercise 5 creates a specialized helper: a custom documentation specialist mode to review and enforce standards more consistently."

"And now we'll start Exercise 5."

While Copilot creates the mode file (optional filler):

"The goal is not magic. It's repeatability: the mode encodes a persona and a checklist so reviews are consistent."

"After creating it, make sure it appears in the mode selector. If it doesn't, reload VS Code."

## Exercise 6 (Intro)

Say:

"Exercise 6 is Agent mode: we will ask Copilot to generate multiple documentation files and cross-references. Your job is supervision: review every diff and reject hallucinations."

"And now we'll start Exercise 6."

While Agent is running (optional filler):

"Watch the plan and the file list. If it starts doing too much, stop and split the task into smaller chunks."

"For docs, the biggest risks are invented endpoints, invented data models, and broken links. Verify against the code."

## After The Last Exercise (Closing Script)

Say:

"We just finished the last exercise. Before we wrap up: take 30 seconds and look at the files we touched. The real win is the workflow: understand -> document -> standardize -> scale -> automate -> verify."

"Key takeaways from today:"

- "Choose the right interaction method: Ask for understanding, Edit for controlled changes, Agent for multi-file work, Plan for structuring complex tasks."
- "Context is everything: the better the context, the better the output."
- "Standards are leverage: `.github/copilot-instructions.md` removes repetition and improves consistency."
- "Supervision is mandatory: always review diffs and test examples when you can."

"I'll now paste the survey link. Please fill it in; it's very important for improving the program."

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
