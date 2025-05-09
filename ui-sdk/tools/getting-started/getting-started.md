# Getting Started with Alquimia Tools

This guide will walk you through setting up an AI assistant in your Next.js application using Alquimia Tools and UI components.

## Installation

1. First, set up your Next.js project (version 14.2.15 or higher):

```bash
npx create-next-app@latest my-ai-app --typescript --tailwind
```

2. Install the required packages:

```bash
npm install @alquimia-ai/tools @alquimia-ai/ui
# or
yarn add @alquimia-ai/tools @alquimia-ai/ui
```

## Configuration

1. Create an SDK configuration file (`assistant.config.ts`):

```typescript
import { AlquimiaSDK } from "@alquimia-ai/tools/sdk";

const config = AlquimiaSDK.configure(
  process.env.ALQUIMIA_API_KEY!,
  `/api/chat`, // chat endpoint, in this case the endpoint is directed to an API route
  `/api/stream`, // stream endpoint, in this case the endpoint is directed to an API route
  process.env.NEXT_PUBLIC_ASSISTANT_ID! //assistant id
);

const sdk = new AlquimiaSDK(config, false);

export { sdk };
```

2. Set up your environment variables (`.env.local`):

```env
ALQUIMIA_API_KEY=your-api-key
NEXT_PUBLIC_ASSISTANT_ID=your-assistant-id
```

## Core Elements

### AlquimiaSDK

The SDK is the core client that handles all interactions with the Alquimia API. Key features include:

- **Configuration Management**:

  - Handles API keys and endpoints
  - Manages chat and stream URLs
  - Configures assistant IDs

- **Conversation Management**:

  - Maintains conversation state
  - Handles session IDs
  - Manages stream IDs for real-time communication

- **Provider Integration**: Supports multiple providers for services like:

  - Speech-to-text and text-to-speech
  - Image generation
  - Character analysis
  - Ratings and logging

- **Error Handling**:

  - Built-in axios interceptors for error management
  - Integrated logging for server errors
  - Provider-specific error handling

- **Tool Management**:
  - Supports custom tool integration
  - Handles extra data and profile forcing
  - Flexible tool configuration through builder pattern

Example SDK initialization:

```typescript
const sdk = new AlquimiaSDK(config)
  .withWhisperProvider(new WhisperProvider())
  .withStableDiffusionProvider(new StableDiffusionProvider())
  .withTools([
    /* your tools */
  ])
  .withExtraData({
    /* custom data */
  });
```

### useAlquimia Hook

A React hook that provides a complete chat interface implementation. Main features:

- **Message Management**:

  - Maintains message history array
  - Handles real-time message streaming
  - Processes message chunks for smooth updates
  - Supports message metadata
  - Supports system messages

- **State Management**:

  - Input handling and validation
  - Loading states for UI feedback
  - Message streaming states
  - Audio recording states
  - Session management

- **Tool Integration**:

  - Supports dynamic tool activation
  - Tracks active tools
  - Processes tool responses

- **Session Handling**:

  - Manages conversation sessions via cookies
  - Supports session persistence
  - Handles session restoration

- **Error Management**:
  - Error state tracking
  - Error message processing
  - Recovery mechanisms

Example hook usage:

```typescript
const {
  messages,
  input,
  handleSubmit,
  handleInputChange,
  isMessageStreaming,
  streamingMessageId,
  // ... other utilities
} = useAlquimia(sdk);
```

The hook provides all necessary functions and state management for building a complete chat interface, while the SDK handles the underlying API communication and service integration. Together, they form a powerful foundation for building AI-powered chat assistants.

## Implementation

1. Create your Assistant component (`components/AssistantComponent.tsx`). This component will use the useAlquimia hook to manage the AI interactions, along with the sdk initialized in the config file. Its important to initialize the sdk in the config file, and pass it to the component as a prop.

```typescript
"use client";

import React, { useState, useEffect, useRef } from "react";
import { Message } from "ai";
import { AssistantMessageArea, AssistantInput } from "@alquimia-ai/ui";
import { useAlquimia } from "@alquimia-ai/tools/hooks";
import { initConversation } from "@alquimia-ai/tools/actions";
import { useToast } from "@alquimia-ai/ui";
import { AlquimiaSDK } from "@alquimia-ai/tools/sdk";

interface AssistantSnippetProps {
  sdk: AlquimiaSDK;
  assistantHelpText?: string;
}

export const AssistantSnippet: React.FC<AssistantSnippetProps> = ({
  sdk,
  assistantHelpText,
}) => {
  const {
    messages,
    input,
    handleSubmit,
    handleInputChange,
    isMessageStreaming,
    streamingMessageId,
  } = useAlquimia(sdk);

  // Initialize the conversation with a session ID, which will be stored in cookies.
  useEffect(() => {
    (async () => {
      await initConversation(true);
    })();
  }, []);

  return (
    <div>
      <div>
        // assistant body
        <AssistantMessageArea
          messages={messages}
          messagesEndRef={messagesEndRef}
          streamingMessageId={streamingMessageId}
          actions={messageActions}
        />
      </div>
      <div>
        // assistant footer
        <AssistantInput
          sendMessageFunc={handleSubmit}
          isButtonDisabled={isButtonDisabled}
          input={input}
          handleInputChange={handleInputChange}
          isMessageStreaming={isMessageStreaming}
        />
      </div>
    </div>
  );
};
```

