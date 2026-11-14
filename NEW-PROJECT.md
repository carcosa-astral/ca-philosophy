# NEW-PROJECT.md: Starter Message

Paste the message below into Claude Code to start a new project. It works with the standards in `CLAUDE.md`.

## How to use

1. Make a new empty folder for the project and open Claude Code in it.
2. Copy the message below and fill in the four blanks.
3. Attach the design PDF.
4. Send it.

## The message

```
New project. Follow the new project checklist in the standards.

Name:
Type: (desktop or web)
What it does:
Day one features:
-

The attached PDF is the design spec for this project. Do not ask me about Hali.

Order of work:
1. Download the latest CLAUDE.md into this folder and tell me its version.
2. Tell me to create the new private GitHub repo, and wait for me.
3. Save the PDF in design/. Read it and give me a short summary of what you see: colors, fonts, layout, and screens. Wait for my yes.
4. Ask me your starting questions in one multiple-choice round, up to four questions.
5. Finish the rest of the checklist.
6. Show me a short plan, then build.
```

## What happens

- Claude Code downloads the latest standards, so every project starts on the current rules.
- It waits for you to create the repo before it saves anything to git.
- It reads the design PDF and tells you what it understood. Nothing gets built until you confirm.
- It asks its questions all at once so you can answer them in one pass.

## No design PDF yet?

Delete the two design lines and step 3 from the message. Claude Code will then ask which design to use (Hali, a spec you provide, or something else).
