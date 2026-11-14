# NEW-PROJECT.md: Starter Message

Paste the message below into Claude Code to start a new project. It works with the standards in `CLAUDE.md`.

## How to use

1. Make a new empty folder for the project and open Claude Code in it.
2. Copy the message below and fill in the four blanks.
3. Attach the design PDF. If you already have a spec document for the app, attach that too.
4. Send it.

## The message

```
New project. Follow the new project checklist in the standards.

Name:
Type: (desktop or web)
What it does:
Day one features:
-

Attached files:
- Design PDF: this is the design spec for this project. Do not ask me about Hali.
- Spec document (optional): if one is attached, read it. It overrides my "Day one features" list above, and you do not need to ask me feature questions.

Order of work:
1. Download the latest standards from https://github.com/carcosa-astral/ca-philosophy/raw/refs/heads/main/CLAUDE.md and save it unchanged as CLAUDE.md in this folder. Read it, follow it, and tell me its version.
2. Tell me to create the new private GitHub repo, and wait for me.
3. Save the design PDF in design/ and the spec document (if any) in docs/.
4. Read the design PDF and give me a short summary of what you see: colors, fonts, layout, and screens. If there is a spec document, summarize it too, in a few lines. Wait for my yes.
5. Ask me your starting questions in one multiple-choice round, up to four questions. If there is a spec document, skip questions about features.
6. Finish the rest of the checklist.
7. Show me a short plan, then build.
```

## What happens

- Claude Code downloads the latest standards from this repo, so every project starts on the current rules.
- It waits for you to create the repo before it saves anything to git.
- It reads the design PDF, and the spec document if you attached one, and tells you what it understood. Nothing gets built until you confirm.
- If there is a spec document, it wins over the feature list in your message, and Claude Code does not ask feature questions.
- It asks its questions all at once so you can answer them in one pass.

## No design PDF yet?

Delete the design line under "Attached files" and the design parts of steps 3 and 4. Claude Code will then ask which design to use (Hali, a spec you provide, or something else).

## No spec document?

Delete the spec line under "Attached files" and the spec parts of steps 3, 4, and 5. Fill in the "Day one features" list instead.
