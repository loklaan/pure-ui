## Collapsible

An interactive component that expands and collapses a panel. Use it to show and hide content sections such as details, settings, or supplementary information.

Built on `@base-ui/react/collapsible`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/collapsible"
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

3. Copy the component source into your project at `components/ui/collapsible.tsx`.

### Anatomy

```tsx
import {
  Collapsible,
  CollapsibleTrigger,
  CollapsiblePanel,
} from "@/components/ui/collapsible";

<Collapsible>
  <CollapsibleTrigger>Toggle</CollapsibleTrigger>
  <CollapsiblePanel>Content goes here.</CollapsiblePanel>
</Collapsible>
```

### Props

#### Collapsible

Accepts all props from `@base-ui/react/collapsible` Root, including `open`, `onOpenChange`, and `defaultOpen` for controlled and uncontrolled state.

#### CollapsibleTrigger

Accepts all props from `@base-ui/react/collapsible` Trigger.

#### CollapsiblePanel

Accepts all props from `@base-ui/react/collapsible` Panel.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| animationPreset | "none" \| "scale" \| "fade" \| "slideOutside" \| "slideInside" \| "motion" \| "motionBlur" \| "perspective" \| "perspectiveBlur" | "fade" | Controls the open/close animation style |
| transitionPreset | string | "outQuint" | Easing curve for the transition (see transition presets below) |
| reduceMotion | boolean | false | Disables all animations when true |

### Animation Presets

Use the `animationPreset` prop on `CollapsiblePanel` to change the animation style.

Values: `"none"` | `"scale"` | `"fade"` | `"slideOutside"` | `"slideInside"` | `"motion"` | `"motionBlur"` | `"perspective"` | `"perspectiveBlur"`
Default: `"fade"`

- `"none"` -- no animation.
- `"fade"` -- fades content in with a height transition.
- `"scale"` -- scales and fades content in from a smaller size.
- `"slideOutside"` -- slides content downward while fading in.
- `"slideInside"` -- slides content upward while fading in.
- `"motion"` -- combines 3D rotation, scale, and translation for a dramatic entrance.
- `"motionBlur"` -- same as `"motion"` with an added blur effect.
- `"perspective"` -- rotates content in from a 3D perspective along the X axis.
- `"perspectiveBlur"` -- same as `"perspective"` with an added blur effect.

```tsx
<CollapsiblePanel animationPreset="scale">
  Content here
</CollapsiblePanel>
```

### Transition Presets

Use the `transitionPreset` prop on `CollapsiblePanel` to control the easing curve. The component provides 24 named presets:

`"inExpo"` | `"outExpo"` | `"inOutExpo"` | `"anticipate"` | `"quickOut"` | `"overshootOut"` | `"swiftOut"` | `"snappyOut"` | `"in"` | `"out"` | `"inOut"` | `"outIn"` | `"inQuad"` | `"outQuad"` | `"inOutQuad"` | `"inCubic"` | `"outCubic"` | `"inOutCubic"` | `"inQuart"` | `"outQuart"` | `"inOutQuart"` | `"inQuint"` | `"outQuint"` | `"inOutQuint"` | `"inCirc"` | `"outCirc"` | `"inOutCirc"` | `"inOutBase"`

Default: `"outQuint"`

```tsx
<CollapsiblePanel animationPreset="scale" transitionPreset="snappyOut">
  Content here
</CollapsiblePanel>
```

### Usage

#### Basic

```tsx
import {
  Collapsible,
  CollapsibleTrigger,
  CollapsiblePanel,
} from "@/components/ui/collapsible";

export function CollapsibleBasic() {
  return (
    <Collapsible>
      <CollapsibleTrigger>Open details</CollapsibleTrigger>
      <CollapsiblePanel>Here are the details.</CollapsiblePanel>
    </Collapsible>
  );
}
```

#### Scale Animation

```tsx
import {
  Collapsible,
  CollapsibleTrigger,
  CollapsiblePanel,
} from "@/components/ui/collapsible";

export function CollapsibleScale() {
  return (
    <Collapsible>
      <CollapsibleTrigger>Toggle</CollapsibleTrigger>
      <CollapsiblePanel animationPreset="scale">
        Panel content with scale animation.
      </CollapsiblePanel>
    </Collapsible>
  );
}
```

#### Slide Outside Animation

```tsx
import {
  Collapsible,
  CollapsibleTrigger,
  CollapsiblePanel,
} from "@/components/ui/collapsible";

export function CollapsibleSlideOutside() {
  return (
    <Collapsible>
      <CollapsibleTrigger>Toggle</CollapsibleTrigger>
      <CollapsiblePanel animationPreset="slideOutside">
        Panel content with slide-outside animation.
      </CollapsiblePanel>
    </Collapsible>
  );
}
```

#### Perspective Animation

```tsx
import {
  Collapsible,
  CollapsibleTrigger,
  CollapsiblePanel,
} from "@/components/ui/collapsible";

export function CollapsiblePerspective() {
  return (
    <Collapsible>
      <CollapsibleTrigger>Toggle</CollapsibleTrigger>
      <CollapsiblePanel animationPreset="perspective">
        Panel content with perspective animation.
      </CollapsiblePanel>
    </Collapsible>
  );
}
```

#### Reduced Motion

Set `reduceMotion` to `true` on `CollapsiblePanel` to disable all animations.

```tsx
import {
  Collapsible,
  CollapsibleTrigger,
  CollapsiblePanel,
} from "@/components/ui/collapsible";

export function CollapsibleReducedMotion() {
  return (
    <Collapsible>
      <CollapsibleTrigger>Toggle</CollapsibleTrigger>
      <CollapsiblePanel reduceMotion>
        Panel content with no animation.
      </CollapsiblePanel>
    </Collapsible>
  );
}
```

#### Controlled State

Use the `open` and `onOpenChange` props on `Collapsible` to control the expanded state externally.

```tsx
import { useState } from "react";
import {
  Collapsible,
  CollapsibleTrigger,
  CollapsiblePanel,
} from "@/components/ui/collapsible";

export function CollapsibleControlled() {
  const [open, setOpen] = useState(false);

  return (
    <Collapsible open={open} onOpenChange={setOpen}>
      <CollapsibleTrigger>
        {open ? "Close" : "Open"}
      </CollapsibleTrigger>
      <CollapsiblePanel>
        Controlled panel content.
      </CollapsiblePanel>
    </Collapsible>
  );
}
```

### Notes

- The trigger sets a `data-panel-open` attribute when the panel is expanded. Use the `group-data-panel-open:` Tailwind modifier on trigger children to animate icons (e.g. rotating a chevron).
- The `render` prop on `CollapsibleTrigger` can be used to render it as a different element. This is Base UI's equivalent of Radix UI's `asChild`.
- `className` on all sub-components is merged via `cn()`.
