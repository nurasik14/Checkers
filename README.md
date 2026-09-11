# Checkers

A modern, multiplayer web checkers game built with plain JavaScript and Firebase. The project is designed as a deployable online product (lobby, profiles, chat, match history, server-side move validation), not just a demo.

## Table of contents
- [Demo](#demo)
- [Features](#features)
- [How to play](#how-to-play)
- [Technology stack](#technology-stack)
- [Architecture overview](#architecture-overview)
- [Getting started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Local development](#local-development)
  - [Firebase setup](#firebase-setup)
- [Project structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)
- [Author](#author)

## Demo
(No hosted demo included in the repository.)  
The app renders an 8×8 checkers board in the browser, provides a lobby for creating/joining games, supports spectators and chat, and saves match history.

## Features
- Online lobby with game slots and connection status
- Create a new game or join by Game ID
- Google sign-in and guest mode
- Spectator mode to watch matches
- Real-time game state: turn, mode, spectators count
- Built-in chat with avatar and timestamp
- "Show moves" helper to highlight legal moves
- Surrender and quick return to lobby
- Player profiles with match history and win/loss statistics
- Two game modes provided: Classic and Atari (extendable)
- "Go Pro" UI element as a monetization prototype
- Server-side move validation and anti-cheat implemented with Firebase Cloud Functions
- Local dev support via Firebase Emulator Suite

## How to play
1. Open the lobby.
2. Create a new game or enter an existing Game ID to join.
3. Players move pieces diagonally. Captures, kinging, and forced captures follow standard checkers rules implemented in the game engine.
4. Use "Spectate" to watch another match.
5. Chat with participants during the game.
6. Use "Surrender" to end a match early; the app also handles disconnects automatically.

## Technology stack
- HTML / CSS / JavaScript (frontend)
- Firebase Realtime Database
- Firebase Authentication (Google + guest)
- Firebase Cloud Functions (server-side validation)
- Firebase Emulator Suite (local development)

## Architecture overview
- Frontend subscribes to `games/{gameId}` in Realtime Database and receives real-time updates.
- All game actions (createGame, makeMove, surrenderGame, claimWin, joinSpectator, etc.) are validated server-side by Cloud Functions to prevent cheating.
- `onDisconnect` handlers ensure reliable presence updates when a player disconnects.
- Player profiles, history, and statistics are stored under `players/{playerId}`.

## Project structure
- `public/` — static frontend files (HTML, CSS, JS)
  - key JS modules: `main.js`, `game.js`, `ui.js`, `engine.js`, `module.js`, `auth.js`, `firebase.js`
- `functions/` — Firebase Cloud Functions (server-side validation, game lifecycle, scheduled cleanup)

## Getting started

### Prerequisites
- Node.js and npm
- Firebase CLI (for deployment / emulator)
- A Firebase project (or use the Emulator Suite for local development)

### Local development
1. Open the project in your editor (e.g., VS Code).
2. Install functions dependencies:
   ```
   cd functions
   npm install
   ```
3. Start the frontend by serving the `public/` directory with any static server (or use Live Server extension).
4. For full local emulation, configure Firebase emulators and run:
   ```
   firebase emulators:start
   ```
5. Open the site in your browser and sign in with Google or as a guest.

### Firebase setup
- Create a Firebase project and enable:
  - Realtime Database
  - Authentication (Google provider)
  - Cloud Functions
- Configure your frontend `firebase.js` with your Firebase project credentials.
- Deploy functions when ready:
  ```
  cd functions
  firebase deploy --only functions
  ```

## Contributing
Contributions, bug reports, and feature requests are welcome. Recommended workflow:
- Fork the repo
- Create a branch for your feature/fix
- Open a PR with a clear description and any testing instructions

## License
See the LICENSE file in the repository for license details.

## Author
nurasik14
