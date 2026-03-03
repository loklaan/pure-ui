## Theming

Pure UI uses CSS custom properties (variables) for theming. All colors are defined in the OKLCh color space and organized into semantic tokens. Light and dark modes are handled by redefining the same variables under a `.dark` class.

### How It Works

The theming system is built on Tailwind CSS v4's theme configuration. The setup involves three layers in your global CSS file:

1. **`:root` block** -- defines light mode color values as CSS custom properties.
2. **`.dark` block** -- redefines the same properties for dark mode.
3. **`@theme inline` block** -- maps custom properties to Tailwind's theme namespace so they can be used as utility classes (e.g., `bg-primary`, `text-muted-foreground`).

Dark mode is activated by applying the `dark` class to a parent element (typically the `html` or `body` tag). The custom variant is declared as:

```css
@custom-variant dark (&:is(.dark *));
```

### Color Space: OKLCh

All color values use the `oklch()` function. OKLCh is a perceptually uniform color space with three channels:

- **L** -- Lightness (0 to 1)
- **C** -- Chroma (0 to ~0.4, saturation)
- **h** -- Hue angle (0 to 360)

Example: `oklch(0.637 0.237 25.331)` is a red used for the destructive color.

Some variables use alpha transparency via the `oklch(L C h / alpha%)` syntax (e.g., `oklch(0 0 0 / 10%)` for borders in light mode).

### Naming Convention

Variables follow a semantic naming pattern with background/foreground pairing:

- A variable without a suffix is a **background** color (e.g., `--accent`).
- A variable with `-foreground` is the **text** color intended to sit on that background (e.g., `--accent-foreground`).

Use the matching pair together to guarantee readable contrast:

```tsx
<div className="bg-accent text-accent-foreground">Readable text</div>
```

### The `@theme inline` Directive

The `@theme inline` block bridges CSS custom properties to Tailwind CSS v4's theme system. Each mapping follows the pattern:

```css
--color-{name}: var(--{name});
```

This allows Tailwind utility classes like `bg-primary`, `text-muted-foreground`, and `border-border` to resolve to the CSS variables. Without this block, Tailwind would not recognize the custom color names.

The `inline` keyword tells Tailwind to inline the variable references rather than generating static values, so the colors remain reactive to the `:root` / `.dark` context at runtime.

### CSS Variables Reference

#### Base Radius

| Variable | Default | Description |
|----------|---------|-------------|
| --radius | 0.625rem | Base radius value used to derive all radius tokens |

The `@theme inline` block derives four radius tokens from this single base value:

| Tailwind Token | Derivation | Description |
|----------------|------------|-------------|
| --radius-sm | calc(var(--radius) - 4px) | Small radius |
| --radius-md | calc(var(--radius) - 2px) | Medium radius |
| --radius-lg | var(--radius) | Large radius (equal to base) |
| --radius-xl | calc(var(--radius) + 4px) | Extra-large radius |

Use via Tailwind utilities: `rounded-sm`, `rounded-md`, `rounded-lg`, `rounded-xl`.

#### UI Colors

