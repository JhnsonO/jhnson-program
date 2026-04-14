# jhnson-program

Personal football development program for a Step 6 → Step 5 winger/wingback targeting a professional contract within 18 months.

**Live:** [jhnsono.github.io/jhnson-program](https://jhnsono.github.io/jhnson-program/)

---

## What it is

A weekly program builder that generates a personalised 7-day training plan based on a short check-in, plus a required daily readiness check-in. Designed around one core principle: make a better footballer first, fitter second, stronger third.

The weekly check-in takes 30 seconds. Answer 4 questions — body status, injury location, weekly focus, week type — and get a full week with real time slots, structured sessions, and fallback options for low-energy days.

Before viewing the weekly plan each day, the app now runs a **Daily Check-In (V2)** for:
- Sleep (hours)
- Energy (1–5)
- Soreness (1–5)
- Pain (0–10)

If today's daily check-in already exists, the app opens directly to the weekly plan and shows a "Today" readiness bar at the top.

---

## Weekly structure

| Day | Block |
|-----|-------|
| Monday | Pitch (1v1 + shooting) → Gym (lower/power) |
| Tuesday | Pitch (conditioning) → Gym (upper/pull) |
| Wednesday | Pitch (left foot + technical) → Gym (push) → Kickabout |
| Thursday | Gym (heavy lower) |
| Friday | Pitch (1v1 + shooting) → Gym (full body) → Kickabout |
| Saturday | Active recovery + match study |
| Sunday | Rest + week prep |

Morning block: **5:00am pitch → gym → done by 8:30am**

---

## Non-negotiables (every single day)

- Ball mastery at home before leaving — 10 min
- Rehab: Copenhagens + hip flexion + isometric split squat hold
- Mental: rotate visualisation / match study / breathing (5 min)

Rehab is structural not optional. The injury cycle (groin/hamstring recurrence) exists because rehab stops when it feels fine. It doesn't stop.

---

## Features

- **Daily Check-In (V2)** — one entry per day saved to `localStorage` (`jhnson_daily`)
- **Today bar** — shows today's sleep/energy/soreness/pain on the weekly screen
- **Dynamic intensity layering** — daily adjustments applied on top of weekly logic:
  - pain ≥ 6 → pitch sessions replaced by rehab blocks
  - soreness ≥ 4 → sprint/conditioning drill lines removed
  - energy ≤ 2 → day replaced with ED minimum fallback
  - sleep < 5h → final block removed from each day (volume reduction)
- **Injury mode** — tick injured in check-in and all pitch/lower body sessions are replaced with upper body gym + rehab blocks
- **Real time slots** — every session has a time (5:00, 5:20, 6:35 etc), not just a label
- **Structured pitch drills** — cone setups, shot counts, crossing zones, sprint finishes. Not reminders — actual sessions.
- **Confidence focus** — 1v1 and shooting are locked into Monday and Friday every week regardless of check-in answers
- **Executive dysfunction fallback** — every day has a single-sentence minimum version
- **Juggling trick tracker** — weekly dot progress (green = progressing, red = stalling)
- **Injury/niggle log** — rate each area, add notes
- **Player to study** — random pick each week from a curated list of fullbacks/wingers worth studying
- **Dark mode** — system preference
- **localStorage persistence** — juggling and injury data persists across sessions

---

## Stack

Single HTML file. Vanilla JS. No build step. No dependencies. localStorage for persistence.

---

## Updating

```bash
# Edit index.html, then:
B64=$(base64 -w 0 index.html)
SHA=$(curl -s https://api.github.com/repos/JhnsonO/jhnson-program/contents/index.html \
  -H "Authorization: token YOUR_TOKEN" | python3 -c "import sys,json; print(json.load(sys.stdin)['sha'])")
curl -X PUT https://api.github.com/repos/JhnsonO/jhnson-program/contents/index.html \
  -H "Authorization: token YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d "{\"message\":\"update\",\"content\":\"$B64\",\"sha\":\"$SHA\"}"
```
