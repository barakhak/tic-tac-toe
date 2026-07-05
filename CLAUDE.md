# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

A single-page Tic Tac Toe game. No build system, package manager, bundler, or test suite — it's plain HTML/CSS/JS with no external dependencies.

## Running it

There is no build/lint/test command. Open the file directly in a browser, or serve it locally, e.g.:

```
start index.html          # Windows: open directly
python -m http.server     # or serve the directory and browse to it
```

## Structure

- `index.html` and `tictactoe.html` are intentionally identical, self-contained files (HTML + inline `<style>` + inline `<script>`, no separate assets). Both are kept in the repo by explicit user choice — **when editing game logic or styling, apply the same change to both files** so they stay in sync.

## Architecture (within the HTML file)

All logic lives in one inline `<script>` block using an IIFE, no modules/frameworks:

- `board` is a flat length-9 array of `'X' | 'O' | null`; `WIN_LINES` lists the 8 index triples that count as a win.
- Two modes toggle via `vsComputer`: 2-player (both sides driven by clicks on `.cell` elements) and vs-computer (O is played automatically by `computerMove`).
- The computer is an unbeatable player using `minimax` over the full game tree (no pruning/depth limit needed since the board is only 9 cells).
- `scores` (`X`/`O`/`D`) persists only for the current page session (in-memory, not stored) and resets via the "Reset Scores" button; "New Round" clears the board without touching scores.

## Git workflow

This repo is pushed to `github.com/barakhak/tic-tac-toe`. Commit and push changes with clear, descriptive commit messages so there's always a revertible saved version — this was set up explicitly so changes can be rolled back easily.
