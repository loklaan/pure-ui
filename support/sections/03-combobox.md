## Combobox

An input combined with a filterable dropdown list of predefined items. Supports single and multiple selection, object items, grouping, clearable input, and input placement inside the popup.

Built on `@base-ui/react/combobox`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/combobox"
```

#### Manual

1. Install dependencies:

```bash
npm install clsx tailwind-merge @base-ui/react
pnpm add clsx tailwind-merge @base-ui/react
yarn add clsx tailwind-merge @base-ui/react
bun add clsx tailwind-merge @base-ui/react
```

2. Add the `cn` utility (if not already present):

```ts
import { clsx, type ClassValue } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

3. Copy the component source into your project at `components/ui/combobox.tsx`.

The Combobox component also depends on the `Input`, `Label`, and `ScrollArea` registry components. Install them separately or let the CLI resolve them automatically.

### Anatomy

```tsx
import {
  Combobox,
  ComboboxInput,
  ComboboxPopup,
  ComboboxList,
  ComboboxItem,
  ComboboxEmpty,
} from "@/components/ui/combobox";

<Combobox items={items}>
  <ComboboxInput placeholder="Select..." />
  <ComboboxPopup>
    <ComboboxEmpty>No results found.</ComboboxEmpty>
    <ComboboxList>
      {(item) => (
        <ComboboxItem key={item} value={item}>
          {item}
        </ComboboxItem>
      )}
    </ComboboxList>
  </ComboboxPopup>
</Combobox>
```

Additional sub-components for grouping, multi-select, labels, and triggers:

```tsx
import {
  Combobox,
  ComboboxInput,
  ComboboxPopup,
  ComboboxList,
  ComboboxItem,
  ComboboxEmpty,
  ComboboxLabel,
  ComboboxValue,
  ComboboxTrigger,
  ComboboxClear,
  ComboboxChips,
  ComboboxChip,
  ComboboxCollection,
  ComboboxRow,
  ComboboxGroup,
  ComboboxGroupLabel,
  ComboboxSeparator,
} from "@/components/ui/combobox";
```

Three SVG icon components are also exported: `ChevronsUpDownIcon`, `CloseIcon`, `CheckIcon`.

### Props

#### Combobox

Root wrapper. Generic over `Value` and `Multiple`. Accepts all props from `@base-ui/react/combobox` Root.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| items | Value[] \| Group[] | -- | Array of items or grouped items to display |
| value | Value \| Value[] \| null | -- | Controlled selected value |
| defaultValue | Value \| Value[] \| null | -- | Initial selected value (uncontrolled) |
| onValueChange | (value: Value \| Value[] \| null) => void | -- | Called when the selected value changes |
| multiple | boolean | false | Enables multiple selection mode |
| autoHighlight | boolean | false | Automatically highlights the first matching item as the user types |
| itemToStringLabel | (item: Value) => string | -- | Maps an object item to a display string for the input field |

#### ComboboxInput

Input field for filtering items. In single-select mode, renders using the `Input` registry component via the `render` prop. In multi-select mode, renders a plain input element.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| isClearable | boolean | false | Shows a clear button inside the input when a value is selected |
| showTrigger | boolean | true | Shows the dropdown trigger icon inside the input |

#### ComboboxPopup

Dropdown popup container. Wraps the content in a Portal and Positioner. Anchors to the chips container in multi-select mode.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| sideOffset | number | 0 | Offset from the anchor element |

#### ComboboxItem

Individual option in the list. Includes a check indicator that displays when the item is selected. Accepts all props from `@base-ui/react/combobox` Item.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| value | Value | -- | The value this item represents (must match the type of items in the array) |

#### ComboboxChip

Chip displayed for each selected item in multi-select mode. Includes a built-in remove button. Accepts all props from `@base-ui/react/combobox` Chip.

#### ComboboxChips

Container for chips in multi-select mode. Renders as a flex-wrap container with input-like styling. Accepts all props from `@base-ui/react/combobox` Chips.

#### ComboboxValue

