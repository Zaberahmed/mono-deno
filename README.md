# Deno Monorepo Template with tRPC, React, Vite, TanStack Query, and Shadcn UI

A full-stack monorepo template built with Deno for both frontend and backend, featuring modern tools and type-safe API communication between client and server.

## Features

- **Monorepo Structure**: Well-organized workspace with shared code between applications
- **Full-Stack TypeScript**: End-to-end type safety with shared types between frontend and backend
- **tRPC Integration**: Type-safe API layer without schemas or code generation
- **Vite + React**: Fast development experience with HMR
- **TanStack Query**: Powerful data fetching and caching for React
- **Shadcn UI**: Beautiful, accessible, and customizable React components
- **Tailwind CSS**: Utility-first CSS framework for rapid UI development
- **Deno Deploy Ready**: Configured for easy deployment to Deno Deploy

## Project Structure

```
.
├── apps/
│   ├── api/                # Backend tRPC API server
│   │   ├── trpc/           # tRPC configuration and routers
│   │   └── index.ts        # Main entrypoint
│   └── web/                # Frontend React application
│       ├── src/            # React application source code
│       │   ├── configs/    # Configuration for trpc and react-query
│       │   ├── providers/  # React context providers
│       │   └── constants/  # Application constants and shared values
│       ├── tailwind.config.js # Tailwind CSS configuration
│       └── vite.config.ts  # Vite configuration
├── packages/
│   └── shadcn/            # Shared UI component library
│       ├── src/           # Source code for components
│       │   ├── components/ # UI components built with Tailwind and Radix
│       │   ├── lib/        # Utility functions
│       │   └── styles/     # Global styles and CSS variables
│       └── deno.json      # Package configuration
├── .github/              # GitHub Actions workflows
├── deno.json             # Root workspace configuration
└── .env.*.example        # Environment variable templates
```

## Prerequisites

- [Deno](https://deno.com/) v2.0.0 or later

## Getting Started

1. **Clone the template**

   ```bash
   git clone https://github.com/yourusername/deno-monorepo-template.git
   cd deno-monorepo-template
   ```

2. **Set up environment variables**

   Copy the example environment files and configure them:

   ```bash
   cp .env.dev.example .env.dev
   cp .env.production.example .env.production
   ```

   Edit the `.env.dev` file to set your development environment variables:

   ```
   # API server
   API_LOCAL_PORT = 6200
   VITE_API_URL = http://localhost:6200

   # Web client
   WEB_LOCAL_PORT = 5173
   WEB_URL = http://localhost:5173
   ```

3. **Start the development servers**

   Start both the API and web servers in development mode:

   ```bash
   deno task dev
   ```

   Or run them separately:

   ```bash
   # Run API server only
   deno task dev:api

   # Run web server only
   deno task dev:web
   ```

4. **Access the applications**

   - API: http://localhost:6200
   - Web: http://localhost:5173

## Building for Production

Build the web application for production:

```bash
deno task build:web
```

You can preview the built web application locally:

```bash
deno task preview:web
```

## Deployment

This template is configured for deployment to [Deno Deploy](https://deno.com/deploy).

### Manual Deployment

You can manually deploy using the Deno Deploy CLI:

```bash
# Deploy API server
deno task deploy:api

# Deploy web application
deno task deploy:web

# Deploy both
deno task deploy
```

### GitHub Actions Deployment

This template includes a disabled GitHub Actions workflow that can be enabled to automatically deploy to Deno Deploy when you push to the main branch.

To enable the GitHub Actions workflow:

1. Locate the file `.github/workflows/deploy.yml.disabled` in your repository
2. Remove the `.disabled` extension so the filename becomes `deploy.yml`
3. Create your Deno Deploy projects:
   - `deno-monorepo-api` for the API server
   - `deno-monorepo-web` for the web application
4. Set up GitHub repository variables:
   - `VITE_API_URL`: The URL of your deployed API server (e.g., `https://deno-monorepo-api.deno.dev`)
5. Make sure to update the project names in the workflow file if you're using different project names in Deno Deploy
6. Push to the main branch to trigger deployment

## Customizing

### Adding a new tRPC endpoint

1. Create a new router file in `apps/api/trpc/routers/`
2. Add your procedures to the router
3. Add your router to `apps/api/trpc/routers/index.ts`
4. Your new endpoints will be automatically available to the frontend through tRPC

### Adding a new UI component

This template uses Shadcn UI for components:

1. Create a new component file in `packages/shadcn/src/components/ui/`
2. Export the component in the package's `deno.json` exports
3. Import and use the component in your web application

### Environment Variables

- **Development**: Edit `.env.dev` for development settings
- **Production**: Edit `.env.production` for production settings

## License

MIT
