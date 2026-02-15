# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

A 4-week "Break the Caffeine-Sleep Cycle" wellness app — a single-file HTML application with embedded CSS and vanilla JavaScript. No frameworks, no npm dependencies.

## Build & Run

- **Build:** `./build.sh` (copies HTML files to `dist/`)
- **Run:** Open `index.html` in a browser. No server required.
- **No automated tests or linting** are configured.

## Architecture

Everything lives in `index.html` (~1400 lines): embedded CSS, HTML structure, and JavaScript.

### JavaScript Structure

**Program timing:** The app uses a dynamic start date (`programStartDate` in localStorage). `getDayNumber(date)` computes the current day (1–29) and `getWeekAndDay()` maps that to a week (1–4) and day-of-week (1–7). Days follow a 7-day cycle: Test → Lower → Upper → Lower → Upper → Lower → Rest.

**Workout data:** The `workouts` object holds 4 weeks of structured exercises (lower body, upper body, recovery, test day). The `weeks` object holds caffeine/sleep goals per week with progressive targets.

**Daily view:** `updateDailyView()` drives the main UI, calling `renderTodayPlan()` which switches content based on day type. Navigation via `changeDay(delta)` and `goToToday()`.

**Progress tracking:** Three localStorage-backed JSON objects:
- `completedDays` — weekly day completion
- `exerciseDays` — 7-day exercise cycle tracking (with test day highlighting)
- `testResults` — weekly test metrics (push-ups, wall sit, glute bridges, plank, goblet squats, balance) with PR detection

**Data migration:** `migrateOldData()` handles migration from the original fixed-date format to the dynamic start date system.

### Data Persistence

All state is in browser `localStorage`. There is no backend.