Displays the selected value. Accepts a render function as children for custom rendering. Accepts all props from `@base-ui/react/combobox` Value.

#### ComboboxTrigger

Button that opens the dropdown. Accepts all props from `@base-ui/react/combobox` Trigger.

#### ComboboxClear

Button that clears the current selection. Accepts all props from `@base-ui/react/combobox` Clear.

#### ComboboxList

Scrollable list of items. Wraps content in a `ScrollArea` with vertical scroll shadows. Children is a render function that receives each item. Accepts all props from `@base-ui/react/combobox` List.

#### ComboboxEmpty

Content displayed when no items match the filter. Accepts all props from `@base-ui/react/combobox` Empty.

#### ComboboxGroup

Groups related items together. Accepts all props from `@base-ui/react/combobox` Group.

#### ComboboxGroupLabel

Label for an item group. Renders as a sticky header within the scroll area. Accepts all props from `@base-ui/react/combobox` GroupLabel.

#### ComboboxCollection

Wrapper for nested item collections within groups. Accepts all props from `@base-ui/react/combobox` Collection.

#### ComboboxSeparator

Visual divider between groups. Accepts all props from `@base-ui/react/combobox` Separator.

#### ComboboxLabel

Label for the combobox. Wraps the `Label` registry component. Accepts all props from the `Label` component.

### Usage

#### Basic

Use an array of primitive values (strings) as items. The `ComboboxList` children is a render function that receives each item.

```tsx
import {
  Combobox,
  ComboboxEmpty,
  ComboboxInput,
  ComboboxItem,
  ComboboxList,
  ComboboxPopup,
} from "@/components/ui/combobox";

const fruits = [
  "Apple", "Banana", "Orange", "Pineapple", "Grape",
  "Mango", "Strawberry", "Blueberry", "Cherry", "Peach",
];

export function ComboboxBasicDemo() {
  return (
    <Combobox items={fruits}>
      <ComboboxInput placeholder="Select a fruit..." />
      <ComboboxPopup>
        <ComboboxEmpty>No fruits found.</ComboboxEmpty>
        <ComboboxList>
          {(fruit: string) => (
            <ComboboxItem key={fruit} value={fruit}>
              {fruit}
            </ComboboxItem>
          )}
        </ComboboxList>
      </ComboboxPopup>
    </Combobox>
  );
}
```

#### With Object Items

Use an array of objects as items. The `value` prop on each `ComboboxItem` must match the type of items in the array -- pass the entire object as the value.

When items have a `label` property, it is used by default as the display string in the input. For items without a `label` property, use `itemToStringLabel` on the `Combobox` root to specify how to convert an item to a display string.

```tsx
import {
  Combobox,
  ComboboxEmpty,
  ComboboxInput,
  ComboboxItem,
  ComboboxList,
  ComboboxPopup,
} from "@/components/ui/combobox";

const users = [
  { id: "u1", label: "Alice Johnson", email: "alice@example.com" },
  { id: "u2", label: "Bob Lee", email: "bob@example.com" },
  { id: "u3", label: "Cathy Kim", email: "cathy@example.com" },
];

type User = (typeof users)[number];

export function ComboboxWithObjectsDemo() {
  return (
    <Combobox items={users}>
      <ComboboxInput placeholder="Select a user..." />
      <ComboboxPopup>
        <ComboboxEmpty>No users found.</ComboboxEmpty>
        <ComboboxList>
          {(user: User) => (
            <ComboboxItem key={user.id} value={user}>
              <div>
                <div className="font-medium">{user.label}</div>
                <div className="text-xs text-muted-foreground">
                  {user.email}
                </div>
              </div>
            </ComboboxItem>
          )}
        </ComboboxList>
      </ComboboxPopup>
    </Combobox>
  );
}
```

#### Custom Item Label

Use `itemToStringLabel` to control how object items display in the input when selected. This is required when items lack a `label` property.

