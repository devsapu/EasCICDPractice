# Documentation index

This folder contains end-to-end documentation for the **EasCICDPractice** repo: the Ignite (React Native + Expo) app and its CI/CD pipeline.

Use this page to quickly find which document covers what.

---

## Quick reference

| Document | What it contains |
|----------|-------------------|
| **[01-SETUP.md](./01-SETUP.md)** | Prerequisites, local environment setup, first-time clone and run. |
| **[02-SERVICES-AND-TOOLS.md](./02-SERVICES-AND-TOOLS.md)** | Short descriptions of services and tools: Expo, EAS, Ignite, React Native, and how they fit together. |
| **[03-CI-CD-PIPELINE.md](./03-CI-CD-PIPELINE.md)** | GitHub Actions workflow: triggers, jobs (lint, Prettier, test, EAS build), and required secrets. |
| **[04-USAGE.md](./04-USAGE.md)** | Day-to-day usage: npm scripts, running the app, lint/format/test, and EAS build commands. |
| **[05-EAS-BUILD-SETUP.md](./05-EAS-BUILD-SETUP.md)** | EAS-specific setup: Expo account, `EXPO_TOKEN`, first cloud build, and troubleshooting. |

---

## Recommended reading order

1. **New to the repo or setting up your machine** → [01-SETUP.md](./01-SETUP.md)  
2. **Want to understand the stack** → [02-SERVICES-AND-TOOLS.md](./02-SERVICES-AND-TOOLS.md)  
3. **Using the app and scripts daily** → [04-USAGE.md](./04-USAGE.md)  
4. **Enabling or debugging CI/CD** → [03-CI-CD-PIPELINE.md](./03-CI-CD-PIPELINE.md)  
5. **Configuring EAS or first cloud build** → [05-EAS-BUILD-SETUP.md](./05-EAS-BUILD-SETUP.md)

---

## Repo structure

```
EasCICDPractice/
├── .github/workflows/   # GitHub Actions (CI/CD)
├── docs/                # This documentation
├── EasCICDApp/          # Ignite React Native + Expo app
│   ├── app/             # Screens, components, theme, i18n
│   ├── assets/
│   ├── eas.json         # EAS build/submit profiles
│   ├── package.json
│   └── ...
└── README.md            # Root repo overview
```

For more detail on the app structure, see [EasCICDApp/README.md](../EasCICDApp/README.md).
