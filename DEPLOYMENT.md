# Deployment Guide - Sithmi Sasanka Portfolio

This guide provides detailed instructions for deploying your portfolio website to various hosting platforms.

## Table of Contents

- [Vercel Deployment (Recommended)](#vercel-deployment-recommended)
- [GitHub Pages Deployment](#github-pages-deployment)
- [Netlify Deployment](#netlify-deployment)
- [Other Platforms](#other-platforms)
- [Custom Domain Setup](#custom-domain-setup)
- [Environment Variables](#environment-variables)
- [Troubleshooting](#troubleshooting)

---

## Vercel Deployment (Recommended)

Vercel is the recommended platform for deploying Vite applications. It offers zero-configuration deployment, automatic HTTPS, and excellent performance.

### Prerequisites

- A Vercel account (free) - [Sign up here](https://vercel.com/signup)
- Your portfolio code in a Git repository (GitHub, GitLab, or Bitbucket)

### Method 1: Deploy via Vercel Dashboard (Easiest)

#### Step 1: Connect Your Repository

1. Go to [vercel.com](https://vercel.com) and log in
2. Click **"Add New..."** → **"Project"**
3. Click **"Import Git Repository"**
4. If this is your first time:
   - Click **"Connect Git Provider"**
   - Authorize Vercel to access your repositories
5. Select your portfolio repository from the list

#### Step 2: Configure Project

Vercel will automatically detect your Vite configuration. You should see:

- **Framework Preset:** Vite
- **Build Command:** `vite build`
- **Output Directory:** `dist`
- **Install Command:** `npm install`

**You don't need to change anything!** Vercel handles everything automatically.

#### Step 3: Deploy

1. Click **"Deploy"**
2. Wait for the build to complete (usually 1-2 minutes)
3. Once deployed, you'll get a URL like: `https://your-portfolio-xxx.vercel.app`

#### Step 4: Automatic Deployments

Vercel automatically sets up continuous deployment:

- Every push to your **main/master** branch → Production deployment
- Every push to other branches → Preview deployment
- Pull requests → Automatic preview deployments

### Method 2: Deploy via Vercel CLI

#### Step 1: Install Vercel CLI

```bash
npm install -g vercel
```

#### Step 2: Login to Vercel

```bash
vercel login
```

Follow the prompts to authenticate.

#### Step 3: Deploy

Navigate to your project directory and run:

```bash
cd "/Users/sahanwasala/Downloads/Portfolio - Sithmi"
vercel
```

Follow the prompts:

- **Set up and deploy?** → Yes
- **Which scope?** → Select your account
- **Link to existing project?** → No (first time) or Yes (subsequent deployments)
- **What's your project's name?** → sithmi-sasanka-portfolio (or your choice)
- **In which directory is your code located?** → ./ (press Enter)

Vercel will:

1. Detect your framework (Vite)
2. Build your project
3. Deploy to a preview URL

#### Step 4: Deploy to Production

```bash
vercel --prod
```

### Vercel Project Settings

After deployment, you can configure additional settings:

1. Go to your project dashboard on Vercel
2. Click **"Settings"**

**Useful settings:**

- **General** → Change project name
- **Domains** → Add custom domain
- **Environment Variables** → Add secrets (if needed)
- **Git** → Configure which branches trigger deployments

---

## GitHub Pages Deployment

GitHub Pages is a free hosting service for static websites directly from your GitHub repository.

### Prerequisites

- A GitHub account
- Your portfolio code in a GitHub repository
- `gh-pages` package (already included in dependencies)

### Step 1: Verify Configuration

Check that your `package.json` has the correct homepage:

```json
{
  "homepage": "https://YOUR_GITHUB_USERNAME.github.io/SithmiSasankaPortfolio/"
}
```

**Important:** Replace `YOUR_GITHUB_USERNAME` with your actual GitHub username.

### Step 2: Add Deployment Scripts

Your `package.json` should include these scripts:

```json
"scripts": {
  "dev": "vite",
  "build": "tsc && vite build",
  "preview": "vite preview",
  "predeploy": "npm run build",
  "deploy": "gh-pages -d dist"
}
```

If they're not present, add the `predeploy` and `deploy` scripts.

### Step 3: Update Vite Configuration

Ensure your `vite.config.js` has the correct base path:

```javascript
export default defineConfig({
  plugins: [react()],
  base: './', // This ensures relative paths work
  // ... other config
});
```

### Step 4: Deploy

Run the deployment command:

```bash
npm run deploy
```

This will:

1. Run `npm run build` (via predeploy script)
2. Create a production build in `dist/`
3. Push the `dist/` folder to the `gh-pages` branch
4. Make it available on GitHub Pages

### Step 5: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **"Settings"** (top navigation)
3. Scroll down to **"Pages"** (left sidebar)
4. Under **"Source"**:
   - Branch: Select `gh-pages`
   - Folder: Select `/ (root)`
5. Click **"Save"**

### Step 6: Access Your Site

Your portfolio will be live at:

```
https://YOUR_GITHUB_USERNAME.github.io/SithmiSasankaPortfolio/
```

**Note:** It may take a few minutes for changes to appear.

### Updating Your Site

Every time you want to update your deployed site:

```bash
npm run deploy
```

This rebuilds and redeploys automatically.

---

## Netlify Deployment

Netlify offers continuous deployment, serverless functions, and form handling.

### Method 1: Deploy via Netlify Dashboard

#### Step 1: Sign Up/Login

Go to [netlify.com](https://www.netlify.com) and create an account or log in.

#### Step 2: Import Project

1. Click **"Add new site"** → **"Import an existing project"**
2. Choose your Git provider (GitHub, GitLab, Bitbucket)
3. Authorize Netlify to access your repositories
4. Select your portfolio repository

#### Step 3: Configure Build Settings

Netlify should auto-detect Vite, but verify these settings:

- **Base directory:** (leave empty)
- **Build command:** `npm run build`
- **Publish directory:** `dist`

#### Step 4: Deploy

1. Click **"Deploy site"**
2. Wait for the build to complete
3. Your site will be live at: `https://random-name-12345.netlify.app`

#### Step 5: Change Site Name (Optional)

1. Go to **"Site settings"** → **"General"** → **"Site details"**
2. Click **"Change site name"**
3. Enter a custom name: `sithmi-sasanka-portfolio`
4. Your new URL: `https://sithmi-sasanka-portfolio.netlify.app`

### Method 2: Deploy via Netlify CLI

#### Step 1: Install Netlify CLI

```bash
npm install -g netlify-cli
```

#### Step 2: Login

```bash
netlify login
```

This opens a browser window for authentication.

#### Step 3: Initialize and Deploy

```bash
cd "/Users/sahanwasala/Downloads/Portfolio - Sithmi"

# Build the project
npm run build

# Initialize Netlify
netlify init

# Or deploy directly
netlify deploy --prod --dir=dist
```

Follow the prompts to complete setup.

### Method 3: Drag and Drop Deploy

1. Build your project locally:

   ```bash
   npm run build
   ```

2. Go to [app.netlify.com/drop](https://app.netlify.com/drop)

3. Drag and drop your `dist/` folder

4. Your site is live instantly!

---

## Other Platforms

### AWS Amplify

1. Go to [AWS Amplify Console](https://console.aws.amazon.com/amplify/)
2. Click **"New app"** → **"Host web app"**
3. Connect your Git repository
4. Build settings:
   - Build command: `npm run build`
   - Output directory: `dist`
5. Deploy

### Firebase Hosting

```bash
# Install Firebase CLI
npm install -g firebase-tools

# Login
firebase login

# Initialize
firebase init hosting

# Build
npm run build

# Deploy
firebase deploy
```

### Cloudflare Pages

1. Go to [Cloudflare Pages](https://pages.cloudflare.com/)
2. Click **"Create a project"**
3. Connect your Git repository
4. Build settings:
   - Build command: `npm run build`
   - Output directory: `dist`
5. Deploy

---

## Custom Domain Setup

### Vercel

1. Go to your project on Vercel
2. Click **"Settings"** → **"Domains"**
3. Enter your custom domain (e.g., `sithmisasanka.com`)
4. Click **"Add"**
5. Update your domain's DNS settings:
   - **A Record:** Point to Vercel's IP: `76.76.21.21`
   - **CNAME Record:** Point `www` to `cname.vercel-dns.com`
6. Wait for DNS propagation (up to 48 hours, usually much faster)

### GitHub Pages

1. Go to repository **"Settings"** → **"Pages"**
2. Under **"Custom domain"**, enter your domain
3. Click **"Save"**
4. Update your domain's DNS:
   - **A Records:** Point to GitHub's IPs:

     ```
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
     ```

   - **CNAME Record:** Point `www` to `YOUR_GITHUB_USERNAME.github.io`

### Netlify

1. Go to **"Site settings"** → **"Domain management"**
2. Click **"Add custom domain"**
3. Enter your domain
4. Update DNS settings as instructed by Netlify
5. Enable HTTPS (automatic with Let's Encrypt)

---

## Environment Variables

If your portfolio uses environment variables (e.g., for API keys):

### Vercel

1. Go to **"Settings"** → **"Environment Variables"**
2. Add variables:
   - **Name:** `VITE_API_KEY`
   - **Value:** Your API key
   - **Environment:** Production, Preview, Development
3. Redeploy for changes to take effect

### Netlify

1. Go to **"Site settings"** → **"Environment variables"**
2. Click **"Add a variable"**
3. Enter key and value
4. Redeploy

### GitHub Pages

GitHub Pages doesn't support environment variables. For sensitive data:

- Use a backend service
- Or deploy to Vercel/Netlify instead

**Important:** Never commit sensitive keys to Git! Use `.env` files and add them to `.gitignore`.

---

## Troubleshooting

### Build Fails on Deployment

**Issue:** Build succeeds locally but fails on deployment

**Solutions:**

1. Check Node.js version:

   ```json
   // Add to package.json
   "engines": {
     "node": ">=16.0.0"
   }
   ```

2. Clear cache and rebuild:
   - **Vercel:** Redeploy with "Clear cache and redeploy"
   - **Netlify:** Site settings → Build & deploy → Clear cache

3. Check build logs for specific errors

### 404 Errors on Refresh

**Issue:** Page not found when refreshing on routes

**Solution:** Configure redirects

**Vercel:** Create `vercel.json`:

```json
{
  "rewrites": [
    { "source": "/(.*)", "destination": "/index.html" }
  ]
}
```

**Netlify:** Create `public/_redirects`:

```
/*    /index.html   200
```

### Assets Not Loading

**Issue:** CSS/JS files return 404

**Solution:** Check `base` path in `vite.config.js`:

- For Vercel/Netlify: `base: './'` or `base: '/'`
- For GitHub Pages: `base: '/SithmiSasankaPortfolio/'`

### Slow Build Times

**Solutions:**

1. Use build caching (enabled by default on most platforms)
2. Optimize dependencies - remove unused packages
3. Consider using `vite build --mode production` for optimizations

### Custom Domain Not Working

**Solutions:**

1. Wait for DNS propagation (up to 48 hours)
2. Check DNS settings with: `dig yourdomain.com`
3. Ensure HTTPS is enabled
4. Clear browser cache

---

## Performance Optimization

### Enable Compression

Most platforms enable Gzip/Brotli compression automatically. Verify in Network tab (DevTools).

### CDN and Caching

- **Vercel:** Automatic global CDN
- **Netlify:** Automatic CDN with edge caching
- **GitHub Pages:** Uses Fastly CDN

### Lighthouse Score

Test your deployed site:

1. Open Chrome DevTools
2. Go to **"Lighthouse"** tab
3. Run audit
4. Aim for 90+ scores in all categories

---

## Continuous Deployment Workflow

### Recommended Git Workflow

```bash
# Make changes
git add .
git commit -m "Update portfolio content"

# Push to trigger deployment
git push origin main
```

### Branch-based Deployments

- **main/master** → Production
- **develop** → Staging/Preview
- **feature branches** → Preview deployments (Vercel/Netlify)

---

## Support and Resources

### Vercel

- [Documentation](https://vercel.com/docs)
- [Community](https://github.com/vercel/vercel/discussions)

### GitHub Pages

- [Documentation](https://docs.github.com/en/pages)
- [Troubleshooting](https://docs.github.com/en/pages/getting-started-with-github-pages/troubleshooting-404-errors-for-github-pages-sites)

### Netlify

- [Documentation](https://docs.netlify.com/)
- [Community](https://answers.netlify.com/)

---

**Need help?** Open an issue on your repository or consult the platform-specific documentation.

**Happy deploying! 🚀**