```tsx
import {
  Combobox,
  ComboboxEmpty,
  ComboboxInput,
  ComboboxItem,
  ComboboxList,
  ComboboxPopup,
} from "@/components/ui/combobox";

const users = [
  { id: "u1", name: "Alice Johnson", email: "alice@example.com" },
  { id: "u2", name: "Bob Lee", email: "bob@example.com" },
];

type User = (typeof users)[number];

export function ComboboxItemToStringLabelDemo() {
  return (
    <Combobox items={users} itemToStringLabel={(user: User) => user.name}>
      <ComboboxInput placeholder="Select a user..." />
      <ComboboxPopup>
        <ComboboxEmpty>No users found.</ComboboxEmpty>
        <ComboboxList>
          {(user: User) => (
            <ComboboxItem key={user.id} value={user}>
              <div>
                <div className="font-medium">{user.name}</div>
                <div className="text-xs text-muted-foreground">
                  {user.email}
                </div>
              </div>
            </ComboboxItem>
          )}
        </ComboboxList>
      </ComboboxPopup>
    </Combobox>
  );
}
```

#### Controlled

Use `value` and `onValueChange` to control the selected item.

```tsx
import {
  Combobox,
  ComboboxEmpty,
  ComboboxInput,
  ComboboxItem,
  ComboboxList,
  ComboboxPopup,
} from "@/components/ui/combobox";
import { useState } from "react";

const users = [
  { id: "u1", name: "Alice Johnson", email: "alice@example.com" },
  { id: "u2", name: "Bob Lee", email: "bob@example.com" },
  { id: "u3", name: "Cathy Kim", email: "cathy@example.com" },
];

type User = (typeof users)[number];

export function ComboboxControlledDemo() {
  const [selectedUser, setSelectedUser] = useState<User | null>(null);

  return (
    <Combobox
      items={users}
      itemToStringLabel={(user: User) => user.name}
      value={selectedUser}
      onValueChange={setSelectedUser}
    >
      <ComboboxInput placeholder="Select a user..." />
      <ComboboxPopup>
        <ComboboxEmpty>No users found.</ComboboxEmpty>
        <ComboboxList>
          {(user: User) => (
            <ComboboxItem key={user.id} value={user}>
              <div>
                <div className="font-medium">{user.name}</div>
                <div className="text-xs text-muted-foreground">
                  {user.email}
                </div>
              </div>
            </ComboboxItem>
          )}
        </ComboboxList>
      </ComboboxPopup>
    </Combobox>
  );
}
```

#### With Label

Use `ComboboxLabel` to associate a label with the combobox input.

```tsx
import {
  Combobox,
  ComboboxEmpty,
  ComboboxInput,
  ComboboxItem,
  ComboboxLabel,
  ComboboxList,
  ComboboxPopup,
} from "@/components/ui/combobox";

const fruits = ["Apple", "Banana", "Orange", "Pineapple", "Grape"];

export function ComboboxWithLabelDemo() {
  return (
    <Combobox items={fruits}>
      <ComboboxLabel>Select a fruit</ComboboxLabel>
      <ComboboxInput placeholder="Select a fruit..." />
      <ComboboxPopup>
        <ComboboxEmpty>No fruits found.</ComboboxEmpty>
        <ComboboxList>
          {(fruit: string) => (
            <ComboboxItem key={fruit} value={fruit}>
              {fruit}
            </ComboboxItem>
          )}
        </ComboboxList>
      </ComboboxPopup>
    </Combobox>
  );
}
```

#### Auto Highlighting

Set `autoHighlight` to automatically highlight the first matching item as the user types. Press Enter to select the highlighted item.

```tsx
<Combobox items={fruits} autoHighlight>
  <ComboboxInput placeholder="Select a fruit..." />
  <ComboboxPopup>
    <ComboboxEmpty>No fruits found.</ComboboxEmpty>
    <ComboboxList>
      {(fruit: string) => (
        <ComboboxItem key={fruit} value={fruit}>
          {fruit}
        </ComboboxItem>
      )}
    </ComboboxList>
  </ComboboxPopup>
</Combobox>
```

