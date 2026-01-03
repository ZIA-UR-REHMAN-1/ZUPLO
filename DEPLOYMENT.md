# Deployment Guide - GitHub to Vercel

This guide will help you deploy the Online Files Portal to Vercel via GitHub.

## Prerequisites

1. GitHub account
2. Vercel account (sign up at https://vercel.com)
3. Node.js 18+ installed locally

## Step 1: Prepare Your Code

All code is already prepared and fixed:
- ✅ All infinite loop issues fixed
- ✅ API endpoints corrected
- ✅ Error handling improved
- ✅ Vercel configuration ready

## Step 2: Push to GitHub

### Initialize Git (if not already done)

```bash
# Navigate to project directory
cd "Online Files Portal"

# Initialize git repository
git init

# Add all files
git add .

# Create initial commit
git commit -m "Initial commit: Online Files Portal ready for deployment"

# Add your GitHub repository as remote (replace with your repo URL)
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git

# Push to GitHub
git branch -M main
git push -u origin main
```

### If repository already exists

```bash
git add .
git commit -m "Prepare for Vercel deployment"
git push
```

## Step 3: Deploy to Vercel

### Option A: Via Vercel Dashboard (Recommended)

1. **Go to Vercel Dashboard**
   - Visit https://vercel.com
   - Sign in or create an account

2. **Import Project**
   - Click "Add New..." → "Project"
   - Select "Import Git Repository"
   - Choose your GitHub repository
   - Click "Import"

3. **Configure Project**
   - **Framework Preset**: Vite (should auto-detect)
   - **Root Directory**: `./` (leave as default)
   - **Build Command**: `npm run build` (auto-filled)
   - **Output Directory**: `dist` (auto-filled)
   - **Install Command**: `npm install` (auto-filled)

4. **Environment Variables**
   Click "Environment Variables" and add:
   
   **Required:**
   - `JWT_SECRET` - Generate a secure random string (e.g., use: `openssl rand -base64 32`)
   
   **Optional (for Netlify Blobs):**
   - `NETLIFY_SITE_ID` - Your Netlify site ID (if using Netlify Blobs)
   - `NETLIFY_API_TOKEN` - Your Netlify API token (if using Netlify Blobs)
   - `ADMIN_PASSWORD` - Default admin password for initial setup

5. **Deploy**
   - Click "Deploy"
   - Wait for build to complete
   - Your app will be live at `https://your-project.vercel.app`

### Option B: Via Vercel CLI

```bash
# Install Vercel CLI globally
npm i -g vercel

# Login to Vercel
vercel login

# Deploy (from project directory)
vercel

# Follow the prompts:
# - Set up and deploy? Yes
# - Which scope? Select your account
# - Link to existing project? No (first time) or Yes (updates)
# - Project name? online-files-portal (or your choice)
# - Directory? ./
# - Override settings? No

# For production deployment
vercel --prod
```

## Step 4: Configure Environment Variables (CLI Method)

If using CLI, set environment variables:

```bash
# Set JWT_SECRET (required)
vercel env add JWT_SECRET

# Set optional variables
vercel env add NETLIFY_SITE_ID
vercel env add NETLIFY_API_TOKEN
vercel env add ADMIN_PASSWORD
```

Or set them in the Vercel Dashboard:
- Go to your project
- Settings → Environment Variables
- Add each variable

## Step 5: Verify Deployment

1. **Check Build Logs**
   - Go to your project in Vercel Dashboard
   - Check "Deployments" tab
   - Verify build completed successfully

2. **Test Your Application**
   - Visit your deployment URL
   - Test login functionality
   - Test file upload
   - Test all features

3. **Check Function Logs**
   - Go to "Functions" tab in Vercel Dashboard
   - Monitor for any errors

## Troubleshooting

### Build Fails

**Error: Module not found**
```bash
# Clear cache and reinstall
rm -rf node_modules package-lock.json
npm install
git add .
git commit -m "Fix dependencies"
git push
```

**Error: TypeScript errors**
```bash
# Check for TypeScript errors locally
npx tsc --noEmit

# Fix any errors before deploying
```

### Functions Not Working

**Check Function Logs:**
- Go to Vercel Dashboard → Your Project → Functions
- Check for runtime errors
- Verify environment variables are set

**Verify API Routes:**
- All API calls should go to `/api/*`
- Functions are in `netlify/functions/` directory
- Vercel will automatically serve them

### Environment Variables Not Working

1. **Verify in Dashboard:**
   - Settings → Environment Variables
   - Ensure variables are set for "Production", "Preview", and "Development"

2. **Redeploy:**
   - After adding/changing env vars, redeploy
   - Go to Deployments → Click "..." → Redeploy

### Storage Issues

**If using Netlify Blobs:**
- Ensure `NETLIFY_SITE_ID` and `NETLIFY_API_TOKEN` are set
- You need a Netlify account with Blobs enabled

**Alternative: Use Vercel KV**
- Create KV database in Vercel Dashboard
- Update `netlify/functions/_utils.ts` to use Vercel KV
- See README.md for migration guide

## Post-Deployment Checklist

- [ ] Application loads successfully
- [ ] Login works
- [ ] File upload works
- [ ] Notes creation works
- [ ] Collections work
- [ ] Admin dashboard accessible
- [ ] No console errors
- [ ] All API endpoints responding
- [ ] Environment variables configured
- [ ] Custom domain configured (optional)

## Updating Your Deployment

After making changes:

```bash
# Make your changes
git add .
git commit -m "Your change description"
git push

# Vercel will automatically redeploy
# Or manually trigger:
vercel --prod
```

## Custom Domain (Optional)

1. Go to Vercel Dashboard → Your Project → Settings → Domains
2. Add your domain
3. Follow DNS configuration instructions
4. Wait for DNS propagation (can take up to 24 hours)

## Support

- **Vercel Docs**: https://vercel.com/docs
- **Vercel Support**: https://vercel.com/support
- **Project Issues**: Check GitHub repository issues

---

**Your application is now ready for production! 🚀**

