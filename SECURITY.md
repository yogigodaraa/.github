# Security policy

## Reporting a vulnerability

**Please don't open a public issue for security problems.**

Report privately through GitHub: open the affected repository, go to
**Security → Report a vulnerability** (private vulnerability reporting).

Please include:

- the repository and commit or version affected
- steps to reproduce, or a proof of concept
- the impact as you understand it

I'll acknowledge reports within 7 days and keep you updated until it's resolved.
These are personal and student projects, so there is no bug bounty, but credit is
given in the fix unless you'd rather stay anonymous.

## Supported versions

Only the latest commit on the default branch (`main`) is supported.

## Secrets and keys

Several projects are **bring-your-own-key (BYOK)**: you supply your own LLM or broker
API keys at runtime. Keys belong in a local `.env` file or the deployment platform's
secret store, never in the repository. If you spot a committed credential, report it
through the private channel above.
