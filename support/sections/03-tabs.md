## Tabs

A component for toggling between related panels on the same page. Each tab trigger switches the visible panel while an animated indicator tracks the active tab.

Built on `@base-ui/react/tabs`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/tabs"
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

3. Copy the component source into your project at `components/ui/tabs.tsx`.

### Anatomy

```tsx
import {
  Tabs,
  TabsList,
  TabsTrigger,
  TabsPanel,
  TabsPanelsWrapper,
} from "@/components/ui/tabs";

<Tabs defaultValue="tab-1">
  <TabsList>
    <TabsTrigger value="tab-1">Tab One</TabsTrigger>
    <TabsTrigger value="tab-2">Tab Two</TabsTrigger>
  </TabsList>
  <TabsPanel value="tab-1">Content for tab one</TabsPanel>
  <TabsPanel value="tab-2">Content for tab two</TabsPanel>
</Tabs>
```

`TabsPanelsWrapper` is optional. Use it to wrap `TabsPanel` elements when tab panels vary in height and you want animated height transitions between them.

### Props

#### Tabs

Root wrapper that provides variant context to all child components. Accepts all props from `@base-ui/react/tabs` Root.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| defaultValue | string \| number \| null | -- | Initial active tab value (uncontrolled) |
| value | string \| number \| null | -- | Controlled active tab value |
| onValueChange | (value: string \| number \| null) => void | -- | Called when the active tab changes |
| variant | "segmented" \| "underline" \| "card" | "segmented" | Visual style of the tabs |
| orientation | "horizontal" \| "vertical" | "horizontal" | Layout direction of the tab list |

#### TabsList

Container for tab triggers. Renders a Base UI `Tabs.List` with an animated `Tabs.Indicator` inside. Accepts all props from `@base-ui/react/tabs` List.

#### TabsTrigger

Individual tab button. Accepts all props from `@base-ui/react/tabs` Tab.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| value | string \| number | -- | Unique identifier matching a corresponding `TabsPanel` |

#### TabsPanel

Content area shown when its matching tab is active. Accepts all props from `@base-ui/react/tabs` Panel.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| value | string \| number | -- | Unique identifier matching a corresponding `TabsTrigger` |

#### TabsPanelsWrapper

Wrapper that uses a `ResizeObserver` to animate the height transition when switching between panels of different sizes. Does not accept additional props beyond `children`.

### Variants

#### variant

Values: `"segmented"` | `"underline"` | `"card"`
Default: `"segmented"`

- `"segmented"` -- tab list has a muted background with rounded corners; the active indicator is a card-like highlight behind the active trigger.
- `"underline"` -- no background on the list; the active indicator is a thin line along the bottom (horizontal) or side (vertical) edge.
- `"card"` -- similar to segmented but with a secondary background indicator and border.

```tsx
<Tabs defaultValue="tab-1" variant="underline">
  <TabsList>
    <TabsTrigger value="tab-1">Tab One</TabsTrigger>
    <TabsTrigger value="tab-2">Tab Two</TabsTrigger>
  </TabsList>
</Tabs>
```

```tsx
<Tabs defaultValue="tab-1" variant="card">
  <TabsList>
    <TabsTrigger value="tab-1">Tab One</TabsTrigger>
    <TabsTrigger value="tab-2">Tab Two</TabsTrigger>
  </TabsList>
</Tabs>
```

### Usage

#### Basic

```tsx
import { Tabs, TabsList, TabsTrigger } from "@/components/ui/tabs";

export function TabsDemo() {
  return (
    <Tabs defaultValue="docs">
      <TabsList>
        <TabsTrigger value="docs">Docs</TabsTrigger>
        <TabsTrigger value="components">Components</TabsTrigger>
        <TabsTrigger value="blocks">Blocks</TabsTrigger>
      </TabsList>
    </Tabs>
  );
}
```

#### With Panels

Use `TabsPanel` to render content associated with each tab.

