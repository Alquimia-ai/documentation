# Alquimia AI Widget

A lightweight, embeddable chat widget that allows you to integrate the Alquimia AI assistant into any website. The widget appears as a floating button that expands into a full chat interface when clicked.

The widget repository is available at [@Alquimia-ai/alquimia-widget](https://github.com/Alquimia-ai/alquimia-widget). Note that the widget must be deployed to a server before it can be consumed by a parent application using the script tag integration.

## Overview

This widget application provides:
- A floating chat button
- Expandable chat interface
- Seamless integration with Alquimia AI's assistant
- Responsive design for all devices
- Customizable appearance

## How It Works

The widget implementation follows these key steps:

1. When you include the widget script via `/api/widget`, it:
   - Creates an iframe element on your webpage
   - Positions it in the bottom-right corner
   - Loads the widget interface within the iframe for security and style isolation

2. The widget consists of two main states:
   - A floating button (minimized state)
   - A full chat interface (expanded state)

## Integration

To add the widget to your website, include the following script tag:

```html
<script src="https://<app_url>/api/widget"></script>
```

The widget will automatically initialize and appear as a floating button in the bottom-right corner of your page.

## Development

To run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

Then open [http://localhost:3000](http://localhost:3000) to view the widget demo page.

## Docker Deployment

### Prerequisites
- Docker
- Docker Compose

### Docker Configuration

The application uses a multi-stage build process for optimal production deployment:

1. **Builder Stage**: Compiles and builds the Next.js application
2. **Runner Stage**: Creates a lightweight production image

### Environment Variables

Create a `.env` file with the required variables:

```bash
NEXT_PUBLIC_DEFAULT_ASSISTANT_ID=
NEXT_PUBLIC_ASSISTANT_BASEURL=
ALQUIMIA_ASSISTANT_API_KEY=
NEXT_PUBLIC_APP_URL=
APP_ROOT=
```

### Building and Running with Docker

1. Build and start the container:

```bash
docker-compose up --build
```

2. Run in detached mode:

```bash
docker-compose up -d
```

3. Stop the container:

```bash
docker-compose down
```

### Docker Health Checks

The service includes health checks that:
- Monitor the application every 30 seconds
- Timeout after 10 seconds
- Allow 3 retries before marking unhealthy

### Volume Mounts

The following directories are mounted as volumes:
- `./public:/app/public`: For static files
- `./.next:/app/.next`: For Next.js build output


## API Endpoints

- `/api/widget`: Serves the widget script that can be embedded in any website
