# GharVerified — Verified Rental Listings (Demo)

A working front-end for a verified rentals platform: renter search/browse
side + a password-protected owner/admin dashboard for approving and
verifying listings — backed by a real shared **Supabase** database.

## 1. Create the Supabase project
1. Go to [supabase.com](https://supabase.com) → New project (free tier is fine).
2. Once it's ready, open **SQL Editor** → New query, paste the contents of
   `supabase_schema.sql` from this folder, and click **Run**. This creates
   the `listings` table, locks it down with Row Level Security, and seeds 3
   demo listings.
3. Go to **Project Settings → API** and copy your **Project URL** and
   **anon public key**.
4. Open `index.html` and near the top of the `<script>` block, replace:
   ```js
   const SUPABASE_URL = 'https://YOUR-PROJECT-REF.supabase.co';
   const SUPABASE_ANON_KEY = 'YOUR-ANON-PUBLIC-KEY';
   ```
   with your real values. (The anon key is safe to ship in front-end code —
   Row Level Security is what actually controls who can read/write what.)

## 2. Create an admin login
Go to **Authentication → Users → Add user** in the Supabase dashboard and
create yourself an account with an email + password. That's what you'll use
to sign in on the "Owner / Admin" tab — only signed-in users can add,
approve, verify, or block listings; anonymous visitors can only read
listings marked `approved`.

## 3. Run it
Just open `index.html` in a browser. No build step, no install — it talks
to Supabase directly over the internet.

## What's inside
- **Renter view:** filter by location, rent, BHK/room type, furnishing,
  family/bachelor. Verified listings show a gold seal badge.
- **Admin/Owner view:** password-gated (demo password `admin123`). Add a
  listing, approve/block it, toggle its verified badge, see quick stats.

## Push this to your own GitHub
I can't push to your GitHub account directly — I don't have your login or a
token. Run this from a terminal on your machine, inside this folder:

```bash
git init
git add .
git commit -m "Initial commit: GharVerified rental platform demo"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

(Create the empty repo on github.com first, or use `gh repo create` if you
have the GitHub CLI installed.)

## Turning this into a real product
- ~~Backend/database~~ — done via Supabase above.
- ~~Auth~~ — done via Supabase Auth above. Next step: separate "owner" vs
  "admin" roles (right now any signed-in user is treated as admin) — add a
  `role` column to a `profiles` table and check it in the RLS policies.
- **File uploads:** photos/videos and verification documents need real file
  storage (S3, Cloudinary, Firebase Storage) instead of the placeholder
  colored thumbnails used here.
- **Payments:** for Featured Listing / premium owner plans, add Razorpay or
  Stripe.
- **Reviews & chat:** currently stubbed out — add a reviews table and a
  simple chat/enquiry log tied to each listing.

This matches the MVP scope you outlined: free listings first, with Featured
Listing (₹299–₹999) as the first thing to test paying demand for.
