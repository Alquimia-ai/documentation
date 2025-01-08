# Alquimia-AI Tools

Library providing essential SDK functionality, hooks, and utilities for building **Alquimia AI** applications. This library serves as the core integration layer for AI-powered chat assistants. Its core components are the SDK and the useAlquimia hook, which are used to manage the assitant interactions, along with the UI components.

## Overview

Alquimia Tools provides a comprehensive SDK and React UI components designed for building AI-powered chat assistants. Built with TypeScript and following best practices, it offers a flexible and maintainable solution for integrating **Alquimia AI** capabilities.

## Key Features

- 🔧 **Core SDK**
  - AI Service Integration
  - Message Management
  - Streaming Support
  - Provider System

- 🎣 **React Integration**
  - Custom Hooks
  - State Management
  - Real-time Updates
  - TypeScript Support

- 🛠️ **Tech Stack**
  - Next.js 14+
  - React 18+
  - TypeScript 5.3+

- 🎯 **Other Features**
  - Speech-to-Text (Whisper)
  - Image Generation
  - Content Analysis
  - Feedback Collection
  - Logging System

## Quick Links

- [Getting Started](#installation)
- [SDK Reference](#sdk-configuration)
- [Hooks Reference](#main-hook-usealquimia)
- [API Reference](#available-exports)

## Installation

```bash
# Using npm
npm install @alquimia-ai/tools

# Using yarn
yarn add @alquimia-ai/tools

# Using pnpm
pnpm add @alquimia-ai/tools
```

Basic usage:

Initialize the SDK in a config file, and use the useAlquimia hook in your components.

```typescript
import { AlquimiaSDK } from '@alquimia-ai/tools/sdk'
import { useAlquimia } from '@alquimia-ai/tools/hooks'

// Initialize SDK
const sdk = new AlquimiaSDK({
  apiKey: 'your-api-key',
  chatUrl: 'your-chat-url',
  streamUrl: 'your-stream-url',
  assistantId: 'your-assistant-id'
})

// Use in components
function ChatComponent() {
  const { messages, input, handleSubmit } = useAlquimia(sdk)
  // Your implementation
}
```

To see full example, check the [Getting Started](getting-started/getting-started.md) section.

## Package Structure

```
@alquimia-ai/tools/
├── sdk/
├── hooks/
├── providers/
├── utils/
├── types/
└── actions/
```

## Core Modules

### SDK Configuration

The SDK supports various providers and configurations:

```typescript
const sdk = new AlquimiaSDK(config)
  .withWhisperProvider(whisperProvider)
  .withRatingsProvider(ratingsProvider)
  .withLoggerProvider(loggerProvider)
```

### Available Providers
- WhisperProvider (Speech-to-Text)
- StableDiffusionProvider (Image Generation)
- CharacterizationProvider (Content Analysis)
- RatingsProvider (Feedback)
- LoggerProvider (Logging)

### Utility Functions
- Message formatting
- Error handling
- Data transformation

## Integration with UI Package

While usable independently, this package is designed to work seamlessly with `@alquimia-ai/ui`, providing:

- Ready-to-use chat interfaces
- Message streaming visualization
- Audio input/output handling
- Rating and feedback components

## Best Practices

1. Always initialize SDK with proper configuration
2. Use the useAlquimia hook for managing chat state
3. Implement server actions with API Routes
4. Leverage TypeScript for type safety

## Related Links

- [Alquimia AI Website](https://alquimia.ai)
- [Alquimia AI Docs](https://alquimia.gitbook.io/alquimia-docs)
- [UI Package Documentation](../ui/README.md)

## License

MIT © [Alquimia AI](LICENSE)

---

[Next: Getting Started →](getting-started/getting-started.md)