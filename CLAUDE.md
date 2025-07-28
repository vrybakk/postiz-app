# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Essential Commands

### Development
- `bun install` - Install dependencies
- `bun run dev` - Run all apps in development mode (frontend, backend, workers, extension)
- `bun run dev:backend` - Run backend only
- `bun run dev:frontend` - Run frontend only
- `bun run dev:workers` - Run workers only
- `bun run dev:cron` - Run cron service only

### Building
- `bun run build` - Build frontend, backend, workers, and cron
- `bun run build:backend` - Build backend only
- `bun run build:frontend` - Build frontend only
- `bun run build:workers` - Build workers only
- `bun run build:extension` - Build browser extension

### Database Operations
- `bun run prisma-generate` - Generate Prisma client
- `bun run prisma-db-push` - Push schema changes to database
- `bun run prisma-reset` - Reset database (force reset and push)

### Testing
- `bun test` - Run Jest tests with coverage

### Production
- `bun run start:prod:backend` - Start backend in production
- `bun run start:prod:frontend` - Start frontend in production
- `bun run start:prod:workers` - Start workers in production

### Docker
- `bun run dev:docker` - Start development dependencies (PostgreSQL, Redis)

## Architecture Overview

Postiz is a social media scheduling platform built as a monorepo with the following structure:

### Core Applications (`apps/`)
- **frontend** - Next.js 14 app with React 18, TailwindCSS, and Mantine UI
- **backend** - NestJS API server with Swagger documentation
- **workers** - Background job processing using BullMQ
- **cron** - Scheduled task service for recurring operations
- **extension** - Browser extension built with Vite and React
- **sdk** - TypeScript SDK for external integrations
- **commands** - CLI utilities and maintenance tasks

### Shared Libraries (`libraries/`)
- **nestjs-libraries** - Core backend services, database models, integrations, and business logic
- **react-shared-libraries** - Reusable React components and utilities
- **helpers** - Common utility functions and services

### Key Technologies
- **Database**: PostgreSQL with Prisma ORM (schema: `libraries/nestjs-libraries/src/database/prisma/schema.prisma`)
- **Queue System**: Redis with BullMQ for background jobs
- **Authentication**: JWT with OAuth providers (Google, GitHub, Farcaster, Wallet)
- **Email**: Resend for transactional emails
- **File Storage**: Configurable (Local, CloudFlare R2, AWS S3)
- **Package Manager**: Bun with workspace configuration

### Social Media Integrations
The platform supports 15+ social media platforms including X (Twitter), Instagram, LinkedIn, Facebook, TikTok, YouTube, Discord, Reddit, Medium, Pinterest, Bluesky, Mastodon, and more. Integration providers are located in `libraries/nestjs-libraries/src/integrations/social/`.

### Database Schema
- Organizations manage users, posts, integrations, and billing
- Posts support scheduling, media attachments, and cross-platform publishing
- Users can belong to multiple organizations with role-based permissions
- Integrations handle OAuth connections to social platforms
- Marketplace enables post buying/selling between users

### Development Requirements
- Node.js 20.17.0 (managed by Volta)
- Bun 1.0.0+
- PostgreSQL database
- Redis instance

### Environment Setup
The project requires environment variables for database, Redis, OAuth providers, and external services. Reference `.env.example` for required variables.

### Testing
Jest is configured for unit testing with coverage reporting. Test files follow the `.spec.ts` or `.test.ts` convention.

### Deployment
The application supports Docker deployment with configurations in `docker-compose.dev.yaml` and production build scripts.