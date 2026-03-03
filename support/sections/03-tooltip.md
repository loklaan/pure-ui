## Tooltip

A floating label that appears on hover or focus to describe an element. Use it for brief, supplementary text such as icon-button labels, keyboard shortcuts, or status descriptions.

Built on `@base-ui/react/tooltip`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/tooltip"
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

3. Copy the component source into your project at `components/ui/tooltip.tsx`.

### Anatomy

```tsx
import {
  Tooltip,
  TooltipTrigger,
  TooltipPopup,
  TooltipProvider,
} from "@/components/ui/tooltip";

<TooltipProvider>
  <Tooltip>
    <TooltipTrigger>Trigger element</TooltipTrigger>
    <TooltipPopup>Tooltip content</TooltipPopup>
  </Tooltip>
</TooltipProvider>
```

`TooltipProvider` is optional. Use it to wrap multiple tooltips so they share delay settings and group together (once one tooltip opens, adjacent tooltips open instantly).

### Props

#### TooltipProvider

Accepts all props from `@base-ui/react/tooltip` Provider.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| delay | number | 300 | Delay in milliseconds before the tooltip opens |

#### Tooltip

Accepts all props from `@base-ui/react/tooltip` Root, including `open`, `onOpenChange`, and `defaultOpen` for controlled and uncontrolled state.

#### TooltipTrigger

Accepts all props from `@base-ui/react/tooltip` Trigger, including `render`, `delay`, and `closeDelay`.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| delay | number | -- | Override the open delay for this trigger |
| closeDelay | number | -- | Delay in milliseconds before the tooltip closes |

#### TooltipPopup

Accepts all props from `@base-ui/react/tooltip` Popup. Also accepts positioning props that are forwarded to the internal Positioner.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| animationPreset | "none" \| "scale" \| "fade" \| "slideOutside" \| "slideInside" \| "wipe" \| "wipeScale" \| "motion" \| "motionBlur" | "scale" | Controls the open/close animation style |
| transitionPreset | string | "outQuint" | Easing curve for the transition (see transition presets below) |
| reduceMotion | boolean | false | Disables all animations when true |
| showArrow | boolean | false | Renders a CSS pseudo-element arrow pointing toward the trigger |
| side | "top" \| "right" \| "bottom" \| "left" \| "inline-start" \| "inline-end" | "top" | Preferred side for the tooltip |
| sideOffset | number | 4 | Distance in pixels between the tooltip and the trigger |
| align | "start" \| "center" \| "end" | "center" | Alignment along the side axis |
| alignOffset | number | 0 | Offset in pixels for alignment adjustment |

### Animation Presets

Use the `animationPreset` prop on `TooltipPopup` to change the animation style. All side-aware presets adapt their direction based on the `side` prop.

Values: `"none"` | `"scale"` | `"fade"` | `"slideOutside"` | `"slideInside"` | `"wipe"` | `"wipeScale"` | `"motion"` | `"motionBlur"`
Default: `"scale"`

- `"none"` -- no animation.
- `"scale"` -- scales and fades the tooltip in from a smaller size.
- `"fade"` -- fades and subtly scales the tooltip in.
- `"slideOutside"` -- slides the tooltip away from the trigger while fading in.
- `"slideInside"` -- slides the tooltip toward the trigger while fading in.
- `"wipe"` -- reveals the tooltip with a clip-path wipe from the trigger side.
- `"wipeScale"` -- combines the clip-path wipe with a scale effect.
- `"motion"` -- combines 3D rotation, scale, and translation for a dramatic entrance.
- `"motionBlur"` -- same as `"motion"` with an added blur effect.

```tsx
<TooltipPopup animationPreset="fade">Tooltip content</TooltipPopup>
```

### Transition Presets

Use the `transitionPreset` prop on `TooltipPopup` to control the easing curve. The component provides 24 named presets plus `"none"`:

