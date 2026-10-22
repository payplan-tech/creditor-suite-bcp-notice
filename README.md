# Creditor Suite — holding page

The page visitors see while **Creditor Suite** is unavailable. PayPlan's Business
Continuity Plan is active following the PHP cyber security advisory; this is
where traffic for Creditor Suite is pointed in the meantime.

Static HTML and one stylesheet. No build, no framework, no dependency on any
PayPlan service — it has to render when other things do not.

## Changing the message

Everything editable is in `index.html`, between the `STATUS MESSAGE`
comments. Edit, commit to `main`, and the deploy runs itself; the page is live
within a minute or two. Nothing else in the file needs touching.

Keep it short. Someone reading this is trying to find out what to do instead,
and anything past the first screen is a paragraph they will not reach.

The wording currently on the page is the approved Business Continuity
Notification, including Creditor Relations on 0845 606 6624 and
creditor.relations@payplan.com.

## Deployment

GitHub Actions publishes to GitHub Pages on every push to `main`, and
**Actions → Deploy → Run workflow** republishes without a commit.

One-time repository setup: **Settings → Pages → Build and deployment →
Source: GitHub Actions**. Until that is set the workflow runs and the final
step fails.

### Pointing a domain at it

Add a `CNAME` file at the repository root holding the hostname on its own
line — `creditor-suite.payplan.com`, for example — then set that hostname's
DNS to the Pages target and enter it under **Settings → Pages → Custom
domain**. There is deliberately no `CNAME` committed: one naming a domain
that is not pointed here yet takes the default `github.io` address away and
leaves no working URL at all.

## What is deliberately absent

- **No analytics, tags or cookie banner.** Nothing to consent to, so no
  interstitial between a worried visitor and the message.
- **`noindex, nofollow`.** A holding page must not be left ranking in place
  of the real service once it is back.
- **No auto-refresh.** A page that reloads under someone reading it is worse
  than one they refresh themselves.
- **Brand tokens copied, not imported.** The palette and type scale come from
  `packages/design-tokens/v6.css` in the website repo. Nothing keeps the two
  in step; if the brand changes, change it here too.

## When the service is back

Point the domain back at the real service. Leave this repository as it is —
the next continuity event wants it ready, not rebuilt.
