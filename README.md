# Payout Platform Migration Kit

A browser-based tool for extracting, mapping, and migrating recipient data between payout platforms.

Built as an internal tool at [Trolley](https://trolley.com) to help onboarding teams migrate customers from Stripe Connect (and other platforms) — won first place at the company hackathon.

## Live Demo

👉 **[Try it live](https://migration-kit.netlify.app)** — no API keys needed, sample data included.

## What It Does

Connects to a source platform (currently Stripe Connect), extracts recipient data, previews it, lets you map fields visually, and exports in multiple formats:

- **Recipients CSV** — Ready for bulk import
- **Recipients JSON** — For API-based creation
- **Individual Verifications CSV** — KYC status export
- **Business Verifications CSV** — KYB status export  
- **Offline Payments CSV** — Historical transfer records
- **Direct API Creation** — Push recipients to Trolley via API (HMAC-SHA256 auth)

## How It Works

```
Source Platform → Extract → Preview & Select → Map Fields → Export
```

1. **Connect** — Enter source platform API key (or use sample data)
2. **Preview** — See all extracted accounts, filter by type, select specific ones
3. **Summary** — Data quality dashboard showing verification readiness and transfer history
4. **Map** — Visual field mapper with pre-configured defaults
5. **Export** — Download CSVs, JSON, or create recipients directly via API

## Architecture

Single HTML file. No server, no build step, no dependencies beyond Tailwind CSS (CDN).

- Stripe API calls run directly in the browser (test mode supports CORS)
- Trolley API auth (HMAC-SHA256) computed client-side using Web Crypto API
- All data stays in the browser — nothing is sent to any third-party server
- Sample data mode generates realistic mock accounts for demo purposes

## Supported Platforms

| Source | Status |
|--------|--------|
| Stripe Connect | ✅ Live |
| Airwallex | 🔜 Planned |
| Tipalti | 🔜 Planned |

| Destination | Status |
|-------------|--------|
| CSV Export | ✅ Live |
| JSON Export | ✅ Live |
| Trolley API | ✅ Live |

## Running Locally

```bash
git clone https://github.com/YOUR_USERNAME/migration-kit.git
cd migration-kit
open index.html
```

That's it. No `npm install`, no build, no server.

## Security

- API keys are only sent to their respective platforms (Stripe → Stripe API, Trolley → Trolley API)
- No data persistence — everything lives in browser memory
- No third-party analytics or tracking
- HMAC-SHA256 signatures generated client-side, secret keys never transmitted

## Background

This tool was built to solve a real problem: when customers migrate between payout platforms, they need to transfer recipient data, verification status, and payment history. Doing this manually is slow and error-prone.

The tool was originally built during a hackathon and later used by the onboarding team to migrate customers with 50-5,000+ recipients from Stripe Connect to Trolley.

### Key Technical Decisions

- **Single HTML file** — Maximizes portability. Anyone can run it by opening a file.
- **No backend** — Eliminates hosting complexity and API key storage concerns.
- **Mapper pattern** — Source fields → Destination fields mapping is extensible to new platforms.
- **CSV format matching** — Exports match the exact CSV templates expected by Trolley's bulk import.

## License

MIT
