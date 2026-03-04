# Plugins Docs

This repository hosts documentation for my Unreal Engine plugins.

## Plugin Documentation

- Replicated Containers docs start here:
  - https://iamsince-1998.github.io/Plugins-Docs/replicated-containers/overview

## Important: GitHub Pages setting (this is the main issue)

If your site is showing README/installation text instead of the Docusaurus docs app, your Pages source is wrong.

Use this:

1. GitHub repo → **Settings** → **Pages**
2. Under **Build and deployment** set **Source = GitHub Actions**
3. Do **not** keep **Deploy from a branch (main/root)**
4. Re-run the latest workflow or push one new commit

After that, open:

- https://iamsince-1998.github.io/Plugins-Docs/

## Local test

```bash
npm ci
npm run start
```

## Production test

```bash
npm run build
npm run serve -- --host 0.0.0.0 --port 4173
```


## If you still see 404 on GitHub Pages

1. Open **Actions** and verify the latest **Deploy to GitHub Pages** workflow is green.
2. Open **Settings → Pages** and set **Source = GitHub Actions**.
3. Open the deployed URL from the workflow summary (this avoids wrong/cached links).
4. Valid project URL should be:
   - `https://iamsince-1998.github.io/Plugins-Docs/`
