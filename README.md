# Webcam Mirror

A minimal webcam mirror app for Cloudflare Workers Static Assets. The camera preview is mirrored horizontally and runs locally in the browser.

## Files
- `index.html` — app, styles, and camera logic
- `wrangler.jsonc` — Cloudflare Worker and static asset configuration

## Deploy from a linked GitHub repository
1. Push these files to the **root** of your GitHub repository.
2. In Cloudflare, open **Workers & Pages** and create a Worker using the GitHub repository integration (the dashboard wording may vary).
3. Use these build settings if prompted:
   - **Build command:** leave blank if the dashboard allows it; otherwise use `npx wrangler deploy`
   - **Deploy command:** `npx wrangler deploy`
   - **Root directory:** `/` (repository root)
   - **Build output directory:** leave blank; the `assets.directory` setting in `wrangler.jsonc` points Wrangler at the static files.
4. Ensure the project is configured as a **Worker** with a `wrangler.jsonc` file, not as a Pages project.
5. Deploy. Cloudflare will provide an HTTPS `workers.dev` URL.

If the dashboard requires a build command, use `npm install` only if you add a `package.json` with Wrangler as a dependency; otherwise Cloudflare's build environment may already provide Wrangler. The most reliable CLI setup is to install Wrangler locally and run `npx wrangler deploy`.

## Run locally
Install Node.js, then from the repository root run:
```sh
npx wrangler dev
```
Open the local URL printed by Wrangler. Camera access works on localhost and HTTPS origins.

## Notes
- The browser asks for camera permission only when Start is clicked.
- No audio is requested. The app does not record or upload the video.
- To add MediaPipe later, load its browser package and run face-landmark detection against the `video` element; draw results on a canvas overlay.
