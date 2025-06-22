# Frontend Guidelines

## 1. Design Principles

- Simplicity and clarity
- Consistency with shadcn/ui conventions
- Mobile-first and responsive design
- Accessibility-first approach (WCAG AA)

## 2. Component Architecture

- **Atomic Design:** Organize UI into Atoms (e.g., buttons, inputs), Molecules (e.g., form fields), and Organisms (e.g., headers, footers).
- **File & Folder Structure:** Group files by feature or domain; use top-level folders like `components/`, `screens/`, `hooks/`, and `utils/`, with folder and file names in kebab-case (e.g., `note-editor.tsx`).
- **Naming Conventions:** File names in kebab-case (e.g., `note-editor.tsx`); component, hook, and variable names in PascalCase (e.g., `NoteEditor`).
- Encapsulation and reusability guidelines

## 3. Styling & Theming

- Tailwind CSS: use utility classes and custom tokens
- Theme configuration (dark/light modes) via CSS variables
- Integration with shadcn/ui components and overriding styles
- Responsive breakpoints guidelines

## 4. State Management & Data Fetching

- Global state: React Context for UI state
- Server state: TanStack Query patterns (queries, mutations, caching)
- Optimistic updates and error handling

## 5. PWA & Offline Support

- Service worker registration and caching strategies
- Offline note storage and sync patterns
- Handling AI feature fallbacks when offline

## 6. Accessibility

- Semantic HTML usage
- Keyboard navigation and focus management
- ARIA attributes and roles guidelines
- Color contrast checks and tooling

## 7. Performance

- Code-splitting and dynamic imports
- Image optimization and lazy loading
- Minimizing bundle size (analyze and monitor)

## 8. Testing & Quality

- Unit testing (optional MVP): Vitest + React Testing Library
- End-to-end testing suggestions (Cypress, Playwright)
- Accessibility testing (axe-core)
- Linting (ESLint rules) and formatting (Prettier)

## 9. CI/CD & Developer Workflow

- Pre-commit hooks (lint-staged) and commit message conventions
- Branching model and PR review checklist
- Local development scripts and debug tips

## 10. Code Examples & Snippets

- Common patterns (custom hooks, API calls, error boundary)
- Example of using autocomplete hook
- Chat panel integration snippet
