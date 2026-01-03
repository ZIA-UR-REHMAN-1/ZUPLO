# Online Files Portal

A modern, secure file management and storage application built with React, TypeScript, and Vite.

## Features

- 🔐 Secure authentication system
- 📁 File upload and management
- 📝 Notes and text vault
- 📚 Collections organization
- 👥 Admin dashboard
- 📊 Analytics and activity tracking
- 🎨 Modern, responsive UI with dark mode

## Tech Stack

- **Frontend**: React 18, TypeScript, Vite
- **Styling**: Tailwind CSS, Framer Motion
- **Backend**: Serverless Functions (Vercel/Netlify)
- **Storage**: Netlify Blobs / Vercel KV
- **Authentication**: JWT tokens

## Getting Started

### Prerequisites

- Node.js 18+ and npm
- Git

### Installation

1. Clone the repository:
```bash
git clone <your-repo-url>
cd "Online Files Portal"
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm run dev
```

4. Open your browser and navigate to `http://localhost:5173`

## Deployment to Vercel

### Option 1: Deploy via Vercel Dashboard

1. Push your code to GitHub
2. Go to [Vercel Dashboard](https://vercel.com)
3. Click "New Project"
4. Import your GitHub repository
5. Vercel will automatically detect the configuration
6. Click "Deploy"

### Option 2: Deploy via Vercel CLI

1. Install Vercel CLI:
```bash
npm i -g vercel
```

2. Login to Vercel:
```bash
vercel login
```

3. Deploy:
```bash
vercel
```

4. For production:
```bash
vercel --prod
```

### Environment Variables

If you're using Netlify Blobs, you'll need to set these environment variables in Vercel:

- `NETLIFY_SITE_ID` - Your Netlify site ID (if using Netlify Blobs)
- `NETLIFY_API_TOKEN` - Your Netlify API token (if using Netlify Blobs)
- `ADMIN_PASSWORD` - Default admin password (optional, for initial setup)
- `JWT_SECRET` - Secret key for JWT tokens (generate a secure random string)

To set environment variables in Vercel:
1. Go to your project settings
2. Navigate to "Environment Variables"
3. Add the required variables

### Storage Options

#### Option 1: Netlify Blobs (Current)
The project currently uses Netlify Blobs. To use this on Vercel:
- Set `NETLIFY_SITE_ID` and `NETLIFY_API_TOKEN` environment variables
- The functions will work as-is

#### Option 2: Vercel KV (Recommended for Vercel)
To migrate to Vercel KV:
1. Create a Vercel KV database in your Vercel dashboard
2. Update `netlify/functions/_utils.ts` to use Vercel KV instead of Netlify Blobs
3. Install `@vercel/kv`: `npm install @vercel/kv`

## Project Structure

```
├── src/                    # Frontend source code
│   ├── components/        # React components
│   ├── screens/          # Page components
│   ├── hooks/            # Custom React hooks
│   ├── lib/              # Utility libraries
│   └── router.tsx        # React Router configuration
├── netlify/functions/     # Serverless functions
│   ├── _utils.ts         # Shared utilities
│   └── *.ts              # API endpoints
├── public/               # Static assets
├── dist/                 # Build output (gitignored)
└── vercel.json          # Vercel configuration
```

## API Endpoints

All API endpoints are prefixed with `/api/`:

- `POST /api/auth-login` - User authentication
- `GET /api/files-list` - List files
- `POST /api/files-upload` - Upload file
- `POST /api/files-delete` - Delete file
- `GET /api/notes-list` - List notes
- `POST /api/notes-create` - Create note
- `PUT /api/notes-update` - Update note
- `DELETE /api/notes-delete` - Delete note
- `GET /api/collections-list` - List collections
- `POST /api/collections-create` - Create collection
- And more...

## Build

To build for production:

```bash
npm run build
```

The output will be in the `dist/` directory.

## Development

```bash
npm run dev
```

## Troubleshooting

### Stack Overflow Errors
All infinite loop issues have been fixed. If you encounter any:
1. Clear browser cache
2. Check browser console for specific errors
3. Ensure all dependencies are installed: `npm install`

### API Errors
- Check that environment variables are set correctly
- Verify serverless functions are deployed
- Check Vercel function logs in the dashboard

### Build Errors
- Ensure Node.js version is 18+
- Delete `node_modules` and `package-lock.json`, then run `npm install`
- Check TypeScript errors: `npx tsc --noEmit`

## License

Private project - All rights reserved

## Support

For issues or questions, please check the project documentation or create an issue in the repository.