```tsx
import {
  Tabs,
  TabsList,
  TabsTrigger,
  TabsPanel,
} from "@/components/ui/tabs";

export function TabsPanelDemo() {
  return (
    <Tabs defaultValue="docs">
      <TabsList>
        <TabsTrigger value="docs">Docs</TabsTrigger>
        <TabsTrigger value="components">Components</TabsTrigger>
        <TabsTrigger value="blocks">Blocks</TabsTrigger>
      </TabsList>
      <TabsPanel value="docs">
        <p>Documentation content here.</p>
      </TabsPanel>
      <TabsPanel value="components">
        <p>Components content here.</p>
      </TabsPanel>
      <TabsPanel value="blocks">
        <p>Blocks content here.</p>
      </TabsPanel>
    </Tabs>
  );
}
```

#### Animated Panel Height

When panel content varies in height, wrap all `TabsPanel` elements in `TabsPanelsWrapper` for smooth height transitions.

```tsx
import {
  Tabs,
  TabsList,
  TabsTrigger,
  TabsPanel,
  TabsPanelsWrapper,
} from "@/components/ui/tabs";

export function TabsAutoHeightDemo() {
  return (
    <Tabs defaultValue="docs">
      <TabsList>
        <TabsTrigger value="docs">Docs</TabsTrigger>
        <TabsTrigger value="components">Components</TabsTrigger>
        <TabsTrigger value="blocks">Blocks</TabsTrigger>
      </TabsList>
      <TabsPanelsWrapper>
        <TabsPanel value="docs">
          <p>Short content.</p>
        </TabsPanel>
        <TabsPanel value="components">
          <p>This panel has more content and is taller than the others.</p>
          <p>The wrapper animates the height change smoothly.</p>
        </TabsPanel>
        <TabsPanel value="blocks">
          <p>Another panel with different height.</p>
        </TabsPanel>
      </TabsPanelsWrapper>
    </Tabs>
  );
}
```

#### Vertical Orientation

Set `orientation="vertical"` to render the tab list and panels side by side. All three variants support vertical orientation.

```tsx
import { Tabs, TabsList, TabsTrigger } from "@/components/ui/tabs";

export function TabsVerticalDemo() {
  return (
    <Tabs defaultValue="docs" orientation="vertical" variant="segmented">
      <TabsList>
        <TabsTrigger value="docs">Docs</TabsTrigger>
        <TabsTrigger value="components">Components</TabsTrigger>
        <TabsTrigger value="blocks">Blocks</TabsTrigger>
      </TabsList>
    </Tabs>
  );
}
```

#### Triggers with Icons

Tab triggers accept children, so you can include icons alongside text.

```tsx
import { Tabs, TabsList, TabsTrigger } from "@/components/ui/tabs";
import { Code2, Layers, Box } from "lucide-react";

export function TabsWithIconsDemo() {
  return (
    <Tabs defaultValue="code" variant="underline">
      <TabsList>
        <TabsTrigger value="code">
          <Code2 />
          Code
        </TabsTrigger>
        <TabsTrigger value="layers">
          <Layers />
          Layers
        </TabsTrigger>
        <TabsTrigger value="blocks">
          <Box />
          Blocks
        </TabsTrigger>
      </TabsList>
    </Tabs>
  );
}
```

### Notes

- The tab indicator animates between triggers with a CSS transition on `translate` and `width`. The animation is driven by Base UI's `Tabs.Indicator` which tracks the active tab's position via CSS custom properties (`--active-tab-left`, `--active-tab-width`, `--active-tab-height`, `--active-tab-bottom`).
- Each `TabsTrigger` and `TabsPanel` must share the same `value` prop to link them together.
- In horizontal orientation the tab list scrolls horizontally on small screens (`overflow-x-auto`).
- SVG icons inside triggers are automatically sized to `1rem` via the `[&_svg]:size-4` utility class.
- Base UI's `render` prop is the equivalent of Radix UI's `asChild` for polymorphic rendering.
