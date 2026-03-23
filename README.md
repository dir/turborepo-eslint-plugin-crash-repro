# `eslint-plugin-turbo` crash reproduction

> [!IMPORTANT]
> This bug has been resolved in https://github.com/vercel/turborepo/pull/12411.

## Info

`eslint-plugin-turbo` crashes at import time (i.e. running ESLint) when a [package configuration](https://turborepo.dev/docs/reference/package-configurations) (`turbo.json`/`turbo.jsonc`) does not define the `"tasks"` (or legacy `"pipeline"`) key. I have tested this bug on numerous versions of `turbo`, `eslint-plugin-turbo`, as well as on ESLint 9 & 10. The error occurs in all variations. This project is using ESLint 10, `turbo@canary`, and `eslint-plugin-turbo@canary`.

## Steps

1. Install deps with `pnpm i`
2. Run `pnpm lint`, observe the error (`TypeError: Cannot convert undefined or null to object`).
3. Navigate to the package configuration at [`./apps/app-a/turbo.json`](./apps/app-a/turbo.json)
4. Uncomment/add the `tasks` key back to the object
5. Re-run `pnpm lint`, error gone.
