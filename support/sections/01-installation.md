## Installation

Pure UI requires **React 19** and **Tailwind CSS v4**. Components are distributed as a shadcn-compatible registry. You install them with the shadcn CLI, which copies component source files into your project.

### Prerequisites

- React 19
- Tailwind CSS v4
- TypeScript (recommended)
- A path alias configured so `@/` resolves to your source root

### Adding Components

Once your project is set up (see framework guides below), add any component with the shadcn CLI:

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/button"
```

Replace `button` with the component name. The CLI downloads the component source and its dependencies into your project.

Import the component from the local path:

```tsx
import { Button } from "@/components/ui/button";
```

**Note:** The shadcn init step installs `class-variance-authority` as a dependency. Pure UI uses `tailwind-variants` instead, so you can remove `class-variance-authority` if no other part of your project needs it.

---

### Framework Setup

Each framework requires slightly different scaffolding. All paths converge on the same result: a Tailwind CSS v4 project with the shadcn CLI configured and the Pure UI CSS variables in your global stylesheet.

#### Next.js

1. Create a project:

```bash
npx create-next-app@latest my-app
pnpm dlx create-next-app@latest my-app
yarn create-next-app@latest my-app
bunx --bun create-next-app@latest my-app
```

Select TypeScript, Tailwind CSS, the `src/` directory, and App Router when prompted.

2. Replace the contents of `src/app/globals.css` with the CSS variables block (see the full block in the "CSS Variables" section below).

3. Run the shadcn init command:

```bash
npx shadcn@latest init
pnpm dlx shadcn@latest init
yarn shadcn@latest init
bunx --bun shadcn@latest init
```

4. Add components:

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/separator"
```

```tsx
import { Separator } from "@/components/ui/separator";

export default function Home() {
  return (
    <div>
      <Separator />
    </div>
  );
}
```

#### Vite

1. Create a project (select the React + TypeScript template):

```bash
npm create vite@latest
pnpm create vite@latest
yarn create vite@latest
bun create vite@latest
```

2. Install Tailwind CSS and the Vite plugin:

```bash
npm install tailwindcss @tailwindcss/vite
pnpm add tailwindcss @tailwindcss/vite
yarn add tailwindcss @tailwindcss/vite
bun add tailwindcss @tailwindcss/vite
```

3. Replace `src/index.css` with:

```css
@import "tailwindcss";
```

4. Add `baseUrl` and `paths` to both `tsconfig.json` and `tsconfig.app.json`:

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

5. Install node types and update `vite.config.ts`:

```bash
npm install -D @types/node
pnpm add -D @types/node
yarn add -D @types/node
bun add -D @types/node
```

```ts
import path from "path";
import tailwindcss from "@tailwindcss/vite";
import react from "@vitejs/plugin-react";
import { defineConfig } from "vite";

export default defineConfig({
  plugins: [react(), tailwindcss()],
  resolve: {
    alias: {
      "@": path.resolve(__dirname, "./src"),
    },
  },
});
```

6. Run shadcn init, then add components as shown in the Next.js section.

#### React Router

1. Create a project:

```bash
npx create-react-router@latest my-app
pnpm dlx create-react-router@latest my-app
yarn create-react-router@latest my-app
bunx --bun create-react-router@latest my-app
```

2. Run shadcn init:

```bash
npx shadcn@latest init
pnpm dlx shadcn@latest init
yarn shadcn@latest init
bunx --bun shadcn@latest init
```

3. Add components. React Router uses the `~/` import alias by default:

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/button"
```

```tsx
import { Button } from "~/components/ui/button";

export default function Home() {
  return (
    <div className="flex min-h-svh flex-col items-center justify-center">
      <Button>Click me</Button>
    </div>
  );
}
```

#### TanStack Start

Setup instructions are not yet available. Follow the manual installation guide below.

#### TanStack Router

Setup instructions are not yet available. Follow the manual installation guide below.

#### Manual Installation

Use this approach when your framework is not listed above or when you need full control over the setup.

1. Install Tailwind CSS v4 following the official Tailwind CSS documentation for your build tool.

2. Install core dependencies:

```bash
npm install @base-ui/react motion clsx tailwind-merge tailwind-variants
pnpm add @base-ui/react motion clsx tailwind-merge tailwind-variants
yarn add @base-ui/react motion clsx tailwind-merge tailwind-variants
bun add @base-ui/react motion clsx tailwind-merge tailwind-variants
```

3. Configure path aliases in `tsconfig.json`:

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./*"]
    }
  }
}
```

