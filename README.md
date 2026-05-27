# ⚡ Lightning Decoder

A free, client-side web tool to inspect Lightning Network strings. Paste an **LNURL**, **Lightning Address**, or **BOLT11 invoice** and see what's inside — without sending your data to any server.

> Live demo: https://shanzy39.github.io/lightning-decoder

## Features

- **Auto-detects** LNURL, Lightning Address, and BOLT11 invoice formats
- **LNURL** → reveals the underlying HTTPS URL, host, and action type (pay / withdraw / auth / channel)
- **Lightning Address** → resolves `user@domain.com` to its `.well-known/lnurlp/` URL
- **BOLT11** → decodes amount, description, payee, payment hash, created/expires timestamps
- **Optional endpoint fetch** — click "Fetch endpoint" to see the actual JSON response from a Lightning Address or LNURL-pay server
- **No backend, no tracking, no analytics** — everything runs in your browser
- **Mobile-friendly** dark UI
- Pure HTML + vanilla JS, one file

## Why this exists

Lightning Network strings are opaque by design. Before you scan a QR code and hand over Bitcoin, it can be useful to know:

- What domain is this LNURL pointing to? (anti-phishing)
- What action will the wallet take? (pay vs withdraw vs login)
- What's the amount / description / expiry on this BOLT11 invoice?
- Is this Lightning Address valid before I share it?

This tool answers those questions in your browser without ever sending the string to a third-party service.

## Supported formats

| Format | Example | Decoded shows |
|---|---|---|
| **LNURL** | `LNURL1DP68GURN8GHJ7...` | Underlying HTTPS URL, host, action type |
| **Lightning Address** | `satoshi@walletofsatoshi.com` | Well-known URL, optional server JSON |
| **BOLT11 Invoice** | `lnbc2500u1...` | Amount, description, payee, payment hash, expiry |

The `lightning:` URI prefix is automatically stripped if present.

## Privacy

- **All decoding happens client-side.** The LNURL bech32 decoder, format detection, and BOLT11 parsing run entirely in your browser.
- **Endpoint fetches are opt-in.** Clicking "Fetch endpoint" makes a single CORS request from your browser directly to the Lightning server. The data never passes through any other server.
- **No tracking, no analytics, no cookies.**
- The BOLT11 decoder library is loaded from [esm.sh](https://esm.sh) (a CDN) the first time you decode a BOLT11 invoice.

## Run locally

No build step. Just open `index.html` in a browser, or serve the folder:

```bash
# Option 1: open directly
open index.html

# Option 2: serve with a simple HTTP server (recommended for ESM imports)
python3 -m http.server 8000
# Then visit http://localhost:8000
```

## Deploy to GitHub Pages

1. Push this repo to GitHub
2. Go to **Settings → Pages**
3. Set **Source** to `Deploy from a branch`, branch `main`, folder `/ (root)`
4. Save. Your site will be live at `https://<your-username>.github.io/lightning-decoder/`

## Built with

- [`light-bolt11-decoder`](https://github.com/jb55/light-bolt11-decoder) — BOLT11 parsing (loaded via esm.sh)
- Inline bech32 implementation for LNURL decoding
- No frameworks, no build tools

## Companion projects

- [BTCLN-QR-Generator](https://github.com/shanzy39/BTCLN-QR-Generator) — Flipper Zero app to generate Bitcoin and Lightning QR codes
- [USD-To-Sats-Chrome-Extension](https://github.com/shanzy39/USD-To-Sats-Chrome-Extension) — Right-click any USD amount to convert to sats

## License

MIT
