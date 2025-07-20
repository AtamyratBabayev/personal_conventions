## Project structure
```
/src
│
├── /app                 # Global app setup (navigation, themes, providers)
│   ├── navigation       # Stack/Tab navigation
│   ├── theme            # Theme (colors, fonts)
│   └── providers        # Contexts or Zustand-stores
│
├── /shared              # Reusable parts (UI и utilities)
│   ├── components       # Generic UI-components (Button, Input)
│   ├── hooks            # Custom hooks
│   ├── types            # Global types
│   ├── utils            # Utilities (formatDate, validators и т.д.)
│   └── assets           # Images, icons, font files
│
├── /features            # Features (each in their own folder)
│   ├── /auth
│   │   ├── screens
│   │   ├── components
│   │   ├── hooks
│   │   ├── api.ts
│   │   ├── types.ts
│   │   └── index.ts
│   │
│   ├── /todos
│   │   ├── screens
│   │   ├── components
│   │   ├── hooks
│   │   ├── store.ts         # Zustand or Context
│   │   ├── api.ts
│   │   ├── types.ts
│   │   └── index.ts
│   │
│   └── /profile
│       ├── screens
│       ├── components
│       ├── hooks
│       ├── api.ts
│       └── types.ts
│
├── /config              # Settings and variables (API_URL, env)
├── App.tsx              # Entry point
└── index.js             # Export src
```
## Feature structure
```
/features/todos
├── screens
│   ├── TodoListScreen.tsx
│   └── AddTodoScreen.tsx
│
├── components
│   └── TodoCard.tsx
│
├── hooks
│   └── useFilteredTodos.ts
│
├── store.ts         # Zustand/Context
├── api.ts           # Server/AsyncStorage
├── types.ts         # Interfaces Todo, filters etc.
└── index.ts         # Export feature
```

## Index.js usage (Be ready to add alias to have more clear imports)

This table summarizes where `index.ts` files should or shouldn't be added according to your project structure and why.

| Path                                     | `index.ts` | Reason                                                                 |
|------------------------------------------|------------|------------------------------------------------------------------------|
| `/src/app`                               | ❌         | App setup code is internal and not reused outside                     |
| `/src/app/navigation`                    | ❌         | Only used in app bootstrap, not reused                                |
| `/src/app/theme`                         | ❌         | Theme files are consumed via direct import                            |
| `/src/app/providers`                     | ✅ *       | If providers are reused across features, then an index.ts is useful   |
|                                          |            | Example: `export * from './AuthProvider'`                            |
| `/src/shared`                            | ❌         | Root shared folder acts as container only                             |
| `/src/shared/components`                 | ✅         | For clean imports like `import { Button } from '@/shared/components'` |
| `/src/shared/hooks`                      | ✅         | For centralizing reusable custom hooks                                |
| `/src/shared/types`                      | ✅         | Optional — helpful if you want centralized type exports               |
| `/src/shared/utils`                      | ✅         | To group and export utility functions                                 |
| `/src/shared/assets`                     | ❌         | Static files like images/fonts are not exported via JS                |
| `/src/features`                          | ❌         | Container folder — no exports directly                                |
| `/src/features/auth`                     | ✅         | Acts as public entry point to the feature                             |
| `/src/features/auth/screens`             | ❌         | Screens are usually imported individually                             |
| `/src/features/auth/components`          | ✅ *       | Only if components are reused across features                         |
| `/src/features/auth/hooks`               | ✅ *       | Only if hooks are reused across the app                               |
| `/src/features/auth/api.ts`              | ✅ *       | Export via feature index if reused                                    |
| `/src/features/auth/types.ts`            | ✅ *       | Export via feature index for typing reuse                             |
| `/src/features/auth/store.ts`            | ✅ *       | Store is part of public API of the feature                            |
| `/src/config`                            | ✅         | For centralizing config (e.g. `export * from './env'`)                |
| `/src/index.js`                          | ✅         | Usually re-exports from `App.tsx` or root entry setup                 |

