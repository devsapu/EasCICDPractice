# 01 – Setup (end-to-end)

How to set up your machine and run the project from a fresh clone.

---

## Prerequisites

- **Node.js** ≥ 20 (see `EasCICDApp/package.json` `engines.node`).
- **npm** (comes with Node) or yarn.
- **Git**
- **For iOS development:** macOS, Xcode, CocoaPods, iOS Simulator.
- **For Android development:** Android Studio, Android SDK, emulator or device.
- **For EAS (cloud builds):** Expo account ([expo.dev](https://expo.dev)).

Optional but useful:

- **Watchman** (recommended on macOS for Metro).
- **UTF-8 locale** for CocoaPods (e.g. `export LANG=en_US.UTF-8` and `LC_ALL=en_US.UTF-8` in `~/.zshrc`).

---

## Clone and install

```bash
git clone https://github.com/devsapu/EasCICDPractice.git
cd EasCICDPractice/EasCICDApp
npm install
```

If you hit peer dependency issues, try:

```bash
npm install --legacy-peer-deps
```

---

## Run the app

- **iOS Simulator**
  ```bash
  npm run ios
  ```
  Or start Metro then press `i`: `npm start` → `i`.

- **Android**
  ```bash
  npm run android
  ```
  Or `npm start` → `a`.

- **Web**
  ```bash
  npm run web
  ```

On first `npm run ios`, native dependencies (CocoaPods) will install; ensure your shell uses UTF-8 (see Prerequisites) if you see encoding errors.

---

## Verify setup

- **Lint**
  ```bash
  npm run lint:check
  ```
- **Format (Prettier)**
  ```bash
  npm run format:check
  ```
- **Tests**
  ```bash
  npm test
  ```

All commands above are run from `EasCICDPractice/EasCICDApp/`.

---

## Next steps

- **Daily commands and scripts** → [04-USAGE.md](./04-USAGE.md)  
- **What each service/tool does** → [02-SERVICES-AND-TOOLS.md](./02-SERVICES-AND-TOOLS.md)  
- **EAS and CI/CD** → [03-CI-CD-PIPELINE.md](./03-CI-CD-PIPELINE.md), [05-EAS-BUILD-SETUP.md](./05-EAS-BUILD-SETUP.md)
