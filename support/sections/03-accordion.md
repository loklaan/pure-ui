## Accordion

A collapsible component that displays a list of sections which can expand and collapse to reveal content. Each section has a trigger that toggles the visibility of its associated panel.

Built on `@base-ui/react/accordion`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/accordion"
```

#### Manual

1. Install dependencies:

```bash
npm install clsx tailwind-merge @base-ui/react motion
pnpm add clsx tailwind-merge @base-ui/react motion
yarn add clsx tailwind-merge @base-ui/react motion
bun add clsx tailwind-merge @base-ui/react motion
```

2. Add the `cn` utility (if not already present):

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

3. Copy the component source into your project at `components/ui/accordion.tsx`.

### Anatomy

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

`AccordionHeader` is also exported but is rendered automatically by `AccordionTrigger`. Use it directly only when you need a custom header structure.

### Props

#### Accordion

Root wrapper that manages expand/collapse state and provides context to all child components. Accepts all props from `@base-ui/react/accordion` Root.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| value | number[] | -- | Controlled array of open item indices |
| defaultValue | number[] | [] | Initial open items (uncontrolled) |
| onValueChange | (value: number[], eventDetails: object) => void | -- | Called when the set of open items changes |
| multiple | boolean | false | Allows multiple items to be open at the same time |
| variant | "default" \| "card" \| "swiss" | "default" | Visual style of the accordion |
| animationPreset | "none" \| "fade" \| "scale" \| "slide" \| "perspective" \| "perspectiveBlur" | "fade" | CSS animation applied when panels open and close |
| transitionPreset | string | "outQuad" | Easing curve for the panel animation (see Transition Presets below) |
| reduceMotion | boolean | false | Disables all animations |

#### AccordionItem

Individual collapsible section. Accepts all props from `@base-ui/react/accordion` Item.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| value | string \| number | -- | Unique identifier for the item (required) |
| disabled | boolean | false | Prevents the item from being toggled |
| onOpenChange | (open: boolean, eventDetails: object) => void | -- | Called when the item opens or closes |

#### AccordionHeader

Wrapper for the trigger element. Accepts all props from `@base-ui/react/accordion` Header. Rendered automatically by `AccordionTrigger` -- use directly only when building a custom header layout.

#### AccordionTrigger

Clickable element that toggles its parent `AccordionItem`. Accepts all props from `@base-ui/react/accordion` Trigger.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| icon | (props: { open: boolean }) => ReactNode | -- | Replaces the default plus/minus indicator icon |

#### AccordionPanel

Collapsible content area. Accepts all props from `@base-ui/react/accordion` Panel. Animation and transition settings are inherited from the parent `Accordion` via context.

### Variants

#### variant

Values: `"default"` | `"card"` | `"swiss"`
Default: `"default"`

The `"default"` variant renders items inside a single bordered container with dividers between items. The `"card"` variant renders each item as a separate card with spacing between them. The `"swiss"` variant renders items in a stacked layout where the open item gains a border, rounded corners, and vertical margin separation.

```tsx
<Accordion variant="card">
  <AccordionItem value="item-1">
    <AccordionTrigger>Title</AccordionTrigger>
    <AccordionPanel>Content</AccordionPanel>
  </AccordionItem>
</Accordion>
```

```tsx
<Accordion variant="swiss">
  <AccordionItem value="item-1">
    <AccordionTrigger>Title</AccordionTrigger>
    <AccordionPanel>Content</AccordionPanel>
  </AccordionItem>
</Accordion>
```

#### animationPreset

Values: `"none"` | `"fade"` | `"scale"` | `"slide"` | `"perspective"` | `"perspectiveBlur"`
Default: `"fade"`

Controls the CSS animation applied when accordion panels expand and collapse.

- `"none"` -- no animation
- `"fade"` -- opacity and height transition
- `"scale"` -- scales content from 85% while fading
- `"slide"` -- slides content vertically while fading
- `"perspective"` -- 3D rotation from the top edge
- `"perspectiveBlur"` -- 3D rotation with a blur effect

```tsx
<Accordion animationPreset="perspective">
  ...
