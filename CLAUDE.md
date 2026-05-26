# Group Workout Builder

A single-page PWA for planning group fitness sessions. No framework, no build step — pure HTML/CSS/JS in `index.html`.

## Structure

```
index.html        ← Entire app (HTML + CSS + JS all in one file)
manifest.json     ← PWA config
sw.js             ← Service worker (offline support)
icons/            ← App icons (192px, 512px)
netlify.toml      ← Netlify deploy config
package.json      ← Just for local dev server
```

## Run locally

```bash
npm install
npm run dev
# Opens at http://localhost:3000
```

## Deploy to Netlify

```bash
# Option 1: Drag the folder onto netlify.com/drop
# Option 2: Connect GitHub repo in Netlify dashboard — auto-deploys on push
```

## App architecture

Everything lives in `index.html`:

- **CSS** — CSS variables for theming, mobile-responsive grid layout
- **EXERCISES array** — the full exercise library (~217 moves, categorized)
- **PAST_WORKOUTS / CREST_WORKOUTS** — preloaded session templates
- **State** — plain JS variables (`sections`, `favorites`, `savedWorkouts`)
- **Persistence** — `localStorage` for saved sessions and favorites
- **Coach View** — full-screen exercise-by-exercise display mode
- **PWA** — manifest + service worker for home screen install + offline use

## Key functions

| Function | What it does |
|---|---|
| `renderLibrary()` | Renders filtered exercise list |
| `renderBuilder()` | Renders all sections + exercises |
| `addSection()` | Adds a new section to the builder |
| `openPickSection(name)` | Opens modal to choose which section to add exercise to |
| `openComboBuilder()` | Opens combo move builder modal |
| `splitIntoSets(id)` | Splits a section into numbered sub-sets |
| `openCoachView()` | Launches full-screen coach display |
| `saveCurrentWorkout()` | Saves to localStorage |
| `randomizeWorkout()` | Generates a random session from the library |

## Adding exercises

Find the `EXERCISES` array in `index.html` and add entries:

```js
{ name: "Your Exercise Name", cat: "legs" },
// cats: warmup | legs | upper | core | cardio | full
```

## Updating the PWA cache

Bump the cache version in `sw.js` when making changes:
```js
const CACHE = 'workout-builder-v2'; // increment this
```
