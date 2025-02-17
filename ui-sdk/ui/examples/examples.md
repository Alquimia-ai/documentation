# Examples

## Implementing the Floating Assistant Button

This guide will show you how to implement the floating assistant button using `@alquimia-ai/ui` and `@alquimia-ai/tools`. The assistant button opens a drawer containing a chatbot interface that interacts with the Alquimia AI assistant.

## Installation

Ensure you have installed the necessary Alquimia packages:

```sh
npm install @alquimia-ai/ui @alquimia-ai/tools
```

## Usage

To integrate the floating assistant button in your application, create a component as demonstrated below. The component should receive the `sdk` object, which is the Alquimia SDK instance. Refer to the [Getting Started](../getting-started/getting-started.md) guide for more information on how to initialize the SDK.

### Import Dependencies

```tsx
"use client";

import React, { useState, useEffect, useRef } from "react";
import { Message } from "ai";
import {
  ToastAction,
  Typography,
  Drawer,
  DrawerContent,
  DrawerHeader,
  DrawerTitle,
  DrawerDescription,
  DrawerFooter,
  Loader,
  ThinkIndicator,
} from "@alquimia-ai/ui/components/atoms";
import {
  AssistantMessageArea,
  AssistantInput,
} from "@alquimia-ai/ui/components/organisms";
import { AssistantButton } from "@alquimia-ai/ui/components/molecules";
import { useAlquimia } from "@alquimia-ai/tools/hooks";
import { useToast } from "@alquimia-ai/ui/components/hooks";
import { AlquimiaSDK } from "@alquimia-ai/tools/sdk";
import { initConversation } from "@alquimia-ai/tools/actions";
import { startManagedTransaction } from "@alquimia-ai/tools/services";

import { Copy, MessageCircle, Target, HelpCircle, Users } from "lucide-react";
```

### Component Breakdown

#### `AssistantButton`

- Displays a floating button with an icon.
- Opens the assistant drawer when clicked.
- Includes predefined suggestions that users can select for quick interactions.

#### `Message Suggestions`

The `AssistantButton` component can be configured with predefined message suggestions that appear when users hover over the button. Each suggestion consists of:

- `label`: The text displayed to the user
- `icon`: An icon component to visually represent the suggestion
- `action`: A callback function that triggers when the suggestion is selected

These suggestions help users quickly access common queries or actions without typing them manually.

#### `Drawer`

- A modal-like container that slides in from the bottom.
- Contains the chatbot interface where users can interact with the assistant.
- You can customize the drawer using the `DrawerContent` component. In this example, we set the `h-[80%]` class to limit the height of the drawer.

#### `AssistantMessageArea`

- Displays messages exchanged between the user and the assistant.
- Handles streaming messages.

#### `AssistantInput`

- A text input field for users to type their messages.
- Disables the send button while streaming messages.

### State Management

The component maintains several pieces of state:

- `isDrawerOpen`: Tracks whether the assistant drawer is open.
- `isLoading`: Indicates whether the assistant is processing a message.
- `isTextStreaming`: Tracks whether a message is being streamed.
- `pendingSuggestion`: Stores a suggested query selected by the user.

### Implementing the Component

```tsx
const AssistantSnippet: React.FC<AssistantSnippetProps> = ({
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
    handleLoadingCancel,
    handleReplaceInput,
  } = useAlquimia(sdk);

  const { logInfoMessage, logErrorMessage, logInternalMessageError } =
    useLogger();
  const messagesEndRef = useRef<HTMLDivElement>(null);
  const [isDrawerOpen, setIsDrawerOpen] = useState(false);
  const [isLoading, setIsLoading] = useState(false);
  const [pendingSuggestion, setPendingSuggestion] = useState<string | null>(
    null
  );
  const [isTextStreaming, setIsTextStreaming] = useState(false);
  const isStreaming = isMessageStreaming || isTextStreaming;

  useEffect(() => {
    (async () => {
      await initConversation(true);
    })();
  }, []);

  const handleOpenDrawer = () => setIsDrawerOpen(true);
  const handleCloseDrawer = () => setIsDrawerOpen(false);

  const handleOpenSuggestion = (suggestion: string) => {
    handleReplaceInput(suggestion);
    setIsDrawerOpen(true);
  };

  const messageSuggestions = [
    {
      label: "Suggestion 1",
      icon: HelpCircle,
      action: () => handleOpenSuggestion("Suggestion 1"),
    },
    {
      label: "Suggestion 2",
      icon: Target,
      action: () => handleOpenSuggestion("Suggestion 2"),
    },
    {
      label: "Suggestion 3",
      icon: Users,
      action: () => handleOpenSuggestion("Suggestion 3"),
    },
  ];

  return (
    <div className="flex items-center gap-x-2">
      <Drawer open={isDrawerOpen} onOpenChange={setIsDrawerOpen}>
        <AssistantButton icon={MessageCircle} clickAction={handleOpenDrawer} />
        <DrawerContent className="h-[80%]">
          <DrawerHeader className="border-b border-border alq--drawer-assistant-header">
            <DrawerTitle className="text-primary text-left">
              Asistente
            </DrawerTitle>
            <DrawerDescription>
              Haga sus consultas de forma clara y sencilla
            </DrawerDescription>
          </DrawerHeader>
          {isLoading ? (
            <div className="flex items-center justify-center h-full">
              <Loader size="large" />
            </div>
          ) : (
            <AssistantMessageArea
              messages={messages}
              messagesEndRef={messagesEndRef}
              streamingMessageId={streamingMessageId}
            />
          )}
          <DrawerFooter>
            <AssistantInput
              sendMessageFunc={handleSubmit}
              isButtonDisabled={isStreaming}
              input={input}
              handleInputChange={handleInputChange}
            />
          </DrawerFooter>
        </DrawerContent>
      </Drawer>
    </div>
  );
};
```

You can also use our Dialog component to implement the assistant button.

```tsx
  return (
    <div className="flex items-center gap-x-2">
      <Dialog open={isDrawerOpen} onOpenChange={setIsDrawerOpen}>
        <DialogTrigger asChild>
          <AssistantButton icon={MessageCircle} clickAction={handleOpenDrawer} />
        </DialogTrigger>
        <DialogContent className="h-[80vh] max-h-[800px] w-[90vw] max-w-[500px] flex flex-col p-0">
          <DialogHeader className="border-b border-border p-6 alq--dialog-assistant-header">
            <DialogTitle className="text-primary text-left">
              Asistente
            </DialogTitle>
            <DialogDescription>
              Haga sus consultas de forma clara y sencilla
            </DialogDescription>
          </DialogHeader>
          
          <div className="flex-1 overflow-y-auto px-6">
            {isLoading ? (
              <div className="flex items-center justify-center h-full">
                <Loader size="large" />
              </div>
            ) : (
              <AssistantMessageArea
                messages={messages}
                messagesEndRef={messagesEndRef}
                streamingMessageId={streamingMessageId}
              />
            )}
          </div>

          <DialogFooter className="border-t border-border p-6">
            <AssistantInput
              sendMessageFunc={handleSubmit}
              isButtonDisabled={isStreaming}
              input={input}
              handleInputChange={handleInputChange}
            />
          </DialogFooter>
        </DialogContent>
      </Dialog>
    </div>
  );
};
```

## Summary

- The `AssistantButton` provides a floating button to open the assistant.
- The `Drawer` component acts as a container for the chatbot UI.
- The `AssistantMessageArea` displays assistant messages.
- The `AssistantInput` allows users to send messages.
- State is managed to control loading, streaming, and error handling.
