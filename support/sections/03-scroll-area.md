## Scroll Area

A native scroll container with custom scrollbars. Provides styled vertical, horizontal, or bidirectional scrolling with optional scroll shadow indicators.

Built on `@base-ui/react/scroll-area`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/scroll-area"
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

3. Copy the component source into your project at `components/ui/scroll-area.tsx`.

### Anatomy

```tsx
import {
  ScrollArea,
  ScrollAreaContent,
  ScrollBar,
} from "@/components/ui/scroll-area";

<ScrollArea>
  <ScrollAreaContent>
    {/* scrollable content */}
  </ScrollAreaContent>
</ScrollArea>
```

`ScrollArea` renders the viewport, scrollbar(s), and corner internally. Use `ScrollAreaContent` to wrap the scrollable content. `ScrollBar` is exported for cases where you need an additional explicit scrollbar (the `ScrollArea` root already renders scrollbars based on the `orientation` prop).

### Props

#### ScrollArea

Accepts all props from `@base-ui/react/scroll-area` (Root).

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| orientation | "horizontal" \| "vertical" \| "both" | "vertical" | Scroll direction; controls which scrollbars are rendered |
| scrollShadow | "vertical" \| "horizontal" \| "both" \| "none" | "none" | Shows gradient shadow indicators at scroll edges |

The `className` prop is applied to the viewport element and merged via `cn()`.

#### ScrollAreaContent

Accepts all props from `@base-ui/react/scroll-area` (Content).

No additional props. The `className` prop is merged via `cn()`.

#### ScrollBar

Accepts all props from `@base-ui/react/scroll-area` (Scrollbar).

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| orientation | "horizontal" \| "vertical" | "vertical" | Direction of the scrollbar |

The `className` prop is merged via `cn()`. The scrollbar auto-hides with an opacity transition and becomes visible on hover or while scrolling.

### Usage

#### Basic

A vertical scroll area with text content. Set a fixed height on `ScrollArea` and wrap content in `ScrollAreaContent`.

```tsx
import {
  ScrollArea,
  ScrollAreaContent,
} from "@/components/ui/scroll-area";

export function ScrollAreaDemo() {
  return (
    <ScrollArea className="h-64 rounded-md max-w-sm w-full">
      <ScrollAreaContent className="flex flex-col gap-4 py-3 pr-6 pl-4 pb-4 text-sm leading-5.5 text-foreground">
        <p>
          Cricket is a bat-and-ball game played between two teams of eleven
          players each. It originated in England and has become incredibly
          popular in countries such as India, Australia, and South Africa.
        </p>
        <p>
          Matches can last between several hours and up to five days, depending
          on the format. Cricket is known for its strategic depth, unique rules,
          and traditions such as tea breaks in longer matches.
        </p>
      </ScrollAreaContent>
    </ScrollArea>
  );
}
```

#### Horizontal

Set `orientation="horizontal"` for horizontal scrolling. Content does not need `ScrollAreaContent` when you manage the layout yourself.

```tsx
import { ScrollArea } from "@/components/ui/scroll-area";

const items = [
  "Item 1", "Item 2", "Item 3", "Item 4", "Item 5",
  "Item 6", "Item 7", "Item 8", "Item 9", "Item 10",
];

export function ScrollAreaHorizontalDemo() {
  return (
    <ScrollArea className="max-w-96 rounded-md border" orientation="horizontal">
      <div className="flex w-max gap-4 p-4">
        {items.map((item) => (
          <div
            className="flex h-20 w-32 shrink-0 items-center justify-center rounded-md bg-muted"
            key={item}
          >
            <span className="font-medium text-center text-sm">{item}</span>
          </div>
        ))}
      </div>
    </ScrollArea>
  );
}
```

#### Both Directions

Set `orientation="both"` to enable scrolling in both directions. This renders both a vertical and a horizontal scrollbar plus a corner element.

```tsx
import {
  ScrollArea,
  ScrollAreaContent,
} from "@/components/ui/scroll-area";

export function ScrollAreaBothScrollDemo() {
  return (
    <ScrollArea className="max-w-96 h-96 rounded-md border" orientation="both">
      <ScrollAreaContent className="p-5">
        <ul className="m-0 grid list-none grid-cols-[repeat(10,6.25rem)] grid-rows-[repeat(10,6.25rem)] gap-3 p-0">
          {Array.from({ length: 100 }, (_, i) => (
            <li
              key={i}
              className="flex items-center justify-center rounded-lg bg-muted text-sm font-medium text-muted-foreground"
            >
              {i + 1}
            </li>
          ))}
        </ul>
      </ScrollAreaContent>
    </ScrollArea>
  );
}
```

#### Vertical Scroll Shadow

Scroll shadows are gradient overlays at the scroll edges that indicate more content is available. Set `scrollShadow="vertical"` to show top and bottom shadows.

```tsx
import {
  ScrollArea,
  ScrollAreaContent,
} from "@/components/ui/scroll-area";

export function ScrollAreaVerticalShadowDemo() {
  return (
    <ScrollArea
      className="h-64 rounded-md max-w-sm w-full"
      scrollShadow="vertical"
    >
      <ScrollAreaContent className="flex flex-col gap-4 py-3 pr-6 pl-4 pb-4 text-sm leading-5.5 text-foreground">
        <p>Content that scrolls vertically with shadow indicators...</p>
      </ScrollAreaContent>
    </ScrollArea>
  );
}
```

#### Horizontal Scroll Shadow

Set `scrollShadow="horizontal"` for left and right edge shadows.

```tsx
import {
  ScrollArea,
  ScrollAreaContent,
} from "@/components/ui/scroll-area";

export function ScrollAreaHorizontalShadowDemo() {
  return (
    <ScrollArea
      className="max-w-96 w-full rounded-md border whitespace-nowrap"
      scrollShadow="horizontal"
    >
      <ScrollAreaContent className="flex w-max space-x-4 p-4">
        {/* horizontally scrolling content */}
      </ScrollAreaContent>
    </ScrollArea>
  );
}
```

#### Both Scroll Shadows

Set `scrollShadow="both"` together with `orientation="both"` to show shadows on all four edges.

```tsx
import {
  ScrollArea,
  ScrollAreaContent,
} from "@/components/ui/scroll-area";

export function ScrollAreaBothShadowDemo() {
  return (
    <ScrollArea
      className="max-w-96 h-96 rounded-md border"
      orientation="both"
      scrollShadow="both"
    >
      <ScrollAreaContent className="p-5">
        {/* content that overflows in both directions */}
      </ScrollAreaContent>
    </ScrollArea>
  );
}
```

### Notes

- The scrollbar is hidden by default and appears with an opacity transition on hover or while actively scrolling. It auto-hides after scrolling stops.
- Scroll shadows use CSS gradient pseudo-elements whose size is driven by `--scroll-area-overflow-*` CSS variables provided by Base UI. The shadows automatically appear and disappear as content overflows in each direction.
- The viewport has built-in focus-visible ring styling for keyboard accessibility.
- `ScrollArea` renders a border on its viewport by default. Override or remove it via `className`.
