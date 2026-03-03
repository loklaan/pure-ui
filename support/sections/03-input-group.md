## Input Group

A container for composing an input or textarea with addons such as icons, text labels, buttons, spinners, or menus. InputGroup provides six sub-components that arrange themselves around a central input control.

InputGroup does not wrap a single Base UI primitive directly. It composes the Input, Textarea, and Button registry components internally.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/input-group"
```

#### Manual

1. Install dependencies:

```bash
npm install clsx tailwind-merge tailwind-variants @base-ui/react
pnpm add clsx tailwind-merge tailwind-variants @base-ui/react
yarn add clsx tailwind-merge tailwind-variants @base-ui/react
bun add clsx tailwind-merge tailwind-variants @base-ui/react
```

2. Add the `cn` utility (if not already present):

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

3. Install the registry dependencies: `input`, `textarea`, and `button`.

4. Copy the component source into your project at `components/ui/input-group.tsx`.

### Anatomy

```tsx
import {
  InputGroup,
  InputGroupAddon,
  InputGroupButton,
  InputGroupInput,
  InputGroupText,
  InputGroupTextarea,
} from "@/components/ui/input-group";

<InputGroup>
  <InputGroupInput />
  <InputGroupAddon>
    {/* icons, text, buttons, or other content */}
  </InputGroupAddon>
</InputGroup>
```

All sub-components except `InputGroupInput` or `InputGroupTextarea` are optional. Use only the parts you need.

### Props

#### InputGroup

Extends `React.ComponentProps<"div">`. Renders a `div` with `role="group"` and `data-slot="input-group"`. The `className` prop is merged via `cn()`.

Set `data-disabled` on InputGroup to visually dim the entire group.

#### InputGroupAddon

Extends `React.ComponentProps<"div">`. Wraps icons, text, buttons, or other content placed beside the input.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| align | "inline-start" \| "inline-end" \| "block-start" \| "block-end" | "inline-start" | Position of the addon relative to the input |

- `inline-start` places the addon to the left of the input (or right in RTL).
- `inline-end` places the addon to the right of the input (or left in RTL).
- `block-start` places the addon above the input. The group switches to a vertical flex layout.
- `block-end` places the addon below the input. The group switches to a vertical flex layout.

Clicking the addon area focuses the adjacent input (unless the click target is a button or link).

#### InputGroupButton

Renders a Button component styled for use inside the group.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| size | "xs" \| "sm" \| "icon-xs" \| "icon-sm" | "xs" | Size preset for the button |
| variant | same as Button variant | "ghost" | Visual style of the button |
| type | "submit" \| "reset" \| "button" | "button" | HTML button type |

Accepts all other Button props except `size` (which is overridden with the group-specific sizes above).

#### InputGroupText

Extends `React.ComponentProps<"span">`. Renders a `span` with `data-slot="input-group-text"` for displaying text labels, character counts, or status messages.

#### InputGroupInput

Renders an Input component with border, background, and shadow removed so it integrates with the group container. Accepts all Input props.

#### InputGroupTextarea

Renders a Textarea component with border, background, and shadow removed. Accepts all Textarea props.

### Usage

#### Basic

```tsx
import { SearchIcon } from "lucide-react";
import {
  InputGroup,
  InputGroupAddon,
  InputGroupInput,
} from "@/components/ui/input-group";

export function InputGroupBasic() {
  return (
    <InputGroup>
      <InputGroupInput placeholder="Search..." />
      <InputGroupAddon>
        <SearchIcon />
      </InputGroupAddon>
    </InputGroup>
  );
}
```

#### Icon Addons

Place icons inside `InputGroupAddon`. Use the `align` prop to position icons on either side.

```tsx
import { CreditCardIcon, CheckIcon } from "lucide-react";
import {
  InputGroup,
  InputGroupAddon,
  InputGroupInput,
} from "@/components/ui/input-group";

export function InputGroupIconExample() {
  return (
    <InputGroup>
      <InputGroupInput placeholder="Card number" />
      <InputGroupAddon>
        <CreditCardIcon />
      </InputGroupAddon>
      <InputGroupAddon align="inline-end">
        <CheckIcon />
      </InputGroupAddon>
    </InputGroup>
  );
}
```

#### Text Addons

Use `InputGroupText` inside `InputGroupAddon` for prefix and suffix text.

```tsx
import {
  InputGroup,
  InputGroupAddon,
  InputGroupInput,
  InputGroupText,
} from "@/components/ui/input-group";

export function InputGroupTextExample() {
  return (
    <InputGroup>
      <InputGroupAddon>
        <InputGroupText>$</InputGroupText>
      </InputGroupAddon>
      <InputGroupInput placeholder="0.00" />
      <InputGroupAddon align="inline-end">
        <InputGroupText>USD</InputGroupText>
      </InputGroupAddon>
    </InputGroup>
  );
}
```

#### Button Addons

Use `InputGroupButton` inside `InputGroupAddon` for action buttons.

```tsx
import {
  InputGroup,
  InputGroupAddon,
  InputGroupButton,
  InputGroupInput,
} from "@/components/ui/input-group";

