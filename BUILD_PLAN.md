# FULL BUILD PLAN — ON THE WING

This is the execution roadmap for turning the design documents in this repository into the largest coherent Android-playable build possible. The model should not treat these phases as separate future projects; it should move through them continuously in one run and stop only when genuinely blocked.

---

# PHASE 0 — REPOSITORY AND UNITY BOOTSTRAP

## Goals

Produce a valid Unity project that can be opened, compiled and eventually built for Android.

## Tasks

- Create Unity 6 LTS project files.
- Configure URP.
- Set landscape orientation.
- Add/verify Input System.
- Add/verify AI Navigation.
- Add Test Framework.
- Create project namespace/folder structure.
- Add `Bootstrap`, `MainMenu`, `CharacterSelect`, `Wing_A` scenes or a practical runtime-generated equivalent.
- Create bootstrap/session services.
- Configure build scene list.
- Set package identifier.
- Add `.gitignore` appropriate for Unity.
- Add README build/run notes.
- Add version string/build number.

## Deliverable

Game launches to a title screen and can enter a placeholder character-select screen without compile errors.

---

# PHASE 1 — MOBILE INPUT FOUNDATION

## Goals

Make the game immediately testable as a mobile third-person game.

## Tasks

### Unified input

- Define an input abstraction shared by touch and keyboard/mouse.
- Keyboard development controls: WASD, mouse look, interact key, sprint, combat keys.

### Floating movement joystick

- Left-side floating joystick.
- Dead zone.
- Analog magnitude.
- Multi-touch safe.
- Recenter/release correctly.
- Safe-area aware.

### Camera look

- Right-side swipe zone.
- Ignore touches starting on action buttons.
- Yaw/pitch.
- Vertical clamp.
- Adjustable sensitivity.
- Optional invert Y.

### Player movement

- CharacterController or stable equivalent.
- Camera-relative movement.
- Walk/jog/sprint.
- Smooth rotation.
- Gravity.
- Slope/stair handling.
- Stamina cost for sprint.

### Camera rig

- Third-person follow.
- Smooth damping.
- Collision avoidance.
- Narrow-cell behavior.

## Deliverable

Player can move through a test room comfortably on touchscreen and editor controls.

---

# PHASE 2 — UK-STYLE WING GREYBOX

## Goals

Create the game’s core visual space early so every later system can be tested in context.

## Geometry specification

- Long rectangular atrium.
- Three levels.
- Cells on two opposing long sides.
- No main cell rows on short ends.
- Upper landings outside cells.
- Railings.
- Open central void.
- Safety net visual.
- Stairs at ends/appropriate circulation points.
- Ground-floor association space.
- Officer desk/station placeholder.
- Wing gate/entry placeholder.
- Attached shower room.
- Attached yard.
- Training/gym area.
- Cleaning/job storage area.
- Games table.

## Modular components

Create reusable:

- Cell shell.
- Cell door.
- Landing segment.
- Railing segment.
- Stair module/ramp navigation proxy.
- Wall/floor module.
- Fluorescent light fixture visual.
- Noticeboard/signage placeholder.

## Cell detail

At minimum:

- Player cell fully enterable.
- 4–8 NPC cells enterable.
- Remaining doors can be decorative/closed.

Player cell includes:

- bed.
- storage/shelf placeholder.
- desk/chair or small surface.
- door interaction.
- safe spawn point.

## Materials

Create coherent palette:

- worn painted walls.
- concrete floor.
- dark metal.
- muted accent color.
- yard concrete.
- safety mesh.

## Lighting

- functional fluorescent/institutional appearance.
- mobile-friendly.
- limit real-time shadow lights.

## Deliverable

Player can leave their cell, walk the upper landing, use stairs, cross the ground floor and enter the attached gameplay areas.

---

# PHASE 3 — INTERACTION FRAMEWORK

## Goals

Avoid one-off button scripts by creating a reusable context interaction layer.

## Tasks

- `IInteractable` or equivalent.
- Player interaction scanner.
- Candidate scoring by distance/facing.
- Context action button.
- Prompt label/icon.
- Interaction lock/player mode changes.

## Initial interactables

- Cell door.
- NPC talk.
- Shower.
- Pull-up/training station.
- Job task point.
- Bed/sleep.
- Board-game table.
- Sit point.
- Inspectable prop.

## Deliverable

