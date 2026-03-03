## Spinner

An indicator that shows a loading state. Renders an animated SVG spinner with configurable size.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/spinner"
```

#### Manual

1. Install dependencies:

```bash
npm install tailwind-variants tailwind-merge @base-ui/react clsx
pnpm add tailwind-variants tailwind-merge @base-ui/react clsx
yarn add tailwind-variants tailwind-merge @base-ui/react clsx
bun add tailwind-variants tailwind-merge @base-ui/react clsx
```

2. Add the `cn` utility (if not already present):

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

3. Copy the component source into your project at `components/ui/spinner.tsx`.

### Anatomy

```tsx
import { Spinner } from "@/components/ui/spinner";

<Spinner />
```

The Spinner is a single-part component. It renders a `span` wrapper (with `data-slot="spinner"`) containing an SVG with a rotating animation.

### Props

#### Spinner

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| size | "sm" \| "md" \| "lg" \| "xl" | "md" | Size of the spinner |

The Spinner also accepts all standard SVG element props except `display`, `opacity`, and `color`.

### Variants

#### size

Values: `"sm"` | `"md"` | `"lg"` | `"xl"`
Default: `"md"`

- `"sm"` -- 16px (`size-4`)
- `"md"` -- 24px (`size-6`)
- `"lg"` -- 32px (`size-8`)
- `"xl"` -- 40px (`size-10`)

```tsx
<Spinner size="lg" />
```

### Usage

#### Basic

```tsx
import { Spinner } from "@/components/ui/spinner";

export function SpinnerDemo() {
  return <Spinner />;
}
```

#### Sizes

```tsx
import { Spinner } from "@/components/ui/spinner";

export function SpinnerSizesDemo() {
  return (
    <div className="flex items-center gap-8">
      <Spinner size="sm" />
      <Spinner size="md" />
      <Spinner size="lg" />
      <Spinner size="xl" />
    </div>
  );
}
```

### Notes

- The spinner uses `currentColor` for its fill, so it inherits the text color of its parent. Set a text color utility on the parent or the Spinner itself to change the color.
- When used inside a Toast content slot, the spinner auto-sizes to 20px (`size-5`) regardless of the `size` prop.
- The SVG has `aria-hidden` and `role="presentation"` set. Provide your own accessible label on the surrounding context (e.g. a visually hidden "Loading" text) if the spinner is the only indication of a loading state.
