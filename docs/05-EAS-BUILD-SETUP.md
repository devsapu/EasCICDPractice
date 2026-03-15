# 05 – EAS build setup

How to set up EAS (Expo Application Services) so the app can be built in the cloud and so the GitHub Actions pipeline can run EAS build on merge to `main`.

---

## What you need

- An **Expo account** ([expo.dev](https://expo.dev)).
- **EAS CLI** (installed via project or globally): `npm install -g eas-cli` or use `npx eas` from the project.
- For **CI:** an **Expo access token** stored as the `EXPO_TOKEN` secret in GitHub (see [03-CI-CD-PIPELINE.md](./03-CI-CD-PIPELINE.md)).

---

## First-time EAS setup (one-time per project) — required for CI

**Important:** CI runs `eas build` in non-interactive mode. You must run **`npx eas init`** locally once (while logged in) so EAS links the app to an Expo project and adds `projectId` to your config. Commit and push that change. Otherwise CI fails with **"EAS project not configured"**.

1. **Log in**
   ```bash
   cd EasCICDApp
   npx eas login
   ```
   Use your Expo account email/password or SSO.

2. **Configure the project for EAS (if not already)**
   - The repo already has `eas.json` with profiles: `development`, `development:device`, `preview`, `preview:device`, `production`.
   - Link the project to your Expo account (first time only):
     ```bash
     npx eas build:configure
     ```
   - If the project is not yet on Expo’s servers, you may be prompted to create it; follow the prompts.

3. **Run a build yourself (optional but recommended)**
   ```bash
   npx eas build --platform ios --profile preview --non-interactive
   ```
   Or Android: `--platform android`. Or both: `--platform all`.

   This checks that your Expo account, project, and `eas.json` are correct. Builds run at [expo.dev](https://expo.dev) → your account → project → **Builds**.

---

## Token for GitHub Actions (EXPO_TOKEN)

The CI workflow runs `eas build` only on **push to main**. It needs an Expo token so it can authenticate to EAS.

1. **Create an Expo access token**
   - Go to [expo.dev](https://expo.dev) → log in.
   - Open **Account settings** → **Access tokens** (or [expo.dev/accounts/…/settings/access-tokens](https://expo.dev)).
   - Create a new token (e.g. name: “GitHub Actions CI”). Copy the value.

2. **Add the token in GitHub**
   - Open your repo on GitHub → **Settings** → **Secrets and variables** → **Actions**.
   - **New repository secret**
   - Name: **`EXPO_TOKEN`**
   - Value: paste the token.

3. **Trigger a build from CI**
   - Merge a change to `main` (or push to `main`). The **EAS Build** job in the Actions tab will use `EXPO_TOKEN` to run `eas build --platform all --profile preview --non-interactive`.

If you don’t add `EXPO_TOKEN`, the EAS build step in CI will fail until the secret is set. You can temporarily remove or comment out the **eas-build** job in `.github/workflows/ci.yml` if you only want lint/format/test (see [03-CI-CD-PIPELINE.md](./03-CI-CD-PIPELINE.md)).

---

## Build profiles (eas.json)

| Profile | Typical use |
|--------|-------------|
| **development** | Dev client, simulator (iOS) / debug (Android). |
| **development:device** | Dev client on physical device. |
| **preview** | Internal/testing builds (e.g. APK, simulator build). **Used by CI.** |
| **preview:device** | Preview on physical device. |
| **production** | Store-ready builds. |

CI uses **preview** so every merge to `main` produces installable builds without submitting to stores. To use another profile in CI, edit the `eas build` command in `.github/workflows/ci.yml`.

---

## Useful EAS commands (from EasCICDApp/)

| Command | What it does |
|---------|----------------|
| `npx eas build --platform all --profile preview` | Build iOS + Android with `preview` profile. |
| `npx eas build:list` | List recent builds. |
| `npx eas build:view` | Open build page in browser. |
| `npx eas whoami` | Show current Expo user. |

---

## Troubleshooting

- **“Not logged in”**  
  Run `npx eas login` from `EasCICDApp/`.

- **“Project not found” / “Invalid project”**  
  Run `npx eas build:configure` and ensure the project is linked to your Expo account. Check `app.json` / `app.config.ts` for correct `slug` and `owner` if you use a custom organization.

- **CI fails on EAS build with “EXPO_TOKEN”**  
  Add the `EXPO_TOKEN` repository secret in GitHub (see above). If you don’t want EAS in CI yet, disable the **eas-build** job in `ci.yml` (see [03-CI-CD-PIPELINE.md](./03-CI-CD-PIPELINE.md)).

- **Build fails on EAS servers**  
  Check the build log on [expo.dev](https://expo.dev) → project → Builds. Common causes: wrong Node version, missing env vars, or native dependency issues. Our CI uses Node 20; EAS uses the project’s config.

For pipeline behavior and job details, see [03-CI-CD-PIPELINE.md](./03-CI-CD-PIPELINE.md). For daily usage of scripts and EAS, see [04-USAGE.md](./04-USAGE.md).
