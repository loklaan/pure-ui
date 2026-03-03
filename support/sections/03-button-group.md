## Button Group

Groups related buttons into a single visual unit with connected borders. Use it to combine actions that belong together, such as toolbar controls, split buttons, or paginated navigation.

Uses `@base-ui/react/merge-props` and `@base-ui/react/use-render` for polymorphic rendering of the text segment.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/button-group"
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

3. Copy the component source into your project at `components/ui/button-group.tsx`.

**Registry dependency:** This component imports `Separator` from `@/components/ui/separator`. Install the Separator component first if not already present.

### Anatomy

```tsx
import {
  ButtonGroup,
  ButtonGroupSeparator,
  ButtonGroupText,
} from "@/components/ui/button-group";
import { Button } from "@/components/ui/button";

<ButtonGroup>
  <Button>Action 1</Button>
  <Button>Action 2</Button>
</ButtonGroup>
```

- **ButtonGroup** -- wrapper `div` with `role="group"`. Strips inner border radii so children appear connected.
- **ButtonGroupText** -- text segment within the group. Renders a `div` by default and supports the `render` prop for polymorphic rendering.
- **ButtonGroupSeparator** -- visual divider between group items. Wraps the Separator component.

### Props

#### ButtonGroup

Accepts all props from a standard `div` element.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| orientation | "horizontal" \| "vertical" | "horizontal" | Layout direction of the group |

#### ButtonGroupText

Accepts all props from `@base-ui/react/use-render` `ComponentProps<"div">`, including the `render` prop for polymorphic rendering.

#### ButtonGroupSeparator

Accepts all props from the `Separator` component.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| orientation | "horizontal" \| "vertical" | "horizontal" | Separator direction (use `"vertical"` in a horizontal group) |

### Exported Utilities

- `buttonGroupVariants` -- the `tailwind-variants` config object. Import it when you need to apply button group styles outside the `ButtonGroup` component.

```tsx
import { buttonGroupVariants } from "@/components/ui/button-group";
```

### Variants

#### orientation

Values: `"horizontal"` | `"vertical"`
Default: `"horizontal"`

- `"horizontal"` -- buttons are laid out in a row. Inner left/right border radii are removed and left borders are collapsed.
- `"vertical"` -- buttons are stacked vertically. Inner top/bottom border radii are removed and top borders are collapsed.

```tsx
<ButtonGroup orientation="vertical">
  <Button variant="outline">Top</Button>
  <Button variant="outline">Bottom</Button>
</ButtonGroup>
```

### Usage

#### Basic

```tsx
import { ButtonGroup } from "@/components/ui/button-group";
import { Button } from "@/components/ui/button";

export function ButtonGroupBasic() {
  return (
    <ButtonGroup>
      <Button variant="outline">Files</Button>
      <Button variant="outline">Media</Button>
    </ButtonGroup>
  );
}
```

#### Vertical Orientation

Set `orientation="vertical"` for a stacked layout.

```tsx
import { ButtonGroup } from "@/components/ui/button-group";
import { Button } from "@/components/ui/button";
import { PlusIcon, MinusIcon } from "lucide-react";

export function ButtonGroupVertical() {
  return (
    <ButtonGroup orientation="vertical" aria-label="Media controls">
      <Button variant="outline" size="icon">
        <PlusIcon />
      </Button>
      <Button variant="outline" size="icon">
        <MinusIcon />
      </Button>
    </ButtonGroup>
  );
}
```

#### Sizes

ButtonGroup does not have its own size prop. Control button sizes through the `size` prop on individual `Button` children.

