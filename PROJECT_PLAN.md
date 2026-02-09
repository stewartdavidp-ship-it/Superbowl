# SB Squares — Project Plan

## Mission

Provide a fun, easy-to-use Super Bowl squares game that friends and family can play together in real-time during the big game.

## Completed Features

### Core Game (v1.x–v3.x)
- [x] 10×10 grid with real-time claiming via Firebase
- [x] Google sign-in authentication
- [x] Random number assignment for rows/columns
- [x] Quarter-by-quarter scoring with winner detection
- [x] Game creation with configurable settings

### Multi-Game & Social (v4.x–v5.x)
- [x] Multiple concurrent games per user
- [x] Share codes for game joining
- [x] QR code generation for sharing
- [x] Deep link joining via URL params (?join=CODE)
- [x] Game switcher dropdown
- [x] Player management and display

### Polish & UX (v6.x)
- [x] Configurable payout structures (equal, weighted)
- [x] Cost per square with pot preview
- [x] Random vs manual square selection
- [x] Sound effects (tap, undo, completion, victory)
- [x] Score event timeline
- [x] Legacy data migration from flat to multi-game structure
- [x] Dark theme with team branding
- [x] Mobile-optimized layout

## In Progress

- Nothing active — app is in maintenance mode for current season

## Planned Features

### Near Term
- Post-game summary and payout calculation display
- Historical game archive

### Medium Term
- Support for other sporting events (not just Super Bowl)
- Customizable team names and colors
- Payment tracking (who owes whom)

### Future / Ideas
- Playoff bracket integration
- Group/league management across multiple games
- Push notifications for score updates
- Offline support (PWA)

## Architecture Decisions

- **Vanilla JS over React**: Game is relatively simple UI-wise; vanilla JS keeps bundle size small and avoids framework overhead for a seasonal app
- **Shared Firebase RTDB**: Uses same Firebase project as Word Boxing (`word-boxing-default-rtdb`) to avoid managing multiple Firebase projects
- **Single HTML file**: Follows Game Shelf ecosystem convention for easy deployment via Command Center
- **No PWA**: Seasonal app that doesn't need offline support — keeping it simple
- **6-char join codes**: Short enough to share verbally, collision-resistant enough for small user base

## Open Questions

- Should the app be generalized beyond Super Bowl for other events?
- Archive strategy for past games (keep in Firebase or export?)
