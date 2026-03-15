# 03 – CI/CD pipeline (GitHub Actions)

How the pipeline is triggered, what jobs run, and what you need to configure (including secrets).

---

## Where the workflow lives

- **File:** `.github/workflows/ci.yml`
- **Repository:** [EasCICDPractice](https://github.com/devsapu/EasCICDPractice)

All jobs run with **working directory** `EasCICDApp` (the Ignite app).

---

## When it runs

| Event | Branch | What runs |
|-------|--------|-----------|
| **Push** | `main` | Lint, Prettier, Test, **and** EAS Build |
| **Pull request** | targeting `main` | Lint, Prettier, Test only (no EAS build) |

So: every merge to `main` runs full checks and then triggers an EAS build. PRs only run checks.

---

## Jobs overview

| Job | Purpose |
|-----|--------|
| **lint** | Runs `npm run lint:check` (ESLint). Fails if there are lint errors. |
| **format** | Runs `npm run format:check` (Prettier). Fails if files are not formatted. |
| **test** | Runs `npm test` with `--ci --coverage --watchAll=false`. Fails if tests fail. |
| **eas-build** | Runs only on **push to main** (after lint, format, test pass). Runs `eas build --platform all --profile preview --non-interactive`. **Requires `EXPO_TOKEN` secret.** |

---

## Required secret for EAS build

The **eas-build** job needs an Expo auth token so GitHub Actions can call EAS on your behalf.

1. **Get a token**
   - Log in at [expo.dev](https://expo.dev).
   - Go to **Account settings** → **Access tokens** (or [expo.dev/accounts/[account]/settings/access-tokens](https://expo.dev)).
   - Create a token (e.g. “GitHub Actions CI”). Copy it.

2. **Add it in GitHub**
   - Repo → **Settings** → **Secrets and variables** → **Actions**.
   - **New repository secret**
   - Name: `EXPO_TOKEN`
   - Value: the token you copied.

If `EXPO_TOKEN` is not set, the **eas-build** step will fail. Until you add it, you can either add the secret (recommended) or temporarily disable the `eas-build` job in `ci.yml` (see “Optional: disable EAS build” below).

---

## Node version

The workflow uses **Node 20** (see `NODE_VERSION` in `ci.yml`), matching the app’s `engines` in `package.json`.

---

## Optional: disable EAS build

If you want CI to only run lint, format, and test (e.g. before you have an Expo account or token):

1. Open `.github/workflows/ci.yml`.
2. Remove or comment out the entire **eas-build** job (the second job that uses `expo-github-action` and `eas build`).

You can add the job back and set `EXPO_TOKEN` when you’re ready. See [05-EAS-BUILD-SETUP.md](./05-EAS-BUILD-SETUP.md) for full EAS setup.

---

## Viewing runs

- **GitHub:** Repo → **Actions** tab. Click a run to see logs per job.
- **EAS:** [expo.dev](https://expo.dev) → your project → **Builds** to see builds triggered by CI.

---

## Summary

- **Trigger:** Push to `main` and pull requests targeting `main`.
- **Quality gates:** Lint, Prettier, and tests must pass.
- **EAS:** Only on push to `main`; requires `EXPO_TOKEN` in GitHub secrets.
- **Build profile used in CI:** `preview` (see `EasCICDApp/eas.json`). Change the workflow if you want a different profile (e.g. `production`).

For first-time EAS and token setup, see [05-EAS-BUILD-SETUP.md](./05-EAS-BUILD-SETUP.md).