Approaching objects changes the context button correctly and actions trigger the relevant component.

---

# PHASE 4 — CHARACTER SELECTION AND PLAYER DATA

## Goals

Make the six character choices mechanically meaningful from the first build.

## Character definitions

Implement:

1. Fighter.
2. Hustler.
3. Veteran.
4. First-Timer.
5. Athlete.
6. Thinker.

Each stores:

- stable ID.
- name.
- short bio.
- adult age.
- build description.
- base stats.
- growth multipliers.
- passive bonus.
- disadvantage.
- initial prisoner reputation.
- initial staff standing.
- optional unique dialogue tag.

## Character select UI

- swipe/scroll cards or large touchable selection.
- display strengths/weaknesses clearly.
- confirm button.
- no tiny text.

## Runtime

- selected definition creates `PlayerProgressState`.
- starting stats feed combat/training/dialogue.
- save selected ID.

## Deliverable

Starting as Fighter versus Thinker produces clearly different values and at least one different early dialogue/reaction.

---

# PHASE 5 — STATS, NEEDS AND PROGRESSION

## Core stats

Physical:

- Strength.
- Fitness.
- Stamina.
- Fighting.

Mental:

- Intelligence.
- Awareness.
- Nerve.

Social:

- Persuasion.
- Intimidation.
- Social Skill.

Prison-life:

- Work Skill.
- Street Smarts.
- Prison Knowledge.
- Game Skill.

## Dynamic conditions

- Health.
- Energy.
- current Stamina.
- Hygiene.
- Stress.
- lightweight meal/hunger state.

## XP

- configurable XP curves.
- growth multiplier from character.
- diminishing gains from repeated identical action.
- event on level/value increase.

## UI

Character screen showing values/progress.

Do not clutter gameplay HUD with all stats.

## Deliverable

Training, work, dialogue and minigame hooks can add relevant XP and the chosen character’s growth modifiers visibly matter.

---

# PHASE 6 — CLOCK AND DAILY ROUTINE

## Goals

Turn the environment into a place with time and structure.

## Game clock

- Day number.
- Minute-of-day.
- configurable real-seconds-per-game-minute.
- pause states.
- save/load.

## Routine blocks

Example gameplay schedule:

- Lock-up/night.
- Morning unlock/count.
- Breakfast/association.
- Work/education.
- Lunch/count.
- Afternoon work/yard/exercise.
- Evening meal.
- Evening association.
- Lock-up.

Use fictionalized timings suitable for play.

## World effects

- player cell door changes routine state.
- yard access changes.
- activity availability changes.
- HUD label updates.

## Compliance

- expected zone/activity per relevant routine.
- grace period.
- warning.
- reliability/trust consequence for repeated miss.

## Deliverable

A whole prison day can play through, with visible world/routine changes rather than only a clock number.

---

# PHASE 7 — NPC POPULATION AND AI SCHEDULES

## Goals

Populate the wing with a believable minimum community.

## Important NPCs

Create data for all 15 inmates and 5 officers in `NPCS_AND_MISSIONS.md`.

## First visible population target

- 8–15 important inmate actors.
- 3–5 officer actors.
- optional 10+ simplified background inmates if performance allows.

## NPC brain states

- InCell.
- WalkingToRoutine.
- Working.
- Eating/standing at meal activity.
- Exercising.
- Socializing.
- GameTable.
- TalkingToPlayer.
- Conflict.
- ReturningToCell.
- LockedUp.

## Activity slots

- social points.
- gym points.
- work points.
- game seats.
- cell idle points.

## Navigation

- NavMesh on ground floor, landings, cells, yard.
- links/proxies for difficult stairs if needed.
- stagger route updates.

## Performance

- off-screen simplified state.
- lower-frequency thought ticks.
- no full behavior evaluation every frame.

## Deliverable

NPCs visibly wake, leave cells, move to different activities, return later, and can resume schedule after talking to player.

---

# PHASE 8 — HYGIENE AND SHOWER LOOP

## Goals

Prove everyday routine feeds social gameplay.

## Mechanics

- Hygiene decays slowly.
- extra decay after training/fight.
- shower restores it.
- low-Hygiene status tag.
- NPC dialogue variants/comments.
- very low Hygiene can cause some social refusal/penalty.

## Visual

Optional mild dirty/sweaty material state.

No explicit shower visuals required; transition/animation can remain modest.

## Deliverable