| Variable | Light Value | Dark Value | Purpose |
|----------|-------------|------------|---------|
| --background | oklch(1 0 0) | oklch(0.141 0.005 285.823) | Page background |
| --foreground | oklch(0.21 0.006 285.885) | oklch(0.967 0.001 286.375) | Default text color |
| --card | oklch(1 0 0) | color-mix(in srgb, oklch(0.21 0.006 285.885) 80%, oklch(0.141 0.005 285.823)) | Card background |
| --card-foreground | oklch(0.21 0.006 285.885) | oklch(0.967 0.001 286.375) | Card text color |
| --popover | oklch(1 0 0) | oklch(0.21 0.006 285.885) | Popover/dropdown background |
| --popover-foreground | oklch(0.21 0.006 285.885) | oklch(0.967 0.001 286.375) | Popover text color |
| --primary | oklch(0.274 0.006 286.033) | oklch(0.967 0.001 286.375) | Primary action background |
| --primary-foreground | oklch(0.985 0 0) | oklch(0.21 0.006 285.885) | Primary action text |
| --secondary | oklch(0 0 0 / 4%) | oklch(1 0 0 / 6%) | Secondary action background |
| --secondary-foreground | oklch(0.21 0.006 285.885) | oklch(0.967 0.001 286.375) | Secondary action text |
| --muted | oklch(0 0 0 / 4%) | oklch(1 0 0 / 6%) | Muted/subtle background |
| --muted-foreground | oklch(0.442 0.017 285.786) | oklch(0.705 0.015 286.067) | Muted/subtle text |
| --accent | oklch(0 0 0 / 4%) | oklch(1 0 0 / 6%) | Accent/hover background |
| --accent-foreground | oklch(0.21 0.006 285.885) | oklch(0.967 0.001 286.375) | Accent text |
| --destructive | oklch(0.637 0.237 25.331) | oklch(0.637 0.237 25.331) | Destructive/danger background |
| --destructive-foreground | oklch(0.505 0.213 27.518) | oklch(0.704 0.191 22.216) | Destructive text |
| --info | oklch(0.623 0.214 259.815) | oklch(0.623 0.214 259.815) | Informational background |
| --info-foreground | oklch(0.488 0.243 264.376) | oklch(0.707 0.165 254.624) | Informational text |
| --success | oklch(0.696 0.17 162.48) | oklch(0.696 0.17 162.48) | Success background |
| --success-foreground | oklch(0.508 0.118 165.612) | oklch(0.765 0.177 163.223) | Success text |
| --warning | oklch(0.769 0.188 70.08) | oklch(0.769 0.188 70.08) | Warning background |
| --warning-foreground | oklch(0.555 0.163 48.998) | oklch(0.828 0.189 84.429) | Warning text |
| --border | oklch(0 0 0 / 10%) | oklch(1 0 0 / 12%) | Default border color |
| --input | oklch(0 0 0 / 10%) | oklch(1 0 0 / 12%) | Input field border color |
| --ring | oklch(0.705 0.015 286.067) | oklch(0.552 0.016 285.938) | Focus ring color |

#### Chart Colors

Five chart colors for data visualization:

| Variable | Light Value | Dark Value |
|----------|-------------|------------|
| --chart-1 | oklch(0.646 0.222 41.116) | oklch(0.488 0.243 264.376) |
| --chart-2 | oklch(0.6 0.118 184.704) | oklch(0.696 0.17 162.48) |
| --chart-3 | oklch(0.398 0.07 227.392) | oklch(0.769 0.188 70.08) |
| --chart-4 | oklch(0.828 0.189 84.429) | oklch(0.627 0.265 303.9) |
| --chart-5 | oklch(0.769 0.188 70.08) | oklch(0.645 0.246 16.439) |

#### Sidebar Colors

| Variable | Light Value | Dark Value | Purpose |
|----------|-------------|------------|---------|
| --sidebar | oklch(0.985 0 0) | color-mix(in srgb, oklch(0.21 0.006 285.885) 32%, oklch(0.141 0.005 285.823)) | Sidebar background |
| --sidebar-foreground | oklch(0.21 0.006 285.885) | oklch(0.967 0.001 286.375) | Sidebar text |
| --sidebar-primary | oklch(0.274 0.006 286.033) | oklch(0.967 0.001 286.375) | Sidebar primary action |
| --sidebar-primary-foreground | oklch(0.985 0 0) | oklch(0.21 0.006 285.885) | Sidebar primary text |
| --sidebar-accent | oklch(0 0 0 / 4%) | oklch(1 0 0 / 8%) | Sidebar accent/hover |
| --sidebar-accent-foreground | oklch(0.21 0.006 285.885) | oklch(0.967 0.001 286.375) | Sidebar accent text |
| --sidebar-border | oklch(0 0 0 / 10%) | oklch(1 0 0 / 12%) | Sidebar border |
| --sidebar-ring | oklch(0.705 0.015 286.067) | oklch(0.705 0.015 286.067) | Sidebar focus ring |

### Base Layer Defaults

The `@layer base` block applies default styles globally:

```css
@layer base {
  * {
    @apply border-border outline-ring/50;
  }
  body {
    @apply bg-background text-foreground;
  }
}
```

All elements default to `border-border` for border color and `outline-ring/50` for outline color. The body uses `bg-background` and `text-foreground`.

### Customizing Colors

