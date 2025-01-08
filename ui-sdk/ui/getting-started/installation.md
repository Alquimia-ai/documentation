# Installation

This guide will help you set up Alquimia UI in your project.

## Prerequisites

Before installing Alquimia UI, ensure you have the following dependencies:

```bash
npm install react react-dom tailwindcss postcss autoprefixer
```

## Installing Alquimia UI

1. Install the Alquimia UI package:

```bash
npm install @alquimia-ai/ui

# or with yarn
yarn add @alquimia-ai/ui

# or with pnpm
pnpm add @alquimia-ai/ui
```

2. Install required dependencies:

```bash
npm install tailwind-merge tailwindcss-animate tsparticles-engine
```

## Configuration

### 1. Tailwind CSS Setup

Create or update your `tailwind.config.js`:

```javascript
const baseConfig = require("@alquimia-ai/ui/tailwind.config")

/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./app/**/*.{js,ts,jsx,tsx,mdx}",
    "./pages/**/*.{js,ts,jsx,tsx,mdx}",
    "./components/**/*.{js,ts,jsx,tsx,mdx}",
    ...baseConfig.content,
  ],
  theme: {
    extend: {
      // Your custom theme extensions
    },
  },
  plugins: [
    require("tailwindcss-animate"),
    // Your other plugins
  ],
}
```

### 2. CSS Setup

If you dont't have a global CSS file, add the following to your global CSS file:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 222.2 84% 4.9%;

    --card: 0 0% 100%;
    --card-foreground: 222.2 84% 4.9%;
 
    --popover: 0 0% 100%;
    --popover-foreground: 222.2 84% 4.9%;
 
    --primary: 222.2 47.4% 11.2%;
    --primary-foreground: 210 40% 98%;
 
    --secondary: 210 40% 96.1%;
    --secondary-foreground: 222.2 47.4% 11.2%;
 
    --muted: 210 40% 96.1%;
    --muted-foreground: 215.4 16.3% 46.9%;
 
    --accent: 210 40% 96.1%;
    --accent-foreground: 222.2 47.4% 11.2%;
 
    --destructive: 0 84.2% 60.2%;
    --destructive-foreground: 210 40% 98%;

    --border: 214.3 31.8% 91.4%;
    --input: 214.3 31.8% 91.4%;
    --ring: 222.2 84% 4.9%;
 
    --radius: 0.5rem;
  }
 
  .dark {
    --background: 222.2 84% 4.9%;
    --foreground: 210 40% 98%;
 
    --card: 222.2 84% 4.9%;
    --card-foreground: 210 40% 98%;
 
    --popover: 222.2 84% 4.9%;
    --popover-foreground: 210 40% 98%;
 
    --primary: 210 40% 98%;
    --primary-foreground: 222.2 47.4% 11.2%;
 
    --secondary: 217.2 32.6% 17.5%;
    --secondary-foreground: 210 40% 98%;
 
    --muted: 217.2 32.6% 17.5%;
    --muted-foreground: 215 20.2% 65.1%;
 
    --accent: 217.2 32.6% 17.5%;
    --accent-foreground: 210 40% 98%;
 
    --destructive: 0 62.8% 30.6%;
    --destructive-foreground: 210 40% 98%;
 
    --border: 217.2 32.6% 17.5%;
    --input: 217.2 32.6% 17.5%;
    --ring: 212.7 26.8% 83.9%;
  }
}
```

## Usage Example

You can use atomic component types such as atoms, molecules, organisms, to build your own components. This specific set of components is oriented to build products for **Alquimia AI**.

```tsx
import { Button } from '@alquimia-ai/ui/components/atoms'

export default function App() {
  return (
    <div>
      <Button variant="default">Click me</Button>
    </div>
  )
}
```

All components are typed and available in the [Components](../components/overview.md) section.

## Next Steps

- Check out our [Components](../components/overview.md) documentation
- Learn about our [Styling System](../styling/styling.md)
- Explore [Examples](../examples/basic-usage.md)