4. Add the CSS variables block to your global stylesheet (see the full block in the "CSS Variables" section below).

5. Create the `cn` helper at `lib/classes.ts`:

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

6. Create `components.json` in the project root:

```json
{
  "$schema": "https://ui.shadcn.com/schema.json",
  "style": "new-york",
  "rsc": false,
  "tsx": true,
  "tailwind": {
    "config": "",
    "css": "src/styles/globals.css",
    "baseColor": "neutral",
    "cssVariables": true,
    "prefix": ""
  },
  "aliases": {
    "components": "@/components",
    "utils": "@/lib/utils",
    "ui": "@/components/ui",
    "lib": "@/lib",
    "hooks": "@/hooks"
  },
  "iconLibrary": "lucide",
  "registries": {
    "@pureui": "https://pure.kam-ui.com/r/{name}.json"
  }
}
```

7. Add components:

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/separator"
```

---

### The `cn()` Utility

Every Pure UI component uses the `cn()` helper to merge class names. It combines `clsx` (conditional class joining) with `tailwind-merge` (deduplication of conflicting Tailwind utilities).

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

Place this file at `lib/classes.ts` (or wherever your `components.json` aliases point). The shadcn CLI creates a similar utility during init, but Pure UI imports from `@/lib/classes` rather than `@/lib/utils`.

---

### The `tw-animate-css` Dependency

Pure UI uses the `tw-animate-css` package for animation utilities. It is imported at the top of the global stylesheet alongside Tailwind CSS:

```css
@import "tailwindcss";
@import "tw-animate-css";
```

Install it as a dependency if it is not already present:

```bash
npm install tw-animate-css
pnpm add tw-animate-css
yarn add tw-animate-css
bun add tw-animate-css
```

---

### CSS Variables

Add the following to your global stylesheet (e.g., `app/globals.css` for Next.js, `src/index.css` for Vite). This block defines the full design token system used by all components. Colors use the OKLCh color space.

```css
@import "tailwindcss";
@import "tw-animate-css";

@custom-variant dark (&:is(.dark *));

:root {
  --radius: 0.625rem;
  --background: oklch(1 0 0);
  --foreground: oklch(0.21 0.006 285.885);
  --card: oklch(1 0 0);
  --card-foreground: oklch(0.21 0.006 285.885);
  --popover: oklch(1 0 0);
  --popover-foreground: oklch(0.21 0.006 285.885);
  --primary: oklch(0.274 0.006 286.033);
  --primary-foreground: oklch(0.985 0 0);
  --secondary: oklch(0 0 0 / 4%);
  --secondary-foreground: oklch(0.21 0.006 285.885);
  --muted: oklch(0 0 0 / 4%);
  --muted-foreground: oklch(0.442 0.017 285.786);
  --accent: oklch(0 0 0 / 4%);
  --accent-foreground: oklch(0.21 0.006 285.885);
  --destructive: oklch(0.637 0.237 25.331);
  --destructive-foreground: oklch(0.505 0.213 27.518);
  --info: oklch(0.623 0.214 259.815);
  --info-foreground: oklch(0.488 0.243 264.376);
  --success: oklch(0.696 0.17 162.48);
  --success-foreground: oklch(0.508 0.118 165.612);
  --warning: oklch(0.769 0.188 70.08);
  --warning-foreground: oklch(0.555 0.163 48.998);
  --border: oklch(0 0 0 / 10%);
  --input: oklch(0 0 0 / 10%);
  --ring: oklch(0.705 0.015 286.067);
  --chart-1: oklch(0.646 0.222 41.116);
  --chart-2: oklch(0.6 0.118 184.704);
  --chart-3: oklch(0.398 0.07 227.392);
  --chart-4: oklch(0.828 0.189 84.429);
  --chart-5: oklch(0.769 0.188 70.08);
  --sidebar: oklch(0.985 0 0);
  --sidebar-foreground: oklch(0.21 0.006 285.885);
  --sidebar-primary: oklch(0.274 0.006 286.033);
  --sidebar-primary-foreground: oklch(0.985 0 0);
  --sidebar-accent: oklch(0 0 0 / 4%);
  --sidebar-accent-foreground: oklch(0.21 0.006 285.885);
  --sidebar-border: oklch(0 0 0 / 10%);
  --sidebar-ring: oklch(0.705 0.015 286.067);
}

