# Listing Watch

A dashboard for [gbp-monitor](https://github.com/mavusosesikho40-eng/gbp-monitor), the script that watches a Google Business Profile listing for unauthorised changes.

It has two views, switched at the top of the page:

- **Restaurant**: for the owner and staff. A plain answer ("Your listing is safe" or "Your Google listing was changed"), the time until the next check, the approved name, phone, website and address, and step-by-step instructions when something changes.
- **Operator**: for whoever runs the monitor. Status, setup progress (workflow, secrets, baseline, first check), recent GitHub Actions runs, the full check log with before/after values, a "Run check now" button, and the GitHub connection.

Link straight to a view with `#restaurant` or `#operator` at the end of the URL. Without a connection the page shows example data, and you can preview the "listing changed" and "not set up" states.

It's a single static `index.html` with no build step and no server.

## How it gets data

`gbp-monitor` is private, so the page reads it through the GitHub API using a token you paste in. The token is only sent to `api.github.com`. It stays in this browser's session storage, or in local storage if you tick "Remember on this device".

Create a [fine-grained token](https://github.com/settings/personal-access-tokens/new) limited to the `gbp-monitor` repo with:

| Permission | Needed for |
| --- | --- |
| Contents: read | baseline and check log (required) |
| Actions: read | run history (required) |
| Actions: write | the "Run check now" button (optional) |
| Secrets: read | confirming secrets in the checklist (optional, secret values are never readable) |

Without a token, the page shows clearly labelled example data.

## Hosting

Turn on GitHub Pages for this repo: **Settings → Pages → Build and deployment → Deploy from a branch → `main` / root**. The dashboard will be at `https://mavusosesikho40-eng.github.io/gbp-monitor-interface/`.

You can also open `index.html` straight from disk.
