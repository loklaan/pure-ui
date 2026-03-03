## Kbd

Displays keyboard keys or shortcuts. Use `Kbd` for individual keys and `KbdGroup` to group multiple keys together in a sequence.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/kbd"
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

3. Copy the component source into your project at `components/ui/kbd.tsx`.

### Anatomy

```tsx
import { Kbd, KbdGroup } from "@/components/ui/kbd";

<Kbd>Key</Kbd>

<KbdGroup>
  <Kbd>Key1</Kbd>
  <Kbd>Key2</Kbd>
</KbdGroup>
```

### Props

#### Kbd

Renders a `<kbd>` HTML element. Accepts all standard `<kbd>` element props including `className` and `children`.

#### KbdGroup

Renders a `<kbd>` HTML element with `data-slot="kbd-group"`. Accepts all standard `<div>` element props including `className` and `children`. Groups multiple `Kbd` elements with consistent spacing.

### Usage

#### Basic

```tsx
import { Kbd } from "@/components/ui/kbd";

export function KbdBasic() {
  return <Kbd>F12</Kbd>;
}
```

#### Key Sequence

Use `KbdGroup` to display a keyboard shortcut with multiple keys.

```tsx
import { Kbd, KbdGroup } from "@/components/ui/kbd";

export function KbdSequence() {
  return (
    <KbdGroup>
      <Kbd>Ctrl</Kbd>
      <span>+</span>
      <Kbd>B</Kbd>
    </KbdGroup>
  );
}
```

#### Group

Use `KbdGroup` inline within text to display multiple shortcut combinations.

```tsx
import { Kbd, KbdGroup } from "@/components/ui/kbd";

export function KbdGroupExample() {
  return (
    <p>
      Use{" "}
      <KbdGroup>
        <Kbd>Ctrl + B</Kbd>
        <Kbd>Ctrl + K</Kbd>
      </KbdGroup>{" "}
      to open the command palette
    </p>
  );
}
```

#### Inside a Button

Compose `Kbd` inside a `Button` to show the associated keyboard shortcut alongside the action label.

```tsx
import { Button } from "@/components/ui/button";
import { Kbd } from "@/components/ui/kbd";

export function KbdButtonExample() {
  return (
    <div className="flex flex-wrap items-center gap-4">
      <Button variant="outline" size="sm" className="pr-2">
        Accept <Kbd>⏎</Kbd>
      </Button>
      <Button variant="outline" size="sm" className="pr-2">
        Cancel <Kbd>Esc</Kbd>
      </Button>
    </div>
  );
}
```

#### Inside a Tooltip

Place `Kbd` inside a tooltip to reveal the keyboard shortcut on hover. The `Kbd` component adapts its styling when rendered inside tooltip content.

```tsx
import { Button } from "@/components/ui/button";
import { Kbd, KbdGroup } from "@/components/ui/kbd";
import {
  Tooltip,
  TooltipPopup,
  TooltipProvider,
  TooltipTrigger,
} from "@/components/ui/tooltip";

export function KbdTooltipExample() {
  return (
    <TooltipProvider>
      <Tooltip>
        <TooltipTrigger render={<Button size="sm" variant="outline" />}>
          Save
        </TooltipTrigger>
        <TooltipPopup>
          <div className="flex items-center gap-2">
            Save Changes <Kbd>S</Kbd>
          </div>
        </TooltipPopup>
      </Tooltip>
      <Tooltip>
        <TooltipTrigger render={<Button size="sm" variant="outline" />}>
          Print
        </TooltipTrigger>
        <TooltipPopup>
          <div className="flex items-center gap-2">
            Print Document{" "}
            <KbdGroup>
              <Kbd>Ctrl</Kbd>
              <Kbd>P</Kbd>
            </KbdGroup>
          </div>
        </TooltipPopup>
      </Tooltip>
    </TooltipProvider>
  );
}
```

#### Inside an Input Group

Use `Kbd` inside `InputGroupAddon` to display a search shortcut hint within an input field.

```tsx
import { SearchIcon } from "lucide-react";
import {
  InputGroup,
  InputGroupAddon,
  InputGroupInput,
} from "@/components/ui/input-group";
import { Kbd } from "@/components/ui/kbd";

export function KbdInputGroupExample() {
  return (
    <InputGroup>
      <InputGroupInput placeholder="Search..." />
      <InputGroupAddon>
        <SearchIcon />
      </InputGroupAddon>
      <InputGroupAddon align="inline-end">
        <Kbd>⌘</Kbd>
        <Kbd>K</Kbd>
      </InputGroupAddon>
    </InputGroup>
  );
}
```

### Notes

- `Kbd` renders a native `<kbd>` element, which provides semantic meaning for keyboard input.
- SVG icons placed inside `Kbd` are automatically sized to `0.75rem` (12px) unless they have an explicit `size-*` class.
- When `Kbd` is rendered inside tooltip content (detected via `in-data-[slot=tooltip-content]`), it uses an adapted colour scheme for contrast.
