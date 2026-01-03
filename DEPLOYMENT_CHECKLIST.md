# ✅ Deployment Checklist - Step by Step

Use this checklist to ensure 100% accurate deployment with zero errors.

---

## Phase 1: Database Setup (Supabase) ⚠️ DO THIS FIRST

- [ ] **Step 1.1:** Opened Supabase Dashboard
  - URL: https://supabase.com/dashboard/project/svfdzphvftiwcjqbqquo

- [ ] **Step 1.2:** Created database tables
  - Opened SQL Editor
  - Copied contents from `lib/db/schema.sql`
  - Pasted and ran in SQL Editor
  - ✅ Got "Success. No rows returned"

- [ ] **Step 1.3:** Disabled Row Level Security (RLS)
  - Ran SQL to disable RLS on all tables
  - ✅ Got "Success. No rows returned"

- [ ] **Step 1.4:** Created admin password
  - Generated bcrypt hash at https://bcrypt-generator.com/
  - Inserted into `passwords` table via SQL or Table Editor
  - ✅ Verified password entry exists in database

- [ ] **Step 1.5:** Verified database setup
  - ✅ All 5 tables exist: `files`, `notes`, `collections`, `activity_logs`, `passwords`
  - ✅ Admin password entry exists with `enabled = true`

---

## Phase 2: GitHub Deployment

- [ ] **Step 2.1:** Verified `.gitignore`
  - ✅ `.env.local` is in `.gitignore`
  - ✅ No sensitive files will be committed

- [ ] **Step 2.2:** Initialized Git (if needed)
  ```powershell
  git init
  git add .
  git commit -m "Initial commit"
  ```

- [ ] **Step 2.3:** Created GitHub repository
  - ✅ Repository created on GitHub
  - ✅ Copied repository URL

- [ ] **Step 2.4:** Pushed to GitHub
  ```powershell
  git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
  git branch -M main
  git push -u origin main
  ```
  - ✅ Code is on GitHub
  - ✅ All files visible in repository

---

## Phase 3: Vercel Deployment

- [ ] **Step 3.1:** Connected GitHub to Vercel
  - ✅ Signed in to Vercel
  - ✅ Imported GitHub repository
  - ✅ Project imported successfully

- [ ] **Step 3.2:** Configured project settings
  - ✅ Framework: Vite (auto-detected)
  - ✅ Root Directory: `./`
  - ✅ Build Command: `npm run build`
  - ✅ Output Directory: `dist`
  - ✅ Install Command: `npm install`

- [ ] **Step 3.3:** Added environment variables
  - [ ] `NEXT_PUBLIC_SUPABASE_URL` = `https://svfdzphvftiwcjqbqquo.supabase.co`
    - ✅ Production, Preview, Development checked
  - [ ] `NEXT_PUBLIC_SUPABASE_ANON_KEY` = (your anon key)
    - ✅ Production, Preview, Development checked
  - [ ] `SUPABASE_SERVICE_ROLE_KEY` = (your service role key)
    - ✅ Production, Preview, Development checked
  - [ ] `NEXTAUTH_SECRET` = (generated secure string)
    - ✅ Production, Preview, Development checked
  - [ ] `NEXTAUTH_URL` = (will update after first deploy)
    - ✅ Production, Preview, Development checked

- [ ] **Step 3.4:** Deployed to Vercel
  - ✅ Clicked "Deploy"
  - ✅ Build completed successfully
  - ✅ Got deployment URL

- [ ] **Step 3.5:** Updated NEXTAUTH_URL
  - ✅ Copied deployment URL
  - ✅ Updated `NEXTAUTH_URL` in Vercel settings
  - ✅ Redeployed

---

## Phase 4: Testing & Verification

- [ ] **Step 4.1:** Database connection test
  - ✅ Opened Vercel deployment URL
  - ✅ Opened browser console (F12)
  - ✅ No 404 errors
  - ✅ No "Database not configured" errors
  - ✅ No Supabase connection errors

- [ ] **Step 4.2:** Login test
  - ✅ Login page loads
  - ✅ Can log in with admin password
  - ✅ Dashboard displays after login

- [ ] **Step 4.3:** Feature testing
  - [ ] ✅ File upload works
  - [ ] ✅ File list displays
  - [ ] ✅ Notes creation works
  - [ ] ✅ Collections work
  - [ ] ✅ Admin dashboard accessible (if admin)
  - [ ] ✅ No console errors
  - [ ] ✅ No network errors

- [ ] **Step 4.4:** Vercel logs check
  - ✅ Opened Vercel Dashboard → Functions
  - ✅ No runtime errors
  - ✅ No timeout errors
  - ✅ All API routes responding

---

## Phase 5: Final Verification

### Application Status
- [ ] ✅ Application loads at Vercel URL
- [ ] ✅ No 404 errors
- [ ] ✅ No 500 errors
- [ ] ✅ All pages load correctly

### Database Status
- [ ] ✅ Database connection works
- [ ] ✅ Can read from database
- [ ] ✅ Can write to database
- [ ] ✅ All tables accessible

### Authentication Status
- [ ] ✅ Login works
- [ ] ✅ Logout works
- [ ] ✅ Session persists
- [ ] ✅ Admin access works (if admin user)

### Features Status
- [ ] ✅ File upload works
- [ ] ✅ File download/view works
- [ ] ✅ File delete works
- [ ] ✅ Notes create/edit/delete works
- [ ] ✅ Collections create/edit/delete works
- [ ] ✅ Activity logs work
- [ ] ✅ Admin dashboard works (if admin)

### Security Status
- [ ] ✅ `.env.local` NOT in GitHub
- [ ] ✅ Environment variables set in Vercel
- [ ] ✅ Service role key kept secret
- [ ] ✅ NEXTAUTH_SECRET is strong

---

## 🎉 Deployment Complete!

If all items above are checked:
- ✅ **100% Deployed**
- ✅ **100% Functional**
- ✅ **Zero Errors**

---

## Quick Reference

**Your Supabase Project:**
- URL: https://svfdzphvftiwcjqbqquo.supabase.co
- Project ID: svfdzphvftiwcjqbqquo

**Important URLs:**
- Supabase Dashboard: https://supabase.com/dashboard/project/svfdzphvftiwcjqbqquo
- Vercel Dashboard: https://vercel.com/dashboard
- GitHub Repository: (your repo URL)

**Password Hash Generator:**
- https://bcrypt-generator.com/

---

## Need Help?

See `COMPLETE_DEPLOYMENT_GUIDE.md` for detailed step-by-step instructions.
