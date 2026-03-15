# EasCICDPractice

Repository for the **EasCICDApp** — an [Ignite](https://github.com/infinitered/ignite) (React Native + Expo) app with CI/CD via GitHub Actions and EAS Build.

---

## What’s in this repo

| Path | Description |
|------|--------------|
| **EasCICDApp/** | The Ignite React Native + Expo app (screens, components, theme, tests). |
| **.github/workflows/** | GitHub Actions CI: lint, Prettier, tests, and EAS build on merge to `main`. |
| **docs/** | End-to-end documentation (setup, services, CI/CD, usage, EAS). |

---

## Quick start

```bash
cd EasCICDApp
npm install
npm run ios    # or: npm run android | npm run web
```

See **[docs/01-SETUP.md](docs/01-SETUP.md)** for full setup and prerequisites.

---

## Documentation (find what you need)

All detailed docs live in **`docs/`**. Use the index to see which file covers what:

- **[docs/README.md](docs/README.md)** — **Start here:** index and short description of each document.
- [docs/01-SETUP.md](docs/01-SETUP.md) — Prerequisites and first-time setup.
- [docs/02-SERVICES-AND-TOOLS.md](docs/02-SERVICES-AND-TOOLS.md) — Expo, EAS, Ignite, React Native, etc.
- [docs/03-CI-CD-PIPELINE.md](docs/03-CI-CD-PIPELINE.md) — GitHub Actions: triggers, jobs, secrets.
- [docs/04-USAGE.md](docs/04-USAGE.md) — Daily usage: scripts, lint, format, test, EAS.
- [docs/05-EAS-BUILD-SETUP.md](docs/05-EAS-BUILD-SETUP.md) — EAS credentials, EXPO_TOKEN, first build.

---

## CI/CD at a glance

- **On every push to `main` and on pull requests to `main`:** Lint (ESLint), format (Prettier), and tests (Jest) run in GitHub Actions.
- **On push to `main` only:** An EAS Build (preview profile, all platforms) runs after checks pass. Requires `EXPO_TOKEN` in repo secrets.

See **[docs/03-CI-CD-PIPELINE.md](docs/03-CI-CD-PIPELINE.md)** and **[docs/05-EAS-BUILD-SETUP.md](docs/05-EAS-BUILD-SETUP.md)** for setup and details.
