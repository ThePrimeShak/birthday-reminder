# Birthday Reminder

Birthday Reminder is a mobile-first Persian web app for tracking friends' Solar Hijri birthdays and saving gift ideas for each friend. The repository currently contains the Next.js starter and project documentation.

## Run locally

Use Node.js 20.9 or newer and npm.

```bash
npm ci
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to see the starter. Run `npm run lint` for linting, `npm run build` for a production build, and `npm run start` to serve that build.

## Project documents

- [Project overview](context/project-overview.md) covers the product, milestones, and open decisions.
- [Repository instructions](AGENTS.md) link to the coding and review workflow.
- [Current feature](context/current-feature.md) records the active spec and completion history.

## Configure Context7 for Codex

In a trusted project, merge the Context7 settings from the [MCP example](context/codex-mcp.toml) into `.codex/config.toml`. The same example includes an optional read-only Neon connection.

```bash
codex mcp login context7
codex mcp list
```

Confirm that Context7 is listed, then request a documentation lookup to verify the connection.
