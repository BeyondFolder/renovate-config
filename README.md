# renovate-config

Shared [Renovate](https://docs.renovatebot.com/) preset for BeyondFolder Nuxt projects. Use it from a repo's `renovate.json`:

```json
{ "extends": ["github>BeyondFolder/renovate-config"] }
```

- Extends the official Nuxt preset (`github>nuxt/renovate-config-nuxt`): weekly schedule, non-major updates grouped, 25h minimum release age.
- Auto-merges minor/patch/pin/digest updates and lockfile maintenance, but only after every status check is green (Renovate merges itself, `platformAutomerge: false`, since these private repos have no branch protection).
- Majors and 0.x minor bumps are never auto-merged.
- `wrangler` and `@cloudflare/workers-types` are updated together, since wrangler minors can require a new workers-types major.
- The AI SDK packages (`ai`, `@ai-sdk/*`, `workers-ai-provider`, `ai-gateway-provider`, `@openrouter/ai-sdk-provider`) are updated together, since their majors depend on each other.
- `typescript` stays below 7. TypeScript 7.0 is the Go port and ships no JS API, which vue-tsc (`nuxt typecheck`), typescript-eslint and `nuxt prepare` rely on ([announcement](https://devblogs.microsoft.com/typescript/announcing-typescript-7-0/)). Lift it once vue-tsc ([vuejs/language-tools#5381](https://github.com/vuejs/language-tools/issues/5381)) and typescript-eslint ([#10940](https://github.com/typescript-eslint/typescript-eslint/issues/10940)) support it.
- Lockfiles are updated with npm 11 (`constraints.npm`), matching the npm bundled with Node 26. npm 12 fails with `EALLOWREMOTE` on packages that bundle their dependencies, such as `@tailwindcss/oxide-wasm32-wasi` ([npm/cli#9800](https://github.com/npm/cli/issues/9800)). Remove the constraint once that is fixed.
