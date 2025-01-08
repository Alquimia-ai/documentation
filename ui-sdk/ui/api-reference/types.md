# API Types Reference

This page documents the core types used in the Alquimia API.

## Document Types

### AlquimiaDocument
Represents a document in the system.

```typescript
{
  id: string;
  name: string;
  description?: string;
  isActive: boolean;
  contentType: string;
  url: string;
  updatedAt?: string;
}
```

### AlquimiaTopic
Represents a topic that can contain multiple documents.

```typescript
{
  id: string;
  externalCollectionId: string;
  isActive: boolean;
  name: string;
  description: string;
  createdAt?: string;
  updatedAt?: string;
  files: AlquimiaDocument[];
  ratings?: TopicRating[];
}
```

### AlquimiaFile
Represents a file object.

```typescript
{
  id: string;
  file: Blob;
}
```

## Rating Types

### TopicRating
Basic rating information for a topic.

```typescript
{
  id: number;
  sessionId: string;
}
```

### RatingData
Detailed rating information including assistant and session data.

```typescript
{
  assistantId: string;
  sessionId: string;
  topicId: number;
  score?: number;
  emoji?: string;
  description?: string;
}
```

## Status Enums

### EditingStatus
Represents the current editing state.

```typescript
enum EditingStatus {
  EDITING = 'EDITING',
  FINISHED = 'FINISHED'
}
```

## Response Types

### ActionResponse<T>
Generic response wrapper for actions.

```typescript
{
  success: boolean;
  data?: T;
  error?: ActionError;
}
```

### ActionError
Error information for action responses.

```typescript
{
  message: string;
  code?: string;
  details?: ErrorDetails;
}
```

### ErrorDetails
Additional error details.

```typescript
{
  status: string;
  statusText?: string;
}
```

### ApiError
Extended Error type with additional API-specific fields.

```typescript
Error & {
  message: string;
  name: string;
  cause: string;
  code?: string | number;
  status?: string | number;
}
```

## Server Action Types

### TWYDServerActions
Interface defining available server actions.

```typescript
{
  getDocument?: (id: string) => Promise<ActionResponse<Blob>>;
  sendRating?: (ratingData: RatingData) => Promise<any>;
  logError?: (message: string, error: Error, data?: Record<string, any>) => Promise<any>;
}
```