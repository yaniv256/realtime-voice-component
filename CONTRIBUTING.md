# Contributing

Thanks for helping improve `realtime-voice-component`.

## Local Setup

```bash
git clone https://github.com/openai/realtime-voice-component.git
cd realtime-voice-component
npm install
```

## Common Commands

```bash
npm test
npm run typecheck
npm run demo
```

Run the demo after copying `demo/.env.example` to `demo/.env.local` and setting
`OPENAI_API_KEY`.

## Pull Requests

- Keep changes focused and small enough to review.
- Use Conventional Commits for commit messages and PR titles.
- When package behavior, examples, or docs change, update `README.md`,
  `LLM.txt`, `docs/`, and `demo/` together when relevant so they do not drift.
- Add or update tests for behavior changes when practical.

## Reporting Issues

Use GitHub issues for bugs, docs problems, and feature requests.

Do not report security vulnerabilities in public issues. Follow
[SECURITY.md](./SECURITY.md) instead.