.dark {
  --background: oklch(0.145 0 0);
  --foreground: oklch(0.985 0 0);
  --card: oklch(0.145 0 0);
  --card-foreground: oklch(0.985 0 0);
  --popover: oklch(0.145 0 0);
  --popover-foreground: oklch(0.985 0 0);
  --primary: oklch(0.985 0 0);
  --primary-foreground: oklch(0.205 0 0);
  --secondary: oklch(0.269 0 0);
  --secondary-foreground: oklch(0.985 0 0);
  --muted: oklch(0.269 0 0);
  --muted-foreground: oklch(0.708 0 0);
  --accent: oklch(0.269 0 0);
  --accent-foreground: oklch(0.985 0 0);
  --destructive: oklch(0.396 0.141 25.723);
  --destructive-foreground: oklch(0.637 0.237 25.331);
  --border: oklch(0.269 0 0);
  --input: oklch(0.269 0 0);
  --ring: oklch(0.439 0 0);
  --chart-1: oklch(0.488 0.243 264.376);
  --chart-2: oklch(0.696 0.17 162.48);
  --chart-3: oklch(0.769 0.188 70.08);
  --chart-4: oklch(0.627 0.265 303.9);
  --chart-5: oklch(0.645 0.246 16.439);
  --sidebar: oklch(0.205 0 0);
  --sidebar-foreground: oklch(0.985 0 0);
  --sidebar-primary: oklch(0.488 0.243 264.376);
  --sidebar-primary-foreground: oklch(0.985 0 0);
  --sidebar-accent: oklch(0.269 0 0);
  --sidebar-accent-foreground: oklch(0.985 0 0);
  --sidebar-border: oklch(0.269 0 0);
  --sidebar-ring: oklch(0.439 0 0);
}

@theme inline {
  --color-background: var(--background);
  --color-foreground: var(--foreground);
  --color-card: var(--card);
  --color-card-foreground: var(--card-foreground);
  --color-popover: var(--popover);
  --color-popover-foreground: var(--popover-foreground);
  --color-primary: var(--primary);
  --color-primary-foreground: var(--primary-foreground);
  --color-secondary: var(--secondary);
  --color-secondary-foreground: var(--secondary-foreground);
  --color-muted: var(--muted);
  --color-muted-foreground: var(--muted-foreground);
  --color-accent: var(--accent);
  --color-accent-foreground: var(--accent-foreground);
  --color-destructive: var(--destructive);
  --color-destructive-foreground: var(--destructive-foreground);
  --color-border: var(--border);
  --color-input: var(--input);
  --color-ring: var(--ring);
  --color-chart-1: var(--chart-1);
  --color-chart-2: var(--chart-2);
  --color-chart-3: var(--chart-3);
  --color-chart-4: var(--chart-4);
  --color-chart-5: var(--chart-5);
  --radius-sm: calc(var(--radius) - 4px);
  --radius-md: calc(var(--radius) - 2px);
  --radius-lg: var(--radius);
  --radius-xl: calc(var(--radius) + 4px);
  --color-sidebar: var(--sidebar);
  --color-sidebar-foreground: var(--sidebar-foreground);
  --color-sidebar-primary: var(--sidebar-primary);
  --color-sidebar-primary-foreground: var(--sidebar-primary-foreground);
  --color-sidebar-accent: var(--sidebar-accent);
  --color-sidebar-accent-foreground: var(--sidebar-accent-foreground);
  --color-sidebar-border: var(--sidebar-border);
  --color-sidebar-ring: var(--sidebar-ring);
}

@layer base {
  * {
    @apply border-border outline-ring/50;
  }
  body {
    @apply bg-background text-foreground;
  }
}
```

The `@theme inline` block maps CSS variables to Tailwind theme tokens, allowing you to use classes like `bg-primary`, `text-muted-foreground`, and `rounded-lg` throughout your components. The `@custom-variant dark` directive enables dark mode via the `.dark` class on a parent element.
