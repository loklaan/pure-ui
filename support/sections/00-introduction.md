## Introduction

Pure UI is a collection of accessible, animated React components distributed as a shadcn registry. It builds on Base UI headless primitives (`@base-ui/react`), adding opinionated styling with Tailwind CSS v4, variant management with `tailwind-variants`, and animations with Motion (`motion`). Components are installed into your project as source code, giving you full control over markup, styling, and behaviour.

### Tech Stack

- **Base UI** (`@base-ui/react`) -- Headless, accessible React primitives. Every Pure UI component that wraps a primitive delegates accessibility, keyboard handling, and ARIA attributes to Base UI.
- **Tailwind CSS v4** -- Utility-first CSS framework. Pure UI requires Tailwind CSS v4 and uses its CSS variable theming system (`@theme inline`).
- **tailwind-variants** (`tailwind-variants`) -- Type-safe variant API for Tailwind classes. Components define their visual variants (size, colour, radius, etc.) through `tv()` configs and expose them as props.
- **Motion** (`motion`) -- Animation library used by components that need enter/exit or layout animations (e.g. Accordion, Dialog, Toast).
- **clsx** + **tailwind-merge** -- Combined in the `cn()` utility (see below) for conditional class merging without conflicts.
- **tw-animate-css** -- CSS animation presets used by the theme layer.

### The shadcn Registry Model

Pure UI is not installed as an npm package. It uses the shadcn registry pattern:

1. The library publishes a `registry.json` manifest describing every component, its dependencies, and its source files.
2. You add components to your project using the shadcn CLI. The CLI fetches the component source and copies it into your codebase (by default at `components/ui/`).
3. Because the code lives in your project, you can modify any component freely.

The registry URL is `https://pure.kam-ui.com/r/`. To add a component:

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/button"
```

The CLI resolves dependencies automatically. For example, adding `button-group` also installs `separator` because the registry declares it as a dependency.

### The `cn()` Utility

Every component imports a `cn()` function from `@/lib/classes`. It combines `clsx` (conditional class joining) with `tailwind-merge` (intelligent deduplication of Tailwind classes). This allows user-supplied `className` props to override component defaults without conflicts.

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

The `cn()` utility is installed automatically when you add your first component via the CLI. For manual installation, create this file at `lib/classes.ts` (or wherever your project resolves `@/lib/classes`).

### How Components Are Composed

Pure UI components follow two patterns depending on complexity:

#### Single-Part Components

Components like Button, Input, and Badge are single elements. They wrap a Base UI primitive (or a plain HTML element), apply variant styles via `tailwind-variants`, and forward all remaining props.

```tsx
import { Button } from "@/components/ui/button";

<Button variant="outline" size="sm">Save</Button>
```

Variant props (like `variant`, `size`, `radius`) map directly to the `tv()` config defined in the component source. The component merges variant classes with any user-provided `className` through `cn()`.

#### Multi-Part Components

Components like Accordion, Dialog, and Select are composed from multiple sub-components that must be nested in a specific tree structure. Each sub-component wraps a corresponding Base UI primitive.

```tsx
import {
  Accordion,
  AccordionItem,
  AccordionTrigger,
  AccordionPanel,
} from "@/components/ui/accordion";

<Accordion>
  <AccordionItem value="item-1">
    <AccordionTrigger>Section title</AccordionTrigger>
    <AccordionPanel>Section content</AccordionPanel>
  </AccordionItem>
</Accordion>
```

Parent components pass configuration to children through React context. For instance, the `Accordion` root provides animation and variant settings that `AccordionPanel` and `AccordionTrigger` consume internally.

### Migration from Radix UI

Pure UI uses Base UI, not Radix UI. The main API difference: Base UI uses a `render` prop where Radix uses `asChild`. If you are migrating from shadcn/ui or Radix-based components, replace `asChild` with the `render` prop pattern. Individual component sections note specific migration details where applicable.

### Component List

The registry contains 30 UI components: Accordion, Avatar, Badge, Button, Button Group, Calendar, Card, Checkbox, Collapsible, Combobox, Dialog, Input, Input Group, Input OTP, Kbd, Label, Menu, Number Field, Popover, Radio Group, Scroll Area, Select, Separator, Sheet, Spinner, Switch, Tabs, Textarea, Toast, and Tooltip.

Each component is documented in its own section below with installation instructions, anatomy, props, and usage examples.
