## Avatar

Displays a user image with an automatic fallback for when the image is unavailable. Use avatars to represent users or entities in lists, cards, and headers.

Built on `@base-ui/react/avatar`.

### Installation

#### CLI

```bash
npx shadcn@latest add "https://pure.kam-ui.com/r/avatar"
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

3. Copy the component source into your project at `components/ui/avatar.tsx`.

### Anatomy

Avatar is a multi-part component with three sub-components.

```tsx
import { Avatar, AvatarImage, AvatarFallback } from "@/components/ui/avatar";

<Avatar>
  <AvatarImage src="/path/to/image.png" alt="User name" />
  <AvatarFallback>JD</AvatarFallback>
</Avatar>
```

`AvatarImage` renders the user photo. When the image fails to load or is missing, `AvatarFallback` is displayed instead. The fallback typically contains initials or an icon.

### Props

#### Avatar

Accepts all props from `@base-ui/react/avatar` `Root`.

No component-specific props. Size and border radius are controlled via `className`.

#### AvatarImage

Accepts all props from `@base-ui/react/avatar` `Image`.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| src | string | -- | URL of the avatar image |
| alt | string | -- | Accessible alternative text for the image |

#### AvatarFallback

Accepts all props from `@base-ui/react/avatar` `Fallback`.

No component-specific props. Pass text (e.g. initials) or a React node as children.

### Usage

#### Basic

```tsx
import { Avatar, AvatarImage, AvatarFallback } from "@/components/ui/avatar";

export function AvatarBasic() {
  return (
    <Avatar>
      <AvatarImage src="https://github.com/shadcn.png" alt="@shadcn" />
      <AvatarFallback>CN</AvatarFallback>
    </Avatar>
  );
}
```

#### Size

Avatar defaults to `size-10` (40px). Override the size by passing a Tailwind size class through `className`.

```tsx
import { Avatar, AvatarImage, AvatarFallback } from "@/components/ui/avatar";

export function AvatarSizes() {
  return (
    <div className="flex items-center gap-4">
      <Avatar>
        <AvatarImage alt="User" src="/avatars/user.png" />
        <AvatarFallback>AV</AvatarFallback>
      </Avatar>
      <Avatar className="size-12">
        <AvatarImage alt="User" src="/avatars/user.png" />
        <AvatarFallback>AV</AvatarFallback>
      </Avatar>
      <Avatar className="size-16">
        <AvatarImage alt="User" src="/avatars/user.png" />
        <AvatarFallback>AV</AvatarFallback>
      </Avatar>
    </div>
  );
}
```

#### Radius

Avatar defaults to `rounded-full` (circular). Override the border radius by passing a Tailwind radius class through `className`.

```tsx
import { Avatar, AvatarImage, AvatarFallback } from "@/components/ui/avatar";

export function AvatarRadius() {
  return (
    <div className="flex items-center gap-4">
      <Avatar className="rounded-none">
        <AvatarImage alt="User" src="/avatars/user.png" />
        <AvatarFallback>AV</AvatarFallback>
      </Avatar>
      <Avatar className="rounded-md">
        <AvatarImage alt="User" src="/avatars/user.png" />
        <AvatarFallback>AV</AvatarFallback>
      </Avatar>
      <Avatar className="rounded-xl">
        <AvatarImage alt="User" src="/avatars/user.png" />
        <AvatarFallback>AV</AvatarFallback>
      </Avatar>
      <Avatar className="rounded-full">
        <AvatarImage alt="User" src="/avatars/user.png" />
        <AvatarFallback>AV</AvatarFallback>
      </Avatar>
    </div>
  );
}
```

#### Grouping

Stack avatars by applying negative horizontal spacing and a ring to each avatar.

```tsx
import { Avatar, AvatarImage, AvatarFallback } from "@/components/ui/avatar";

export function AvatarGrouping() {
  return (
    <div className="-space-x-[0.6rem] flex">
      <Avatar className="ring-2 ring-background">
        <AvatarImage alt="U1" src="/avatars/user1.png" />
        <AvatarFallback>U1</AvatarFallback>
      </Avatar>
      <Avatar className="ring-2 ring-background">
        <AvatarImage alt="U2" src="/avatars/user2.png" />
        <AvatarFallback>U2</AvatarFallback>
      </Avatar>
      <Avatar className="ring-2 ring-background">
        <AvatarImage alt="U3" src="/avatars/user3.png" />
        <AvatarFallback>U3</AvatarFallback>
      </Avatar>
    </div>
  );
}
```

### Notes

- Each sub-component sets a `data-slot` attribute (`"avatar"`, `"avatar-image"`, `"avatar-fallback"`) that can be used for parent-level styling with Tailwind's `*:data-[slot=avatar]:` selector.
- Size and radius have no dedicated props. Control them entirely through Tailwind utility classes on the `Avatar` root via `className`.
- `AvatarFallback` is shown automatically by Base UI when the image has not loaded or fails to load. No manual visibility logic is needed.
