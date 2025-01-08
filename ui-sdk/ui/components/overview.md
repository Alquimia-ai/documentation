# Components Overview

Alquimia UI follows the Atomic Design methodology, organizing components into a hierarchical structure that promotes reusability and maintainability.

## Component Structure

```
components/
├── atoms/        # Basic building blocks
├── molecules/    # Compound components
├── organisms/    # Complex UI patterns
└── templates/    # Page-level layouts
```

## Atomic Design Hierarchy

### Atoms
Fundamental building blocks of the interface. These are the smallest possible components that can be reused.

```typescript
import { Button } from '@alquimia-ai/ui/components/atoms'
import { Input } from '@alquimia-ai/ui/components/atoms'
```

Available components:
- Input
- Select
- Avatar
- ScrollArea
- Dialog
- Tabs
- Button
- Checkbox
- Label
- Switch
- Toggle
- Tooltip

### Molecules
Combinations of atoms that form more complex components.

```typescript
import { PdfViewer } from '@alquimia-ai/ui/components/molecules/viewers'
import { DocumentViewer } from '@alquimia-ai/ui/components/molecules/documents'
```

Available components:
- Document Viewers
  - PDF Viewer
  - Plain Text Viewer
- Rich Text Components
- Navigation Menu
- Toast Notifications

### Organisms
Complex UI components composed of molecules and/or atoms.

```typescript
import { Whisper, SpeechToText } from "@alquimia-ai/ui/components/organisms";
```

Available components:
- Complex Forms
- Data Tables
- Navigation Systems
- Document Management Interfaces

## Component Standards

All components follow shadcn's standards and are built with:

- Chat Assistant and document viewer oriented components
- Radix UI primitives for accessibility
- Tailwind CSS for styling
- TypeScript for type safety
- CSS variables for theming

## Styling System

Components use a consistent styling approach:

```typescript
import { cn } from '@alquimia-ai/ui/lib/utils'

// Example of component styling
const Component = ({ className, ...props }) => {
  return (
    <div
      className={cn(
        "base-styles",
        "variant-styles",
        className,
        "alq--component-name" // this is a fixed class based on the component name
      )}
      {...props}
    />
  )
}
```

## Dependencies

Our components are built with the following core dependencies:

```json
{
  "@radix-ui/react-*": "^1.x.x",
  "class-variance-authority": "^0.7.0",
  "tailwind-merge": "^2.5.2",
  "tailwindcss-animate": "^1.0.7",
  "pdfjs-dist": "4.4.168",
  "react-pdf": "9.1.1",
  "lucide-react": "^0.436.0"
}
```

## Usage Example

```tsx
import { Button } from '@alquimia-ai/ui/components/atoms'
import {
  CallOut,
  CallOutActions,
  CallOutMessage,
  CallOutResponse,
  CallOutDate,
} from "@alquimia-ai/ui/components/molecules";

function MyComponent() {
  return (
    <div>
        <Button variant="default">
            Click me
        </Button>
        <CallOut key={index} role={message.role} message={message}>
        <div>
            <CallOutDate className="text-sm text-gray-500 mx-2 pb-1">
            {message.timestamp.toLocaleString("en-GB", {
                day: "2-digit",
                month: "2-digit",
                year: "numeric",
                hour: "2-digit",
                minute: "2-digit",
                second: "2-digit",
            })}
            </CallOutDate>
            <CallOutResponse role={message.role}>
            {message.content}
            </CallOutResponse>
            <CallOutActions actions={baseActions} role={message.role} />
        </div>
        </CallOut>
    </div>
  )
}
```

## Next Steps

- [Explore Atoms](./atoms.md)
- [Explore Molecules](./molecules.md)
- [Explore Organisms](./organisms.md)
- [Styling Guide](../styling/styling.md)