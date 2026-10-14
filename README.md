# Listing Watch

A dashboard for [gbp-monitor](https://github.com/mavusosesikho40-eng/gbp-monitor), the script that watches a Google Business Profile listing for unauthorised changes.

It shows:

- **Current state**: listing matches, change detected, check failing, no recent checks, or setup needed
- **Trusted listing**: the fields saved in `baseline.json`, with the live value next to any field that has changed
- **Check history**: every entry in `change_log.jsonl`, with before/after values for changes
- **Monitor runs**: recent GitHub Actions runs, plus a button to start a check now
- **Setup checklist**: workflow registered, baseline saved, secrets present, first check done

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
