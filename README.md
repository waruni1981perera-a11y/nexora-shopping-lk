# Nexora Shopping LK

Luxury-dark e-commerce starter project for GitHub Pages + Supabase.

## Can I make it on GitHub?
Yes. GitHub Pages can host the static HTML/CSS/JavaScript files for free. Supabase provides the real database and customer authentication. GitHub Pages alone cannot securely store accounts, orders or messages, so configure Supabase before using the store with customers.

## Files
- `index.html` — storefront, login/signup, cart, checkout, message form and admin panel.
- `style.css` — responsive luxury black-and-gold design.
- `app.js` — frontend logic and Supabase connection.
- `supabase-setup.sql` — database tables, access rules and sample products.

## Step 1 — Create the Supabase backend
1. Create a project at https://supabase.com/.
2. Open **SQL Editor** in your Supabase project.
3. Paste all of `supabase-setup.sql` and run it.
4. Go to **Project Settings → API** (or **Data API**) and copy the Project URL and `anon` / publishable key.
5. Open `app.js` and replace:
   - `YOUR_SUPABASE_PROJECT_URL`
   - `YOUR_SUPABASE_ANON_PUBLIC_KEY`
6. Save the file. The anon/publishable key is designed for browser use with RLS. NEVER put a `service_role` or secret key in `app.js`.

## Step 2 — Create your admin account
1. Open the website and use **Create account** to register with your own email.
2. Confirm your email if Supabase asks you to.
3. In Supabase, open **Authentication → Users** and copy your user's UUID.
4. In SQL Editor, run this command with your real UUID:
   ```sql
   insert into public.admin_users (user_id)
   values ('PASTE-YOUR-USER-UUID-HERE');
   ```
5. Sign in on the website. Press **Ctrl + Shift + A** on Windows (or open the admin shortcut after signing in) to open the admin dashboard.
6. Use the dashboard to add products. Orders and messages appear there.

## Step 3 — Publish on GitHub Pages
1. Sign in to https://github.com/ and create a new public repository, e.g. `nexora-shopping-lk`.
2. Upload `index.html`, `style.css`, and `app.js` to the repository root. Keep the filenames unchanged.
3. Open repository **Settings → Pages**.
4. Under **Build and deployment**, choose **Deploy from a branch**.
5. Select branch `main` and folder `/ (root)`, then click **Save**.
6. Wait for GitHub Pages to publish. Your site URL will look like `https://YOUR-USERNAME.github.io/nexora-shopping-lk/`.

## Important before accepting real orders
- Configure your Supabase project and test sign-up, email confirmation, sign-in, product loading, checkout, and admin access.
- GitHub Pages is static hosting. Do not put passwords, private API keys, or service-role keys in frontend files.
- The current checkout supports **Cash on Delivery** and **Bank Transfer (manual confirmation)**. Add your bank details and a process for checking transfers before launch.
- Card payments are deliberately disabled in the form. To accept cards, integrate a payment provider that supports your business and Sri Lanka, using its secure server-side checkout flow and verified payment callbacks. Do not mark an order paid just because the browser says payment succeeded.
- Delivery fees, stock validation, tax, refunds, order-status editing, email notifications, and payment verification should be added/tested before a commercial launch.
- The admin dashboard shortcut is `Ctrl + Shift + A`. Admin access is controlled by the Supabase `admin_users` table, not by a hard-coded PIN.

## Local preview
You can double-click `index.html` for a visual preview. For the Supabase-connected version, use a local web server or your published GitHub Pages URL.
