# Cuci Penapis Challenge (web game MVP)

This is a phone-first 3D web game for the top of the Fixers Academy funnel. It runs from one file, `index.html`, built with Three.js from a CDN. The game has no build step and stores no personal data.

## Play locally

```bash
python3 -m http.server 8795 --directory ~/Projects/FixersSimulator/webgame/cuci-penapis
```

Then open http://localhost:8795. To test from a given step, add `?step=N` to the address, with N from 1 to 15. Best times are not saved in that mode.

## Flow (15 steps, about 2 minutes)

The steps follow Fixers C1-01 (Basic Hygiene) and the owner-manual guides (Samsung, LG, Daikin).

1. **Selamat (safety)**
   - Take a "before" photo.
   - Turn the unit off with the remote, then the wall switch.
   - Lift the front panel. Touching the unit while the switch is ON fails the run at once.
2. **Penapis (filters)**
   - Pull both filters down and out.
   - Vacuum the dust.
   - Answer a question: which side to rinse from? The correct answer is the back.
   - Wash the filters.
   - Dry them in the shade. Choosing the sun counts as a mistake.
3. **Dalam (inside the unit)**
   - Pop the caps, then unscrew 3 casing screws anticlockwise.
   - Remove the casing.
   - Brush the coil fins up and down only. Brushing sideways counts as a mistake.
   - Refit the casing and tighten the screws clockwise.
4. **Uji (test)**
   - Collect the filters once they are dry.
   - Push them back up into place and close the panel.
   - Turn on the wall switch, then the remote.
   - Take an "after" photo.

**Scoring:**
- Stars: 3 with no mistakes, 2 with one mistake, 1 with more.
- XP adds a time bonus and subtracts a penalty for each mistake.
- Ranks are Perantis, Juruteknik Muda and Pro Fixers.
- Every player gets the badge "Penapis Bersih".

**Brand and video (7 Nov 2026):**
- The game uses the Fixers palette (#eac1d8 pink on #191a18), the real wordmark (`media/wordmark.svg`) and the film's fonts (Archivo Black, Poppins).
- MULA plays `media/intro.mp4` once per session (the film's 11-second hook, skippable with LANGKAU), then the game starts.
- The cohort screen has "Tonton kisah Ali (58 s)", which plays `media/kisah-ali.mp4`, the full film.
- To update both clips, re-cut them from `film/jalan-ketiga/renders/` (720x1280, H.264, faststart).

After the reward screen comes the cohort pitch. The "Saya berminat" button opens `academy.fixers.my/?src=cuci-penapis&who=<spm|kerja|belajar|lain>`.

## UI and gamification (7 Nov 2026)

The UI ports the LihFolk "Ink and Candy" kit (from the Roblox skills) to the web, in Fixers colours.

**Look:**
- Thick ink outlines.
- Tactile slabs with a darker lip that sink when pressed.
- Faint candy stripes.
- Fredoka display type with an ink stroke.
- Every emoji is replaced by a drawn icon (34 symbols) in the LihFolk glossy style: a light and a shade facet, a white shine and a tip glint. The sources are in `parts/` (`icons.svg`, `style.css`, `body.html`), already inlined in `index.html`.

**Points:**
- 100 for each step done right.
- +50 "LAJU!" when a step is under its target time.
- A combo bonus of +20 to +100 for steps in a row without a mistake, with a flame "x3" badge.
- Small rewards along the way: remote off +20, wall switch in the right order +40, each filter +25, each screw +15, every 25% of cleaning +10, each proof photo +50, a correct quiz answer +50, drying in the shade +20.
- A mistake costs 75 and resets the combo.

**Ranks:** PERANTIS from 0, JURUTEKNIK MUDA from 1600, PRO FIXERS from 2800. A gold bar fills toward the next rank, and a rank-up shows a sunburst.

**Sounds:** files in `media/sfx` (chime, ping, pop, sparkle, error, whoosh, key press, click). The synthesised sounds remain as a fallback.

**Results screen:** the stars pop in one by one, the score counts up, and the best score is kept on the phone.

## Job call and walk-in (7 Nov 2026)

After MULA (and the intro clip), the game runs a short opening before the work:
1. **Incoming job:** the Fixers app phone rings with a new job: customer, area and distance, the service, the time, and the pay (`jobPay` RM80, plus `jobBonus` RM20 for a job with no mistakes). TOLAK only shakes the phone ("Rezeki jangan ditolak!").
2. **Walk-in:** TERIMA starts a first-person walk from the Fixers van to the customer's terrace house (No. 12), with footsteps. The door swings open, the view fades, and you walk into the room to the aircond.
3. **Greeting:** the customer says the aircond isn't cold, and the timer starts.

The 3D street sits at z 170, out of the room camera's range. The results screen counts up the pay with a chime. The money figures are placeholders that Fixers must approve.

## Settings

The settings live in `CONFIG` at the top of the script:
- `draft`: shows the "DRAF" warning on the cohort screen.
- `signupUrl`: where the "Saya berminat" button goes.
- `salary`: the pay line on the cohort screen.
- `dryingSeconds`: how long the filters take to dry.
- `jobPay`, `jobBonus`, `customer`, `area`: the job card on the phone and the pay on the results screen.

## Fixers must confirm before release

- **Cohort-screen claims:** "Gaji permulaan RM2,000 – RM2,500", "Jaminan kerja sebaik kamu mula", "Tak perlu PTPTN / percuma", 8–10 seats, and the priority groups.
- **Casing screws:** the number and position of the screws vary by model. Removing the casing goes beyond basic filter cleaning, so Cikgu John should confirm whether this step stays in the game.
- **Rinsing from the back:** this is common advice. Fixers should confirm it.
- **Sign-up page:** academy.fixers.my needs a free-cohort page that reads `src` and `who`.
- **Branding:** the logo and colours are placeholders in Fixers pink.
