## Separator

A visual divider that separates content into distinct sections. Use it horizontally between stacked content or vertically between inline items.

Built on `@base-ui/react/separator`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/separator"
```

#### Manual

1. Install dependencies:

```bash
npm install @base-ui/react clsx tailwind-merge
pnpm add @base-ui/react clsx tailwind-merge
yarn add @base-ui/react clsx tailwind-merge
bun add @base-ui/react clsx tailwind-merge
```

2. Add the `cn` utility (if not already present):

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

3. Copy the component source into your project at `components/ui/separator.tsx`.

### Anatomy

```tsx
import { Separator } from "@/components/ui/separator";

<Separator />
```

### Props

#### Separator

Accepts all props from `@base-ui/react/separator`.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| orientation | "horizontal" \| "vertical" | "horizontal" | Direction of the separator line |

The `className` prop is merged via `cn()`.

### Usage

#### Basic

```tsx
import { Separator } from "@/components/ui/separator";

export function SeparatorBasic() {
  return (
    <div>
      <h4 className="text-sm font-medium">Pure UI</h4>
      <p className="text-sm text-muted-foreground">
        Unstyled, accessible primitives for fast product UI and design systems.
      </p>
      <Separator className="my-4" />
      <p className="text-sm">Content below the separator.</p>
    </div>
  );
}
```

#### Vertical

Set `orientation="vertical"` to render a vertical divider between inline items. A vertical separator stretches to fill its parent height by default.

```tsx
import { Separator } from "@/components/ui/separator";

export function SeparatorVertical() {
  return (
    <div className="flex items-center gap-4 text-sm">
      <div>Blog</div>
      <Separator orientation="vertical" />
      <div>Docs</div>
      <Separator orientation="vertical" />
      <div>Source</div>
      <Separator orientation="vertical" />
      <div>Releases</div>
    </div>
  );
}
```

### Notes

- A horizontal separator renders as a full-width 1px line. A vertical separator renders as a 1px-wide line that stretches to the height of its parent container.
- The separator uses the `bg-border` theme colour. Override it by passing a custom `className`.