To customize the theme, override the CSS variables in your `globals.css` file. Change values in both `:root` (light) and `.dark` (dark) blocks.

**Change the primary color:**

```css
:root {
  --primary: oklch(0.6 0.2 260);
  --primary-foreground: oklch(0.98 0 0);
}

.dark {
  --primary: oklch(0.7 0.18 260);
  --primary-foreground: oklch(0.15 0 0);
}
```

**Change the border radius globally:**

```css
:root {
  --radius: 0.5rem;
}
```

All radius tokens (`--radius-sm`, `--radius-md`, `--radius-lg`, `--radius-xl`) derive from this single value, so changing `--radius` adjusts the entire radius scale.

**Add a custom semantic color:**

To add a color that works with Tailwind utilities, define the variable and add the `@theme inline` mapping:

```css
:root {
  --brand: oklch(0.65 0.2 145);
  --brand-foreground: oklch(0.98 0 0);
}

.dark {
  --brand: oklch(0.55 0.18 145);
  --brand-foreground: oklch(0.15 0 0);
}

@theme inline {
  --color-brand: var(--brand);
  --color-brand-foreground: var(--brand-foreground);
}
```

This makes `bg-brand`, `text-brand-foreground`, and other Tailwind color utilities available.

### Full CSS Variables Block

The complete CSS setup for your `globals.css`:

