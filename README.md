# renovate-config

Shared [Renovate](https://docs.renovatebot.com/) preset for BeyondFolder Nuxt projects. Use it from a repo's `renovate.json`:

```json
{ "extends": ["github>BeyondFolder/renovate-config"] }
```

- Extends the official Nuxt preset (`github>nuxt/renovate-config-nuxt`): weekly schedule, non-major updates grouped, 25h minimum release age.
- Auto-merges minor/patch/pin/digest updates and lockfile maintenance, but only after every status check is green (Renovate merges itself, `platformAutomerge: false`, since these private repos have no branch protection).
- Majors and 0.x minor bumps are never auto-merged.
- `wrangler` and `@cloudflare/workers-types` are updated together, since wrangler minors can require a new workers-types major.
- Lockfiles are updated with npm 11 (`constraints.npm`), matching the npm bundled with Node 26. npm 12 fails with `EALLOWREMOTE` on packages that bundle their dependencies, such as `@tailwindcss/oxide-wasm32-wasi` ([npm/cli#9800](https://github.com/npm/cli/issues/9800)). Remove the constraint once that is fixed.
