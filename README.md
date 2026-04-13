# Skills Quick Guide

Use this repo with the Skills ecosystem at [skills.sh](https://skills.sh/).

## Install a skill

Run:

```bash
npx skills add <owner/repo>
```

Example:

```bash
npx skills add vercel-labs/skills
```

## Find skill names

1. Open [skills.sh](https://skills.sh/)
2. Search for the skill you want
3. Copy the `owner/repo` value
4. Install with `npx skills add <owner/repo>`

## Verify installation

After install, run:

```bash
npx skills list
```

## Update installed skills

```bash
npx skills update
```

## Notes

- Use Node.js 18+ for best compatibility with modern CLI tools.
- If `npx` prompts for confirmation, select `y`.
- If install fails, retry with a different network/VPN and run the command again.
