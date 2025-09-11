# 🧪 ts-checks

**Modular TypeScript hygiene for CI pipelines.**  
Runs formatting, linting, and tests with clarity, edge case awareness, and zero boilerplate.

---

## 🚀 Overview

`ts-checks` is a composite GitHub Action that validates TypeScript and JavaScript projects using your own scripts. It handles:

- ✅ Dependency installation (`npm ci`)
- ✅ Script presence validation (`format`, `lint`, `test`)
- ✅ Execution of hygiene steps
- ✅ Output reporting (`checks-passed: true|false`)
- ✅ Graceful failure for missing `package.json` or scripts

Designed for **modular CI**, **reviewer-centric workflows**, and **self-documenting repos**.

---

## 📦 Usage

### Minimal Workflow

```yaml
jobs:
  ts-checks-test:
    runs-on: ubuntu-latest
    steps:
      - uses: owen-6936/ts-checks@v1.0.0
```

### With Output

```yaml
jobs:
  ts-checks-test:
    runs-on: ubuntu-latest
    steps:
      - name: Run ts-checks
        id: checks
        uses: owen-6936/ts-checks@v1.0.0

      - name: Report Result
        run: echo "✅ checks-passed: ${{ steps.checks.outputs.checks-passed }}"
```

---

## ⚙️ Inputs

| Name          | Description                          | Default |
|---------------|--------------------------------------|---------|
| `node-version` | Node.js version to use               | `20`    |

---

## 📤 Outputs

| Name            | Description                                |
|-----------------|--------------------------------------------|
| `checks-passed` | `true` if all checks succeeded, else `false` |

---

## 🧠 Script Requirements

Your `package.json` must define the following scripts:

```json
{
  "scripts": {
    "format": "prettier --write .",
    "lint": "eslint . --ext .ts,.tsx,.js",
    "test": "jest"
  }
}
```

If any are missing, the action will fail with a clear message.

---

## 🧱 What It Does

| Step                  | Description                                      |
|-----------------------|--------------------------------------------------|
| `checkout`            | Clones your repo                                 |
| `setup-node`          | Sets up Node.js                                  |
| `npm ci`              | Installs dependencies                            |
| `script validation`   | Ensures `format`, `lint`, `test` scripts exist   |
| `run format`          | Executes `npm run format`                        |
| `run lint`            | Executes `npm run lint`                          |
| `run test`            | Executes `npm run test`                          |
| `output checks-passed`| Emits result for downstream jobs                 |

---

## 🧩 Philosophy

- **Modular**: No assumptions about your framework or tooling
- **Expressive**: Clear logs, emoji feedback, and output signaling
- **Reviewer-friendly**: Fails early, explains clearly, respects authorship
- **Future-proof**: Designed to support `yarn`, `bun`, and custom script names

---

## 🔮 Roadmap

- `v1.1.0`: Add support for `yarn` and `bun`
- `v1.2.0`: Optional scaffolding for missing `package.json`
- `v1.3.0`: Custom script names via inputs

---

## 🛡️ License

MIT — build freely, review kindly.

---

## 💬 Feedback

Open an issue or discussion if you hit an edge case or want to extend support.  
This action is part of the **expo-ci basic family** — modular DX tools for expressive CI.
