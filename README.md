# Radni Gade & Suyash — A Celebration of Love

An original, mobile-first Indian wedding invitation built with React 19, TypeScript, TanStack Start, Vite, and Cloudflare Workers. It includes the click-to-open cover, invitation details, countdown, calendar download, family introductions, ceremonies, WhatsApp sharing, background music, and a browser-only RSVP preview.

The invitation makes no RSVP backend requests and does not save guest details.

## Deploy to Cloudflare Workers

This project uses TanStack Start (server rendering), so deploy it to **Cloudflare Workers** using Cloudflare's Vite plugin rather than uploading the source as a static Pages folder.

### 1. Requirements

- Node.js 22.13 or newer
- npm
- A free Cloudflare account
- A GitHub account (recommended for keeping a backup and connecting Cloudflare Builds)

### 2. Install and test locally

From the project folder:

```sh
npm install
npm run dev
```

Open the local URL printed by Vite. To create a production build:

```sh
npm run build
```

### 3. Sign in to Cloudflare and deploy

```sh
npx wrangler login
npm run deploy
```

Wrangler will build the app and publish it to your Cloudflare account. The first deployment will prompt you to confirm the Worker name if needed. Your site will be available at:

`https://radni-suyash-wedding-invite.<your-subdomain>.workers.dev`

You can also connect a custom domain in the Cloudflare dashboard under **Workers & Pages → your Worker → Settings → Domains & Routes**.

### 4. Deploy automatically from GitHub (optional)

1. Push this project to a GitHub repository.
2. In Cloudflare, open **Workers & Pages → Create application → Workers → Import a repository** (the exact dashboard wording may vary).
3. Select the repository and configure the build command as `npm run build` and the deploy command as `npx wrangler deploy`.
4. Keep the `wrangler.jsonc` configuration in the repository. Cloudflare's Workers Builds can then build and deploy updates from your chosen branch.

For the first deployment, the simplest route is to run `npx wrangler login` and `npm run deploy` from your computer.

## Free plan and usage

Cloudflare Workers has a free plan with usage limits. This wedding invitation is mostly static content and does not use a database or server-side RSVP submission, so it should be lightweight. Check the current Workers pricing and limits in your Cloudflare dashboard before sharing the link widely. Custom-domain registration, if you need to buy a domain, is separate from hosting.

## Personalise the invitation

Edit `src/wedding.config.ts`. It contains the couple's names, family details, date, venue, story, music URL, RSVP deadline, and individual ceremonies.

- Keep dates in ISO format, including `+05:30` for India.
- Update `date`, `endDate`, and `dateLabel` together.
- Set a ceremony's `enabled` to `false` to hide it from the itinerary and RSVP options.
- Set `story.enabled` to `false` to hide the story and its navigation link.
- Set `rsvpDeadline` to your response deadline.
- The original palace artwork is `public/img/palace.png`; `heroImage` points directly to that local file.

## Music

The supplied track is configured at `/music/wedding.m4a`. Playback starts only after a guest opens the invitation, and the visible control allows guests to pause or resume it. Set `musicUrl` to an empty string to remove music.

## RSVP behaviour — important

The RSVP form currently validates the guest's choices in the browser and shows a local thank-you screen only. It **does not send or save** responses. Guests must contact the hosts directly to confirm attendance. This preserves the existing behaviour; it is not an online RSVP collection system.

## Before sharing

- Run `npm run build`.
- Preview the deployed site on a phone and desktop.
- Test the invitation opening, music play/pause, countdown, calendar download, ceremony links, WhatsApp sharing, and RSVP preview.
- Confirm names, dates, venue details, and the Google Maps link in `src/wedding.config.ts`.