Ignoring Hygiene has a real gameplay effect and showering fixes it.

---

# PHASE 9 — TRAINING LOOP

## Stations

At least:

- pull-ups.
- bodyweight/push-up station.
- cardio/running interaction.

Optional:

- weights.

## Interaction

- enter station.
- short timing/hold/repetition mechanic.
- spend Energy/Stamina.
- gain relevant XP.
- Hygiene cost.
- same-day diminishing returns.

## Social hooks

- Reece/Cal observe some training actions.
- challenge availability can test stats/training history.

## Deliverable

A weak character can become measurably stronger across several in-game days.

---

# PHASE 10 — JOB SYSTEM

## First job

Wing orderly/cleaning detail.

## Requirements

- assignment state.
- schedule window.
- attendance tracking.
- grace period.
- task list.
- completion result.
- pay.
- Work Skill XP.
- Staff Trust/Reliability.
- missed shift consequences.
- possible job loss after repeated misses.

## First tasks

Use harmless ordinary actions:

- clean marked floor/area.
- collect cleaning item token.
- return supplies.
- complete checklist.

## Future definitions

Scaffold:

- laundry.
- kitchen.
- workshop.
- library.
- servery.

## Deliverable

Doing a job competes meaningfully with social opportunities and changes player’s staff-facing state.

---

# PHASE 11 — ECONOMY, ITEMS AND FAVORS

## Money

- integer legitimate pay balance.
- basic approved shop/inventory scaffolding.

## Inventory

- stable item IDs.
- add/remove/count.
- stack rules.
- simple menu.
- save/load.

## Favor system

Per NPC:

- favors owed to player.
- favors player owes.

## Story items

Abstract tokens only.

No real-world recipes, smuggling methods, concealment mechanics or security bypass procedures.

## Deliverable

Money and favors exist as separate resources and can be checked by mission/dialogue conditions.

---

# PHASE 12 — RELATIONSHIPS AND NPC MEMORY

## Relationship dimensions

Per NPC:

- Affinity.
- Trust.
- Fear.
- favors.

## Structured memory

Event types include:

- HelpedMe.
- RefusedMe.
- KeptPromise.
- BrokePromise.
- BeatMeAtGame.
- FoughtMe.
- HelpedAlly.
- HarmedAlly.
- AssociatedWithRival.
- ReliableWorker.
- MissedWork.
- PublicSupport.
- PublicHumiliation.

## Memory behavior

- timestamp.
- magnitude.
- decay policy.
- query tags.
- permanent important memories.
- aggregate/remove trivial old memories.

## Indirect reactions

Use NPC-to-NPC links:

- allies care how player treats allies.
- rivals notice association.
- cautious characters care about Heat.

## Deliverable

An NPC can reference or behaviorally react to something the player did on a previous day.

---

# PHASE 13 — GLOBAL PRISONER REPUTATION

## Values

- Respect.
- Trust.
- Fear.
- Influence.

## Event sources

- fights.
- promises.
- mediation.
- public choices.
- side missions.
- favors.

## Threshold effects

- dialogue.
- challenge availability.
- NPC approach frequency.
- influence requests.

## Deliverable

A player can be feared without trusted, or trusted without physically respected.

---

# PHASE 14 — STAFF TRUST, SUSPICION AND HEAT

## Values

- Staff Trust.
- Suspicion.
- Heat.
- Reliability.

## Heat reasons

- witnessed fight.
- repeated routine trouble.
- association patterns with high-attention NPCs.
- story incidents.

## Decay

- gradual.
- slightly improved by stable routine/reliability.

## Thresholds

Warm:

- extra barks.

Hot:

- more warnings/attention.
- cautious NPCs uncomfortable.

Red Hot:

- some NPCs refuse risky conversations.
- job/story opportunities may temporarily pause.
- Senior Officer consequences possible.

## Safety/fiction rule

Officer intelligence is an abstract game system. Do not implement ways to defeat searches or evade real security.

## Deliverable

The world reacts differently when the player is red hot and can recover after keeping a low profile.

---

# PHASE 15 — DIALOGUE SYSTEM

## Requirements

Data-driven nodes supporting:

- line.
- choice.
- conditions.
- actions.
- end.

## Conditions

- character archetype.
- stat threshold.
- relationship.
- memory.
- global reputation.
- Staff Trust/Heat.
- mission state.
- current routine.
- job.
- item/favor.

