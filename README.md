# tecron-legal

Static Privacy Policy and Terms of Service for the Tecron budgeting service,
hosted on GitHub Pages at **tecron.be**. These URLs are what Enable Banking (and
later Stripe / app footer) point at.

- `https://tecron.be/privacy`
- `https://tecron.be/terms`

## ⚠️ Before you start: is anything already live on `tecron.be`?

Pointing the **apex** domain (`tecron.be`) at GitHub Pages means the whole apex
serves these pages. If `tecron.be` already hosts a website, **don't** repoint the
apex — use a subdomain instead (see "Subdomain fallback" below), e.g.
`https://legal.tecron.be/privacy`. If the apex serves nothing today, the apex
setup below is fine.

## Fill in the placeholders first

Search the two HTML files for these and replace:

- `[VAT / BCE number]`
- `[registered address]`
- `[court location, e.g. Antwerp]`

Also make sure the **`privacy@tecron.be`** mailbox actually exists / is routed at
Telenet, or privacy requests will bounce.

## 1. Create the repo and push

```bash
cd tecron-legal
git init
git add .
git commit -m "Privacy Policy + Terms of Service"
gh repo create tecron-legal --public --source . --push   # or create on github.com and push
```

## 2. Enable GitHub Pages

Repo → **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main`,
folder `/ (root)` → Save. The `CNAME` file (already in this repo, contains
`tecron.be`) tells Pages to serve on your custom domain. Tick **Enforce HTTPS**
once the cert is issued.

## 3. DNS at Telenet (apex domain)

GitHub Pages apex domains use **A records** (an apex can't be a CNAME). At
`cloud.telenet.be`, for `tecron.be` add these four A records:

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

(Optionally also the AAAA/IPv6 records `2606:50c0:8000::153`,
`2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`.)

DNS can take up to a few hours to propagate. GitHub Pages then verifies the
domain and issues a free HTTPS certificate automatically.

## Subdomain fallback (if the apex is in use)

Instead of the four A records, delete the `CNAME` file's `tecron.be` and set it to
`legal.tecron.be`, then at Telenet add **one CNAME**:

```
legal.tecron.be  →  <your-github-username>.github.io
```

URLs become `https://legal.tecron.be/privacy` and `/terms` — register those in
Enable Banking instead.

## Verify

```
https://tecron.be/            → links page
https://tecron.be/privacy     → Privacy Policy
https://tecron.be/terms       → Terms of Service
```

Then paste the privacy + terms URLs into the Enable Banking app registration.

---

_Note: these documents are honest, service-specific templates, not legal advice.
Fine for restricted-production / household use. Have a professional review them
before any broad public launch or SaaS offering._