#### Multiple Selection

Set `multiple` on the `Combobox` root to allow selecting multiple items. Use `ComboboxChips`, `ComboboxValue`, and `ComboboxChip` to display selected items as removable chips.

```tsx
import {
  Combobox,
  ComboboxChip,
  ComboboxChips,
  ComboboxEmpty,
  ComboboxInput,
  ComboboxItem,
  ComboboxList,
  ComboboxPopup,
  ComboboxValue,
} from "@/components/ui/combobox";
import { useState } from "react";

const items = [
  { label: "Apple", value: "apple" },
  { label: "Banana", value: "banana" },
  { label: "Orange", value: "orange" },
  { label: "Grape", value: "grape" },
  { label: "Strawberry", value: "strawberry" },
];

type Item = (typeof items)[number];

export function ComboboxMultipleSelectionDemo() {
  const [selectedItems, setSelectedItems] = useState<Item[]>([]);

  return (
    <Combobox
      value={selectedItems}
      onValueChange={setSelectedItems}
      items={items}
      multiple
    >
      <ComboboxChips>
        <ComboboxValue>
          {(value: Item[]) => (
            <>
              {value?.map((item) => (
                <ComboboxChip aria-label={item.label} key={item.value}>
                  {item.label}
                </ComboboxChip>
              ))}
              <ComboboxInput
                aria-label="Select a item"
                placeholder={
                  value.length > 0 ? undefined : "Select a item..."
                }
              />
            </>
          )}
        </ComboboxValue>
      </ComboboxChips>

      <ComboboxPopup>
        <ComboboxEmpty>No items found.</ComboboxEmpty>
        <ComboboxList>
          {(item: Item) => (
            <ComboboxItem key={item.value} value={item}>
              {item.label}
            </ComboboxItem>
          )}
        </ComboboxList>
      </ComboboxPopup>
    </Combobox>
  );
}
```

#### Clearable

Set `isClearable` on `ComboboxInput` to show a clear button that resets the selection.

```tsx
import {
  Combobox,
  ComboboxEmpty,
  ComboboxInput,
  ComboboxItem,
  ComboboxList,
  ComboboxPopup,
} from "@/components/ui/combobox";

const users = [
  { id: "u1", label: "Alice Johnson", value: "alice@example.com" },
  { id: "u2", label: "Bob Lee", value: "bob@example.com" },
  { id: "u3", label: "Cathy Kim", value: "cathy@example.com" },
];

type User = (typeof users)[number];

export function ComboboxClearableDemo() {
  return (
    <Combobox items={users}>
      <ComboboxInput placeholder="Select a user..." isClearable />
      <ComboboxPopup>
        <ComboboxEmpty>No users found.</ComboboxEmpty>
        <ComboboxList>
          {(user: User) => (
            <ComboboxItem key={user.id} value={user}>
              <div>
                <div className="font-medium">{user.label}</div>
                <div className="text-xs text-muted-foreground">
                  {user.value}
                </div>
              </div>
            </ComboboxItem>
          )}
        </ComboboxList>
      </ComboboxPopup>
    </Combobox>
  );
}
```

#### Input Inside Popup

Place the `ComboboxInput` inside the `ComboboxPopup` for a trigger-button-opens-search pattern. Use a `ComboboxTrigger` with a `Button` as the top-level control. Set `showTrigger={false}` on the `ComboboxInput` to avoid a duplicate trigger inside the popup.

