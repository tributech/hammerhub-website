# HammerHub Website — Launch Checklist

## Netlify Setup

- [ ] Connect `tributech/hammerhub-website` repo in Netlify
- [ ] Set base directory (if monorepo): `hammerhub-website`
- [ ] Build command: `pnpm build`
- [ ] Publish directory: `dist`
- [ ] Node version: `24` (set in `netlify.toml` already)
- [ ] Add custom domain `hammerhub.com` in Netlify → Domain settings
- [ ] Enable HTTPS (auto via Netlify's Let's Encrypt)
- [ ] Set `www.hammerhub.com` → redirect to `hammerhub.com` (or vice versa — pick one canonical)

## Environment Variables (Netlify → Site settings → Environment)

- [ ] `PUBLIC_OWR_URL` = `https://oldworldrankings.com`
- [ ] `PUBLIC_GA_ID` = `G-XXXXXXXXXX` ← add once GA property is created (see below)

## Google Analytics

- [ ] Create a GA4 property at [analytics.google.com](https://analytics.google.com) for `hammerhub.com`
- [ ] Copy the Measurement ID (`G-XXXXXXXXXX`)
- [ ] Add it as `PUBLIC_GA_ID` env var in Netlify
- [ ] Verify events are firing after first deploy (check Realtime report)
- [ ] Set up a conversion event for form submissions (`generate_lead` or custom `email_signup`)

## Lead List / Email Capture

- [ ] Confirm Netlify Forms is enabled on the site (Forms tab in Netlify dashboard)
- [ ] Submit a test email via the live site and verify it appears under **Forms → notify**
- [ ] Set up email notifications: Netlify → Forms → notify → **Form notifications** → add your email
- [ ] Optional: connect Netlify Forms to a Zapier/Make webhook to pipe leads into a CRM or spreadsheet
- [ ] Optional: migrate to [Mailchimp](https://mailchimp.com) / [ConvertKit](https://convertkit.com) / [Loops](https://loops.so) if you want to send launch emails to the list later (Loops is recommended — built for SaaS, simple, has a free tier)

## SEO

- [x] Add `public/robots.txt`
- [x] Enable Astro's sitemap integration (`@astrojs/sitemap`) — auto-generates `/sitemap-index.xml` at build time
- [ ] Submit sitemap to [Google Search Console](https://search.google.com/search-console) once domain is live
- [ ] Submit sitemap to [Bing Webmaster Tools](https://www.bing.com/webmasters)
- [ ] Add OG image (`/public/og-image.png`, 1200×630px) and wire it up in `Layout.astro`:
  ```html
  <meta property="og:image" content="https://hammerhub.com/og-image.png" />
  <meta name="twitter:image" content="https://hammerhub.com/og-image.png" />
  <meta name="twitter:card" content="summary_large_image" />
  ```
- [ ] Verify meta title + description on both pages look good in [metatags.io](https://metatags.io)
- [ ] Check Lighthouse score (target 90+ on Performance, 100 on SEO, Accessibility, Best Practices)

## DNS

- [ ] Point `hammerhub.com` A record (or CNAME for `www`) to Netlify's load balancer IP
- [ ] Confirm DNS propagation with `dig hammerhub.com`
- [ ] Verify redirect: `http://hammerhub.com` → `https://hammerhub.com`

## Pre-Launch QA

- [ ] Test on mobile (iOS Safari, Android Chrome)
- [ ] Test email signup form end-to-end on the live URL (not localhost — Netlify Forms only works on deployed site)
- [x] Verify all external links open in new tab and pass referrer to `oldworldrankings.com` (`rel="noopener"` only)
- [ ] Spell-check all copy
- [ ] Confirm favicons appear correctly in browser tab + iOS home screen bookmark

## Post-Launch

- [ ] Announce on OWR (`oldworldrankings.com`) — add a banner or footer link pointing to HammerHub
- [ ] Share the link in relevant communities (Warhammer: The Old World discords, Reddit, Facebook groups)
- [ ] Monitor Netlify Forms submissions weekly
- [ ] Check GA for traffic sources
