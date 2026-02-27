# Quiz CLI

An interactive command-line quiz game for learning programming fundamentals (JavaScript + Node.js).

## Table of contents
- [Project overview](#project-overview)
- [Features](#features)
- [Setup](#setup)
- [Usage](#usage)
- [Question data format](#question-data-format)
- [Scripts](#scripts)
- [File structure](#file-structure)
- [How it works (high level)](#how-it-works-high-level)
- [License](#license)

## Project overview
Quiz CLI is a small Node.js (ES Modules) terminal application that loads multiple-choice questions from JSON and runs an interactive quiz session.

It’s intentionally dependency-free (no third-party packages) and demonstrates common JavaScript/Node concepts such as async/await, file I/O, readline-based input, and basic OOP.

## Features
- Multiple categories (loaded from `data/questions.json`)
- Choose how many questions to answer (all / 3 / 5 depending on availability)
- Shuffled questions per run
- Colored terminal output (ANSI escape codes)
- Progress bar + end-of-quiz summary
- Review section listing incorrect answers

## Setup
### Prerequisites
- Node.js **18+** (see `package.json` → `engines.node`)

### Install
```bash
git clone https://github.com/PavloPak/elitea-test.git
cd elitea-test
npm install
```

> This project has no external runtime dependencies, but `npm install` is still a convenient, standard setup step.

## Usage
Run the quiz:
```bash
npm start
```

Or directly:
```bash
node index.js
```

Typical flow:
1. Choose a category
2. Choose number of questions
3. Answer by entering the option number
4. Review results and optionally play again

## Question data format
Questions live in `data/questions.json`.

Structure (simplified):
- `categories`: object keyed by category id
  - `name`: display name
  - `questions`: array of question objects
    - `question`: string
    - `options`: string[]
    - `answer`: number (0-based index into `options`)
    - `explanation`: string (optional)

## Scripts
From `package.json`:
- `npm start` → `node index.js`
- `npm test` → `node --test`

## File structure
```text
.
├── index.js              # Entry point: loads questions, runs main app loop
├── package.json          # Project metadata + scripts (ESM via "type": "module")
├── data/
│   └── questions.json    # Quiz categories + questions
└── src/
    ├── colors.js         # ANSI color helpers (no deps)
    ├── input.js          # readline prompts/select/confirm helpers
    └── quiz.js           # Quiz class: shuffle, scoring, results rendering
```

## How it works (high level)
- `index.js` loads question data using `node:fs/promises`, then orchestrates the UI flow.
- `src/input.js` wraps Node’s `readline` API with Promise-based helpers (`select`, `confirm`, etc.).
- `src/quiz.js` encapsulates quiz state (current question, score, answers) and renders progress/results.
- `src/colors.js` provides simple formatting utilities using ANSI escape codes.

## License
MIT (see `package.json`).
