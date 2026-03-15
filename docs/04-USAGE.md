# 04 – Usage (day-to-day)

How to run the app, fix code style, run tests, and trigger builds. All commands below are from **`EasCICDApp/`** unless noted.

---

## Running the app

| Command | What it does |
|---------|----------------|
| `npm start` | Starts Metro bundler (Expo dev client). Then press `i` (iOS) or `a` (Android). |
| `npm run ios` | Builds/opens iOS app in simulator (uses native build if needed). |
| `npm run android` | Builds/opens Android app in emulator or connected device. |
| `npm run web` | Runs the app in the browser. |

---

## Lint and format

| Command | What it does |
|---------|----------------|
| `npm run lint:check` | Runs ESLint in check-only mode (no file changes). Use this in CI. |
| `npm run lint` | Runs ESLint with `--fix` (auto-fixes what it can). |
| `npm run format:check` | Checks if files are formatted with Prettier (no writes). Use this in CI. |
| `npm run format` | Formats all files with Prettier. |

**Recommendation:** Before pushing, run `npm run lint` and `npm run format` so CI (lint + format checks) passes.

---

## Tests

| Command | What it does |
|---------|----------------|
| `npm test` | Runs Jest once (default). |
| `npm run test:watch` | Runs Jest in watch mode (re-runs on file changes). |
| `npm test -- --coverage` | Runs tests and generates coverage report. |

CI runs: `npm test -- --ci --coverage --watchAll=false`.

---

## Type checking

| Command | What it does |
|---------|----------------|
| `npm run compile` | Runs `tsc --noEmit` (type-check only, no emit). |

Useful before committing to catch TypeScript errors.

---

## EAS builds (local or cloud)

These run from `EasCICDApp/` and use profiles from `eas.json`.

| Command | What it does |
|---------|----------------|
| `eas build --platform ios --profile preview` | Build iOS with “preview” profile (e.g. internal distribution). |
| `eas build --platform android --profile preview` | Build Android with “preview” profile. |
| `eas build --platform all --profile preview` | Build both platforms (same as CI’s EAS job). |

**Package.json shortcuts (examples):**

- `npm run build:ios:sim` – development build for iOS simulator (local).
- `npm run build:ios:device` – development build for iOS device (local).
- `npm run build:ios:preview` – preview iOS (local).
- `npm run build:android:preview` – preview Android (local).

For first-time EAS setup and token, see [05-EAS-BUILD-SETUP.md](./05-EAS-BUILD-SETUP.md). For what runs in CI, see [03-CI-CD-PIPELINE.md](./03-CI-CD-PIPELINE.md).

---

## Other useful commands

| Command | What it does |
|---------|----------------|
| `npm run prebuild:clean` | Regenerates `ios/` and `android/` with `expo prebuild --clean`. |
| `npm run align-deps` | Aligns Expo-related dependency versions (`npx expo install --fix`). |
| `npx ignite-cli generate screen MyScreen` | Generates a new screen (Ignite CLI). |
| `npx ignite-cli generate component MyComponent` | Generates a new component. |

---

## Quick pre-push checklist

1. From `EasCICDApp/`: `npm run lint` and `npm run format`
2. `npm run lint:check` and `npm run format:check` (should pass)
3. `npm test`
4. Optionally: `npm run compile`
5. Commit and push; CI will run the same checks and, on `main`, trigger an EAS build.

For setup and tools overview, see [01-SETUP.md](./01-SETUP.md) and [02-SERVICES-AND-TOOLS.md](./02-SERVICES-AND-TOOLS.md).
