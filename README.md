# PEPE ON BAG — GitHub Pages site

Everything you need is in this one folder.

```
pepeonbag/
  index.html        ← the site
  pepe-bag.jpg      ← hero image
  ca.txt            ← contract address lives here
  CNAME             ← pepeonbag.xyz (already set)
  CNAME.example     ← same domain, keep as backup
  README.md
```

## 1. Put it on GitHub

1. Create a new public repo (example name: `pepeonbag`).
2. Upload **the files inside this folder** to the repo root — not the folder itself.
   You want `index.html` at:
   `https://github.com/YOURUSER/pepeonbag/blob/main/index.html`
3. Repo → **Settings** → **Pages**
   - Source: **Deploy from a branch**
   - Branch: `main` / `/ (root)`
   - Save
4. Wait a minute. Site will be at:
   `https://YOURUSER.github.io/pepeonbag/`

If you want a clean URL like `https://YOURUSER.github.io/` instead, create the repo named `YOURUSER.github.io` and put these files in that repo’s root.

## 2. Contract address (`ca.txt`)

The site reads the first non-comment line of `ca.txt`.

Edit `ca.txt` in the repo to:

```
# comments are ignored
YOURCONTRACTADDRESSHERE
```

Commit. The live site picks it up on refresh (hard refresh if your browser cached the old file).

No rebuild needed. No HTML edit needed.

## 3. Custom domain + nameserver / DNS

Domain: **pepeonbag.xyz**

The `CNAME` file in this folder is already set to that.

### A. Tell GitHub the domain

1. Commit `CNAME` to the repo root (already contains `pepeonbag.xyz`).
2. GitHub Pages → Custom domain → enter `pepeonbag.xyz` → Save.
3. Check **Enforce HTTPS** after DNS finishes (minutes to a few hours).

### B. What to add at your registrar / nameserver

Use **one** of these setups.

#### Option 1 — Cloudflare (easiest)

Add the domain to Cloudflare and use Cloudflare’s nameservers at your registrar.

Then in Cloudflare DNS:

| Type  | Name | Content                 | Proxy |
|-------|------|-------------------------|-------|
| CNAME | www  | YOURUSER.github.io      | DNS only (grey cloud) |
| A     | @    | 185.199.108.153         | DNS only |
| A     | @    | 185.199.109.153         | DNS only |
| A     | @    | 185.199.110.153         | DNS only |
| A     | @    | 185.199.111.153         | DNS only |

Optional IPv6:

| Type | Name | Content            |
|------|------|--------------------|
| AAAA | @    | 2606:50c0:8000::153 |
| AAAA | @    | 2606:50c0:8001::153 |
| AAAA | @    | 2606:50c0:8002::153 |
| AAAA | @    | 2606:50c0:8003::153 |

Keep records **DNS only** (grey cloud) at first so GitHub can issue the SSL cert. You can orange-cloud later if you want.

#### Option 2 — Registrar DNS only (Namecheap / Porkbun / Google)

Same records as above, pointed at GitHub’s IPs.

If the domain is at gkg.net (or any registrar), leave the existing nameservers alone unless you intentionally move DNS. Just add the A and CNAME records above in that DNS panel.

Do **not** change nameservers unless you are moving DNS to Cloudflare or another DNS host on purpose.

### C. www vs apex

- `pepeonbag.xyz` → the four A records on `@`
- `www.pepeonbag.xyz` → CNAME `www` → `YOURUSER.github.io`

Put the exact hostname you care about in the `CNAME` file. GitHub will redirect the other one if both records exist.

## 4. Local preview

If you just open `index.html` as a file, `ca.txt` may not load (browser security). Use any tiny server from this folder:

```bash
python3 -m http.server 8080
```

Then open `http://localhost:8080`

## 5. What you can change later

- Telegram is already set to `https://t.me/pepeonbag`
- Swap `pepe-bag.jpg` with another square image (keep the filename, or update `index.html`)
- Copy in `index.html` is short on purpose so the bag stays the focus
