# 📁 Project Structure Guidelines

This project follows a **feature-oriented, scalable architecture** designed for long-term maintainability and clarity.
Every folder has a clear responsibility — follow these conventions strictly to keep the codebase healthy and predictable.

---

### `assets/`

> 📦 **Static resources only.**

* Purpose: Images, SVGs, fonts, logos, and any other static assets that are imported by components.
* Usage: Import them directly inside components (e.g., `import logo from '@assets/logo.svg'`).
* ❌ Do **not** store public CDN files or dynamic content here.

---

### `components/`

> 🧱 **Reusable, dumb UI building blocks.**

* Purpose: Stateless, presentational components that are **UI-only** and **context-agnostic**.
* Examples: `Button.tsx`, `Modal.tsx`, `Card.tsx`, `Spinner.tsx`
* ✅ Should not fetch data or contain feature-specific logic.
* ✅ Should be reusable across multiple pages or features.
* 📁 Naming: `PascalCase` for components (`UserAvatar.tsx`), `index.ts` for exports.

If a component starts handling domain logic or state → **move it to `features/`.**

---

### `features/`

> 🧩 **Domain-specific functionality (encapsulated vertical slices).**

* Purpose: Each subfolder here represents a standalone feature.
  If removed, that functionality should disappear from the app.
* Examples:

  * `auth/` → login, logout, session management
  * `leaderboard/` → fetching, rendering, and updating leaderboard
  * `profile/` → user settings and info

Each feature may include:

```
features/
└─ auth/
   ├─ ui/           # UI components specific to this feature
   ├─ api/          # API calls
   ├─ model/        # Types, hooks, local state
   └─ index.ts      # Feature entry point
```

* ✅ Use `camelCase` or `kebab-case` for folders (`leaderboard/`, `user-profile/`).
* ✅ Export public interfaces from `index.ts`.

---

### `pages/`

> 🗺️ **Route-level containers.**

* Purpose: These are the top-level views tied directly to the router.
* Role: Compose features and components into a page view.
* Examples: `HomePage.tsx`, `DashboardPage.tsx`, `SettingsPage.tsx`
* ✅ Should **not** contain domain logic or state beyond page composition.
* ✅ Folder name matches the route name if possible.

---

### `hooks/`

> 🔁 **Custom React hooks.**

* Purpose: Share reusable logic across components or features.
* Examples: `useDebounce.ts`, `useLocalStorage.ts`, `useIntersectionObserver.ts`
* ✅ Must start with `use`.
* ✅ Should be pure and easily testable.
* ❌ Avoid direct API calls here (those belong to `features/*/api` or `lib/`).

---

### `utils/`

> 🧪 **Pure helper functions.**

* Purpose: Small, stateless, side-effect-free functions.
* Examples: `formatDate.ts`, `slugify.ts`, `deepClone.ts`
* ✅ Should not depend on React or global state.
* ❌ Avoid using them for anything that touches external services or the DOM.

---

### `lib/`

> 🔌 **External integrations and side-effect services.**

* Purpose: This is where your project talks to the outside world.
* Examples:

  * `httpClient.ts` (Axios setup)
  * `firebase.ts` (Firebase init)
  * `analytics.ts` (Telemetry)
* ✅ Centralize third-party config and clients here.
* ✅ Re-export SDKs with typed wrappers if possible.

---

### `styles/`

> 🎨 **Global design layer.**

* Purpose: Global CSS files, Tailwind extensions, theme variables, resets, etc.
* Examples: `globals.css`, `theme.css`, `tailwind.config.ts`
* ✅ Keep design tokens here (colors, spacing, typography).
* ❌ Don’t store color constants or styles in `utils/`.

---

### `router/`

> 🧭 **Routing orchestration.**

* Purpose: Central place to define routes and lazy-load pages.
* Examples: `router.tsx`, `ProtectedRoute.tsx`
* ✅ Router logic should be declarative and not mixed into `App.tsx`.

---

### `App.tsx` & `main.tsx`

> 🚪 **Entry points.**

* `main.tsx`: Bootstraps the React application, mounts it to the DOM.
* `App.tsx`: The root component — wraps router, providers, and global context.

💡 Keep these files as simple as possible. They are the “front door” of the app.

---

## 🧱 File Naming Conventions

| Type              | Convention         | Example                  |
| ----------------- | ------------------ | ------------------------ |
| Components        | `PascalCase`       | `UserAvatar.tsx`         |
| Hooks             | `camelCase`        | `useAuth.ts`             |
| Utility functions | `camelCase`        | `formatDate.ts`          |
| Feature folders   | `kebab-case`       | `user-profile/`          |
| Page components   | `PascalCase`       | `DashboardPage.tsx`      |
| API services      | `camelCase`        | `authApi.ts`             |
| Types/interfaces  | `PascalCase`       | `User.ts`, `Campaign.ts` |
| Global constants  | `UPPER_SNAKE_CASE` | `DEFAULT_PAGE_SIZE`      |

---

## 🧠 Best Practices

* ✅ Keep feature boundaries clear — components in `features/leaderboard` **should not import** directly from `features/auth`.
* ✅ Prefer `index.ts` re-exports to simplify imports:

  ```ts
  import { login } from '@features/auth';
  ```
* ✅ One file = one responsibility. If it grows beyond ~150 lines, split it.
* ❌ Don’t put business logic in `pages/` or `components/`.
* ❌ Avoid deeply nested imports (`../../../utils`). Use path aliases.