## Actions

- add memory.
- change relationship.
- start mission.
- progress objective.
- add/remove item.
- modify reputation.
- set world flag.

## Content

Author distinct intro conversations for:

- Malcolm.
- Reece.
- Vince.
- Tobes.
- Daz.
- Ellis.
- Oz.
- Deano.
- Si.
- Cal.
- Nate.
- Vic.
- at least two officers.

## Deliverable

NPC dialogue is not identical and reacts to player state.

---

# PHASE 16 — JOURNAL AND PEOPLE UI

## Journal tabs

- Main Story.
- Side Stories.
- People.
- Routine.
- Discoveries.

## Person entry

- name.
- known summary.
- general relationship description.
- known schedule hints.
- remembered notable interactions.

Never show hidden betrayal/reliability values.

## Deliverable

Player can understand what they have discovered without needing giant map markers.

---

# PHASE 17 — MISSION FRAMEWORK

## Data

- stable mission ID.
- title.
- act.
- prerequisites.
- objective list.
- optional objectives.
- consequences.
- branch state.
- world flags.

## Objective event types

- TalkToNpc.
- EnterZone.
- AttendRoutine.
- CompleteJob.
- TrainStat.
- WinMinigame.
- ReachRelationship.
- ReachReputation.
- ReachHeatState.
- HoldItem.
- DialogueChoice.
- WaitUntilTime.

## Behavior

- subscribe to events.
- avoid frame polling.
- save progress.
- journal update.

## Deliverable

Reusable mission system supports all 30 campaign definitions.

---

# PHASE 18 — MAIN MISSIONS 1–3 FULL IMPLEMENTATION

## Mission 1 — First Morning

- start in cell.
- unlock.
- movement tutorial.
- talk to nearby inmate.
- reach routine zone.
- late/on-time branches.
- unlock Journal.

## Mission 2 — Find Your Feet

Flexible order:

- shower.
- train.
- speak to several NPCs.
- meet officer.
- accept job.

## Mission 3 — Who You Sit With

- competing social invitations.
- group choice.
- witness event.
- relationship consequences.
- side mission unlock differences.

## Deliverable

First 20–30 minutes contain real game progression rather than a tech demo.

---

# PHASE 19 — BOARD-GAME MINIGAME

## Preferred first implementation: Checkers

Requirements:

- 8×8 board.
- selectable pieces.
- legal move generation.
- captures.
- kinging.
- turns.
- win/loss.
- simple AI.
- touchscreen selection.
- opponent skill settings.
- result event.

## Integration

- Malcolm first opponent.
- Oz harder opponent.
- win/loss memory.
- Game Skill XP.
- Mission 5 condition.

## Optional expansion

- chess.
- fictional card game / poker-like / blackjack-like minigame using only fictional in-game points and no real-money gambling.

## Deliverable

A real game can be played from start to finish and the result affects NPC/story state.

---

# PHASE 20 — COMBAT

## Player

- combat mode.
- light attack.
- heavy attack.
- guard/dodge.
- stamina.
- target selection.

## NPC

- attack windows.
- defense chance.
- stamina.
- aggression profile.

## Stats

- Strength affects impact.
- Fighting affects timing/effectiveness.
- Stamina/Fitness affects endurance/recovery.

## Feedback

- animation.
- impact sound hook.
- subtle camera shake.
- hit reaction.
- knockdown/end.

No gore or detailed injury visuals.

## Consequences

- relationship memory.
- Respect/Fear.
- Heat if witnessed.
- temporary Sore/energy condition.
- officer intervention state if observed.

## Deliverable

Cal or another suitable NPC can produce a meaningful early fight whose difficulty changes after training.

---

# PHASE 21 — SIDE MISSIONS AND FREE-ROAM EVENTS

Implement at least five fully if time:

Recommended priority:

1. Best of Three.
2. Tobes’ Million-Pound Idea.
3. Show Up.
4. One More Rep.
5. Marty Needs a Hand.
6. TV War.
7. Keep It Down.
8. Gym Etiquette.

Create data for all 20 listed side missions even if not all fully authored.

Add free-roam event spawner with:

- cooldown.
- condition rules.
- location/activity slots.
- maximum simultaneous events.

## Deliverable

The wing remains interesting between main missions.

---

# PHASE 22 — MAIN CAMPAIGN SCAFFOLD 4–30

