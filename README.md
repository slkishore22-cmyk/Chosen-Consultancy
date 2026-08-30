# chosen

Landing page for Chosen Consultancy — media and marketing for Dubai real estate.

## What's here

| Path | What it is |
| --- | --- |
| `index.html` | The deployable page. Static, no build step. |
| `Chosen Consultancy Landing.dc.html` | Editable source. Image areas are drop zones here; `index.html` has them baked in as files. |
| `assets/` | Logos, dashboard screenshots, and the images used in the page (`assets/slots/`). |
| `fonts/` | Montserrat is loaded from Google Fonts; TT Interphases Pro (trial) is self-hosted here. |
| `support.js` | Runtime the page renders through. |
| `vercel.json` | Cache headers for `assets/` and `fonts/`. |

## Deploying

Static site, no build command and no output directory. On Vercel: import the repo, framework preset **Other**, leave build settings empty, deploy.

Locally:

```
python3 -m http.server 8000
```

Then open http://localhost:8000

## Notes

- The booking button links to https://calendly.com/contact-tharunkumaronline/30min
- TT Interphases Pro is a trial licence. Buy a web licence before this goes to a production domain.
