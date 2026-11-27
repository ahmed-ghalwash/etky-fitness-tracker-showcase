# Etky - Fitness & Habit Tracker

A gentle habit-building fitness app focused on consistency over intensity.

Full-stack concept application: a **React 18** single-page client, a **PHP 8 REST API**
(framework-free, PDO with prepared statements) and a **MySQL** database.

## Features

- Daily habit check-offs with idempotent toggle (unique constraint per habit per day)
- Automatic streak and weekly-count calculation
- Workout library with levels, categories and exercise lists
- Workout completion logging and a weekly progress summary

## Interface

The client ships a hand-written motion layer - CSS keyframes plus a few small React
helpers, no animation library: staged entrances with per-card stagger, hover lift and
cover zoom, numbers that count up, charts that draw themselves, an animated seat map and
boarding pass, confetti only on real success states, and shimmering skeletons while a
request is in flight. All of it switches off under `prefers-reduced-motion: reduce`.

## Tech stack

| Layer | Tech |
| --- | --- |
| Front end | React 18, Vite, React Router |
| Back end | PHP 8.1+, PDO (native prepared statements), PHP sessions |
| Database | MySQL 8 (InnoDB, foreign keys, transactions) |

## Screenshots

| Screen | Desktop | Mobile |
| --- | --- | --- |
| Daily habit ring and check-offs | ![today](screenshots/today.png) | ![today mobile](screenshots/today-mobile.png) |
| Workout library | ![workouts](screenshots/workouts.png) | ![workouts mobile](screenshots/workouts-mobile.png) |
| Workout detail with exercises | ![workout-detail](screenshots/workout-detail.png) | ![workout-detail mobile](screenshots/workout-detail-mobile.png) |
| Weekly progress | ![progress](screenshots/progress.png) | ![progress mobile](screenshots/progress-mobile.png) |

## Engineering

- **API test suite:** 20 end-to-end tests (96 assertions) that start the real PHP front controller and drive it over HTTP: registration and sessions, validation, ownership checks, habit streaks, the 20 habit limit, idempotent check-ins, workout library, history totals and weekly progress. They run against SQLite so no database server is needed; real MySQL is covered by the smoke test below.
- **Docker Compose:** MySQL 8.4, the PHP API and nginx serving the React client start with one command.
- **CI (GitHub Actions):** PHP lint and tests on PHP 8.3, the client production build, and a Docker smoke test that boots the whole stack and checks health, registration and the session endpoint against real MySQL.
- **Endpoints added in this round:** `GET /api/habits/{id}/history` (completion rate), `GET /api/workouts/history` and `GET /api/health`.

## Source code

The full source code for this project - the React client, the PHP REST API, and the
database schema with seed data - is kept in a **private repository**.

It is available on request: reach out through my
[GitHub profile](https://github.com/ahmed-ghalwash) and I will be happy to share it.
