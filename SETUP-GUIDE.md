# CrestFC Admin Portal: setup guide (plain language)

STATUS: This has been tested on a practice copy on my side only. It is NOT live yet.
It becomes live only after you do the steps below and test it once yourself.

Why extra steps are needed: your current site is a set of plain pages that you
drag and drop. An admin portal needs a small server part (Netlify "Functions" and
"Blobs" storage). Netlify only builds those when the site comes from a GitHub
repository, not from drag and drop.

## Step 1: Put the project on GitHub (free, no coding)
1. Create a free account at github.com.
2. Click "New repository". Name it `crestfc`. Choose **Private**. Click Create.
3. Click "uploading an existing file". Unzip `crestfc-with-admin.zip` on your computer,
   open the unzipped folder, select EVERYTHING inside it (the `site` folder,
   `netlify` folder, `netlify.toml`, `package.json`, `.gitignore`), drag it into the page,
   and click "Commit changes".
   (Do not upload a `tests` folder if you see one; it is not needed.)

## Step 2: Connect GitHub to Netlify
Option A (keeps your address crestfc.netlify.app):
1. Netlify > your CrestFC site > Project configuration > Build & deploy >
   Continuous deployment > Link repository (or "Link site to Git") > GitHub >
   choose `crestfc`. Leave build command empty. It should read publish directory `site`
   and functions `netlify/functions` from the file automatically.
Option B (if Option A is not offered): Add new site > Import from Git > choose `crestfc`,
then rename the new site to `crestfc` in Site configuration > Change site name
(you may need to rename or delete the old site first).

## Step 3: Set your admin login (this is the secret part)
Netlify > Site configuration > Environment variables > Add a variable:
- `ADMIN_EMAIL` = the email you will sign in with
- `ADMIN_PASSWORD` = a long unique password, at least 12 characters. Mark it "Contains secret values".
Never send the password to anyone or put it in GitHub.
Then go to Deploys > Trigger deploy > Deploy site (variables apply only to new deploys).

## Step 4: Test it yourself
1. Open https://crestfc.netlify.app/admin/ and sign in.
2. Players: change a shirt number, save, open the public site in another tab, refresh. It should change.
3. Matches: add one match. A "Matches" section should now appear on the public site.
   Delete it and the section disappears again (your site looks like it does today).
4. Site content: edit a heading, save, refresh the public site.

## Good to know
- Change password: edit `ADMIN_PASSWORD` in Netlify, redeploy. Everyone gets signed out.
- Five wrong passwords lock sign-in for 15 minutes.
- Your data is stored in Netlify Blobs, so it survives re-deploys. Deploying new code
  does not erase it.
- Check that your Netlify plan includes Functions and Blobs (the free plan normally does; limits apply).
- Everything is exact-same look as before. Matches stay hidden until you add one.

## If something fails
Send me the exact message you see (a screenshot is fine) and the step you were on.
