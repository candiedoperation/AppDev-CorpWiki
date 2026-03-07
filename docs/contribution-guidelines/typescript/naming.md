---
title: Naming
sidebar_position: 2
---

# Naming

## File & Folder Naming rules
- **Components (`.tsx`)** → `UpperCamelCase`  
  *Example:* `UserProfile.tsx`

- **Custom Hooks** → `camelCase` prefixed with `use`  
  *Example:* `useAuth.ts`, `useTabs.ts`

- **Other files & folders** → `kebab-case`  
  *Example:* `auth-service.ts`, `api-client.ts`

## Identifier Rules

- `UpperCamelCase` → Classes, Interfaces, Types, Enums, React components  
  *Example:* `MapPage`, `AlertProps`, `GeoJsonObject`

- `camelCase` → Variables, Parameters, Functions, Methods, Props  
  *Example:* `onConfirm`, `isEditable`

**Note:** since python will use snake_case, it is okay to use snake_case when referring to keys
directly from a request to the backend. However this is only if it directly used, if there is
some data transformation involved, always switch to lowerCamelCase.

## Abbreviations
Always treat abbreviations like words
```typescript
let loadHttpUrl = 'url here' // good!
let loadHTTPURL = 'url here' // bad
```
