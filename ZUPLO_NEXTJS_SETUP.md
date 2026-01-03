# ZUPLO - Next.js Setup Guide

## 🚀 Complete Vercel-Native Implementation

This is a **complete rewrite** of ZUPLO using Next.js 14 (App Router) for 100% Vercel compatibility.

## Architecture

### Frontend
- ✅ Next.js 14 (App Router)
- ✅ React Server Components
- ✅ TypeScript
- ✅ Tailwind CSS
- ✅ Framer Motion

### Backend
- ✅ Vercel API Routes
- ✅ Server Actions
- ✅ NextAuth for authentication

### Storage
- ✅ Cloudflare R2 (primary)
- ✅ AWS S3 (alternative)
- ✅ Direct client uploads (no Vercel payload)

### Database
- ✅ Supabase (PostgreSQL)
- ✅ Row Level Security (RLS)
- ✅ Real-time subscriptions

## Quick Start

### 1. Install Dependencies

```bash
# Use the Next.js package.json
cp package-nextjs.json package.json
npm install
```

### 2. Set Up Environment Variables

Create `.env.local`:

```env
# Supabase
NEXT_PUBLIC_SUPABASE_URL=your-supabase-url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key

# Storage (R2 or S3)
STORAGE_TYPE=r2
R2_ACCOUNT_ID=your-r2-account-id
R2_ACCESS_KEY_ID=your-access-key
R2_SECRET_ACCESS_KEY=your-secret-key
R2_BUCKET_NAME=your-bucket-name
R2_PUBLIC_URL=https://your-bucket.r2.dev

# Auth
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=generate-with-openssl-rand-base64-32
JWT_SECRET=generate-with-openssl-rand-base64-32
```

### 3. Set Up Database

1. Go to Supabase Dashboard
2. Run the SQL from `lib/db/schema.sql`
3. Configure RLS policies

### 4. Set Up Storage

**Option A: Cloudflare R2**
1. Create R2 bucket
2. Get API credentials
3. Set environment variables

**Option B: AWS S3**
1. Create S3 bucket
2. Configure IAM user
3. Set environment variables

### 5. Run Development Server

```bash
npm run dev
```

Visit http://localhost:3000

## Project Structure

```
app/
├── (auth)/
│   └── login/          # Login page
├── (dashboard)/
│   ├── home/          # ZUPLO Home
│   ├── upload/        # Upload page
│   ├── vault/         # Text Vault
│   └── collections/   # Collections
├── admin/             # Admin dashboard
├── api/               # API routes
│   ├── auth/          # NextAuth
│   ├── files/         # File operations
│   ├── notes/         # Notes CRUD
│   └── collections/   # Collections CRUD
└── layout.tsx         # Root layout

lib/
├── storage/           # Storage adapters (R2/S3)
├── db/               # Database client
└── auth/             # Auth utilities

components/           # React components
types/                # TypeScript types
```

## Key Features Implemented

### ✅ Vercel-Safe File Upload
- Client requests presigned URL
- File uploads directly to storage
- No large payloads through Vercel
- Metadata stored in database

### ✅ Authentication
- NextAuth with password-based login
- Role-based access (user/admin)
- Protected routes via middleware
- JWT sessions

### ✅ Database
- Supabase PostgreSQL
- Row Level Security
- Optimized queries
- Pagination support

### ✅ Storage
- Multiple adapter support
- Presigned URLs
- Direct client uploads
- Secure file serving

## Deployment to Vercel

1. Push to GitHub
2. Import to Vercel
3. Add environment variables
4. Deploy

Vercel will automatically:
- Detect Next.js
- Build the application
- Deploy serverless functions
- Configure edge network

## Migration from Vite

See `MIGRATION_GUIDE.md` for step-by-step migration instructions.

## Next Steps

1. Complete remaining pages (see TODOs)
2. Add remaining API routes
3. Implement all features
4. Test thoroughly
5. Deploy to Vercel

## Support

- Next.js Docs: https://nextjs.org/docs
- Vercel Docs: https://vercel.com/docs
- Supabase Docs: https://supabase.com/docs

