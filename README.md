# CodeCrib

**Offline Programming Snippet and Cheat Sheet Library for Students**

CodeCrib is a mobile app built with **React Native (Expo)** that gives students a pocket library of code examples they can search, save, copy and practise with. It works **fully offline**: there is no login, no server and no internet connection needed. All content ships inside the app, and personal data stays on the device.

---

## Table of contents

1. [What the app does](#what-the-app-does)
2. [Features](#features)
3. [App screens](#app-screens)
4. [Built-in content](#built-in-content)
5. [Tech stack](#tech-stack)
6. [Project structure](#project-structure)
7. [How it works](#how-it-works)
8. [Getting started](#getting-started)
9. [Useful commands](#useful-commands)
10. [Testing and validation](#testing-and-validation)
11. [Design decisions](#design-decisions)
12. [Known limitations](#known-limitations)
13. [Future improvements](#future-improvements)
14. [Author](#author)

---

## What the app does

When a student opens CodeCrib they can:

1. Go through a short **3-slide onboarding** on first launch.
2. See a **home dashboard** with learning stats and shortcuts.
3. **Browse and search** code snippets for six programming languages.
4. Open a snippet to read **syntax-highlighted code**, copy it, favorite it and write a **private note**.
5. **Add their own snippets**, edit them or delete them (with undo).
6. Take a **10-question quiz**, get instant explanations and review wrong answers.
7. Track **progress**: quiz scores, favorites, snippets viewed and learning streak.
8. Change **appearance and display settings** (light/dark mode, code text size, haptics).

## Features

- **Search**: find snippets by title, description or tag, with recent searches.
- **Filter and sort**: filter by language, category and difficulty; sort by name, date or difficulty. Filters live in a sheet that can be applied or reset together.
- **Snippet details**: highlighted code, copy to clipboard, common-mistake tip, related snippets.
- **Favorites**: save snippets and view them in one place.
- **Personal snippets**: create, edit and delete your own examples, with an undo snackbar after deleting.
- **Private notes**: attach a note to any snippet.
- **Randomized quiz**: 10 questions per round with shuffled questions and shuffled answer options, instant feedback and explanations, and wrong-answer review.
- **Progress tracking**: viewing activity, favorite count, quiz average, best score, recent scores and learning streak.
- **Settings**: system, light or dark theme; adjustable code text size; copy haptics on/off; option to reset local data.
- **Help / About** screen and an **error boundary** that recovers from crashes.
- **Accessibility labels** on tabs and main controls.
- **No network use**: no remote APIs, images or fonts. Icons and artwork are bundled locally.

## App screens

| # | Screen | Purpose |
|---|---|---|
| 1 | Onboarding | 3-slide introduction on first launch |
| 2 | Home | Learning dashboard and shortcuts |
| 3 | Snippet Library | Search, filters, sorting and snippet list |
| 4 | Snippet Details | Code, copy, favorite, notes, related snippets |
| 5 | Add / Edit Snippet | Create or update a personal snippet |
| 6 | Favorites ("Saved") | List of favorited snippets |
| 7 | Quiz | Randomized 10-question quiz |
| 8 | Quiz Result | Score and wrong-answer review |
| 9 | Progress | Scores, activity and learning streak |
| 10 | Settings | Theme, code size, haptics, data reset |
| 11 | Help / About | How to use the app and app info |

Bottom tabs: **Home, Library, Saved, Quiz, Settings**.

## Built-in content

| Item | Amount |
|---|---|
| Code snippets | 60 (10 per language) |
| Quiz questions | 60 (10 per language) |
| Languages | JavaScript, Python, Java, SQL, HTML/CSS, C++ |
| Difficulty levels | Beginner, Intermediate, Advanced |
| Categories | 15 (for example Strings, Collections, Functions, SQL Queries, Layout, Async, DOM) |

Every snippet has a title, language, category, difficulty, description, code, tags and a common-mistake note.

## Tech stack

- **Expo SDK 58**, **React Native**, **JavaScript**
- **React Navigation** (native stack + bottom tabs)
- **React Context** for snippets, theme and display preferences
- **AsyncStorage** for personal data and preferences
- **Expo Clipboard, Haptics, Splash Screen, Status Bar** and **Vector Icons**
- **Safe Area Context** and **React Native Screens**
- **ESLint** (Expo config) for code quality

## Project structure

The Expo app lives inside the `CodeCrib/` folder.

```text
CodeCrib/
├── App.js                  # App entry: providers + navigation theme
├── index.js                # Expo registration
├── app.json                # App name, icons, splash settings
├── package.json
├── README.md
├── TESTING.md              # Manual offline / device test checklist
├── ASSIGNMENT_EVIDENCE.md  # Requirement-to-code evidence map
├── assets/                 # App icon, adaptive icon, favicon, logos
├── scripts/
│   └── validate-data.js    # Checks quiz and snippet data quality
└── src/
    ├── navigation/         # AppNavigator, TabNavigator, SnippetsStack
    ├── screens/            # All app screens
    ├── components/         # Reusable UI (cards, code block, search, filters...)
    ├── context/            # Snippets, Theme and AppPreferences providers
    ├── storage/            # AsyncStorage helpers and central keys
    ├── data/               # snippets.json, quiz.json, categories.json
    ├── utils/              # search, highlight, quizBuilder, date helpers
    ├── theme/              # colors, typography, spacing
    └── constants/          # app info
```

## How it works

- **Bundled data:** `snippets.json`, `quiz.json` and `categories.json` are loaded from the app itself.
- **Personal data:** your own snippets, favorites, notes, recent searches, viewed snippets, quiz history, onboarding status and settings are saved with AsyncStorage on the device.
- **State:** `SnippetsContext` merges bundled and personal snippets and shares them with every screen; `ThemeContext` and `AppPreferencesContext` handle appearance and display options.
- **Quiz logic:** `quizBuilder.js` picks random questions and shuffles the options. The correct answer is tracked by its **text**, not by position, so shuffling never breaks scoring.
- **Storage safety:** all storage keys are in `src/storage/keys.js`, and `src/storage/storage.js` handles JSON conversion and errors in one place.

## Getting started

### Requirements

- [Node.js](https://nodejs.org) and npm
- Optional: **Expo Go** on a phone, or an Android/iOS emulator

### Install and run

```sh
git clone https://github.com/Dasun-Gunasekara/CodeCrib.git
cd CodeCrib/CodeCrib
npm install
npx expo start
```

Then:

- press **`w`** to open it in the browser,
- press **`a`** for an Android emulator,
- or scan the QR code with **Expo Go**.

## Useful commands

| Command | What it does |
|---|---|
| `npm start` | Start the Expo development server |
| `npm run web` | Run in the browser |
| `npm run android` | Run on an Android emulator or device |
| `npm run validate:data` | Check snippet and quiz data quality |
| `npx expo lint` | Run ESLint |
| `npx expo-doctor` | Check the project setup |
| `npx expo export --platform web` | Build the web version |
| `npx expo export --platform android` | Build the Android bundle |
| `npx expo start -c` | Start with a clean cache |

## Testing and validation

- `npm run validate:data` checks quiz answer integrity, the language and difficulty spread, snippet counts, categories, tags and example coverage.
- `npx expo lint` checks code style.
- [TESTING.md](./CodeCrib/TESTING.md) is a manual checklist for browsing, editing, favorites, quizzes, progress, settings and restart persistence, including **airplane-mode** checks.
- [ASSIGNMENT_EVIDENCE.md](./CodeCrib/ASSIGNMENT_EVIDENCE.md) maps each assignment requirement to the file that implements it.

For a strict offline test, use an installed preview or release build, because the Expo development server needs a network connection to Metro.

## Design decisions

- **Offline-first:** content ships as local JSON and personal data uses AsyncStorage, so every study flow works without an account or network.
- **Shuffled quiz, scored by text:** randomizing questions and options reduces memorizing answer positions, and text-based scoring stays correct after shuffling.
- **Filters in a sheet:** the library screen stays clean, and the less-used difficulty, category and sort controls sit together where they can be reviewed and applied or reset in one step.
- **Reusable components and central storage keys:** this keeps screens small and avoids duplicated code.

## Known limitations

- The built-in snippets and quiz questions are fixed; new ones need an app update.
- Personal data stays on one device. There is no account, cloud sync or backup/export.
- There is no automated unit-test suite yet. Device, screen-reader and airplane-mode checks are manual.
- App screenshots have not been added yet.

## Future improvements

- Add more student-reviewed snippets and language-specific quiz questions.
- Add import/export of personal snippets using local files.
- Add automated unit tests for storage, filtering and quiz scoring.
- Add real screenshots of the app to this README.

## Author

**Dasun Gunasekara**, [@Dasun-Gunasekara](https://github.com/Dasun-Gunasekara)