Create mission definitions for all remaining campaign missions.

Implement the most possible in order, prioritizing:

- Mission 4 work conflict.
- Mission 5 checkers relationship.
- Mission 6 power structure.
- Mission 9 Red Hot.
- Mission 10 Challenge.
- Mission 12 Get in the Room.

Later acts can initially use data and simple interactions rather than cinematics.

Important:

Do not block on final cutscene art. Use dialogue, world flags and scene transitions.

## Deliverable

The codebase clearly supports the entire campaign and more than the first three missions where time permits.

---

# PHASE 23 — EMERGENT INFLUENCE / “BOSS OF THE WING”

## Compute influence state from

- global Influence.
- Respect.
- key NPC relationships.
- favors.
- story flags.

## Reactions

- NPCs approach player.
- requests become more important.
- disputes can be mediated.
- weak rivals can back down.
- officers may show more attention.

Do not use one “Boss = true” button.

## Deliverable

Player can feel their social position changing organically.

---

# PHASE 24 — SAVE / LOAD

## Save fields

- version.
- selected character.
- day/time.
- safe player location.
- stats/XP.
- conditions.
- inventory/money.
- job.
- mission states.
- NPC relationships/memory summaries.
- global reputation.
- staff standing/Heat.
- world flags.
- minigame/story results.

## Reliability

- temporary file.
- atomic/replace approach.
- backup.
- fallback safe spawn.
- migration hook.

## Autosave

- mission completion.
- end/start day.
- job completion.
- major social decision.

## Deliverable

Closing and reopening game preserves meaningful progress.

---

# PHASE 25 — SETTINGS AND ACCESSIBILITY

Implement:

- camera sensitivity.
- invert Y.
- master volume.
- SFX/music volume.
- vibration toggle if used.
- reduced camera shake.
- quality preset.
- FPS target if practical.

Ensure:

- readable mobile text.
- safe area.
- large touch targets.
- status not communicated by color alone.

---

# PHASE 26 — AUDIO/ATMOSPHERE

Create audio architecture and, where legally redistributable assets are available, add:

- footsteps.
- metal doors.
- wing ambience.
- TV murmur.
- PA ambience.
- yard wind/rain.
- UI.
- training/combat impacts.

No copyrighted commercial-game/movie audio.

If audio assets unavailable, wire categories and placeholders rather than blocking.

---

# PHASE 27 — VISUAL POLISH

After gameplay works:

- improve materials.
- add wear decals/texture detail where cheap.
- institutional signage.
- props.
- optimize cell repetition.
- better lighting.
- simple character visual differentiation.
- mild state visuals for tired/dirty.

Do not sacrifice mobile stability for visual ambition.

---

# PHASE 28 — PERFORMANCE PASS

Profile/inspect:

- AI update rates.
- NavMesh requests.
- active NPC count.
- draw calls/material reuse.
- shadows.
- overdraw.
- allocations.
- save size.

Add:

- NPC simulation LOD.
- quality-based background NPC count.
- pooled UI/effects where beneficial.
- LODGroups if real models exist.
- render-scale/quality settings.

Target stable 30 FPS over visual extravagance.

---

# PHASE 29 — TESTS AND VALIDATION

## EditMode tests

- stats.
- character modifiers.
- clock rollover.
- routine boundaries.
- inventory.
- Heat add/decay.
- relationship memory.
- mission objective progression.
- save round-trip.

## PlayMode smoke tests

- bootstrap.
- player spawn.
- required managers.
- interactable detection.

## Validation tool

Check:

- duplicate IDs.
- missing NPC data.
- missing mission references.
- missing schedule destinations.
- missing build scenes.

---

# PHASE 30 — DEVELOPER MENU

Development-only features:

- advance 10 minutes.
- advance 1 hour.
- set routine.
- set Heat.
- set stats.
- set Hygiene.
- add money.
- teleport to areas.
- show NPC state.
- start/complete early missions.
- force save/load.

This is essential for fast phone testing.

---

# PHASE 31 — ANDROID CI / GITHUB DELIVERY

Create GitHub Actions workflow:

- manual dispatch.
- checkout.
- Unity build via compatible free CI method/GameCI.
- Library cache.
- Android APK.
- artifact upload.

Optional:

- tag-based GitHub Release.

Document owner-only Unity Personal activation steps/secrets.

Never commit private license material.

