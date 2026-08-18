# Minimal Hugo Blog

A tiny Hugo blog with no third-party theme dependency, built by GitHub Actions and hosted on GitHub Pages.

## 1. Edit the site identity

Open `hugo.toml` and change:

- `baseURL`
- `title`
- `params.author`
- `params.description`

The GitHub Pages workflow overrides `baseURL` during deployment, so local placeholder values do not prevent deployment.

## 2. Develop on NixOS

```bash
nix develop
hugo server -D
```

## 3. Create a post

```bash
hugo new content posts/my-new-post.md
```

Edit the file, then change `draft: true` to `draft: false` when ready.

## 4. Push to GitHub

Create an empty GitHub repository, then from this directory:

```bash
git init
git add .
git commit -m "Initial Hugo blog"
git branch -M main
git remote add origin git@github.com:YOUR_USERNAME/YOUR_REPOSITORY.git
git push -u origin main
```

On GitHub go to:

**Repository → Settings → Pages → Build and deployment → Source → GitHub Actions**

Every later push to `main` will rebuild and deploy the site.

## 5. Custom domain

In GitHub:

**Repository → Settings → Pages → Custom domain**

Enter your domain before changing DNS.

### Apex domain (`example.com`)

Create these A records at your DNS provider:

```text
@  A  185.199.108.153
@  A  185.199.109.153
@  A  185.199.110.153
@  A  185.199.111.153
```

Optional IPv6 AAAA records:

```text
@  AAAA  2606:50c0:8000::153
@  AAAA  2606:50c0:8001::153
@  AAAA  2606:50c0:8002::153
@  AAAA  2606:50c0:8003::153
```

For `www`, add:

```text
www  CNAME  YOUR_USERNAME.github.io
```

For a subdomain such as `blog.example.com`, use:

```text
blog  CNAME  YOUR_USERNAME.github.io
```

Because this site is deployed with a custom GitHub Actions workflow, a repository `CNAME` file is not needed.

After DNS is accepted by GitHub, enable **Enforce HTTPS** in Pages settings.