```tsx
import { ButtonGroup } from "@/components/ui/button-group";
import { Button } from "@/components/ui/button";
import { PlusIcon } from "lucide-react";

export function ButtonGroupSizes() {
  return (
    <div className="flex flex-col items-start gap-8">
      <ButtonGroup>
        <Button variant="outline" size="sm">Small</Button>
        <Button variant="outline" size="sm">Button</Button>
        <Button variant="outline" size="sm">Group</Button>
        <Button variant="outline" size="icon-sm">
          <PlusIcon />
        </Button>
      </ButtonGroup>
      <ButtonGroup>
        <Button variant="outline">Default</Button>
        <Button variant="outline">Button</Button>
        <Button variant="outline">Group</Button>
        <Button variant="outline" size="icon">
          <PlusIcon />
        </Button>
      </ButtonGroup>
      <ButtonGroup>
        <Button variant="outline" size="lg">Large</Button>
        <Button variant="outline" size="lg">Button</Button>
        <Button variant="outline" size="lg">Group</Button>
        <Button variant="outline" size="icon-lg">
          <PlusIcon />
        </Button>
      </ButtonGroup>
    </div>
  );
}
```

#### Separator

Use `ButtonGroupSeparator` to visually divide buttons within a group. Buttons with the `outline` variant already have visible borders and typically do not need a separator. For other variants like `secondary`, add a separator to maintain visual hierarchy.

```tsx
import { Button } from "@/components/ui/button";
import {
  ButtonGroup,
  ButtonGroupSeparator,
} from "@/components/ui/button-group";

export function ButtonGroupWithSeparator() {
  return (
    <ButtonGroup>
      <Button variant="secondary" size="sm">Copy</Button>
      <ButtonGroupSeparator orientation="vertical" />
      <Button variant="secondary" size="sm">Paste</Button>
    </ButtonGroup>
  );
}
```

#### Split Button

Combine a primary action button with a secondary icon button separated by `ButtonGroupSeparator` to create a split button.

```tsx
import { PlusIcon } from "lucide-react";
import { Button } from "@/components/ui/button";
import {
  ButtonGroup,
  ButtonGroupSeparator,
} from "@/components/ui/button-group";

export function ButtonGroupSplit() {
  return (
    <ButtonGroup>
      <Button variant="secondary">Button</Button>
      <ButtonGroupSeparator orientation="vertical" />
      <Button size="icon" variant="secondary">
        <PlusIcon />
      </Button>
    </ButtonGroup>
  );
}
```

#### Nested Groups

Nest `ButtonGroup` components inside a parent `ButtonGroup` to create groups with spacing between them. The parent group automatically adds a gap between nested groups.

```tsx
import { ArrowLeftIcon, ArrowRightIcon } from "lucide-react";
import { Button } from "@/components/ui/button";
import { ButtonGroup } from "@/components/ui/button-group";

export function ButtonGroupNested() {
  return (
    <ButtonGroup>
      <ButtonGroup>
        <Button variant="outline" size="sm">1</Button>
        <Button variant="outline" size="sm">2</Button>
        <Button variant="outline" size="sm">3</Button>
        <Button variant="outline" size="sm">4</Button>
        <Button variant="outline" size="sm">5</Button>
      </ButtonGroup>
      <ButtonGroup>
        <Button variant="outline" size="icon-sm" aria-label="Previous">
          <ArrowLeftIcon />
        </Button>
        <Button variant="outline" size="icon-sm" aria-label="Next">
          <ArrowRightIcon />
        </Button>
      </ButtonGroup>
    </ButtonGroup>
  );
}
```

#### With Input

Wrap an `Input` component alongside buttons. The input stretches to fill available space within the group.

```tsx
import { SearchIcon } from "lucide-react";
import { Button } from "@/components/ui/button";
import { ButtonGroup } from "@/components/ui/button-group";
import { Input } from "@/components/ui/input";

export function ButtonGroupWithInput() {
  return (
    <ButtonGroup>
      <Input placeholder="Search..." />
      <Button variant="outline" aria-label="Search">
        <SearchIcon />
      </Button>
    </ButtonGroup>
  );
}
```

#### With Menu

Create a split button group that opens a menu from the secondary trigger.