```css
@import "tailwindcss";
@import "tw-animate-css";

@custom-variant dark (&:is(.dark *));

:root {
  --radius: 0.625rem;
  --background: oklch(1 0 0);
  --foreground: oklch(0.21 0.006 285.885);
  --card: oklch(1 0 0);
  --card-foreground: oklch(0.21 0.006 285.885);
  --popover: oklch(1 0 0);
  --popover-foreground: oklch(0.21 0.006 285.885);
  --primary: oklch(0.274 0.006 286.033);
  --primary-foreground: oklch(0.985 0 0);
  --secondary: oklch(0 0 0 / 4%);
  --secondary-foreground: oklch(0.21 0.006 285.885);
  --muted: oklch(0 0 0 / 4%);
  --muted-foreground: oklch(0.442 0.017 285.786);
  --accent: oklch(0 0 0 / 4%);
  --accent-foreground: oklch(0.21 0.006 285.885);
  --destructive: oklch(0.637 0.237 25.331);
  --destructive-foreground: oklch(0.505 0.213 27.518);
  --info: oklch(0.623 0.214 259.815);
  --info-foreground: oklch(0.488 0.243 264.376);
  --success: oklch(0.696 0.17 162.48);
  --success-foreground: oklch(0.508 0.118 165.612);
  --warning: oklch(0.769 0.188 70.08);
  --warning-foreground: oklch(0.555 0.163 48.998);
  --border: oklch(0 0 0 / 10%);
  --input: oklch(0 0 0 / 10%);
  --ring: oklch(0.705 0.015 286.067);
  --chart-1: oklch(0.646 0.222 41.116);
  --chart-2: oklch(0.6 0.118 184.704);
  --chart-3: oklch(0.398 0.07 227.392);
  --chart-4: oklch(0.828 0.189 84.429);
  --chart-5: oklch(0.769 0.188 70.08);
  --sidebar: oklch(0.985 0 0);
  --sidebar-foreground: oklch(0.21 0.006 285.885);
  --sidebar-primary: oklch(0.274 0.006 286.033);
  --sidebar-primary-foreground: oklch(0.985 0 0);
  --sidebar-accent: oklch(0 0 0 / 4%);
  --sidebar-accent-foreground: oklch(0.21 0.006 285.885);
  --sidebar-border: oklch(0 0 0 / 10%);
  --sidebar-ring: oklch(0.705 0.015 286.067);
}

.dark {
  --background: oklch(0.141 0.005 285.823);
  --foreground: oklch(0.967 0.001 286.375);
  --card: color-mix(
    in srgb,
    oklch(0.21 0.006 285.885) 80%,
    oklch(0.141 0.005 285.823)
  );
  --card-foreground: oklch(0.967 0.001 286.375);
  --popover: oklch(0.21 0.006 285.885);
  --popover-foreground: oklch(0.967 0.001 286.375);
  --primary: oklch(0.967 0.001 286.375);
  --primary-foreground: oklch(0.21 0.006 285.885);
  --secondary: oklch(1 0 0 / 6%);
  --secondary-foreground: oklch(0.967 0.001 286.375);
  --muted: oklch(1 0 0 / 6%);
  --muted-foreground: oklch(0.705 0.015 286.067);
  --accent: oklch(1 0 0 / 6%);
  --accent-foreground: oklch(0.967 0.001 286.375);
  --destructive: oklch(0.637 0.237 25.331);
  --destructive-foreground: oklch(0.704 0.191 22.216);
  --info: oklch(0.623 0.214 259.815);
  --info-foreground: oklch(0.707 0.165 254.624);
  --success: oklch(0.696 0.17 162.48);
  --success-foreground: oklch(0.765 0.177 163.223);
  --warning: oklch(0.769 0.188 70.08);
  --warning-foreground: oklch(0.828 0.189 84.429);
  --border: oklch(1 0 0 / 12%);
  --input: oklch(1 0 0 / 12%);
  --ring: oklch(0.552 0.016 285.938);
  --chart-1: oklch(0.488 0.243 264.376);
  --chart-2: oklch(0.696 0.17 162.48);
  --chart-3: oklch(0.769 0.188 70.08);
  --chart-4: oklch(0.627 0.265 303.9);
  --chart-5: oklch(0.645 0.246 16.439);
  --sidebar: color-mix(
    in srgb,
    oklch(0.21 0.006 285.885) 32%,
    oklch(0.141 0.005 285.823)
  );
  --sidebar-foreground: oklch(0.967 0.001 286.375);
  --sidebar-primary: oklch(0.967 0.001 286.375);
  --sidebar-primary-foreground: oklch(0.21 0.006 285.885);
  --sidebar-accent: oklch(1 0 0 / 8%);
  --sidebar-accent-foreground: oklch(0.967 0.001 286.375);
  --sidebar-border: oklch(1 0 0 / 12%);
  --sidebar-ring: oklch(0.705 0.015 286.067);
}

@theme inline {
  --color-background: var(--background);
  --color-foreground: var(--foreground);
  --color-card: var(--card);
  --color-card-foreground: var(--card-foreground);
  --color-popover: var(--popover);
  --color-popover-foreground: var(--popover-foreground);
  --color-primary: var(--primary);
  --color-primary-foreground: var(--primary-foreground);
  --color-secondary: var(--secondary);
  --color-secondary-foreground: var(--secondary-foreground);
  --color-muted: var(--muted);
  --color-muted-foreground: var(--muted-foreground);
  --color-accent: var(--accent);
  --color-accent-foreground: var(--accent-foreground);
  --color-destructive: var(--destructive);
  --color-destructive-foreground: var(--destructive-foreground);
  --color-info: var(--info);
  --color-info-foreground: var(--info-foreground);
  --color-success: var(--success);
  --color-success-foreground: var(--success-foreground);
  --color-warning: var(--warning);
  --color-warning-foreground: var(--warning-foreground);
  --color-border: var(--border);
  --color-input: var(--input);
  --color-ring: var(--ring);
  --color-chart-1: var(--chart-1);
  --color-chart-2: var(--chart-2);
  --color-chart-3: var(--chart-3);
  --color-chart-4: var(--chart-4);
  --color-chart-5: var(--chart-5);
  --color-sidebar: var(--sidebar);
  --color-sidebar-foreground: var(--sidebar-foreground);
  --color-sidebar-primary: var(--sidebar-primary);
  --color-sidebar-primary-foreground: var(--sidebar-primary-foreground);
  --color-sidebar-accent: var(--sidebar-accent);
  --color-sidebar-accent-foreground: var(--sidebar-accent-foreground);
  --color-sidebar-border: var(--sidebar-border);
  --color-sidebar-ring: var(--sidebar-ring);
  --radius-sm: calc(var(--radius) - 4px);
  --radius-md: calc(var(--radius) - 2px);
  --radius-lg: var(--radius);
  --radius-xl: calc(var(--radius) + 4px);
}

@layer base {
  * {
    @apply border-border outline-ring/50;
  }
  body {
    @apply bg-background text-foreground;
  }
}
```
