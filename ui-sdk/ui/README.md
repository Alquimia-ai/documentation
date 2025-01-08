# Alquimia-AI UI

Library with UI elements built with **React**, **TailwindCSS**, and **ShadCN**. This library follows the **Atomic Design** methodology to help you create modular and reusable components for **Alquimia AI** products.

## Overview

Alquimia UI provides a comprehensive set of React components designed for building web applications. Built with TypeScript and following best practices, it offers a flexible and maintainable solution for building **Alquimia AI** assistants.

## Key Features

- 🎨 **Atomic Design Structure**
  - Atoms: Basic building blocks (buttons, inputs, etc.)
  - Molecules: Compound components
  - Organisms: Complex UI patterns
  - Templates: Page-level layouts

- 🛠️ **Tech Stack**
  - React 18+
  - TypeScript
  - Tailwind CSS
  - Radix UI Primitives

- 📦 **Component Architecture**
  - Built on shadcn/ui standards
  - Fully typed components
  - Easily integrate into any React or Next.js project.

- 🎯 **Other Features**
  - Rich text components
  - Document viewers (PDF, Plain Text)
  - Custom hooks
  - Utility functions

## Quick Links

- [Getting Started](getting-started/installation.md)
- [Components](components/overview.md)
- [Styling](styling/styling.md)
- [API Reference](api-reference/types.md)

## Installation and quick start

```bash
# Using npm
npm install @alquimia-ai/ui

# Using yarn
yarn add @alquimia-ai/ui

# Using pnpm
pnpm add @alquimia-ai/ui
```

To use the components, you need to configure your Tailwind CSS configuration file.

```javascript
// tailwind.config.js

const baseConfig = require("@alquimia-ai/ui/tailwind.config")

module.exports = {
  content: [
    // Your code
    ...baseConfig.content,
  ],
  theme: {
    extend: {
      // Your customizations
    }
  }
}
```

Basic usage:

```tsx
import { Button } from "@alquimia-ai/ui/components/atoms"

const App = () => (
  <Button variant="default" size="lg">
    Click Me
  </Button>
);

export default App;

```

## Package Structure

```
@alquimia-ai/ui/
├── components/
│   ├── atoms/
│   ├── molecules/
│   ├── organisms/
│   └── templates/
├── hooks/
├── utils/
└── types/
```


## Styling System

Alquimia UI is built on top of Tailwind CSS, providing:

- Utility-first styling approach
- Customizable design tokens and classes
- Responsive design utilities
- Custom component classNames


## Component Standards

Built following shadcn/ui principles:

- Style with CSS variables
- Accessible/customizable semantic components

## Documentation Sections

- [Installation & Setup](getting-started/installation.md)
- [Component Library](components/overview.md)
  - [Atoms](components/atoms.md)
  - [Molecules](components/molecules.md)
  - [Organisms](components/organisms.md)
- [Styling Guide](styling/styling.md)
- [API Reference](api-reference/types.md)
  - [Types](api-reference/types.md)

## Related Links

- [Alquimia AI Website](https://alquimia.ai)
- [Alquimia AI Docs](https://alquimia.gitbook.io/alquimia-docs)
- [Radix UI](https://www.radix-ui.com/)
- [TailwindCSS](https://tailwindcss.com/)
- [ShadCN](https://ui.shadcn.com/)


## License

MIT © [Alquimia AI](LICENSE)

---

[Next: Getting Started →](getting-started/installation.md)


