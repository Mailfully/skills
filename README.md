# Add Mailfully: An Agent Skill for Claude Code and Other Coding Agents

This skill wires your app's emails (welcome, password reset, receipts) to [Mailfully](https://mailfully.com), a transactional email API, or moves them there from Resend, SendGrid, Postmark or Nodemailer/SMTP. It works in Node.js, Python, Ruby, Go and PHP projects. Mailfully is free for 3,000 emails a month; paid plans from $5 a month for 10,000 ([pricing](https://mailfully.com/pricing), [docs](https://mailfully.com/docs)).

## What it does

1. Reads your project to find the language, the framework, the Node.js version, the provider you use now and the env file your framework loads.
2. Adds one send helper and points your existing call sites at it. On Node.js 24 or later it installs the Mailfully SDK; older Node projects get a small `fetch` helper instead. Python, Ruby, Go and PHP projects get a small HTTP client, and Django and Rails apps get a Mailfully email backend or delivery method, so existing mailers keep working unchanged.
3. Sends one email in test mode and waits up to two minutes for it to be delivered. Test mail reaches no real inbox, and test mode needs no DNS, so you know the code works before you touch your domain.
4. Sets up a webhook handler if you want delivery events, with a signature check written for Node.js or Python.
5. Prepares the DNS records for your sending domain and checks them once they are published.

A migration ships behind an `EMAIL_PROVIDER` switch that defaults to your current provider. You flip it once your sending domain is verified and your account is approved. New accounts are reviewed before full-volume sending.

## Install

Claude Code users can install it as a plugin; everyone else can use `npx skills add`.

With [skills.sh](https://skills.sh), which installs it for Cursor, Codex and most other coding agents:

```bash
npx skills add Mailfully/skills
```

As a Claude Code plugin:

```text
/plugin marketplace add Mailfully/skills
/plugin install add-mailfully@mailfully
```

From [ClawHub](https://clawhub.ai):

```bash
clawhub install @mailfully/add-mailfully
```

Then ask your agent something like "add Mailfully to this app" or "move our email from SendGrid to Mailfully".

## What it will and won't do

- It never asks you to paste your API key into the chat, and the agent never opens your env file. You create a test key in the Mailfully dashboard and paste it into that file yourself.
- If your env file is missing from `.gitignore`, it adds it there before any key goes in.
- DNS records are printed by default, along with the commands that would add them. The skill writes a record only after you say yes.
- An existing DNS record is never overwritten, and no name gets a second SPF record.
- Marketing and bulk sends stay with your current provider. This version covers transactional email only.
- Nothing is committed unless you agree.

## You will need

- A Mailfully account. Sign up at [mailfully.com](https://mailfully.com); the free plan is enough to try it.
- Node.js 24 or later if you want the skill to use the Mailfully CLI. Without it, you add your domain in the dashboard instead.
- A domain you can add DNS records to, when you are ready to send live mail.

## About this repository

This repository is a published copy of the skill. Changes are made in Mailfully's own repository and synced here, so pull requests can't be merged directly. Questions and bug reports are welcome at contact@mailfully.com.

## License

MIT. See [LICENSE](LICENSE).
