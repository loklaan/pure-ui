## Toast

Displays transient popup messages to inform users of status changes, errors, or successful actions. Toasts stack, animate in and out, support swipe-to-dismiss, and expand on hover.

Built on `@base-ui/react/toast`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/toast"
```

After installing, add the `ToastProvider` to your root layout:

```tsx
import { ToastProvider } from "@/components/ui/toast";

export default function RootLayout({
  children,
}: Readonly<{
  children: React.ReactNode;
}>) {
  return (
    <html lang="en">
      <head />
      <body>
        <ToastProvider>
          <main>{children}</main>
        </ToastProvider>
      </body>
    </html>
  );
}
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

3. Copy the component source into your project at `components/ui/toast.tsx`.

4. Add the `ToastProvider` to your root layout (see CLI section above).

### Anatomy

```tsx
import { ToastProvider, toast } from "@/components/ui/toast";

<ToastProvider position="bottom-right">
  {children}
</ToastProvider>
```

The component has two exports:

- `ToastProvider` -- wraps your app and renders the toast viewport. Place it once near the root of your component tree.
- `toast` -- a singleton toast manager instance. Call its methods from anywhere to create toasts.

Toast rendering (viewport, portal, individual toast roots, content, icons, actions) is handled internally by `ToastProvider`. There are no separate sub-components to compose.

### Props

#### ToastProvider

Accepts all props from `@base-ui/react/toast` Provider.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| position | "top-left" \| "top-center" \| "top-right" \| "bottom-left" \| "bottom-center" \| "bottom-right" | "bottom-right" | Screen corner where toasts appear |

### Toast Manager API

The exported `toast` object is created via `Toast.createToastManager()`. Use it to create, update, and dismiss toasts imperatively.

#### toast.add(options)

Creates a toast and returns its id.

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| title | string | -- | Toast heading text |
| description | string | -- | Secondary descriptive text |
| type | "success" \| "error" \| "info" \| "warning" \| "loading" | -- | Determines the status icon shown beside the title |
| timeout | number | -- | Auto-dismiss delay in milliseconds |
| actionProps | object | -- | Props for an action button (includes `children` and `onClick`) |
| data | { radius?: "none" \| "sm" \| "md" \| "lg" \| "full" } | { radius: "md" } | Custom data; `radius` controls border radius |

#### toast.close(id)

Dismisses the toast with the given id.

#### toast.promise(promise, options)

Tracks a promise through loading, success, and error states, transitioning the toast automatically.

| Option | Type | Description |
|--------|------|-------------|
| loading | { title: string; description?: string } | Content shown while the promise is pending |
| success | (data) => { title: string; description?: string } | Content shown when the promise resolves |
| error | (error) => { title: string; description?: string } | Content shown when the promise rejects |

### Usage

#### Basic

```tsx
"use client";

import { Button } from "@/components/ui/button";
import { toast } from "@/components/ui/toast";

export function ToastBasicExample() {
  return (
    <Button
      variant="outline"
      onClick={() => {
        toast.add({
          title: "Event has been created",
        });
      }}
    >
      Show Toast
    </Button>
  );
}
```

#### With Description

```tsx
"use client";

import { Button } from "@/components/ui/button";
import { toast } from "@/components/ui/toast";

export function ToastDescriptionExample() {
  return (
    <Button
      variant="outline"
      onClick={() => {
        toast.add({
          title: "Event has been created",
          description: "Monday, January 3rd at 6:00pm",
        });
      }}
    >
      With Description
    </Button>
  );
}
```

#### With Status

Set the `type` field to display a status icon. Supported types: `"success"`, `"error"`, `"info"`, `"warning"`.

```tsx
"use client";

import { Button } from "@/components/ui/button";
import { toast } from "@/components/ui/toast";

export function ToastWithStatusExample() {
  return (
    <div className="flex flex-wrap gap-2">
      <Button
        variant="outline"
        onClick={() => {
          toast.add({
            title: "Success!",
            description: "Your changes have been saved.",
            type: "success",
          });
        }}
      >
        Success Toast
      </Button>
      <Button
        variant="outline"
        onClick={() => {
          toast.add({
            title: "Uh oh! Something went wrong.",
            description: "There was a problem with your request.",
            type: "error",
          });
        }}
      >
        Error Toast
      </Button>
      <Button
        variant="outline"
        onClick={() => {
          toast.add({
            title: "Heads up!",
            description: "You can add components to your app using the cli.",
            type: "info",
          });
        }}
      >
        Info Toast
      </Button>
      <Button
        variant="outline"
        onClick={() => {
          toast.add({
            title: "Warning!",
            description: "Your session is about to expire.",
            type: "warning",
          });
        }}
      >
        Warning Toast
      </Button>
    </div>
  );
}
```

