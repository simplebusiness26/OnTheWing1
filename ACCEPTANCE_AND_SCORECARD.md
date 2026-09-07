# ACCEPTANCE, QA AND MODEL-COMPARISON SCORECARD

This repository is being used to compare two coding models from the same starting brief. Judge the models on **working output**, not confidence or explanation length.

Maximum score: **100**.

A category receives points only for functionality that is actually present and plausibly wired into the playable build. Placeholder art is acceptable where the gameplay system works. Empty classes, TODOs, mock screenshots and documentation-only claims receive no implementation credit.

---

# 1. BUILD HEALTH — 10 POINTS

## 1.1 Valid Unity project — 2

Full credit:

- real Unity project structure.
- valid `Assets`, `Packages`, `ProjectSettings`.
- pinned Unity version.

## 1.2 Compile health — 2

Full credit if project is expected to compile with no known C# errors.

## 1.3 Android configuration — 2

- Android target configured.
- landscape.
- sensible package identifier.
- no unnecessary runtime permissions.

## 1.4 GitHub Actions APK pipeline — 3

- workflow exists.
- Android build target.
- artifact upload.
- manual trigger.
- secrets are referenced, not committed.

If Unity Personal activation requires owner action, workflow can still receive full structural credit if exact required setup is documented truthfully.

## 1.5 Build status documentation — 1

`BUILD_STATUS.md` clearly separates working, partial, placeholder and blocked items.

---

# 2. MOBILE MOVEMENT AND CAMERA — 10 POINTS

## 2.1 Floating joystick — 3

- touch movement.
- analog response.
- dead zone/release works.
- safe-area aware.

## 2.2 Third-person movement — 2

- camera-relative.
- smooth rotation.
- gravity/stairs.
- sprint or run behavior.

## 2.3 Swipe camera — 3

- right-side swipe look.
- vertical clamp.
- sensitivity.
- does not fight action buttons.

## 2.4 Camera collision/mobile feel — 2

- cell interiors remain usable.
- camera avoids clipping where possible.

---

# 3. PRISON WING AND WORLD — 10 POINTS

## 3.1 Correct architectural identity — 4

- long rectangular atrium.
- cells on opposing long sides.
- three visible levels.
- upper landings/railings.
- open central void.
- stairs.
- safety-net visual.

## 3.2 Enterable/player spaces — 2

- player cell.
- several cells or meaningful interior spaces.

## 3.3 Attached gameplay areas — 2

Credit for showers, yard, training/gym, job area, game table.

## 3.4 Visual coherence — 2

Even with primitives, materials/lighting/layout create a deliberate gritty institutional look rather than random cubes.

---

# 4. PRISON ROUTINE / LIVING WORLD — 10 POINTS

## 4.1 Game clock — 2

Time advances and saves.

## 4.2 Routine manager — 2

Distinct routine periods exist and change gameplay/world state.

## 4.3 NPC schedules — 4

- at least 8 visible NPCs follow schedules.
- destinations change with routine.
- player conversation does not permanently break schedule.

## 4.4 Player compliance consequences — 2

Missing/ignoring required routine has believable staff-facing effect with grace period.

---

# 5. LIFE SIMULATION AND PROGRESSION — 10 POINTS

## 5.1 Character selection — 2

Six choices exist and actually alter stats/growth/standing.

## 5.2 Stat progression — 2

Relevant activities increase meaningful skills.

## 5.3 Hygiene/shower — 2

Hygiene changes over time/activity, shower restores it, and low Hygiene affects at least one social reaction.

## 5.4 Training — 2

Training costs energy/stamina, grants relevant XP and has sensible anti-spam behavior.

## 5.5 Job loop — 2

At least one real shift can be attended/completed/missed with pay and staff consequences.

---

# 6. SOCIAL SIMULATION — 12 POINTS

## 6.1 Individual relationships — 2

NPC-specific affinity/trust/fear or equivalent exists.

## 6.2 Structured memory — 3

Important actions create queryable memories that later affect behavior/dialogue.

## 6.3 Prisoner reputation — 2

Respect, Trust, Fear and Influence are distinct and used.

## 6.4 Staff standing — 2

Staff Trust, Suspicion, Heat and Reliability are distinct and used.

## 6.5 Association consequences — 2

Being around high-attention people can matter without simply adding Heat every frame.

## 6.6 Indirect social reactions — 1

At least one NPC reacts to player’s relationship/association with another NPC.

---

# 7. HEAT / “RED HOT” SYSTEM — 7 POINTS

## 7.1 Heat events and decay — 2

Heat rises for meaningful reasons and falls over time/good routine.

## 7.2 Officer response — 2

Officer dialogue/state changes with Heat or Suspicion.

## 7.3 Prisoner response — 2

At least one cautious NPC refuses/changes behavior when player is red hot.

## 7.4 Recoverability — 1

Heat does not permanently trap the player in a punishment spiral.

---

# 8. DIALOGUE, MISSIONS AND STORY — 12 POINTS

## 8.1 Data-driven dialogue — 2

Supports conditions/choices/actions without all content hardcoded into random scene scripts.

## 8.2 Mission framework — 2

Reusable objective/condition/progress system exists.

## 8.3 Mission 1 playable — 2

First Morning can be completed.

## 8.4 Mission 2 playable — 2

Find Your Feet can be completed.

## 8.5 Mission 3 playable — 2

Who You Sit With can be completed with consequences.

## 8.6 Campaign scaffolding — 2

30 main mission definitions/data or clearly wired placeholders exist, with early missions most complete.

---

# 9. MINIGAME AND COMBAT — 7 POINTS

## 9.1 Real minigame — 4