export function InputGroupButtonExample() {
  return (
    <InputGroup>
      <InputGroupInput placeholder="Type to search..." />
      <InputGroupAddon align="inline-end">
        <InputGroupButton variant="secondary">Search</InputGroupButton>
      </InputGroupAddon>
    </InputGroup>
  );
}
```

#### Textarea

Use `InputGroupTextarea` instead of `InputGroupInput` for multi-line input. Pair with `block-start` or `block-end` alignment for addons above or below the textarea.

```tsx
import {
  InputGroup,
  InputGroupAddon,
  InputGroupButton,
  InputGroupText,
  InputGroupTextarea,
} from "@/components/ui/input-group";

export function InputGroupTextareaExample() {
  return (
    <InputGroup>
      <InputGroupTextarea
        placeholder="console.log('Hello, world!');"
        className="min-h-[200px]"
      />
      <InputGroupAddon align="block-end" className="border-t">
        <InputGroupText>Line 1, Column 1</InputGroupText>
        <InputGroupButton size="sm" className="ml-auto" variant="default">
          Run
        </InputGroupButton>
      </InputGroupAddon>
      <InputGroupAddon align="block-start" className="border-b">
        <InputGroupText className="font-mono font-medium">
          script.js
        </InputGroupText>
      </InputGroupAddon>
    </InputGroup>
  );
}
```

#### Spinner

Place a Spinner component inside an addon to indicate loading state. Set `data-disabled` on the InputGroup and `disabled` on the input to convey the loading state.

```tsx
import {
  InputGroup,
  InputGroupAddon,
  InputGroupInput,
} from "@/components/ui/input-group";
import { Spinner } from "@/components/ui/spinner";

export function InputGroupSpinnerExample() {
  return (
    <InputGroup data-disabled>
      <InputGroupInput placeholder="Searching..." disabled />
      <InputGroupAddon align="inline-end">
        <Spinner size="sm" />
      </InputGroupAddon>
    </InputGroup>
  );
}
```

#### Label

Place a Label inside an addon with `block-start` alignment to create an integrated label above the input.

```tsx
import {
  InputGroup,
  InputGroupAddon,
  InputGroupInput,
} from "@/components/ui/input-group";
import { Label } from "@/components/ui/label";

export function InputGroupLabelExample() {
  return (
    <InputGroup>
      <InputGroupInput id="email" placeholder="Krishna" />
      <InputGroupAddon>
        <Label htmlFor="email">@</Label>
      </InputGroupAddon>
    </InputGroup>
  );
}
```

#### Tooltip

Render a Tooltip trigger as an `InputGroupButton` using the `render` prop.

```tsx
import { InfoIcon } from "lucide-react";
import {
  InputGroup,
  InputGroupAddon,
  InputGroupButton,
  InputGroupInput,
} from "@/components/ui/input-group";
import {
  Tooltip,
  TooltipTrigger,
  TooltipPopup,
  TooltipProvider,
} from "@/components/ui/tooltip";

export function InputGroupTooltipExample() {
  return (
    <InputGroup>
      <InputGroupInput placeholder="Enter password" type="password" />
      <InputGroupAddon align="inline-end">
        <TooltipProvider>
          <Tooltip>
            <TooltipTrigger
              render={
                <InputGroupButton
                  variant="ghost"
                  aria-label="Info"
                  size="icon-xs"
                />
              }
            >
              <InfoIcon />
            </TooltipTrigger>
            <TooltipPopup>Password must be at least 8 characters</TooltipPopup>
          </Tooltip>
        </TooltipProvider>
      </InputGroupAddon>
    </InputGroup>
  );
}
```

#### Menu

Render a Menu trigger as an `InputGroupButton` using the `render` prop.

```tsx
import { MoreHorizontal } from "lucide-react";
import {
  InputGroup,
  InputGroupAddon,
  InputGroupButton,
  InputGroupInput,
} from "@/components/ui/input-group";
import {
  Menu,
  MenuItem,
  MenuPopup,
  MenuTrigger,
} from "@/components/ui/menu";

export function InputGroupMenuExample() {
  return (
    <InputGroup>
      <InputGroupInput placeholder="Enter file name" />
      <InputGroupAddon align="inline-end">
        <Menu>
          <MenuTrigger
            render={
              <InputGroupButton
                variant="ghost"
                aria-label="More"
                size="icon-xs"
              />
            }
          >
            <MoreHorizontal />
          </MenuTrigger>
          <MenuPopup align="end">
            <MenuItem>Settings</MenuItem>
            <MenuItem>Copy path</MenuItem>
            <MenuItem>Open location</MenuItem>
          </MenuPopup>
        </Menu>
      </InputGroupAddon>
    </InputGroup>
  );
}
```

### Notes

- InputGroup uses CSS `has-[]` selectors to propagate focus and error states from the child input to the group border. When the inner input receives focus, the group shows a focus ring. When the inner input has `aria-invalid="true"`, the group shows destructive border styling.
- Set `data-disabled` on the InputGroup root to visually dim the entire group (opacity reduction on addon content).
- Multiple `InputGroupAddon` elements can be used in the same group with different `align` values.
- `block-start` and `block-end` alignment switch the group to a vertical flex layout, making addons span the full width above or below the input.
- `InputGroupButton` defaults to `type="button"` (not `"submit"`) to prevent accidental form submissions.
- `className` on any sub-component is merged via `cn()`.
