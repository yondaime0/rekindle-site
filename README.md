# rekindle-site

Static pages for Rekindle, served by GitHub Pages from the **public** repo `yondaime0/rekindle-site`:

- https://yondaime0.github.io/rekindle-site/ (home)
- https://yondaime0.github.io/rekindle-site/privacy/ (privacy policy, linked from the app and Google's consent screen)
- https://yondaime0.github.io/rekindle-site/delete-account/ (account deletion, the Play Data safety deletion URL)
- https://yondaime0.github.io/rekindle-site/terms/ (Terms of Use, linked from the paywall)

No JavaScript, no trackers, no build step. Contact: yondaime869@gmail.com.

This folder lives in the private app repo (`site/`) as the source. Publish it as follows.

## Publish (once)

1. Sign in to GitHub CLI as **yondaime0** (`gh auth status` shows who you are):
   ```bash
   gh auth login            # choose GitHub.com, HTTPS, log in as yondaime0
   # or, if both accounts are stored:  gh auth switch -u yondaime0
   ```
2. Create the public repo and push this folder:
   ```bash
   # a separate checkout, so the app repo never contains a nested repo
   cp -R /Users/volodymyr/Documents/projects/ember/site /Users/volodymyr/Documents/projects/rekindle-site
   cd /Users/volodymyr/Documents/projects/rekindle-site
   git init -b main
   git add .
   git commit -m "Rekindle site: home, privacy policy, account deletion"
   gh repo create yondaime0/rekindle-site --public --source . --remote origin --push
   ```
   (Without `gh`: create the repo at github.com/new as yondaime0, name `rekindle-site`, **Public**, no README, then
   `git remote add origin https://github.com/yondaime0/rekindle-site.git && git push -u origin main`.)
3. Turn on Pages: repo → **Settings → Pages** → Source **Deploy from a branch**, branch `main`, folder `/ (root)` → **Save**.
   Or from the terminal:
   ```bash
   gh api -X POST repos/yondaime0/rekindle-site/pages -f 'source[branch]=main' -f 'source[path]=/'
   ```
4. Wait for "Your site is live" (1–2 minutes), then check:
   ```bash
   curl -sf -o /dev/null https://yondaime0.github.io/rekindle-site/privacy/ \
     && curl -sf -o /dev/null https://yondaime0.github.io/rekindle-site/delete-account/ && echo OK
   ```

## Update later

Edit the files here, copy them into `/Users/volodymyr/Documents/projects/rekindle-site` (`rsync -a --delete --exclude .git site/ ../rekindle-site/`), commit and push there.
Pages redeploys on every push to `main`.
