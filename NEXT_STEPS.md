# Next Steps - Complete Setup

✅ **Environment variables have been configured!**

## Step 1: Set Up Database Tables in Supabase

1. **Go to your Supabase Dashboard**
   - Visit: https://supabase.com/dashboard/project/svfdzphvftiwcjqbqquo
   - Or go to https://supabase.com/dashboard and select your project

2. **Open SQL Editor**
   - Click on "SQL Editor" in the left sidebar
   - Click "New query"

3. **Run the Database Schema**
   - Open the file `lib/db/schema.sql` in this project
   - Copy ALL the contents (lines 1-113)
   - Paste into the Supabase SQL Editor
   - Click "Run" (or press Ctrl+Enter)
   - Wait for "Success. No rows returned" message

   This creates all required tables:
   - `files` - for file metadata
   - `notes` - for text notes
   - `collections` - for organizing files
   - `activity_logs` - for activity tracking
   - `passwords` - for user authentication

## Step 2: Create Your Admin Password

You need to create an admin password to log in. You have two options:

### Option A: Using Supabase Dashboard (Easier)

1. Go to **Table Editor** → **passwords** table
2. Click **"Insert row"** or the **"+"** button
3. Fill in:
   - **hash**: You need to generate a bcrypt hash of your password
     - Visit: https://bcrypt-generator.com/
     - Enter your desired password (e.g., "admin123")
     - Set rounds to 10
     - Click "Generate Hash"
     - Copy the hash (starts with $2a$10$...)
   - **role**: `admin`
   - **enabled**: `true` (checkbox)
   - **label**: `Admin` (optional, for your reference)
4. Click **"Save"**

### Option B: Using SQL (Faster)

1. Go to **SQL Editor** in Supabase
2. Run this SQL (replace `YOUR_PASSWORD_HASH` with a bcrypt hash from https://bcrypt-generator.com/):

```sql
-- Example: Password "admin123" hashed
INSERT INTO passwords (hash, role, enabled, label)
VALUES ('$2a$10$N9qo8uLOickgx2ZMRZoMyeIjZAgcfl7p92ldGxad68LJZdL17lhWy', 'admin', true, 'Admin');
```

**To generate a hash:**
- Go to https://bcrypt-generator.com/
- Enter your password
- Copy the generated hash
- Replace the hash in the SQL above

## Step 3: Disable Row Level Security (RLS) for Service Role Access

Since we're using the service role key, we need to allow service role to bypass RLS:

1. Go to **SQL Editor** in Supabase
2. Run this SQL:

```sql
-- Allow service role to bypass RLS (needed for server-side operations)
ALTER TABLE files DISABLE ROW LEVEL SECURITY;
ALTER TABLE notes DISABLE ROW LEVEL SECURITY;
ALTER TABLE collections DISABLE ROW LEVEL SECURITY;
ALTER TABLE activity_logs DISABLE ROW LEVEL SECURITY;
ALTER TABLE passwords DISABLE ROW LEVEL SECURITY;
```

**Note:** This is safe because we're using the service role key only on the server side, not exposed to clients.

## Step 4: Restart Your Development Server

1. **Stop the current server** (if running):
   - Press `Ctrl+C` in the terminal where `npm run dev` is running

2. **Start it again**:
   ```bash
   npm run dev
   ```

   The server will now load the new environment variables from `.env.local`

## Step 5: Test the Application

1. **Open your browser** and go to: http://localhost:3000
2. **You should see the login page** (not a 404 error!)
3. **Log in** with the password you created in Step 2
4. **You should now see the dashboard!**

## Troubleshooting

### Still seeing 404 error?

1. **Check that `.env.local` exists** in the project root
2. **Verify the server was restarted** after creating `.env.local`
3. **Check the terminal** for any error messages
4. **Open browser console** (F12) and check for errors

### Can't log in?

1. **Verify the password was created** in the `passwords` table
2. **Check that `enabled` is set to `true`**
3. **Verify the hash is correct** - try generating a new one

### Database errors?

1. **Check SQL Editor** - make sure all tables were created successfully
2. **Verify RLS is disabled** (Step 3 above)
3. **Check Supabase project status** - make sure it's not paused

## What's Next?

Once you can log in successfully:

- ✅ Upload files
- ✅ Create notes
- ✅ Organize files into collections
- ✅ Access admin dashboard (if logged in as admin)

## Need Help?

- Check `SETUP.md` for more detailed instructions
- Review Supabase logs in the dashboard
- Check browser console (F12) for client-side errors
- Check terminal for server-side errors

---

**You're all set!** 🎉

