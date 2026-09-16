# tecron-legal

Static Privacy Policy and Terms of Service for the Tecron budgeting service, served by
GitHub Pages at **legal.tecron.be**. **Live**, with HTTPS enforced.

- `https://legal.tecron.be/privacy/`
- `https://legal.tecron.be/terms/`

(The URLs without a trailing slash also work; GitHub redirects them.)

These URLs are referenced by:

- the **Enable Banking** app registration (Privacy URL / Terms URL fields);
- the **landing page** at `www.tecron.be` (repo `tecron-site`), in its footer and privacy
  section;
- later, Stripe and the app footer.

## How tecron.be is laid out

| Host | What | Where |
|---|---|---|
| `legal.tecron.be` | These legal pages | this repo |
| `www.tecron.be` | Public landing page | repo `tecron-site` |
| `tecron.be` (apex) | Redirects to `www` once its A/AAAA records point at GitHub | see `tecron-site` README |
| `appmail.tecron.be` | Resend sending domain for app email | DNS only |
| MX for `tecron.be` | Email, on Google Workspace | **do not touch** |

## DNS at Telenet (cloud.telenet.be) — done

This site needs a single record, and it is in place:

```
Host / name:  legal          (i.e. legal.tecron.be)
Type:         CNAME
Value:        eddycornet.github.io
```

The value is the Pages user host `eddycornet.github.io`: no repo path, no `https://`.
`tecron.be` is verified in GitHub, which covers every subdomain, so `legal` and `www` need
no extra verification.

Check it any time:

```
dig +short legal.tecron.be                    # → eddycornet.github.io → Pages IPs
curl -sI https://legal.tecron.be/privacy/     # → 200
```

Keep the `CNAME` file in this repo (`legal.tecron.be`). Deleting it in the GitHub UI
removes the custom domain and takes the site off `legal.tecron.be` until it is restored.

## Editing content

The text lives in `privacy/index.html` and `terms/index.html`. Placeholders are filled in:
VAT `BE0833267216`, `2590 Berlaar`, court `Mechelen`. The **admin@tecron.be** mailbox is
on Google Workspace and must stay active, or privacy requests will bounce. Update the
"Last updated" date on any material change.

**If the bank data provider changes, update the privacy policy.** It names Enable Banking
as the licensed provider and lists the processors data flows through. A switch
(open-banking.io, Yapily — see CLAUDE-API issue #110) changes that list, and
open-banking.io would add its operator as an extra processor on top of Enable Banking.
Update the policy **before** real data flows through the new provider.

---

_Note: these are honest, service-specific templates, not legal advice. Fine for
restricted-production / household use. Have a professional review them before any broad
public launch or SaaS offering._
