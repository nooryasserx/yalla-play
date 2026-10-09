# Yalla Play · يلّا بلاي

A bilingual browser arcade with **20 playable games**, built with vanilla JavaScript, Canvas 2D, HTML and CSS.

Choose a game and play immediately on desktop or mobile. The app supports Arabic with RTL layout and English with LTR layout, without requiring an account or a game download.

![Neon Rush cover artwork](dist/assets/hero-racer.png)

## Features

- **20 games:** racing, action, arcade, puzzles and local two-player games.
- **Game discovery:** search in Arabic or English, category filters and sorting.
- **Your library:** favorites, recently played games and personal best scores.
- **Play controls:** keyboard and touch support, difficulty settings, pause, restart, sound and fullscreen where supported.
- **Saved progress:** continue 2048, Sudoku and Slide Puzzle on the same browser.
- **Two-player modes:** Tic Tac Toe, Connect Four and Pong support a computer opponent or a friend on the same device.
- **Personalization:** optional local nickname, light/dark appearance and language selection.
- **Sharing:** each game has a direct link using a hash route such as `/#play/neon-rush`.
- **Lightweight deployment:** static files, no production dependencies, backend or build step.

## Games

| Game | اللعبة | Type |
| --- | --- | --- |
| Neon Rush | نيون راش | Racing |
| Orbit Defender | حارس المجرّة | Action |
| Gem Garden | جواهر ملوّنة | Match-three puzzle |
| Sky Hop | قفزة للسحاب | Arcade |
| Merge 2048 | تحدّي 2048 | Number puzzle |
| Pixel Run | عدّاء البكسل | Runner |
| Snake Garden | حديقة الثعبان | Arcade |
| Brick Breaker | كسّار الطوب | Arcade |
| Connect Four | أربعة على خط | Computer / local two-player |
| Memory Match | ذاكرة خارقة | Memory puzzle |
| Color Drop | مكعّبات هابطة | Falling-block puzzle |
| Stack Tower | برج التوازن | Timing |
| Paddle Pong | بينغ بونغ | Computer / local two-player |
| Sudoku | سودوكو | Logic puzzle |
| Mine Scout | كاشف الألغام | Logic puzzle |
| Tic Tac Toe | إكس أو | Computer / local two-player |
| Slide Puzzle | لغز الأرقام | Sliding puzzle |
| Color Sequence | إيقاع الألوان | Memory |
| Aim Lab | عين الصقر | Timed target challenge |
| Maze Escape | طريق الخروج | Maze |

## Run locally

The application only needs a static HTTP server. With Python 3 installed, run this command from the repository root:

```bash
python3 -m http.server 8000 --directory dist
```

Then open [http://localhost:8000](http://localhost:8000). Serve the application over HTTP instead of opening `index.html` directly, because it uses JavaScript modules.

## Development and tests

Use Node.js **24.15 or later in the 24.x release line**, or another version supported by the pinned JSDOM development dependency. The project was tested with Node.js 24.19.0.

```bash
npm install
npm run check
npm test
```

`npm install` is only needed for the development tests. The deployed app does not load npm dependencies.

The test suite has **15 tests**, including:

- All 20 game routes launching successfully in a DOM test environment.
- Search, favorites, local profile escaping and saved-game restoration.
- Pause/resume, animation cleanup and touch controls inside the fullscreen player.
- 2048 merges and scoring, Connect Four gravity and win detection, Sudoku rules, mines and solvable puzzles.
- Exhaustive checks that the Tic Tac Toe AI does not lose to a legal human move sequence.
- A local two-player win and the timed Aim Lab round.

DOM tests use JSDOM and a mocked Canvas context. They verify behavior, not visual layout or actual mobile rendering. A visual browser QA pass has not yet been completed.

## Project structure

| Path | Purpose |
| --- | --- |
| `dist/index.html` | App entry point and metadata |
| `dist/app.js` | Navigation, library UI, preferences and game lifecycle |
| `dist/catalog.js` | Game catalog and categories |
| `dist/core.js` | Pure game rules and reusable calculations |
| `dist/arcade.js` | Canvas-based arcade games |
| `dist/puzzles.js` | Interactive board and puzzle games |
| `dist/art.js` | SVG game-card artwork |
| `dist/icons.js` | Interface icons |
| `dist/style.css` | Responsive styles, themes and RTL/LTR layouts |
| `dist/assets/` | Local images and favicon |
| `tests/` | Game-rule and platform integration tests |

To add a game, add its catalog entry, implement its engine, connect the engine dispatch in `app.js`, and add its artwork and controls. Check its win/loss rules and input handling before publishing.

## Deploy

Upload the **contents of `dist/`** to the root of a static host. No build command or server-side application is required. Hash-based game routes work without server rewrite rules.

The app currently uses root-relative asset URLs, so host it at the domain root. A deployment under a subdirectory, such as a GitHub Pages project path, needs its asset paths adjusted first.

The existing [hosted preview](https://yalla-play-arcade.noorbk.chatgpt.site) is owner-private. Repository visibility and website access are separate settings.

## Data and current scope

Favorites, recent games, nicknames, scores and supported game positions are stored in this browser's `localStorage`. They do not sync across devices, and clearing browser data removes them.

The current version has no online accounts, remote multiplayer rooms, global leaderboard, payments or advertisements. Two-player games run on the same device. Shared links open a game without transferring a live session or saved position.

The games and game-card graphics were built for this project. The racing and spacecraft cover images were generated for the project. The application does not embed games from CrazyGames, Poki or other providers. Google Fonts is an optional external font resource; system fonts are used as a fallback.

## بالعربي

**يلّا بلاي** منصة ألعاب متصفح فيها 20 لعبة، مع واجهة عربية وإنجليزية، بحث وتصنيفات ومفضلة وحفظ أفضل النتائج. بتقدر تلعب على الجوال أو الكمبيوتر بدون تسجيل.

لتشغيلها محلياً، نفّذ أمر Python الموجود بالأعلى وافتح `http://localhost:8000`. بيانات اللاعب محفوظة على نفس المتصفح، وألعاب اللاعبين تعمل على نفس الجهاز.

Built by [Noor Yasser](https://github.com/nooryasserx).
