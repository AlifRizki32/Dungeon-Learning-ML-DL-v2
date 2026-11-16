# ⚔️ Dungeon Learning ML & DL — v2

> **Learn Machine Learning & Deep Learning by playing a dungeon crawler.**
> A retro 16-bit pixel-art RPG that turns a 28-topic ML & DL study roadmap into an interactive adventure — in Indonesian.

Clear a floor, defeat its boss, earn XP, and unlock the next one. Every topic is a room. Every boss is a milestone. The Master Tower is the endgame.

---

## ✨ What makes it fun

| | |
|---|---|
| 🗺️ **6 floors to conquer** | 5 dungeon floors + Floor 6, the **Master Tower** |
| 📚 **28 topics** | From basic maths and Python to Transformers, MLOps, Edge AI, and real-world projects |
| 👹 **Boss fights** | One boss per floor — beat the boss to earn its badge and relic |
| ⭐ **XP, levels & badges** | Progress is saved locally, so you can pick up where you left off |
| 🧙 **AI Dungeon Mentor** | A Gemini-powered chatbot that explains concepts when you get stuck |
| 🎮 **Retro pixel art** | 16-bit style, chiptune-inspired music, and a lazy-loaded 3D dungeon view |
| 🧪 **Quizzes & lessons** | Lesson chunks, spellbook quizzes, and review sessions built into the game |

## 🗺️ The roadmap

| Floor | Theme | Topics |
|---|---|---|
| **1 — Foundation** | Maths, probability, statistics, linear algebra, calculus & Python | 1–6 |
| **2 — Classical ML** | ML workflow, regression, model evaluation, trees & unsupervised learning | 7–11 |
| **3 — Deep Learning** | Neural nets from scratch, PyTorch, CNNs, RNN/LSTM, Transformers & training | 12–17 |
| **4 — Edge AI** | MLOps basics, Edge AI / TinyML & an end-to-end project | 18–20 |
| **5 — Real World** | Software engineering, real data, electronics & firmware, evaluation, debugging, communication, solo project management, security & ethics | 21–28 |
| **6 — Master Tower** | 7 endgame *Road to Master* quests: deepen theory, follow courses, read & replicate classic papers, build a portfolio, test yourself under pressure, pick a specialisation, teach others | Quests |

Bosses include the **Raja Matematika** (Floor 1), **Golem Hutan Keputusan** (Floor 2), **Hydra Arsitek Neural** (Floor 3), **Kolosus Mecha-IoT** (Floor 4), and **Raja Deadline Agung** (Floor 5).

> ⚠️ **Content note:** all curriculum content, spellbook quizzes, boss scenarios, and lesson files (`src/data/floor*.content.json`, `src/data/lessons/floor*.lessons.json`) are marked `"reviewStatus": "needs-human-review"`. Questions, worked examples, and explanations should get a human subject-matter review before you rely on them.

---

## 🚀 Quick start

**Requirements:** Node.js 20+ and npm.

```bash
# 1. Install dependencies
npm install

# 2. Start the dev server (game + AI mentor backend)
npm run dev
```

Open **http://localhost:3000** in your browser.

```bash
# Build for production
npm run build

# Validate lesson chunks
npm run check:lessons

# Run the unit tests
npx --yes tsx --test src/game/formulas.test.ts src/game/spellbookEngine.test.ts src/game/campTracker.test.ts src/game/lessonEngine.test.ts src/audio/musicSystem.test.ts src/components/AIChatbot/chatService.test.ts

# Check dependencies for known vulnerabilities
npm audit
```

### 🤖 AI Dungeon Mentor (optional)

The chatbot talks to Google Gemini through the `/api/ai-mentor` backend route. Without a key the game still works — the mentor just falls back to its built-in responses.

```bash
# Copy the example and add your key (never commit a real .env file)
cp .env.example .env
# GEMINI_API_KEY=<redacted>
```

---

## 🛠️ Tech stack

- **React 19** + **TypeScript** — UI and game state
- **Vite 8** — dev server & build
- **Tailwind CSS 4** — styling
- **Framer Motion** — animations
- **Zustand** — state management, persisted to `localStorage` (`dungeon-ml-dl:v1`)
- **Three.js** — lazy-loaded 3D dungeon view
- **Express** + **Google Gen AI SDK** — server and the AI mentor backend

---

## 📁 Project structure

```
src/
├── App.tsx                  # Main shell: map, XP bar, modals, 3D view
├── components/
│   ├── AIChatbot/           # AI Dungeon Mentor (chat UI + service)
│   ├── Dungeon3D/           # Lazy-loaded Three.js dungeon
│   ├── BattleModal.tsx      # Boss fights
│   └── ...                  # Map, inventory, lessons, music, XP bar
├── data/
│   ├── roadmap.js           # ⭐ Single source of truth: floors, topics, bosses, quests
│   ├── floor*.content.json  # Lesson content per floor
│   └── lessons/             # Lesson chunks per floor
├── game/                    # XP formulas, lesson & spellbook engines
├── pages/                   # Title, dashboard, camp, grimoire, review, tower
└── store/useGameStore.ts    # Zustand store + localStorage persistence
server.ts                    # Express server + /api/ai-mentor route
scripts/check-lessons.mjs    # Lesson-chunk validator
```

## ✏️ How to edit the roadmap

Everything lives in **`src/data/roadmap.js`** — floors, topics, bosses, relics, badges, and the Master Tower quests.

- **Topics** (`FLOORS[i].topics`): `id`, `number` (1–28), `floorId`, `name`, `scope`, `weeks` (`{ min, max }`, used by the XP formula `round(((min + max) / 2) * 50)`), `understandingSign` (*"Tanda sudah paham"*), and `parallel` for rooms unlocked from the start of a floor.
- **Bosses** (`FLOORS[i].boss`): `name`, `title`, `challenge`, `badge`, and `relic`.
- **Master Tower** (`TOWER_FLOOR.quests`): the 7 *Road to Master* quests and their book / course / paper references.

---

## 🧹 What's new in v2

This is the cleaned-up version of the original repo. Same game, same features — just lighter and tidier:

- **17 MB → 1.9 MB** — removed the 15 MB `.aistudio/` folder (52 temporary session files), 9 unused images in `public/assets/aistudio/`, and `metadata.json`
- Removed provably unused dependencies: `lucide-react`, `autoprefixer`, `esbuild`
- Removed leftover AI Studio traces: neutralised comments in `.env.example` and `vite.config.ts`, and changed the `User-Agent` in `server.ts` from `aistudio-build` to `dungeon-learning-ml-dl`
- No appearance or gameplay changes — the chatbot, lessons, bosses, and 3D dungeon all work exactly as before

The original v1 repo is untouched at [`AlifRizki32/Dungeon-Learning-ML-DL`](https://github.com/AlifRizki32/Dungeon-Learning-ML-DL).

---

## 🤝 Contributing

Found a wrong answer in a quiz, a typo in a lesson, or a bug in a boss fight? Open an issue or a pull request — and remember the content is still marked `needs-human-review`, so corrections are very welcome.

**Happy dungeon crawling — and happy learning!** 🗡️📖