At least one actual board minigame (preferably checkers) has legal moves, turns, win/loss and NPC result integration. A progress bar labeled “playing chess” earns zero.

## 9.2 Combat — 3

- unarmed mobile controls.
- stats/stamina influence outcome.
- NPC opponent.
- non-graphic feedback.
- relationship/Heat consequence.

---

# 10. SAVE / LOAD — 5 POINTS

## 10.1 Save coverage — 3

Persists core player/time/mission/relationship/reputation state.

## 10.2 Reliability — 1

Versioning/backup/safe spawn or equivalent corruption/position protection.

## 10.3 Resume experience — 1

Loading returns player to a sensible playable state rather than resetting systems.

---

# 11. UX, PERFORMANCE AND POLISH — 5 POINTS

## 11.1 Mobile UI — 1

Readable, touch targets sensible, not overcrowded.

## 11.2 Settings — 1

Camera sensitivity + quality/audio basics.

## 11.3 Performance-minded implementation — 1

Staggered AI, limited lights, sensible NPC count, no obvious per-frame allocation disasters.

## 11.4 Atmosphere — 1

Material/lighting/audio hooks produce coherent mood.

## 11.5 Debug/test tools — 1

Useful developer menu or validation/test helpers.

---

# 12. CODE QUALITY / EXTENSIBILITY — 2 POINTS

## 12.1 Separation — 1

No single giant God-object controls the whole game; systems have sensible responsibilities.

## 12.2 Data-driven expansion — 1

NPCs/missions/items/characters can be extended without rewriting core managers.

---

# 13. BONUS TIEBREAKERS

These do not raise score above 100 but decide close comparisons.

Prefer the model that provides more of the following **without breaking the fundamentals**:

- more than 8 visibly scheduled NPCs.
- more than 3 fully playable main missions.
- side missions with persistent consequences.
- multiple playable jobs.
- both checkers and chess.
- character-specific dialogue.
- relationship callbacks to old memories.
- emergent influence/boss-of-wing reactions.
- richer enterable cells/yard.
- good character animations.
- real audio with valid licenses.
- baked/mobile-efficient lighting.
- automated Unity tests.
- side-by-side installable package identifier.
- downloadable successful APK artifact.

---

# 14. PENALTIES / RED FLAGS

Subtract confidence in the result if:

- documentation claims features not found in code.
- project contains many empty classes/TODO shells.
- no playable world exists.
- controls are desktop-only despite mobile requirement.
- every NPC stands still.
- “missions” are only text files.
- stat values never affect gameplay.
- reputation is really one number with four labels.
- Heat has no world reaction.
- minigames are fake.
- game requires paid services/assets to run.
- copyrighted commercial assets are copied into repo without license.
- Android workflow commits private Unity credentials.
- game implements realistic dangerous/illegal operational instructions rather than abstract fiction.
- violence is made graphic/gory despite specification.

---

# 15. PHONE TEST SCRIPT

When an APK is available, test each model with the same procedure.

## Test A — Install/boot

1. Download APK.
2. Install.
3. Launch.
4. Record load time/crash.
5. Verify landscape UI.

## Test B — Character selection

1. Inspect six characters.
2. Choose Fighter.
3. Note starting stats.
4. Restart/new game if feasible.
5. Choose Thinker.
6. Confirm meaningful stat difference.

## Test C — Movement

1. Walk out of cell.
2. Rotate camera in cell.
3. Walk landing.
4. Use stairs.
5. Try wall/camera collision.
6. Visit opposite side/ground level.

## Test D — Routine

1. Watch time change.
2. Observe at least 3 NPCs before routine change.
3. Observe them after routine change.
4. Intentionally miss a required activity once.
5. Confirm believable consequence.

## Test E — Life systems

1. Train.
2. Confirm relevant XP/stat feedback.
3. Let Hygiene drop or use debug tool.
4. Confirm social consequence.
5. Shower.
6. Confirm recovery.
7. Attend work.
8. Confirm pay/reliability.

## Test F — Social

1. Talk to Malcolm.
2. Make a choice that alters relationship.
3. Return later.
4. Look for memory/dialogue difference.
5. Increase Heat with debug or gameplay.
6. Talk to Nate/other cautious NPC.
7. Confirm red-hot reaction.

## Test G — Minigame

1. Start checkers/chess.
2. Make multiple legal moves.
3. Finish or forfeit game.
4. Confirm result reaches NPC relationship/mission system.

## Test H — Combat

1. Train some stats.
2. Fight a suitable NPC encounter.
3. Confirm stamina/health behavior.
4. Confirm non-graphic consequence.
5. Confirm Heat/reputation changes if witnessed.

## Test I — Story

1. Complete Missions 1–3.
2. Confirm journal updates.
3. Confirm social choice in Mission 3 changes later availability/relationship.

## Test J — Save

1. Save/autosave after changing stats/relationship.
2. Close app.
3. Reopen.
4. Confirm state persists.

---

# 16. MODEL COMPARISON NOTES TEMPLATE

Use this after testing both builds.

```text
MODEL / REPO:
APK VERSION:
DATE TESTED:
DEVICE:

Build/boot: __/10
Controls: __/10
World: __/10
Routine: __/10
Life sim: __/10
Social simulation: __/12
Heat: __/7
Story/missions: __/12
Minigame/combat: __/7
Save: __/5
UX/performance: __/5
Code/extensibility: __/2

TOTAL: __/100

Best moment:

Biggest problem:

Did it feel like living on a prison wing? Yes / Partly / No

Would I keep building from this repo? Yes / Maybe / No
```

The winner should be the repository that provides the strongest **playable foundation for the full game**, not necessarily the one with the flashiest title screen.
