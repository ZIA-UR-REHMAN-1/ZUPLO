# ⚡ Quick Deployment - 5 Minute Guide

**For experienced users who want to deploy fast.**

---

## 1. Database Setup (Supabase)

```sql
-- Run in Supabase SQL Editor
-- 1. Copy/paste contents from lib/db/schema.sql
-- 2. Run this to disable RLS:
ALTER TABLE files DISABLE ROW LEVEL SECURITY;
ALTER TABLE notes DISABLE ROW LEVEL SECURITY;
ALTER TABLE collections DISABLE ROW LEVEL SECURITY;
ALTER TABLE activity_logs DISABLE ROW LEVEL SECURITY;
ALTER TABLE passwords DISABLE ROW LEVEL SECURITY;

-- 3. Create admin password (replace hash):
INSERT INTO passwords (hash, role, enabled, label)
VALUES ('$2a$10$YOUR_HASH_HERE', 'admin', true, 'Admin');
```

## 2. GitHub

```powershell
# Use Next.js package.json
Copy-Item package-nextjs.json package.json -Force
npm install

# Git
git init
git add .
git commit -m "Ready for deployment"
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git branch -M main
git push -u origin main
```

## 3. Vercel

1. **Import from GitHub**
   - Go to https://vercel.com
   - Import your repository
   - Framework: **Next.js** (auto-detect)

2. **Add Environment Variables:**
   ```
   NEXT_PUBLIC_SUPABASE_URL=https://svfdzphvftiwcjqbqquo.supabase.co
   NEXT_PUBLIC_SUPABASE_ANON_KEY=(your anon key)
   SUPABASE_SERVICE_ROLE_KEY=(your service role key)
   NEXTAUTH_SECRET=(generate random string)
   NEXTAUTH_URL=(update after first deploy)
   ```

3. **Deploy** → Wait → Done!

## 4. Update NEXTAUTH_URL

After first deploy, update `NEXTAUTH_URL` in Vercel with your actual URL, then redeploy.

---

**See `COMPLETE_DEPLOYMENT_GUIDE.md` for detailed instructions.**

