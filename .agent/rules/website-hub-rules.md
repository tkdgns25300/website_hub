# 📏 Website Hub Project Rules

This document outlines the coding standards, architectural guidelines, and best practices for the **Website Hub** project. All code must adhere to these rules to ensure maintainability, readability, and a premium quality output.

---

## 1. General Philosophy
- **Readability First**: Write code that is easy to understand. Favor descriptive variable names over clever one-liners.
- **English Only**: All code (variables, functions, comments, commits) must be written in English.
- **Simplicity**: Do not over-engineer. Use the simplest solution that fully solves the problem.
- **Consistency**: Follow the established patterns for file structure, naming, and styling.

## 2. Tech Stack & Architecture
- **Framework**: Next.js 14+ (App Router).
- **Language**: TypeScript (Strict Mode).
- **Styling**: Tailwind CSS (Utility-first).
- **Directory Strategy**: `src/` directory architecture.
- **Data Source**: Local File System (JSON/TS) - No external DB complexity.
- **State Management**: React Context/Hooks (Avoid Redux/Zustand unless absolutely necessary).

## 3. TypeScript Best Practices
- **No `any`**: Explicitly define types. Use `unknown` if strict typing is impossible, but avoid it if you can.
- **Interfaces over Types**: Use `interface` for defining object shapes (props, state, data models) to allow for better error messages and extensibility.
- **Explicit Returns**: Explicitly define return types for all complex functions, especially API handlers and hooks.
- **Type Safety**: Ensure strict null checks are enabled. Handle `undefined` and `null` gracefully.

## 4. Next.js App Router Guidelines
- **Server Components by Default**: All components should be Server Components (`.tsx`) unless they require interactivity (hooks, event listeners).
- **Client Components**: Add `"use client";` at the very top of the file only when necessary.
- **Directory Structure (Src Pattern)**:
  - `src/app/`: Routes and pages.
  - `src/components/`: Reusable UI components.
  - `src/lib/`: Utility functions, data fetching logic, types, and constants.
  - `src/data/`: Local data files (e.g., `db.ts`, `websites.json`).
  - `public/`: Static assets (images, fonts).
- **Data Fetching**: Fetch data directly in Server Components where possible for better performance.

## 5. Coding Standards
- **Functional Programming**: Use functional components and hooks. Avoid class components.
- **Naming Conventions**:
  - **Components**: PascalCase (e.g., `WebsiteCard.tsx`)
  - **Functions/Variables**: camelCase (e.g., `getWebsites`, `isActive`)
  - **Constants**: UPPER_SNAKE_CASE (e.g., `MAX_ITEMS_PER_PAGE`)
  - **Files**: kebab-case or PascalCase (match export). *Recommendation: PascalCase for components, kebab-case for utilities.*
- **Clean Code**:
  - **Destructuring**: Destructure props and objects for cleaner access.
  - **Early Returns**: Use early returns (guard clauses) to reduce nesting.
  - **DRY (Don't Repeat Yourself)**: Extract repeated logic into custom hooks or utility functions.

## 6. Styling (Tailwind CSS)
- **Utility-First**: Use Tailwind utility classes directly in `className`. Avoid creating separate CSS files unless absolutely necessary.
- **Configuration**: Define custom colors, fonts, and breakpoints in `tailwind.config.ts`, not in arbitrary values (e.g., avoid `text-[#123456]`, use `text-primary`).
- **Conditionals**: Use template literals or libraries like `clsx` / `tailwind-merge` for conditional class names.
  - Example: `` `p-4 rounded ${isActive ? 'bg-blue-500' : 'bg-gray-200'}` ``
- **Readability**: Group related classes logically (Layout -> Box Model -> Typography -> Visuals).
- **Responsiveness**: Use mobile-first prefixes (e.g., `w-full md:w-1/2`).

## 7. Local Data Management
- **Immutability**: When reading/writing local files (JSON/TS), treat data as immutable.
- **Validation**: Validate data structure when reading from files to prevent runtime errors.
- **Image Handling**: Store static images in `public/` and reference them via relative paths in your data files.

## 8. Git & Commits
- **Conventional Commits**:
  - `feat`: New feature
  - `fix`: Bug fix
  - `docs`: Documentation only
  - `style`: Formatting, missing semi colons, etc; no code change
  - `refactor`: Refactoring production code
  - `chore`: Build process, auxiliary tools
- **Message Format**: `type(scope): subject` (e.g., `feat(card): add hover animation`)
