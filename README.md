# YPO MENA — Chapter Commitments by Status

A single-page dashboard tracking the 14 chapter commitments across all 27 YPO
Middle East / North Africa chapters, built with React + Vite.

## Run locally

```bash
npm install
npm run dev
```

Then open the URL Vite prints (usually http://localhost:5173).

## Build for production

```bash
npm run build
npm run preview   # sanity-check the production build locally
```

The static output lands in `dist/`.

## Deploy

### GitHub
```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin <your-repo-url>
git push -u origin main
```

### Vercel
1. Go to https://vercel.com/new
2. Import the GitHub repo you just pushed
3. Framework preset: **Vite** (auto-detected)
4. Build command: `npm run build` (default)
5. Output directory: `dist` (default)
6. Deploy

No environment variables or backend are required — all chapter data is
inlined in `src/App.jsx`.

## Updating the data

Chapter scores live in the `ALL_DATA` array near the top of `src/App.jsx`.
Each entry looks like:

```js
{ n: "YPO Morocco Integrated", t: "YPO", s: 14, prev: 14, v: [1,1,1,1,1,1,1,1,1,1,1,1,1,1] }
```

- `n` — chapter name
- `t` — "YPO" or "YPO Gold"
- `g: 1` — add this if it's a YPO Gold chapter (renders the GOLD badge)
- `s` — total commitments met (0–14)
- `prev` — score from the previous snapshot, used for the vs.-last-update tooltip
- `v` — array of 14 booleans (1 = met, 0 = not met), in the order defined by
  the `LABELS` array just above it

## Notes

- The logo is embedded inline in `src/App.jsx` as a base64 PNG with a real
  alpha channel (navy glyph, transparent background), so it can be resized
  freely without a bounding box.
- "Print / Save PDF" uses the browser's native print dialog; a print
  stylesheet hides interactive controls and forces landscape orientation.
