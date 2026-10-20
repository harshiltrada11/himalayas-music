# Himalayas Music

A responsive music-discovery website with a minimal, iOS-inspired transparent glass UI.

## Features
- YouTube Data API v3 search for songs/videos, artist channels, and playlists.
- One default "Popular in India" feed on startup (no automatic search requests).
- Search runs only after the user submits a query; pagination is capped at 12 per request.
- Embedded YouTube playback, queue, play/pause, next/previous, seek, volume, shuffle and repeat.
- Local liked songs, recently played, and locally saved playlists using browser storage.
- Responsive mobile layout and reduced-motion support.
- Server-side API proxy so the API key is not exposed in public browser code.
- Serverless caching headers to reduce repeated quota use.

## Important limitation
No site can literally contain or guarantee playback of every song in the world. This website discovers content indexed by YouTube. Some videos may be unavailable, region-restricted, age-restricted, or disallow embedding. YouTube playback and ads/rights-holder restrictions still apply. This project does not download music or bypass YouTube restrictions.

## Setup (Vercel)
1. Create a YouTube Data API v3 key in Google Cloud Console and enable **YouTube Data API v3** for the project. Set quotas and restrictions in Google Cloud.
2. Upload/extract this project into a GitHub repository, or import the folder using a supported deployment workflow.
3. Deploy the project on Vercel.
4. In Vercel → Project → Settings → Environment Variables, add:
   - Name: `YOUTUBE_API_KEY`
   - Value: your actual API key
   - Environments: Production, Preview, Development as needed
5. Redeploy after setting the environment variable.
6. Open the deployed website. The home feed should load without a search request. Searching consumes YouTube Data API quota.

## Local development
- Install Node.js (LTS).
- In this project folder run `npm install`.
- Copy `.env.example` to `.env.local` and put your key in `.env.local`.
- Run `npm run dev`.
- The `vercel` CLI runs the website and serverless API route locally.

## Security
- Never put your real API key in `public/app.js`, `public/index.html`, or any public static file.
- Restrict the API key in Google Cloud Console to the YouTube Data API and the services/usage you need.
- The proxy caps results at 25 and validates the supported actions, but a public API endpoint can still be abused. For a public launch, add rate limiting/WAF protection and monitor quota usage.
- YouTube API policies apply. Display YouTube attribution/player controls as required and do not hide ads or bypass access restrictions.

## File structure
- `public/index.html` — website structure
- `public/style.css` — styling and glass effects
- `public/app.js` — front-end behavior
- `api/youtube.js` — secure serverless YouTube API proxy
- `vercel.json` — routing
- `.env.example` — environment variable template