</Accordion>
```

#### transitionPreset

24 named easing curves that control the timing of the panel animation. Set on the `Accordion` root.

Default: `"outQuad"`

Available values: `"inExpo"`, `"outExpo"`, `"inOutExpo"`, `"anticipate"`, `"quickOut"`, `"overshootOut"`, `"swiftOut"`, `"snappyOut"`, `"in"`, `"out"`, `"inOut"`, `"outIn"`, `"inQuad"`, `"outQuad"`, `"inOutQuad"`, `"inCubic"`, `"outCubic"`, `"inOutCubic"`, `"inQuart"`, `"outQuart"`, `"inOutQuart"`, `"inQuint"`, `"outQuint"`, `"inOutQuint"`, `"inCirc"`, `"outCirc"`, `"inOutCirc"`, `"inOutBase"`

```tsx
<Accordion transitionPreset="outCubic">
  ...
</Accordion>
```

### Usage

#### Basic

```tsx
import {
  Accordion,
  AccordionItem,
  AccordionTrigger,
  AccordionPanel,
} from "@/components/ui/accordion";

export function AccordionDemo() {
  return (
    <Accordion>
      <AccordionItem value="item-1">
        <AccordionTrigger>What is Next.js?</AccordionTrigger>
        <AccordionPanel>
          <p className="text-sm text-muted-foreground">
            Next.js is a React framework that makes building fast, SEO-friendly
            web apps easy with server rendering and automatic routing.
          </p>
        </AccordionPanel>
      </AccordionItem>
      <AccordionItem value="item-2">
        <AccordionTrigger>Why Use the App Router?</AccordionTrigger>
        <AccordionPanel>
          <p className="text-sm text-muted-foreground">
            The App Router offers layouts, server components, and better
            data-fetching, giving you cleaner structure and faster performance.
          </p>
        </AccordionPanel>
      </AccordionItem>
      <AccordionItem value="item-3">
        <AccordionTrigger>Data Fetching in Next.js</AccordionTrigger>
        <AccordionPanel>
          <p className="text-sm text-muted-foreground">
            Next.js supports static, dynamic, and server-side data fetching,
            letting you choose the best method per component.
          </p>
        </AccordionPanel>
      </AccordionItem>
    </Accordion>
  );
}
```

#### Card Variant

```tsx
import {
  Accordion,
  AccordionItem,
  AccordionTrigger,
  AccordionPanel,
} from "@/components/ui/accordion";

export function AccordionCardVariantDemo() {
  return (
    <Accordion variant="card">
      <AccordionItem value="item-1">
        <AccordionTrigger>What Is Football?</AccordionTrigger>
        <AccordionPanel>
          <p className="text-sm text-muted-foreground">
            A global sport where two teams aim to score goals by getting the
            ball into the opponent's net.
          </p>
        </AccordionPanel>
      </AccordionItem>
      <AccordionItem value="item-2">
        <AccordionTrigger>Duration of the Game</AccordionTrigger>
        <AccordionPanel>
          <p className="text-sm text-muted-foreground">
            A match lasts 90 minutes, divided into two halves, with added
            stoppage time as needed.
          </p>
        </AccordionPanel>
      </AccordionItem>
    </Accordion>
  );
}
```

#### Multiple Expanded

Use the `multiple` prop to allow more than one item to be open simultaneously.

```tsx
import {
  Accordion,
  AccordionItem,
  AccordionTrigger,
  AccordionPanel,
} from "@/components/ui/accordion";

