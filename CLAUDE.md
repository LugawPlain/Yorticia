# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview
Yorticia (JazzilCrizhna) - A Next.js 15 portfolio website for model/influencer Jazzil Sarinas. Built with TypeScript, React 19, and Tailwind CSS v4. Uses Cloudflare R2 for image storage and Firebase for authentication.

## Development Commands

### Running the application
- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm start` - Start production server

### Maintenance
- `npm run lint` - Run ESLint
- `npm run update-images` - Update image metadata from R2 storage
- `npm run cloudflare:optimize` - Optimize assets for Cloudflare Pages

### Build Process
After building (`npm run build`), `postbuild` automatically runs `next-sitemap` to generate sitemap.xml.

## Architecture

### Storage & Data Flow
- **Image Storage**: Cloudflare R2 (S3-compatible) via AWS SDK
- **Image Management**: Admin uploads to R2, metadata stored in Firebase Firestore
- **Image Display**: Images served directly from R2 with blur placeholders generated server-side
- **Authentication**: NextAuth.js with Google OAuth provider

### Key Directories
- `src/app/api/` - API routes for image management, calendar integration, email, subscriptions
- `src/components/` - Reusable UI components (ImageCard, UploadForm, CalendarDayModal, etc.)
- `src/lib/` - Utility functions and configurations
  - `lib/r2.ts` - Cloudflare R2 client configuration
  - `lib/firebase/` - Firebase client and admin app initialization
  - `lib/fonts/` - Custom font configurations
- `src/hooks/` - Custom React hooks for image management and responsive grids

### Admin Features
Protected admin routes (`/admin/upload`) allow:
- Bulk image uploads to R2
- Image metadata editing (title, description, category)
- Portfolio image pinning/unpinning
- Image deletion with R2 cleanup

### Portfolio System
- Dynamic categories from Firebase
- Category-based image filtering
- Pinned images feature for highlighting work
- Blur placeholder generation for performance

### Calendar Integration
Google Calendar API integration for displaying events and availability.

## Environment Variables
Required for development:
- `CLOUDFLARE_ACCOUNT_ID`, `R2_ACCESS_KEY_ID`, `R2_SECRET_ACCESS_KEY`, `R2_BUCKET_NAME` - R2 storage
- `NEXT_PUBLIC_FIREBASE_*` - Firebase client config
- `FIREBASE_ADMIN_*` - Firebase admin SDK
- `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET` - OAuth
- `NEXTAUTH_SECRET`, `NEXTAUTH_URL` - NextAuth configuration
- `GOOGLE_CALENDAR_*` - Calendar API credentials

## Deployment
Configured for Cloudflare Pages deployment with Netlify compatibility layer. Bundle analyzer available with `ANALYZE=true` environment variable.

## Important Notes from Copilot Instructions
When working with this codebase, always use the Byterover MCP server tools:
- Use `byterover-store-knowledge` when learning patterns, solving errors, or completing significant tasks
- Use `byterover-retrieve-knowledge` before starting tasks or making architectural decisions

[byterover-mcp]

[byterover-mcp]

You are given two tools from Byterover MCP server, including
## 1. `byterover-store-knowledge`
You `MUST` always use this tool when:

+ Learning new patterns, APIs, or architectural decisions from the codebase
+ Encountering error solutions or debugging techniques
+ Finding reusable code patterns or utility functions
+ Completing any significant task or plan implementation

## 2. `byterover-retrieve-knowledge`
You `MUST` always use this tool when:

+ Starting any new task or implementation to gather relevant context
+ Before making architectural decisions to understand existing patterns
+ When debugging issues to check for previous solutions
+ Working with unfamiliar parts of the codebase