If feasible use side-by-side application IDs:

- repo 1: `com.simplebusiness.onthewing.one`
- repo 2: `com.simplebusiness.onthewing.two`

This makes direct phone comparison much easier.

---

# PHASE 32 — FINAL QA PASS

Before declaring completion:

- no known compile errors.
- title/menu works.
- character select works.
- player spawns.
- touch controls work.
- camera works in cell.
- stairs usable.
- NPCs move.
- routine advances.
- shower affects Hygiene.
- training affects stats.
- job affects pay/reliability.
- relationship memory persists.
- Heat changes world behavior.
- minigame works.
- combat works non-graphically.
- Missions 1–3 complete.
- save/load works.
- Android workflow present.
- `BUILD_STATUS.md` honest and current.

---

# STRETCH PHASE A — MORE ENTERABLE WORLD

If fundamentals are done, expand:

- more cells.
- library/education.
- kitchen/servery.
- workshop.
- healthcare.
- visits.
- second wing corridor/transition.

Each new area must have at least one routine/gameplay purpose.

---

# STRETCH PHASE B — MORE JOBS

Add functional:

- laundry.
- kitchen.
- library.

Each should expose new NPC routes rather than just reskin cleaning tasks.

---

# STRETCH PHASE C — MORE MINIGAMES

After checkers:

- chess.
- darts or another skill game.
- fictional card-table game with in-game points only.

Integrate results into NPC memory.

---

# STRETCH PHASE D — DEEPER NPC MEMORY

Add:

- group memory summaries.
- relationship propagation.
- contextual bark selection.
- long-term memory callbacks.

Mission 29 should use old memories for personalized farewell dialogue.

---

# STRETCH PHASE E — ENDING SYSTEM

Implement ending calculator using:

- Heat.
- Staff Trust.
- Reliability.
- Respect/Trust/Fear/Influence.
- ally states.
- betrayal flags.
- main branch commitment.
- side mission callbacks.

Use safe cinematic/textual resolution for fictional escape outcome rather than real operational simulation.

---

# STRETCH PHASE F — ART REPLACEMENT PIPELINE

Prepare prototype for later asset upgrades:

- player model slot.
- NPC model variants.
- animator controller.
- modular environment prefab replacement.
- texture sets.
- audio event assignment.

Keep gameplay components independent from placeholder mesh hierarchy.

---

# IMPLEMENTATION PRINCIPLES

1. **Playable before pretty.**
2. **Systems connect to each other.** Hygiene that does nothing socially is incomplete.
3. **NPCs are people, not vending machines for quests.**
4. **Routine is visible in behavior, not just a clock label.**
5. **Stats alter outcomes.**
6. **Failure creates consequences, not constant reloads.**
7. **Player freedom is preserved.** Main missions do not disable free-roam without a story reason.
8. **Mobile first.** Touch controls and performance are not deferred until the end.
9. **No paid dependency is allowed to become essential.**
10. **Abstract dangerous/illegal fiction.** Never turn game mechanics into real-world instructions.
11. **Non-graphic violence.** Intensity through animation, audio, stamina and consequences rather than gore.
12. **Do not stop because final assets are missing.** Use placeholders.
13. **Do not stop because later missions lack cinematics.** Use dialogue/world-state versions.
14. **Do not ask the owner questions already answered by the repository.**
15. **At the end, state exactly what works.**

---

# MINIMUM STRONG RESULT

A model should consider its run successful only if the owner can plausibly reach this experience:

- Launch game.
- Choose one of six characters.
- Spawn in a cell.
- Walk out onto a three-level UK-style wing.
- Look across at opposite cells.
- Move freely with mobile joystick and swipe camera.
- See NPCs moving through a routine.
- Talk to them.
- Notice relationships changing.
- Shower because Hygiene has consequences.
- Train because Strength/Fitness matter.
- Attend or skip work and see consequences.
- Build prisoner Respect/Trust/Fear/Influence.
- Build staff Trust/Suspicion/Heat/Reliability separately.
- Become red hot and see cautious prisoners distance themselves.
- Play a real checkers game with an NPC.
- Experience a non-graphic fight whose difficulty is affected by training.
- Complete the first three main missions.
- Save, close and continue.
- Download future APK builds through GitHub Actions once any owner-only Unity activation is configured.

After achieving this, the model should keep building further down the plan rather than stopping immediately.
