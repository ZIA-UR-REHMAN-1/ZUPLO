# Setup Guide - Fixing 404 NOT_FOUND Error

## Problem

If you're seeing a `404: NOT_FOUND` error when opening the application, it's likely because:

1. **Missing Supabase Configuration** - The app requires Supabase environment variables
2. **Database Tables Not Created** - The Supabase database schema hasn't been set up
3. **Missing Environment Variables** - Required environment variables are not configured

## Solution

### Step 1: Set Up Supabase

1. **Create a Supabase Project**
   - Go to https://supabase.com
   - Sign up or log in
   - Create a new project
   - Wait for the project to be ready (takes a few minutes)

2. **Get Your Supabase Credentials**
   - Go to Project Settings → API
   - Copy the following:
     - **Project URL** (e.g., `https://xxxxx.supabase.co`)
     - **anon/public key** (starts with `eyJ...`)
     - **service_role key** (starts with `eyJ...`) - Keep this secret!

3. **Set Up Database Tables**
   - Go to SQL Editor in your Supabase dashboard
   - Copy the contents of `lib/db/schema.sql`
   - Paste and run it in the SQL Editor
   - This creates all required tables: `files`, `notes`, `collections`, `activity_logs`, `passwords`

### Step 2: Configure Environment Variables

Create a `.env.local` file in the root directory with:

```env
# Supabase Configuration (Required)
NEXT_PUBLIC_SUPABASE_URL=https://your-project-id.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key-here
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key-here

# NextAuth Configuration (Required)
# Generate a secret: openssl rand -base64 32
NEXTAUTH_SECRET=your-generated-secret-here
NEXTAUTH_URL=http://localhost:3000
```

**Important:**
- Replace `your-project-id` with your actual Supabase project ID
- Replace `your-anon-key-here` with your actual anon key
- Replace `your-service-role-key-here` with your actual service role key
- Generate `NEXTAUTH_SECRET` using: `openssl rand -base64 32`

### Step 3: Create Initial Admin Password

After setting up the database, you need to create an admin password:

1. Go to your Supabase dashboard → Table Editor → `passwords`
2. Click "Insert row"
3. Fill in:
   - `hash`: Generate using bcrypt (you can use an online bcrypt generator or Node.js)
   - `role`: `admin`
   - `enabled`: `true`
   - `label`: `Admin` (optional)

Or use this SQL in the SQL Editor:

```sql
-- Replace 'your-hashed-password' with a bcrypt hash of your password
-- You can generate one at https://bcrypt-generator.com/
INSERT INTO passwords (hash, role, enabled, label)
VALUES ('$2a$10$your-hashed-password-here', 'admin', true, 'Admin');
```

### Step 4: Restart Your Development Server

```bash
# Stop the server (Ctrl+C)
# Then restart:
npm run dev
```

## Verification

1. **Check Environment Variables**
   - Make sure `.env.local` exists and has all required variables
   - Restart your dev server after creating/updating `.env.local`

2. **Check Database Tables**
   - Go to Supabase → Table Editor
   - Verify these tables exist: `files`, `notes`, `collections`, `activity_logs`, `passwords`

3. **Test the Application**
   - Open http://localhost:3000
   - You should see the login page (not a 404 error)
   - Try logging in with your admin password

## Troubleshooting

### Still Getting 404 Error?

1. **Check Browser Console**
   - Open Developer Tools (F12)
   - Check the Console tab for specific error messages
   - Check the Network tab to see which requests are failing

2. **Check Server Logs**
   - Look at your terminal where `npm run dev` is running
   - Check for error messages about missing environment variables

3. **Verify Supabase Connection**
   - Make sure your Supabase project is active (not paused)
   - Check that your API keys are correct
   - Verify the project URL is correct

4. **Check Database Schema**
   - Ensure all tables from `schema.sql` have been created
   - Verify RLS (Row Level Security) policies are set up correctly

### Common Issues

**Error: "Missing Supabase environment variables"**
- Solution: Create `.env.local` with all required variables

**Error: "Database not configured"**
- Solution: Set `SUPABASE_SERVICE_ROLE_KEY` in `.env.local`

**Error: "Table does not exist"**
- Solution: Run the SQL from `lib/db/schema.sql` in Supabase SQL Editor

**Error: "Invalid API key"**
- Solution: Double-check your Supabase keys are correct and copied completely

## For Production Deployment

When deploying to Vercel or another platform:

1. Add all environment variables in your hosting platform's dashboard
2. Make sure `NEXTAUTH_URL` is set to your production URL
3. Ensure `SUPABASE_SERVICE_ROLE_KEY` is set (never commit this to git!)

## Need Help?

- Check the main `README.md` for general setup
- Review `DEPLOYMENT.md` for deployment instructions
- Check Supabase documentation: https://supabase.com/docs