```tsx
import {
  ChevronsUpDownIcon,
  Combobox,
  ComboboxEmpty,
  ComboboxInput,
  ComboboxItem,
  ComboboxList,
  ComboboxPopup,
  ComboboxTrigger,
  ComboboxValue,
} from "@/components/ui/combobox";
import { Button } from "@/components/ui/button";

interface Country {
  code: string;
  value: string | null;
  label: string;
}

const countries: Country[] = [
  { code: "", value: null, label: "Select country" },
  { code: "us", value: "united-states", label: "United States" },
  { code: "gb", value: "united-kingdom", label: "United Kingdom" },
  { code: "de", value: "germany", label: "Germany" },
];

export function ComboboxInputInsidePopupDemo() {
  return (
    <Combobox defaultValue={countries[0]} items={countries}>
      <ComboboxTrigger
        render={
          <Button
            className="w-full justify-between font-normal max-w-xs active:scale-100"
            variant="outline"
          />
        }
      >
        <ComboboxValue />
        <ChevronsUpDownIcon className="-me-1!" />
      </ComboboxTrigger>
      <ComboboxPopup aria-label="Select country" sideOffset={8}>
        <div className="border-b p-2">
          <ComboboxInput
            className="rounded-md"
            placeholder="e.g. United Kingdom"
            showTrigger={false}
          />
        </div>
        <ComboboxEmpty>No countries found.</ComboboxEmpty>
        <ComboboxList>
          {(country: Country) => (
            <ComboboxItem key={country.code} value={country}>
              {country.label}
            </ComboboxItem>
          )}
        </ComboboxList>
      </ComboboxPopup>
    </Combobox>
  );
}
```

#### Grouping Items

Use `ComboboxGroup`, `ComboboxGroupLabel`, `ComboboxCollection`, and `ComboboxSeparator` to organize items into labelled groups. Pass grouped data as the `items` array where each group contains a `value` (group name) and `items` (array of group members).

```tsx
import {
  Combobox,
  ComboboxCollection,
  ComboboxEmpty,
  ComboboxGroup,
  ComboboxGroupLabel,
  ComboboxInput,
  ComboboxItem,
  ComboboxList,
  ComboboxPopup,
  ComboboxSeparator,
} from "@/components/ui/combobox";
import { Fragment } from "react";

type Fruit = { id: string; name: string; label: string };
type FruitGroup = { value: string; items: Fruit[] };

const groups: FruitGroup[] = [
  {
    value: "Citrus",
    items: [
      { id: "orange", name: "Orange", label: "Orange" },
      { id: "lemon", name: "Lemon", label: "Lemon" },
    ],
  },
  {
    value: "Berry",
    items: [
      { id: "strawberry", name: "Strawberry", label: "Strawberry" },
      { id: "blueberry", name: "Blueberry", label: "Blueberry" },
    ],
  },
];

export function ComboboxGroupingDemo() {
  return (
    <Combobox
      items={groups}
      itemToStringLabel={(fruit: Fruit) => fruit.name}
    >
      <ComboboxInput placeholder="Search fruits..." />
      <ComboboxPopup>
        <ComboboxEmpty>No fruits found.</ComboboxEmpty>
        <ComboboxList>
          {(group: FruitGroup) => (
            <Fragment key={group.value}>
              <ComboboxGroup items={group.items}>
                <ComboboxGroupLabel>{group.value}</ComboboxGroupLabel>
                <ComboboxCollection>
                  {(fruit: Fruit) => (
                    <ComboboxItem key={fruit.id} value={fruit}>
                      {fruit.name}
                    </ComboboxItem>
                  )}
                </ComboboxCollection>
              </ComboboxGroup>
              <ComboboxSeparator />
            </Fragment>
          )}
        </ComboboxList>
      </ComboboxPopup>
    </Combobox>
  );
}
```

### Notes

- The `value` prop on `ComboboxItem` must match the type of the items array. For object items, pass the entire object.
- When using object items without a `label` property, you must provide `itemToStringLabel` on the `Combobox` root so the input can display the selected item as text.
- In multi-select mode, the `ComboboxInput` renders inside `ComboboxChips` alongside `ComboboxChip` elements. The popup anchors to the chips container.
- When placing `ComboboxInput` inside `ComboboxPopup`, set `showTrigger={false}` on the input to avoid duplicate triggers.
- The `ComboboxList` wraps a `ScrollArea` component internally for scrollable content with vertical scroll shadows.
- Base UI's `render` prop is the equivalent of Radix UI's `asChild` for polymorphic rendering.
