# Reporting a security problem

If you've found something in Relay that looks like a security issue, we want to hear about it. You don't have to be a security researcher to report one. If something feels wrong, send it our way and we'll figure out together whether it's an issue and what to do.

## What counts as a security issue

Roughly, anything that could let someone do something they shouldn't. Examples:

- A way for a website or another app to control Relay against your will.
- A way for Relay to leak something private (your API keys, your captured artifacts, the contents of your screen) somewhere it shouldn't go.
- A way for a malicious mission plan to do something the app wasn't supposed to allow (like running arbitrary shell commands when it was only supposed to be clicking buttons).
- A way to bypass the approval gates that are supposed to pause for your sign-off.
- A way for an agent connected through the Agent Bridge to act above the tier you granted it, or to reach the bridge from somewhere other than your own machine.
- A way for someone with brief access to your unlocked computer to extract more from Relay than they should be able to.

If you're not sure whether what you found counts, send it anyway. We'd rather get something that turns out to be a non-issue than miss something that mattered.

## How to send it

Email us at **<support@meterless.ai>**. That inbox is read by the small team that actually works on Relay, not by a generic support queue.

Please don't file a public GitHub issue for a security problem. We'd rather get the fix out before the details are public.

What's helpful to include:

- A short description of what the issue is.
- Steps to reproduce it, if you have them.
- What you think the impact is. If you're not sure, say so. We can help work that out.
- Your Relay version (Settings → Data & Alerts → App updates) and your Windows version.

What you don't need to include:

- A formal vulnerability disclosure document. A paragraph or two is fine.
- A proof-of-concept exploit. If you have one and want to send it, great. If not, don't worry about it.
- Your real name. If you'd rather report under a handle, that's fine.

## What happens after you send it

We aim to reply within two business days letting you know we got it and what we think initially. If it's a real issue, we'll keep you in the loop on the fix and the timeline. Once a fix is shipped, we'll credit you in the changelog if you want the credit, or leave you out of it if you'd rather stay anonymous.

If you're hoping for a bug bounty, we don't have a formal program yet. We do sometimes send a thank-you, but please don't report things expecting payment.

## What's in scope

The Relay desktop app on Windows. The local data files it writes to your machine. The Agent Bridge, the `relay` CLI and its MCP server. The code in this repository.

What isn't really our scope:

- Issues in the AI provider you've configured (Google, Anthropic, OpenAI, OpenRouter, OpenCode Go, or a server you host). Those should go to them.
- Issues in Windows itself. Microsoft has its own security reporting process.
- Issues that require the attacker to already have admin access to your machine. At that point they can do whatever they want regardless of Relay.

If you found something in a dependency we use, send it our way anyway. We can help route it.

---

Thanks for taking the time. Security reports from real users have made Relay meaningfully safer more than once, and we appreciate every one of them.
