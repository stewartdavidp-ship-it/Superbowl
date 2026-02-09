# SB Squares — Changelog

All notable changes to this project will be documented in this file.

## [6.4.0] — 2026-02-09

### Changed
- **Sequential claim wizard** — replaced single cluttered form with 3-step flow: initials → box count → pick method. Each step gets its own screen with clear focus.
- **No default box count** — dropdown starts with "Select..." placeholder instead of defaulting to 5. Users must actively choose.
- **Smart random pick** — auto-select now avoids placing multiple squares in the same row or column when possible, giving better grid spread instead of pure random shuffle.

### Added
- Step indicator dots showing progress through the claim wizard
- Pick method buttons redesigned as large tappable cards with descriptions
- Back navigation between wizard steps

## [6.3.6] — 2026-02-09

### Current
- Stable release for Super Bowl LX (Patriots vs Seahawks)
- Multi-game support with share codes and QR joining
- Configurable scoring modes and payout structures
- Real-time grid updates via Firebase RTDB
- Sound effects via Web Audio API
- Legacy data migration from flat to multi-game structure