`"inExpo"` | `"outExpo"` | `"inOutExpo"` | `"anticipate"` | `"quickOut"` | `"overshootOut"` | `"swiftOut"` | `"snappyOut"` | `"in"` | `"out"` | `"inOut"` | `"outIn"` | `"inQuad"` | `"outQuad"` | `"inOutQuad"` | `"inCubic"` | `"outCubic"` | `"inOutCubic"` | `"inQuart"` | `"outQuart"` | `"inOutQuart"` | `"inQuint"` | `"outQuint"` | `"inOutQuint"` | `"inCirc"` | `"outCirc"` | `"inOutCirc"` | `"inOutBase"` | `"none"`

Default: `"outQuint"`

```tsx
<TooltipPopup animationPreset="scale" transitionPreset="snappyOut">
  Tooltip content
</TooltipPopup>
```

### Usage

#### Basic

```tsx
import {
  Tooltip,
  TooltipTrigger,
  TooltipPopup,
  TooltipProvider,
} from "@/components/ui/tooltip";

export function TooltipBasic() {
  return (
    <TooltipProvider>
      <Tooltip>
        <TooltipTrigger>
          <p>Hover me</p>
        </TooltipTrigger>
        <TooltipPopup>
          <p>Tooltip Content</p>
        </TooltipPopup>
      </Tooltip>
    </TooltipProvider>
  );
}
```

#### With Arrow

Set `showArrow` on `TooltipPopup` to render an arrow pointing toward the trigger.

```tsx
import {
  Tooltip,
  TooltipTrigger,
  TooltipPopup,
} from "@/components/ui/tooltip";

export function TooltipWithArrow() {
  return (
    <Tooltip>
      <TooltipTrigger>
        <p>Hover me</p>
      </TooltipTrigger>
      <TooltipPopup showArrow>
        <p>Tooltip Content</p>
      </TooltipPopup>
    </Tooltip>
  );
}
```

#### Sides

Use the `side` prop on `TooltipPopup` to control which side the tooltip appears on.

```tsx
import {
  Tooltip,
  TooltipTrigger,
  TooltipPopup,
  TooltipProvider,
} from "@/components/ui/tooltip";

export function TooltipSides() {
  return (
    <TooltipProvider>
      <Tooltip>
        <TooltipTrigger>Top</TooltipTrigger>
        <TooltipPopup side="top">Appears on top</TooltipPopup>
      </Tooltip>
      <Tooltip>
        <TooltipTrigger>Bottom</TooltipTrigger>
        <TooltipPopup side="bottom">Appears on bottom</TooltipPopup>
      </Tooltip>
      <Tooltip>
        <TooltipTrigger>Left</TooltipTrigger>
        <TooltipPopup side="left">Appears on left</TooltipPopup>
      </Tooltip>
      <Tooltip>
        <TooltipTrigger>Right</TooltipTrigger>
        <TooltipPopup side="right">Appears on right</TooltipPopup>
      </Tooltip>
    </TooltipProvider>
  );
}
```

#### Offset

Use the `sideOffset` prop on `TooltipPopup` to change the distance between the tooltip and the trigger.

```tsx
import {
  Tooltip,
  TooltipTrigger,
  TooltipPopup,
  TooltipProvider,
} from "@/components/ui/tooltip";
import { Button } from "@/components/ui/button";

export function TooltipOffset() {
  return (
    <TooltipProvider>
      <Tooltip>
        <TooltipTrigger render={<Button variant="outline" />}>
          Default Offset (4)
        </TooltipTrigger>
        <TooltipPopup sideOffset={4}>
          <p>Tooltip Content</p>
        </TooltipPopup>
      </Tooltip>
      <Tooltip>
        <TooltipTrigger render={<Button variant="outline" />}>
          15 Offset
        </TooltipTrigger>
        <TooltipPopup sideOffset={15}>
          <p>Tooltip Content</p>
        </TooltipPopup>
      </Tooltip>
    </TooltipProvider>
  );
}
```

#### Controlled State

Use `open` and `onOpenChange` on `Tooltip` to control visibility externally.

