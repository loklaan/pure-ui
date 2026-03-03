## Badge

Displays a short label or status indicator. Use badges to tag items, show counts, or highlight status inline with other content.

Uses `@base-ui/react/merge-props` and `@base-ui/react/use-render` for polymorphic rendering.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/badge"
```

#### Manual

1. Install dependencies:

```bash
npm install tailwind-variants clsx tailwind-merge @base-ui/react
pnpm add tailwind-variants clsx tailwind-merge @base-ui/react
yarn add tailwind-variants clsx tailwind-merge @base-ui/react
bun add tailwind-variants clsx tailwind-merge @base-ui/react
```

2. Add the `cn` utility (if not already present):

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

3. Copy the component source into your project at `components/ui/badge.tsx`.

### Anatomy

Badge is a single-part component. It renders a `span` by default.

```tsx
import { Badge } from "@/components/ui/badge";

<Badge>Label</Badge>
```

### Props

#### Badge

Accepts all props from `@base-ui/react/use-render` `ComponentProps<"span">`, including the `render` prop for polymorphic rendering.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| shape | "simple" \| "bar" \| "dot" | "simple" | Controls the badge shape |
| variant | "default" \| "destructive" \| "secondary" \| "outline" | "default" | Controls the colour scheme |
| render | React.ReactElement or function | -- | Renders the badge as a different element |

### Exported Utilities

- `badgeVariants` -- the `tailwind-variants` config object. Import it when you need to apply badge styles outside the `Badge` component (e.g. on a link or button).

```tsx
import { badgeVariants } from "@/components/ui/badge";
```

### Variants

#### shape

Values: `"simple"` | `"bar"` | `"dot"`
Default: `"simple"`

- `"simple"` -- pill-shaped badge with a border.
- `"bar"` -- rounded badge with a vertical bar indicator on the left side.
- `"dot"` -- rounded badge with a circular dot indicator on the left side.

```tsx
<Badge shape="simple">Simple</Badge>
<Badge shape="bar">Bar</Badge>
<Badge shape="dot">Dot</Badge>
```

#### variant

Values: `"default"` | `"destructive"` | `"secondary"` | `"outline"`
Default: `"default"`

```tsx
<Badge variant="default">Default</Badge>
<Badge variant="destructive">Destructive</Badge>
<Badge variant="secondary">Secondary</Badge>
<Badge variant="outline">Outline</Badge>
```

Shapes and variants combine through compound variants. Every shape supports all four variant values.

### Usage

#### Basic

```tsx
import { Badge } from "@/components/ui/badge";

export function BadgeBasic() {
  return <Badge>Badge</Badge>;
}
```

#### Shapes

Use the `shape` prop to control the badge shape.

```tsx
import { Badge } from "@/components/ui/badge";

export function BadgeShapes() {
  return (
    <div className="flex flex-wrap items-center gap-2">
      <Badge shape="simple">Simple</Badge>
      <Badge shape="bar">Bar</Badge>
      <Badge shape="dot">Dot</Badge>
    </div>
  );
}
```

#### Variant Colours

Use the `variant` prop to change the colour scheme.

```tsx
import { Badge } from "@/components/ui/badge";

export function BadgeVariants() {
  return (
    <div className="flex flex-wrap items-center gap-2">
      <Badge variant="default" shape="bar">Default</Badge>
      <Badge variant="destructive" shape="bar">Destructive</Badge>
      <Badge variant="secondary" shape="bar">Secondary</Badge>
      <Badge variant="outline" shape="bar">Outline</Badge>
    </div>
  );
}
```

#### Custom Styling

Override badge colours by passing Tailwind classes through `className`. The `cn()` utility merges your classes with the variant defaults.

```tsx
import { Badge } from "@/components/ui/badge";

export function BadgeCustom() {
  return (
    <Badge
      className="dark:bg-[#1c120d] bg-[#f1763a] border border-[#f1763a] dark:text-[#f1763a] text-[#1c120d]"
      shape="bar"
    >
      Custom
    </Badge>
  );
}
```

#### Rendering as a Link

Use the `render` prop to render the badge as a different element. This is Base UI's equivalent of Radix's `asChild`.

```tsx
import { Badge } from "@/components/ui/badge";

export function BadgeAsLink() {
  return (
    <Badge render={<a href="/status" />}>
      Status
    </Badge>
  );
}
```

When rendered as an anchor (`<a>`), hover styles are automatically applied through the `[a&]:hover:` compound variants.

### Notes

- The `render` prop from Base UI replaces Radix UI's `asChild` pattern. Pass a React element (e.g. `render={<a href="/" />}`) to change the rendered element while keeping badge styling.
- SVG icons placed as children are automatically sized to `0.75rem` (12px) via the `[&>svg]:size-3` utility.