export function AccordionMultipleExpandedDemo() {
  return (
    <Accordion multiple>
      <AccordionItem value="item-1">
        <AccordionTrigger>What Is Cricket?</AccordionTrigger>
        <AccordionPanel>
          <p className="text-sm text-muted-foreground">
            A bat-and-ball sport played between two teams of eleven, focused on
            scoring runs and taking wickets.
          </p>
        </AccordionPanel>
      </AccordionItem>
      <AccordionItem value="item-2">
        <AccordionTrigger>Formats of the Game</AccordionTrigger>
        <AccordionPanel>
          <p className="text-sm text-muted-foreground">
            Cricket has three main formats: Test, ODI, and T20--each with
            different lengths and strategies.
          </p>
        </AccordionPanel>
      </AccordionItem>
    </Accordion>
  );
}
```

#### Custom Indicator

Use the `icon` render prop on `AccordionTrigger` to replace the default plus/minus icon. The function receives `{ open }` to allow open/closed state styling.

```tsx
import { ChevronDown } from "lucide-react";
import {
  Accordion,
  AccordionItem,
  AccordionTrigger,
  AccordionPanel,
} from "@/components/ui/accordion";
import { cn } from "@/lib/classes";

export function AccordionCustomIndicatorDemo() {
  return (
    <Accordion>
      <AccordionItem value="item-1">
        <AccordionTrigger
          icon={({ open }) => (
            <ChevronDown
              className={cn(
                "size-4 transition-transform duration-300 ease",
                open ? "rotate-180" : "rotate-0"
              )}
            />
          )}
        >
          How do I get started?
        </AccordionTrigger>
        <AccordionPanel>
          <p className="text-sm text-muted-foreground">
            Head to the "Quick start" guide in the docs.
          </p>
        </AccordionPanel>
      </AccordionItem>
    </Accordion>
  );
}
```

#### Disabled State

Set `disabled` on individual `AccordionItem` elements to prevent them from being toggled.

```tsx
import {
  Accordion,
  AccordionItem,
  AccordionTrigger,
  AccordionPanel,
} from "@/components/ui/accordion";

export function AccordionDisabledStateDemo() {
  return (
    <Accordion>
      <AccordionItem value="item-1" disabled>
        <AccordionTrigger>This item is disabled</AccordionTrigger>
        <AccordionPanel>
          <p className="text-sm text-muted-foreground">
            This content cannot be revealed.
          </p>
        </AccordionPanel>
      </AccordionItem>
      <AccordionItem value="item-2">
        <AccordionTrigger>This item is enabled</AccordionTrigger>
        <AccordionPanel>
          <p className="text-sm text-muted-foreground">
            This content can be toggled normally.
          </p>
        </AccordionPanel>
      </AccordionItem>
    </Accordion>
  );
}
```

#### Reduce Motion

Set `reduceMotion` on the `Accordion` root to disable all expand/collapse animations.

```tsx
import {
  Accordion,
  AccordionItem,
  AccordionTrigger,
  AccordionPanel,
} from "@/components/ui/accordion";

export function AccordionReduceMotionDemo() {
  return (
    <Accordion reduceMotion>
      <AccordionItem value="item-1">
        <AccordionTrigger>What is Base UI?</AccordionTrigger>
        <AccordionPanel>
          <p className="text-sm text-muted-foreground">
            Base UI is a library of high-quality unstyled React components for
            design systems and web apps.
          </p>
        </AccordionPanel>
      </AccordionItem>
    </Accordion>
  );
}
```

#### Animation Presets

Set `animationPreset` on the `Accordion` root to change the expand/collapse animation style.

```tsx
<Accordion animationPreset="scale">
  ...
</Accordion>
```

```tsx
<Accordion animationPreset="slide">
  ...
</Accordion>
```

```tsx
<Accordion animationPreset="perspective">
  ...
</Accordion>
```

```tsx
<Accordion animationPreset="perspectiveBlur">
  ...
</Accordion>
```

### Notes

- By default, only one item can be open at a time. Set `multiple` on the `Accordion` root to allow simultaneous expansion.
- Each `AccordionItem` requires a unique `value` prop to identify it within the accordion.
- Disabled items render with reduced opacity and prevent pointer interaction.
- The `AccordionTrigger` automatically wraps itself in an `AccordionHeader`. Use `AccordionHeader` directly only when building a custom header layout.
- Base UI's `render` prop is the equivalent of Radix UI's `asChild` for polymorphic rendering.
