# Deploy this existing project to Vercel

This workspace currently has no Git repository/remote and no Vercel project link. To deploy without changing the application:

1. Create a **new empty GitHub repository** in your own GitHub account. Do not initialize it with a README, license, or .gitignore.
2. In PowerShell, from this project folder, run:

   ```powershell
   git init
   git add .
   git status --short
   git commit -m "Initial Sivasakthi Wood Works application"
   git branch -M main
   git remote add origin https://github.com/YOUR_GITHUB_NAME/YOUR_REPOSITORY.git
   git push -u origin main
   ```

   Check that `.env.local` is not staged before committing. The project `.gitignore` excludes `.env.local`, `.env.*`, `node_modules/`, and `dist/`; `.env.example` is allowed.

3. In Vercel, choose **Add New → Project**, import that GitHub repository, and use:
   - Framework preset: Vite (or Other)
   - Build command: `npm run build`
   - Output directory: `dist`
   - Install command: `npm install`
4. In the Vercel project’s **Settings → Environment Variables**, add these for Production (and Preview/Development as desired):
   - `VITE_SUPABASE_URL` — your Supabase project URL
   - `VITE_SUPABASE_PUBLISHABLE_KEY` — your Supabase publishable key

   Never add a Supabase service-role or secret key to frontend environment variables.
5. Deploy. Then add the resulting Vercel domain to Supabase **Authentication → URL Configuration → Redirect URLs** (for example, the exact `https://<deployment-domain>/**` path pattern accepted by that dashboard), save, and redeploy if environment values changed.
6. Open the deployment URL and check product pages and sign-in. Use real test accounts for authenticated flows. Do not place production orders just as a deployment check.
