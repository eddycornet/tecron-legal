# tecron-legal

Static Privacy Policy and Terms of Service for the Tecron budgeting service,
hosted on GitHub Pages at the **legal.tecron.be** subdomain (the `tecron.be`
apex is left untouched). These URLs are what Enable Banking (and later Stripe /
the app footer) point at:

- `https://legal.tecron.be/privacy`
- `https://legal.tecron.be/terms`

## DNS at Telenet — one CNAME record

At `cloud.telenet.be`, add a single **CNAME** record:

```
Host / name:  legal          (i.e. legal.tecron.be)
Type:         CNAME
Value:        eddycornet.github.io
```

Note the value is your Pages user host `eddycornet.github.io` (no repo path, no
`https://`, no trailing dot needed). The apex `tecron.be` is not modified.

Because you already verified `tecron.be` in GitHub, the `legal.` subdomain is
covered too — no extra verification needed.

## After DNS propagates (up to a few hours)

Verify from your Mac:

```
dig +short legal.tecron.be        # should resolve to eddycornet.github.io -> Pages IPs
https://legal.tecron.be/privacy   # Privacy Policy
https://legal.tecron.be/terms     # Terms of Service
```

Then in the repo **Settings → Pages**, tick **Enforce HTTPS** (available once the
certificate has been issued).

## Editing content

The two HTML files (`privacy/index.html`, `terms/index.html`) hold the text.
Placeholders have been filled (VAT `BE0833267216`, `2590 Berlaar`, court
`Mechelen`). Make sure the **admin@tecron.be** mailbox actually exists / routes
at Telenet, or privacy requests will bounce. Update the "Last updated" date on any
material change.

---

_Note: these are honest, service-specific templates, not legal advice. Fine for
restricted-production / household use. Have a professional review them before any
broad public launch or SaaS offering._
