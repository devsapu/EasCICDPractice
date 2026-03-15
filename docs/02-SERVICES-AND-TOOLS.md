# 02 – Services and tools

Short description of the main services and tools used in this repo and how they fit together.

---

## React Native

- **What:** Framework for building native iOS and Android apps using JavaScript/TypeScript and React.
- **In this repo:** The app in `EasCICDApp` is a React Native app (see `react-native` in `package.json`).
- **Docs:** [reactnative.dev](https://reactnative.dev)

---

## Expo

- **What:** Platform and SDK on top of React Native: dev tooling, native APIs (camera, notifications, etc.), and a managed workflow so you can avoid touching native code when possible.
- **In this repo:** The app uses the Expo SDK (`expo` in `package.json`), Expo Router/config, and Expo dev client for development builds.
- **Docs:** [docs.expo.dev](https://docs.expo.dev)

---

## EAS (Expo Application Services)

- **What:** Expo’s cloud service for building and submitting apps. You run builds in the cloud instead of only on your machine.
- **In this repo:** Used for CI builds (see [03-CI-CD-PIPELINE.md](./03-CI-CD-PIPELINE.md)) and for local/cloud builds via `eas build` (see [05-EAS-BUILD-SETUP.md](./05-EAS-BUILD-SETUP.md)). Config lives in `EasCICDApp/eas.json`.
- **Docs:** [expo.dev/eas](https://expo.dev/eas)

---

## Ignite (Infinite Red)

- **What:** Opinionated React Native boilerplate and CLI (generators, structure, theme, testing setup).
- **In this repo:** The app was scaffolded with Ignite; you get the `app/` structure, components, theme, and scripts. Ignite CLI can generate screens/components (`npx ignite-cli generate ...`).
- **Docs:** [docs.infinite.red/ignite-cli](https://docs.infinite.red/ignite-cli/)

---

## GitHub Actions

- **What:** CI/CD platform integrated with GitHub. Workflows run on events like push and pull_request.
- **In this repo:** One workflow (`.github/workflows/ci.yml`) runs lint, Prettier, tests, and (on `main`) EAS build. See [03-CI-CD-PIPELINE.md](./03-CI-CD-PIPELINE.md).
- **Docs:** [docs.github.com/actions](https://docs.github.com/en/actions)

---

## ESLint and Prettier

- **What:** ESLint enforces code quality rules; Prettier enforces formatting.
- **In this repo:** Config in `EasCICDApp/.eslintrc.js` and `EasCICDApp/.prettierrc`. CI runs `lint:check` and `format:check`. Use `npm run lint` / `npm run format` locally to fix.
- **Docs:** [eslint.org](https://eslint.org), [prettier.io](https://prettier.io)

---

## Jest

- **What:** JavaScript/TypeScript test runner.
- **In this repo:** Unit tests in `EasCICDApp` (e.g. `app/`, `test/`). Run with `npm test`. CI runs tests with `--ci --coverage --watchAll=false`.
- **Docs:** [jestjs.io](https://jestjs.io)

---

## How they fit together

```
Developer machine          GitHub                    Expo / EAS
      │                       │                          │
      │  push / merge to main  │                          │
      ├──────────────────────►│  Actions: lint, format,  │
      │                       │  test, then EAS build    │
      │                       ├──────────────────────────►│  Cloud build
      │                       │                          │
      │  npm run ios/android   │                          │
      │  (local dev)          │                          │
```

- **Local:** You use Node, npm, React Native, Expo, and Ignite to develop and run the app.
- **CI:** GitHub Actions runs quality checks and, on `main`, triggers an EAS build.
- **EAS:** Builds produce installable binaries (e.g. preview builds) and can be used for store submission later.

For setup and usage details, see [01-SETUP.md](./01-SETUP.md) and [04-USAGE.md](./04-USAGE.md).