```tsx
import { ChevronDownIcon } from "lucide-react";
import { Button } from "@/components/ui/button";
import { ButtonGroup } from "@/components/ui/button-group";
import {
  Menu,
  MenuPopup,
  MenuItem,
  MenuTrigger,
} from "@/components/ui/menu";

export function ButtonGroupWithMenu() {
  return (
    <ButtonGroup>
      <Button variant="outline">Follow</Button>
      <Menu>
        <MenuTrigger render={<Button variant="outline" className="pl-2!" />}>
          <ChevronDownIcon />
        </MenuTrigger>
        <MenuPopup align="end">
          <MenuItem>Mute Conversation</MenuItem>
          <MenuItem>Mark as Read</MenuItem>
          <MenuItem>Report Conversation</MenuItem>
        </MenuPopup>
      </Menu>
    </ButtonGroup>
  );
}
```

#### With Select

Pair a `Select` component with buttons or inputs inside a group.

```tsx
import { ArrowRightIcon, ChevronsUpDownIcon } from "lucide-react";
import { Button } from "@/components/ui/button";
import { ButtonGroup } from "@/components/ui/button-group";
import { Input } from "@/components/ui/input";
import {
  Select,
  SelectPopup,
  SelectItem,
  SelectTrigger,
  SelectValue,
  SelectList,
  SelectIcon,
} from "@/components/ui/select";

const CURRENCIES = [
  { value: "$", label: "US Dollar" },
  { value: "\u20AC", label: "Euro" },
  { value: "\u00A3", label: "British Pound" },
];

export function ButtonGroupWithSelect() {
  return (
    <ButtonGroup>
      <ButtonGroup>
        <Select defaultValue={CURRENCIES[0]}>
          <SelectTrigger className="w-fit min-w-none">
            <SelectValue>{(currency) => currency.value}</SelectValue>
            <SelectIcon>
              <ChevronsUpDownIcon className="size-3.5" />
            </SelectIcon>
          </SelectTrigger>
          <SelectPopup className="min-w-48" alignItemWithTrigger>
            <SelectList>
              {CURRENCIES.map((curr) => (
                <SelectItem key={curr.value} value={curr}>
                  {curr.value} {curr.label}
                </SelectItem>
              ))}
            </SelectList>
          </SelectPopup>
        </Select>
        <Input placeholder="10.00" pattern="[0-9]*" />
      </ButtonGroup>
      <ButtonGroup>
        <Button aria-label="Send" size="icon" variant="outline">
          <ArrowRightIcon />
        </Button>
      </ButtonGroup>
    </ButtonGroup>
  );
}
```

#### With Popover

Attach a `Popover` to a secondary trigger button within the group.

```tsx
import { BotIcon, ChevronDownIcon } from "lucide-react";
import { Button } from "@/components/ui/button";
import { ButtonGroup } from "@/components/ui/button-group";
import {
  Popover,
  PopoverPopup,
  PopoverTrigger,
} from "@/components/ui/popover";

export function ButtonGroupWithPopover() {
  return (
    <ButtonGroup>
      <Button variant="outline">
        <BotIcon /> Copilot
      </Button>
      <Popover>
        <PopoverTrigger
          render={
            <Button variant="outline" size="icon" aria-label="Open Popover" />
          }
        >
          <ChevronDownIcon />
        </PopoverTrigger>
        <PopoverPopup align="end">
          Popover content goes here.
        </PopoverPopup>
      </Popover>
    </ButtonGroup>
  );
}
```

### Notes

- Always include an `aria-label` on the `ButtonGroup` when the group purpose is not clear from button labels alone.
- ButtonGroup renders a `div` with `role="group"`. Screen readers will announce the grouped buttons as a related set.
- When composing with overlay components (Menu, Select, Popover), use the `render` prop on the overlay trigger to render it as a `Button` so it inherits button group styling.
- The `render` prop on `ButtonGroupText` is Base UI's equivalent of Radix UI's `asChild`. Pass a React element to change the rendered tag.
