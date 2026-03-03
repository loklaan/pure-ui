## Card

A content container for grouping related information. Card provides six composable sub-components for structuring headers, titles, descriptions, content, and footers.

Card does not wrap any Base UI primitive. It renders plain HTML elements (`div`, `h3`, `p`) styled with Tailwind classes.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/card"
```

#### Manual

1. Install dependencies:

```bash
npm install clsx tailwind-merge
pnpm add clsx tailwind-merge
yarn add clsx tailwind-merge
bun add clsx tailwind-merge
```

2. Add the `cn` utility (if not already present):

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

3. Copy the component source into your project at `components/ui/card.tsx`.

### Anatomy

```tsx
import {
  Card,
  CardHeader,
  CardTitle,
  CardDescription,
  CardContent,
  CardFooter,
} from "@/components/ui/card";

<Card>
  <CardHeader>
    <CardTitle />
    <CardDescription />
  </CardHeader>
  <CardContent />
  <CardFooter />
</Card>
```

All sub-components are optional. Use only the parts you need.

### Props

Card and its sub-components accept standard HTML element props. There are no custom props or variants.

#### Card

Extends `React.ComponentProps<"div">`. Renders a `div` with `data-slot="card"`. The `className` prop is merged via `cn()`.

#### CardHeader

Extends `React.ComponentProps<"div">`. Renders a `div` with `data-slot="card-header"`.

#### CardTitle

Extends `React.ComponentProps<"h3">`. Renders an `h3` with `data-slot="card-title"`.

#### CardDescription

Extends `React.ComponentProps<"p">`. Renders a `p` with `data-slot="card-description"`.

#### CardContent

Extends `React.ComponentProps<"div">`. Renders a `div` with `data-slot="card-content"`.

#### CardFooter

Extends `React.ComponentProps<"div">`. Renders a `div` with `data-slot="card-footer"`.

### Usage

#### Basic

```tsx
import {
  Card,
  CardHeader,
  CardTitle,
  CardDescription,
  CardContent,
  CardFooter,
} from "@/components/ui/card";

export function CardBasicExample() {
  return (
    <Card className="w-full max-w-md">
      <CardHeader>
        <CardTitle>Cursor</CardTitle>
        <CardDescription>Introducing IDE Plugins</CardDescription>
      </CardHeader>
      <CardContent>
        <p>Content goes here.</p>
      </CardContent>
      <CardFooter>
        <span className="text-xs">Check out the latest news</span>
      </CardFooter>
    </Card>
  );
}
```

#### Horizontal Layout

Apply `md:flex-row` to the `Card` to switch from vertical to horizontal layout at medium breakpoints.

```tsx
import {
  Card,
  CardHeader,
  CardTitle,
  CardDescription,
  CardFooter,
} from "@/components/ui/card";
import { Button } from "@/components/ui/button";

export function CardHorizontalExample() {
  return (
    <Card className="w-full items-stretch md:flex-row">
      <img
        alt="Demon Slayer: Kimetsu no Yaiba"
        className="rounded-lg pointer-events-none aspect-square w-full select-none object-cover md:max-w-[146px]"
        loading="lazy"
        src="https://pbs.twimg.com/media/G2co19tXoAAnWT8?format=jpg&name=large"
      />
      <div className="flex flex-1 flex-col gap-3">
        <CardHeader className="gap-1 py-1">
          <CardTitle>Demon Slayer: Kimetsu no Yaiba</CardTitle>
          <CardDescription>
            Follow Tanjiro Kamado as he embarks on a journey to become a demon
            slayer and find a cure for his sister Nezuko.
          </CardDescription>
        </CardHeader>
        <CardFooter className="mt-auto flex w-full flex-row items-center justify-between">
          <div className="flex flex-col">
            <span className="text-foreground text-sm font-medium">
              ★ 8.6/10
            </span>
            <span className="text-muted-foreground text-xs">26 episodes</span>
          </div>
          <Button size="sm">Watch Now</Button>
        </CardFooter>
      </div>
    </Card>
  );
}
```

#### With Image

Place an `img` element as a direct child of `Card` alongside the other sub-components.

```tsx
import { Card, CardFooter } from "@/components/ui/card";

export function CardWithImageExample() {
  return (
    <Card className="w-[220px] gap-2 p-1">
      <img
        alt="Harry Potter Collections"
        className="block aspect-square w-full shrink-0 select-none rounded-lg object-cover"
        loading="lazy"
        src="https://pbs.twimg.com/media/G0uYIupbcAQDPry?format=jpg&name=medium"
      />
      <CardFooter className="flex items-center justify-between px-2 text-sm">
        <span>Harry Potter</span>
        <span className="text-muted-foreground">18 pictures</span>
      </CardFooter>
    </Card>
  );
}
```

#### With Background Image

Use absolute positioning on an `img` to create a background image effect. Card has `overflow-hidden` and `relative` positioning by default, so the image fills the card bounds.

```tsx
import { Card, CardHeader } from "@/components/ui/card";
import { Button } from "@/components/ui/button";

export function CardWithBackgroundImageExample() {
  return (
    <Card className="w-[320px] aspect-square before:absolute before:left-0 before:right-0 before:top-0 before:h-[44px] before:bg-linear-to-b before:from-black/80 before:to-transparent before:z-10">
      <img
        alt="Beautiful aerial view"
        aria-hidden="true"
        className="pointer-events-none absolute inset-0 h-full w-full select-none object-cover"
        src="https://pbs.twimg.com/media/G2gchvnWoAAvkGG?format=jpg&name=large"
      />
      <CardHeader className="z-10 flex flex-row items-center justify-between w-full">
        <div>
          <div className="text-sm font-medium text-white">Naruto</div>
          <div className="text-xs text-white/60">Shonen</div>
        </div>
        <Button size="sm" variant="link" className="text-white">
          Season 2
        </Button>
      </CardHeader>
    </Card>
  );
}
```

### Notes

- Card uses `position: relative` and `overflow: hidden` by default. This makes it straightforward to use absolutely-positioned background images.
- Card renders as a flex column (`flex flex-col`) with `gap-3`. Override the gap with `className` when tighter or wider spacing is needed (e.g. `gap-0`, `gap-2`).
- When used inside a `PopoverPopup` (detected via `data-slot="popover-popup"`), Card automatically removes its background and shadow to integrate with the popover styling.
