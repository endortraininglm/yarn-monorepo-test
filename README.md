# 🧪 Mini Monorepo Learning Lab

Sall focused Yarn 3 workspace project designed to experiment and debug:

- Dependency management across apps
- Yarn `workspace:^` linking
- Focused installations with `yarn workspaces focus`
- `node_modules` structure inside workspaces
- Troubleshooting dependency resolution

---

## 🏗 Project Structure

```
/
├── package.json          # Root workspace config
├── yarn.lock             # Single lock file at root
├── .yarnrc.yml           # Yarn 3 config using node-modules linker
└── apps/
    ├── app-admin/        # Depends on app-shared (using workspace:^)
    ├── app-shared/       # Shared module
    └── app-account/      # Standalone React app
```

---

## 📦 Applications

| App           | Description                                              | Notable              |
|---------------|----------------------------------------------------------|----------------------|
| `app-admin`   | Admin panel app. Depends on `shared` using `workspace:^` | Cross-app dependency |
| `app-shared`  | Common utilities library (`lodash` usage)                |                      |
| `app-account` | Independent React-based app                              | Standalone           |

---

## ⚙ Setup Instructions

1. **Install dependencies at the root** (monorepo installation):
   ```bash
   yarn install
   ```

2. **Focus install a single app (optional):**
   Install *only* what's needed for `admin`:
   ```bash
   yarn workspaces focus admin
   ```

3. **Build a specific app:**
   ```bash
   yarn workspace admin build
   ```

4. **General project build:**
   ```bash
   yarn build
   ```
   (You may need simple build scripts inside each app to fully support this.)

---

## 📄 Important Concepts Demonstrated

- **Workspace Linking:**  
  `app-admin` references `app-shared` **locally** via `workspace:^`, meaning Yarn auto-links the dependency instead of fetching it from npm.

- **Single Source of Truth:**  
  Only **one** `yarn.lock` file exists at the root for the entire monorepo.

- **Node_Modules Linker:**  
  Configured to use the **`node_modules`** linker, **not** Plug'n'Play (pnp).

- **Focus Install Behavior:**  
  You can install only the needed dependencies for a single app — useful for CI/CD and limited environments.

---