2. Use the Assistant in your page, or any other component by importing the AssistantComponent and passing the initialized sdk:

```typescript
"use client";

import { AssistantComponent } from "@/components/AssistantComponent";
import { sdk } from "@/assistant.config";

export default function Home() {
  return (
    <main>
      <h1>My AI Assistant</h1>
      <AssistantComponent sdk={sdk} />
    </main>
  );
}
```

## API Routes

If you want to run the assistant in the server, you can use the /tools/actions chat and stream actions inside api routes.

1. Create a chat API route (`app/api/chat/route.ts`):

```typescript
import {
  handleChatRequest,
  ChatRouteContext,
} from "@alquimia-ai/tools/actions";
import { NextRequest, NextResponse } from "next/server";

const assistantBaseUrl = process.env.NEXT_PUBLIC_ASSISTANT_BASEURL || "";
const apiKey = process.env.ALQUIMIA_ASSISTANT_API_KEY || "";

export const POST = async (
  request: NextRequest,
  context: any
): Promise<NextResponse> => {
  const response = await handleChatRequest(request, context, {
    assistantBaseUrl,
    apiKey,
  });

  return NextResponse.json(await response.json(), {
    status: response.status,
    headers: Object.fromEntries(response.headers.entries()),
  });
};
```

2. Create a stream API route (`app/api/stream/route.ts`):

```typescript
import {
  handleStreamRequest,
  ChatRouteContext,
} from "@alquimia-ai/tools/actions";
import { NextRequest, NextResponse } from "next/server";

const assistantBaseUrl = process.env.NEXT_PUBLIC_ASSISTANT_BASEURL || "";
const apiKey = process.env.ALQUIMIA_ASSISTANT_API_KEY || "";

export const GET = async (
  request: NextRequest,
  context: ChatRouteContext
): Promise<NextResponse> => {
  const response = await handleStreamRequest(request, context, {
    assistantBaseUrl,
    apiKey,
  });

  return new NextResponse(response.body, {
    status: response.status,
    headers: Object.fromEntries(response.headers.entries()),
  });
};
```

## Styling

1. Update your `tailwind.config.js` to extend the Alquimia UI configuration:

```javascript
const baseConfig = require("@alquimia-ai/ui/tailwind.config");

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
};
```

## Features

Your AI assistant now includes:

- Real-time message streaming
- Copy message functionality
- Error handling with toast notifications
- Message history
- Loading states


#### User Messages vs. System Messages

In many assistant applications, it's important to distinguish between messages sent by the user and those triggered by the system or application logic. This distinction allows for more flexible, context-aware, and automated assistant behaviors.

- **User Message**: Sent when a user submits input (e.g., via a form or chat box). Use `handleSubmit` for this.
- **System Message**: Sent programmatically by your app, not directly triggered by user input. Use `handleSystemMessage` for this. Examples include:
  - Sending a welcome message when a user opens the chat
  - Triggering a message based on an external event (e.g., onboarding step, notification)

### Sending System Messages

The `useAlquimia` hook supports sending system messages using the `handleSystemMessage` function. This allows you to programmatically send messages to the assistant, which are not directly triggered by user input.

**Example: Sending a Welcome System Message**

```typescript
import { useEffect } from "react";

const { handleSystemMessage } = useAlquimia(sdk);

  const sendInitialMessage = async () => {
    try {
      await handleSystemMessage("Hi, how are you?");
    } catch (error) {
      console.error('error', error)
    }
  };

  // Send a system message when the assistant is first opened
  useEffect(() => {
    sendInitialMessage();
  }, []);

  // ...rest of the implementation
```

**Parameters:**
- `message` (string): The message to send.
- `options` (object, optional):
  - `messageType` (string): Type of the message (defaults to "system").
  - `traceParentId` (string): For tracing requests.
  - `sessionId` (string): Specifies the id of the conversation session.

**When to use system messages:**
- Onboarding flows (e.g., greet the user)
- Automated assistant prompts
- Triggering assistant actions based on app events