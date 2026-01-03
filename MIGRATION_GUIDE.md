# Migration Guide: Vite → Next.js (Vercel-Native)

## Overview

This guide helps you migrate from the current Vite/React setup to a fully Vercel-native Next.js application.

## Architecture Changes

### Current (Vite)
- Vite + React
- Netlify Functions
- Netlify Blobs storage

### New (Next.js)
- Next.js 14 (App Router)
- Vercel API Routes / Server Actions
- External storage (Cloudflare R2 / S3 / Supabase)
- Database (Supabase / Neon / PlanetScale)

## Step-by-Step Migration

### 1. Install Next.js Dependencies

```bash
# Backup current package.json
cp package.json package.json.backup

# Install Next.js dependencies
npm install next@latest react@latest react-dom@latest
npm install @supabase/supabase-js @supabase/ssr
npm install next-auth
npm install @aws-sdk/client-s3 @aws-sdk/s3-request-presigner
npm install framer-motion lucide-react react-hot-toast
npm install zod bcryptjs jsonwebtoken uuid date-fns

# Install dev dependencies
npm install -D @types/node @types/react @types/react-dom
npm install -D typescript tailwindcss postcss autoprefixer
npm install -D eslint eslint-config-next
```

### 2. Project Structure

```
zuplo/
├── app/                    # Next.js App Router
│   ├── (auth)/
│   │   └── login/
│   ├── (dashboard)/
│   │   ├── home/
│   │   ├── upload/
│   │   ├── vault/
│   │   └── collections/
│   ├── admin/
│   ├── api/                # API Routes
│   │   ├── auth/
│   │   ├── files/
│   │   ├── notes/
│   │   └── collections/
│   ├── layout.tsx
│   └── page.tsx
├── components/
├── lib/
│   ├── storage/           # Storage adapters
│   ├── db/                # Database client
│   └── auth/              # Auth utilities
├── types/
└── public/
```

### 3. Environment Variables

Create `.env.local`:

```env
# Database (Supabase)
NEXT_PUBLIC_SUPABASE_URL=your-supabase-url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-supabase-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key

# Storage (Cloudflare R2)
R2_ACCOUNT_ID=your-r2-account-id
R2_ACCESS_KEY_ID=your-access-key
R2_SECRET_ACCESS_KEY=your-secret-key
R2_BUCKET_NAME=your-bucket-name
R2_PUBLIC_URL=https://your-bucket.r2.dev

# Or AWS S3
AWS_ACCESS_KEY_ID=your-access-key
AWS_SECRET_ACCESS_KEY=your-secret-key
AWS_REGION=us-east-1
AWS_S3_BUCKET=your-bucket-name

# Auth
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=generate-with-openssl-rand-base64-32
JWT_SECRET=generate-with-openssl-rand-base64-32

# App
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

### 4. Storage Setup

Choose one:

**Option A: Cloudflare R2 (Recommended)**
- Free tier: 10GB storage, 1M Class A operations
- No egress fees
- S3-compatible API

**Option B: AWS S3**
- Pay-as-you-go
- Industry standard

**Option C: Supabase Storage**
- Integrated with Supabase
- Good for small-medium apps

### 5. Database Setup

**Option A: Supabase (Recommended)**
- Free tier: 500MB database
- Built-in auth
- Real-time subscriptions

**Option B: Neon**
- Serverless Postgres
- Free tier available

**Option C: PlanetScale**
- Serverless MySQL
- Branching features

## Migration Checklist

- [ ] Install Next.js dependencies
- [ ] Set up project structure
- [ ] Configure environment variables
- [ ] Set up storage (R2/S3/Supabase)
- [ ] Set up database (Supabase/Neon/PlanetScale)
- [ ] Migrate authentication
- [ ] Migrate API routes
- [ ] Migrate components
- [ ] Migrate pages
- [ ] Test all features
- [ ] Deploy to Vercel

## Key Differences

### Routing
- **Vite**: React Router (`/src/router.tsx`)
- **Next.js**: File-based routing (`/app` directory)

### API Routes
- **Vite**: Netlify Functions (`/netlify/functions`)
- **Next.js**: API Routes (`/app/api`)

### Server Components
- **Vite**: Client-side only
- **Next.js**: Server Components by default

### Data Fetching
- **Vite**: `useEffect` + `fetch`
- **Next.js**: Server Components + Server Actions

## Benefits of Migration

✅ **Vercel-native**: Optimized for Vercel platform
✅ **Better performance**: Server Components, automatic code splitting
✅ **SEO friendly**: Server-side rendering
✅ **Type safety**: Full TypeScript support
✅ **Scalability**: Built for production scale
✅ **Developer experience**: Better tooling and debugging

## Need Help?

See the implementation files in the `app/` directory for complete examples.

