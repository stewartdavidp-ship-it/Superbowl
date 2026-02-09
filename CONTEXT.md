# SB Squares — CONTEXT.md

> **Read this first** at the start of every session.

## Current Version

**v6.4.0** — Released 2026-02-09

## What SB Squares Is

Super Bowl LX Squares is a multiplayer football squares game for Super Bowl parties. Players create or join games via share codes, claim squares on a 10×10 grid, and win payouts based on score digits at the end of each quarter. Supports multiple concurrent games, configurable payouts, and real-time grid updates via Firebase.

## Architecture

- **Single-file HTML app**: All CSS/JS inline in `superbowl-squares.html` (~2,655 lines)
- **Framework**: Vanilla JS (no React)
- **Data**: Firebase RTDB (auth + realtime database)
- **PWA**: No
- **Deploy target**: GitHub Pages (standalone repo)

## Key Technical Details

### Meta Tags
```html
<meta name="version" content="6.3.6">
<meta name="gs-app-id" content="sb-squares">
```

### Firebase Configuration
- **Database**: `word-boxing-default-rtdb.firebaseio.com` (shared RTDB)
- **Auth**: Google sign-in via Firebase Auth
- **Base path**: `sb-squares-lx/`

### Data Schema (Firebase RTDB)
```
sb-squares-lx/
├── games/{gameId}/
│   ├── config          — Game settings (name, teams, scoring, payouts, cost)
│   ├── grid/{row_col}  — Cell claims (owner, displayName, claimedAt)
│   ├── players/{uid}   — Player data (displayName, boxCount)
│   ├── numbers/        — Assigned column/row numbers (cols[], rows[])
│   ├── scores/         — Quarter scores (q1-q4, each has team1/team2)
│   └── scoreEvents/    — Score update history
├── codes/{code}        — Join code → gameId mapping
├── users/{uid}/games/  — User's game list
└── migrated            — Legacy data migration flag
```

### Key Functions

**Auth & Navigation:**
- `signIn()` / `signOut()` — Google auth
- `showLobby()` — Main lobby with game list
- `checkDeepLink()` — Handle `?join=CODE` URL params

**Game Management:**
- `createGame()` — Create new game with config (teams, scoring mode, payouts)
- `joinGame()` — Join via share code
- `openGame(gameId)` — Load game view with real-time listeners
- `loadMyGames()` / `renderMyGames()` — Lobby game cards
- `buildGameSwitcher()` — Multi-game dropdown

**Grid & Squares:**
- `renderGrid()` — Build/update 10×10 grid display
- `handleCellTap(row, col)` — Claim a square
- `showClaimOverlay()` — Box selection UI
- `setPickMethod(method)` — Random vs manual square selection
- `assignNumbers()` — Randomly assign 0-9 to rows/columns

**Scoring:**
- `buildScoreInputs()` — Quarter score entry UI
- `renderQuarters()` — Quarter results with winner highlighting
- `renderScoreEvents()` — Score update timeline
- `calculatePayouts()` — Determine winners per quarter

**Sharing:**
- `showShareModal()` — Share code + QR code
- `copyShareUrl()` — Copy join link
- `drawQR(text)` — Generate QR code on canvas

**Audio:**
- `playTapSound()` / `playUndoSound()` / `playCompletionSound()` / `playVictorySound()` — Web Audio API sound effects

## Deployment

- **Repo:** standalone repo (sb-squares)
- **SubPath:** none (root)
- **Structure:** Prod only (single repo)
- **Deploy type:** Single HTML file
- **Detection patterns:** `Super Bowl.*Squares`, `sb-squares`, `GAME_REF`

## Conventions

- Vanilla JS with DOM manipulation (no framework)
- Dark theme with team-specific colors (Patriots blue/red, Seahawks navy/green)
- Bebas Neue font for headers, Outfit for body text
- Firebase real-time listeners attached/detached per game session
- Sound effects via Web Audio API (no audio files)
- QR code generation via canvas drawing (no external library)
- Game codes are 6-character alphanumeric strings
- Grid cells addressed as `{row}_{col}` in Firebase

## Recent Changes

### v6.4.0
- Sequential claim wizard: 3-step flow (initials → count → pick method) replaces single cluttered form
- No default box count — users must actively select
- Smart random pick: spreads squares across different rows and columns instead of pure random
- Step indicator dots show progress through wizard

### v6.3.6
- Previous stable release for Super Bowl LX (Patriots vs Seahawks)