```tsx
import { useState } from "react";
import {
  Tooltip,
  TooltipTrigger,
  TooltipPopup,
  TooltipProvider,
} from "@/components/ui/tooltip";

export function TooltipControlled() {
  const [open, setOpen] = useState(false);

  return (
    <TooltipProvider>
      <Tooltip open={open} onOpenChange={setOpen}>
        <TooltipTrigger>
          <p>Hover me</p>
        </TooltipTrigger>
        <TooltipPopup>
          <p>Tooltip Content</p>
        </TooltipPopup>
      </Tooltip>
    </TooltipProvider>
  );
}
```

#### Delay

Control the open and close delay using `delay` and `closeDelay` props on `TooltipTrigger`.

```tsx
import {
  Tooltip,
  TooltipTrigger,
  TooltipPopup,
  TooltipProvider,
} from "@/components/ui/tooltip";
import { Button } from "@/components/ui/button";

export function TooltipDelay() {
  return (
    <TooltipProvider>
      <Tooltip>
        <TooltipTrigger
          delay={1000}
          render={<Button variant="outline" />}
        >
          Delay Open (1000ms)
        </TooltipTrigger>
        <TooltipPopup>
          <p>Tooltip Content</p>
        </TooltipPopup>
      </Tooltip>
    </TooltipProvider>
  );
}
```

#### Custom Content

Place any content inside `TooltipPopup`, including structured layouts.

```tsx
import {
  Tooltip,
  TooltipTrigger,
  TooltipPopup,
  TooltipProvider,
} from "@/components/ui/tooltip";

export function TooltipCustomContent() {
  return (
    <TooltipProvider>
      <Tooltip>
        <TooltipTrigger>
          <p>Hover me</p>
        </TooltipTrigger>
        <TooltipPopup>
          <div className="px-1 py-2">
            <div className="text-sm font-bold">Custom Content</div>
            <div className="text-xs">This is a custom tooltip content</div>
          </div>
        </TooltipPopup>
      </Tooltip>
    </TooltipProvider>
  );
}
```

#### Grouping Tooltips

Wrap multiple tooltips in `TooltipProvider` so they share delay settings. Once one tooltip in the group becomes visible, adjacent tooltips open instantly.

```tsx
import {
  Tooltip,
  TooltipTrigger,
  TooltipPopup,
  TooltipProvider,
} from "@/components/ui/tooltip";
import { Button } from "@/components/ui/button";

export function TooltipGrouped() {
  return (
    <TooltipProvider>
      <Tooltip>
        <TooltipTrigger render={<Button variant="outline" />}>
          Tooltip 1
        </TooltipTrigger>
        <TooltipPopup>Content 1</TooltipPopup>
      </Tooltip>
      <Tooltip>
        <TooltipTrigger render={<Button variant="outline" />}>
          Tooltip 2
        </TooltipTrigger>
        <TooltipPopup>Content 2</TooltipPopup>
      </Tooltip>
    </TooltipProvider>
  );
}
```

#### Animation Preset Example

```tsx
import {
  Tooltip,
  TooltipTrigger,
  TooltipPopup,
  TooltipProvider,
} from "@/components/ui/tooltip";

export function TooltipMotionBlur() {
  return (
    <TooltipProvider>
      <Tooltip>
        <TooltipTrigger>
          <p>Hover me</p>
        </TooltipTrigger>
        <TooltipPopup animationPreset="motionBlur">
          <p>Tooltip Content</p>
        </TooltipPopup>
      </Tooltip>
    </TooltipProvider>
  );
}
```

### Notes

- The `render` prop on `TooltipTrigger` renders the trigger as a different element. This is Base UI's equivalent of Radix UI's `asChild`. For example, `render={<Button variant="outline" />}` renders the trigger as a Button.
- `TooltipPopup` internally wraps content in a Portal and Positioner. You do not need to add these manually.
- The arrow rendered by `showArrow` is a CSS pseudo-element, not a separate component. It is hidden for `inline-start` and `inline-end` sides.
- The `data-instant` attribute on `TooltipPopup` disables transition duration, used internally for instant group tooltips.
- `className` on all sub-components is merged via `cn()`.
