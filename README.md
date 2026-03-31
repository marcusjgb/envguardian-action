

````md
# EnvGuardian Action

Run EnvGuardian in GitHub Actions to detect missing environment variables before deploy.

---

## ✨ What it does

This GitHub Action runs [EnvGuardian](https://www.npmjs.com/package/@marcosjgb/envguardian) in your CI pipeline to:

- detect missing environment variables
- prevent broken deployments
- enforce consistency between `.env` and your code

---

## 🚀 Quick Start

Add this step to your workflow:

```yaml
- uses: actions/checkout@v4

- name: Run EnvGuardian
  uses: marcusjgb/envguardian-action@v1
````

---

## ⚙️ Example with CI setup

```yaml
name: EnvGuardian Check

on:
  pull_request:
  push:
    branches: [ main ]

jobs:
  envguardian:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Create .env for CI
        run: |
          cat > .env <<EOF
          DATABASE_URL=dummy_database_url
          JWT_SECRET=dummy_jwt_secret
          VITE_API_URL=http://localhost:3000
          EOF

      - name: Run EnvGuardian
        uses: marcusjgb/envguardian-action@v1
```

---

## ⚙️ Inputs

### `version`

EnvGuardian version to use.

```yaml
with:
  version: "0.1.3"
```

Default:

```text
0.1.3
```

---

### `args`

Arguments passed to EnvGuardian CLI.

```yaml
with:
  args: "check --ci --only-missing"
```

Default:

```text
check --ci --only-missing
```

---

### `working-directory`

Directory where EnvGuardian will run.

```yaml
with:
  working-directory: "apps/web"
```

Default:

```text
.
```

---

## 🧠 Example with custom inputs

```yaml
- name: Run EnvGuardian
  uses: marcusjgb/envguardian-action@v1
  with:
    version: "0.1.3"
    args: "check --ci"
    working-directory: "apps/api"
```

---

## ❌ Failure behavior

If missing variables are detected:

```text
✖ Missing variables detected
✖ EnvGuardian check failed
```

👉 the workflow will fail automatically.

---

## 🔍 How it works

This action:

1. sets up Node.js
2. installs EnvGuardian
3. runs the CLI inside your repository

---

## 💡 Why use this action?

* avoid runtime crashes due to missing env vars
* enforce env consistency in CI
* catch issues before deploy
* improve team reliability

---

## 🔗 Related

* EnvGuardian CLI: [https://www.npmjs.com/package/@marcosjgb/envguardian](https://www.npmjs.com/package/@marcosjgb/envguardian)
* Main repository: [https://github.com/marcosjgb/envguardian](https://github.com/marcosjgb/envguardian)

---

## 📜 License

MIT

````