#### Loading

Set `type` to `"loading"` to display a spinner icon.

```tsx
"use client";

import { Button } from "@/components/ui/button";
import { toast } from "@/components/ui/toast";

export function ToastLoadingExample() {
  return (
    <Button
      variant="outline"
      onClick={() => {
        toast.add({
          title: "Loading...",
          description: "Please wait while we process your request.",
          type: "loading",
          timeout: 3000,
        });
      }}
    >
      Loading Toast
    </Button>
  );
}
```

#### Action

Pass `actionProps` to add a button to the toast. The `children` property sets the button label.

```tsx
"use client";

import { Button } from "@/components/ui/button";
import { toast } from "@/components/ui/toast";

export function ToastActionExample() {
  return (
    <Button
      variant="outline"
      onClick={() => {
        const id = toast.add({
          title: "Action performed",
          description: "You can undo this action.",
          type: "success",
          actionProps: {
            children: "Undo",
            onClick: () => {
              toast.close(id);
              toast.add({
                title: "Action undone",
                description: "The action has been reverted.",
                type: "info",
              });
            },
          },
        });
      }}
    >
      Perform Action
    </Button>
  );
}
```

#### Promise

Use `toast.promise()` to track a promise through its lifecycle. The toast transitions from loading to success or error automatically.

```tsx
"use client";

import { Button } from "@/components/ui/button";
import { toast } from "@/components/ui/toast";

export function ToastPromiseExample() {
  return (
    <Button
      variant="outline"
      onClick={() => {
        toast.promise(
          new Promise<string>((resolve, reject) => {
            const shouldSucceed = Math.random() > 0.3;
            setTimeout(() => {
              if (shouldSucceed) {
                resolve("Data loaded successfully");
              } else {
                reject(new Error("Failed to load data"));
              }
            }, 2000);
          }),
          {
            loading: {
              title: "Loading...",
              description: "The promise is loading.",
            },
            success: (data: string) => ({
              title: "This is a success toast!",
              description: `Success: ${data}`,
            }),
            error: () => ({
              title: "Something went wrong",
              description: "Please try again.",
            }),
          }
        );
      }}
    >
      Run Promise
    </Button>
  );
}
```

#### Radius

Control the border radius of individual toasts by passing `radius` in the `data` field.

Values: `"none"` | `"sm"` | `"md"` | `"lg"` | `"full"`
Default: `"md"`

```tsx
"use client";

import { Button } from "@/components/ui/button";
import { toast } from "@/components/ui/toast";

export function ToastRadiusExample() {
  return (
    <Button
      variant="outline"
      onClick={() =>
        toast.add({
          title: "Toast title",
          description: "Toast displayed successfully",
          data: {
            radius: "lg",
          },
        })
      }
    >
      Large Radius
    </Button>
  );
}
```

#### Position

Set the `position` prop on `ToastProvider` to control where toasts appear on screen.

Values: `"top-left"` | `"top-center"` | `"top-right"` | `"bottom-left"` | `"bottom-center"` | `"bottom-right"`
Default: `"bottom-right"`

```tsx
<ToastProvider position="top-center">
  {children}
</ToastProvider>
```

### Notes

- `ToastProvider` must wrap your application for toasts to render. Place it once in your root layout.
- The `toast` export is a singleton manager. Import it from `"@/components/ui/toast"` in any client component to create toasts without prop drilling.
- Toasts stack visually and expand on hover to reveal overlapping items.
- Swipe-to-dismiss direction is determined by the `position` value: side-positioned toasts dismiss toward their edge, center-positioned toasts dismiss up or down.
- The action button uses the `Button` component's `xs` size variant internally.
- The loading spinner uses the `Spinner` component internally.
- This is a client component (`"use client"`). The `toast` manager must be called from client-side code.
