# MASTER BUILD PROMPT — ON THE WING

> **This is the primary instruction for the coding model. Read this entire repository specification before changing code. Then build the game. Do not answer with a plan and stop.**

You are acting as the lead engineer, technical game designer, gameplay programmer, tools programmer, UI programmer, build engineer and QA owner for **On The Wing**, a mobile-first third-person open-world prison-life drama game set in a fictional UK prison.

The repository may initially contain only planning documents. Your task is to turn it into the **largest coherent, playable, testable Unity Android build you can complete in one autonomous run**. The owner is deliberately comparing two coding models using identical repositories, so the quality of what actually runs matters more than how persuasive your explanation sounds.

---

## 0. THE NON-NEGOTIABLE EXECUTION RULE

**BUILD, DO NOT MERELY PLAN.**

You must:

1. Read `README.md`, this file, `GAME_DESIGN_SPEC.md`, `TECHNICAL_SPEC.md`, `NPCS_AND_MISSIONS.md`, and `ACCEPTANCE_AND_SCORECARD.md` before major implementation decisions.
2. Inspect the repository before creating files so you do not overwrite useful work.
3. Create a real Unity project if one does not exist.
4. Implement actual C# systems, scenes/prefabs/data structures, UI, controls, game-state logic and Android build configuration.
5. Use coherent placeholder geometry/materials/audio hooks when final assets are unavailable. A greybox that plays is better than a beautiful design document that does not.
6. Keep going through the prioritized backlog until blocked by time, tool limits or an external credential that the repository owner must supply.
7. When blocked on an asset, create a placeholder and continue.
8. When blocked on a secret/license, configure everything possible around the secret, document the exact secret names/steps, and continue building the rest of the game.
9. Do not repeatedly ask the owner design questions that are already answered in these files.
10. Do not leave large systems as empty interfaces, pseudocode or TODO-only shells if a simplified working implementation is possible.
11. Prefer a playable simplified implementation over a theoretically perfect architecture that never reaches the device.
12. At the end, provide a concise `BUILD_STATUS.md` recording what is truly implemented, what is partially implemented, what is placeholder, what remains, and exactly how to obtain/install the APK.

The ideal result is a repository where the owner can trigger a GitHub Actions build, download an APK on an Android phone, install it, select a character, spawn in a cell, walk out onto a UK-style wing, interact with scheduled NPCs, live through a functioning prison day, train/shower/work/socialize, see stats/reputation/heat change, play at least one minigame, engage in a non-graphic fight, and progress through early missions.

---

# 1. PRODUCT NORTH STAR

The player should feel:

**“I live on this wing. The prison carries on whether or not I follow the story, people remember what I do, and ordinary choices affect what becomes possible later.”**

This is not a corridor mission game with a prison skin. It is a **small open world + life simulation + RPG progression + relationship simulation + story campaign**.

The player must be able to ignore the main campaign for several in-game days and still have meaningful things to do.

Core fantasy:

- Arrive as a nobody.
- Learn how the prison works.
- Build a daily routine.
- Improve physical, mental and social abilities.
- Work legitimate jobs and manage money.
- Build friendships and rivalries.
- Decide who to associate with.
- Earn prisoner respect while managing staff attention.
- Discover story opportunities through people and routines rather than only map markers.
- Make choices that alter relationships and later missions.
- Gradually become influential if the player earns it.
- Follow a long fictional story whose central late-game thread can involve an abstract escape plan, transfer, release path or other endings.

Dangerous/illegal real-world conduct must remain fictional and mechanically abstract. Do not encode realistic instructions for making illicit substances, evading real prison security, concealing contraband, defeating searches, escaping real facilities, or harming people. Use generic story tokens, probability/heat systems and invented prison procedures instead of real operational detail.

Violence can feel tense and consequential but must remain **non-graphic**. No gore, dismemberment, exposed wounds or detailed injury depiction. Use impact animation, sound, camera response, stamina, temporary bruised status icons, knockdowns and social consequences.

---

# 2. TARGET PLATFORM AND TECH DIRECTION

Primary target: **Android mobile**.

Engine: **Unity 6 LTS family**, C#, Universal Render Pipeline (URP). Pin the actual editor version in `ProjectSettings/ProjectVersion.txt` once the project is generated. Avoid beta/alpha editor versions.

The game must be designed around a mid-range Android device rather than a gaming PC. The owner tests on a phone and may not have a local development machine.

Target characteristics:

- Landscape orientation.
- 30 FPS minimum target on mid-range hardware.
- Optional 60 FPS mode if affordable.
- Resolution scaling / quality presets.
- Touch-first controls.
- UI safe areas.
- Reasonable APK size during prototyping.
- No paid runtime service required for core gameplay.
- No mandatory account/login.
- Offline single-player.
- All essential state saved locally.

Use URP mobile-friendly settings. Avoid heavyweight post-processing, excessive real-time lights, huge textures, dense skinned-mesh crowds, expensive reflection systems or physics-heavy clutter.

---

# 3. FIRST PLAYABLE EXPERIENCE

The first 10–15 minutes of a successful build should roughly work like this:

1. Launch game.
2. See title screen: `ON THE WING`.
3. Start new game.
4. Choose from six playable inmate archetypes.
5. See short character summary: background, starting traits, strengths, weaknesses.
6. Confirm selection.
7. Load into the player’s cell during morning unlock.
8. Basic tutorial prompts introduce left joystick and camera swipe.
9. Cell door is opened by prison routine/script.
10. Player walks onto an upper landing.
11. Player can look across the central atrium at opposite cells and down into the wing.
12. NPCs begin their own morning schedules.
13. A nearby NPC naturally introduces interaction.
14. Player is free to explore allowed wing space.
15. HUD indicates current time/routine and a minimal context objective.
16. Player can shower, train, talk to NPCs, attend a job/routine activity, sit/rest and inspect stats.
17. Skipping the required activity produces a believable staff consequence.
18. Player can discover the first story mission and at least one side opportunity.
19. Save persists state across restart.

If you can achieve more, continue through the later systems in this document.

---

# 4. WORLD LAYOUT — BUILD THIS SHAPE

The first prison wing is the most important environment.

Build a fictional UK-style rectangular cellular wing with:

- Long rectangular central atrium.
- Cells positioned along the two **long parallel sides**.
- No normal rows of cells on the short ends.
- Three visible residential levels/landings for the first slice.
- Narrow upper-level walkways outside cells.
- Railings along upper landings overlooking the atrium.
- Open vertical void through the center.
- Safety net / mesh structure spanning part of the void below upper landings.
- Opposite cells visible across the atrium.
- Multiple stair flights connecting levels.
- Central ground-floor communal space.
- Officer station / desk zone with good sightlines.
- Wing entrance/security gate represented fictionally.
- Showers connected to the wing.
- Small association/common area.
- Phone/communication prop area as environmental storytelling only.
- Exercise yard accessible during scheduled periods.
- Gym/training corner or room.
- Work room/workshop placeholder area.
- Dining/servery placeholder if feasible.

Visual identity:

- Institutional, worn, gritty, believable.
- Slightly stylized realism for performance.
- Fluorescent industrial lighting.
- Painted concrete/brick/metal surfaces.
- Scratches, chipped paint, noticeboards, doors, railings, institutional signage.
- Strong ambient audio zones: distant voices, door sounds, footsteps, PA ambience, televisions, yard wind/rain.

Do not spend the whole run hand-modeling. Create modular geometry and reusable prefabs. If quality assets are not available, build a clean modular greybox first, then improve materials and props as time allows.

Initial visible capacity: roughly 40–60 cell doors across the environment is acceptable, while only a subset needs fully detailed interiors. At minimum provide:

- Player cell.
- 4–8 enterable NPC cells.
- Others can use closed/low-detail interiors until expanded.

---

# 5. MOBILE CONTROLS

Implement touch controls that feel free and uncluttered.

## Movement

- Left-side floating virtual joystick.
- Analog magnitude controls walk/run blend.
- A larger outer displacement can produce jog/run if comfortable.
- Separate sprint button is optional; if added, keep layout minimal.
- Character movement camera-relative.
- Character rotates smoothly toward movement direction.
- Gravity, stairs/slopes, collision and grounding must be reliable.

## Camera

- Drag/swipe on most of the right half of the screen to orbit.
- Horizontal and vertical camera orbit.
- Vertical clamp.
- Smooth follow.
- Collision avoidance so the camera does not sit inside walls.
- Sensitivity option.
- Optional recenter button.
- Do not require a visible right joystick.

## Interaction

Context-sensitive primary button near the lower-right area. Label/icon changes to current action:

- Talk
- Open/Close
- Use
- Shower
- Train
- Work
- Sit
- Sleep
- Play
- Inspect
- Pick up (for harmless generic game objects)

Secondary buttons should appear only when relevant.

## Combat

Compact, mobile-friendly, non-graphic system:

- Light attack.
- Heavy attack or contextual follow-up.
- Guard/dodge.
- Stamina cost.
- Lock/soft-target nearest hostile NPC within sensible cone.
- Hit reactions and knockdown.
- Do not create gore mechanics.
- AI should disengage based on scripted outcomes, health/stamina, officers, or mission context.

Touch controls must remain usable at 320 CSS-equivalent widths and common Android aspect ratios. Implement safe-area support.

Also implement editor keyboard/mouse controls for development:

- WASD movement.
- Mouse look.
- E interact.
- Shift sprint.
- Basic combat keys.

---

# 6. PLAYER CHARACTER SELECTION

Implement six selectable starting characters using data-driven definitions. Final names can be changed later, but give them memorable working names and distinct silhouettes/colors if only placeholders exist.

Each character needs:

- Name.
- Age band (adult only).
- Fictional conviction/background summary.
- Sentence/background flavor.
- Body/build descriptor.
- Starting attributes.
- Skill-growth modifiers.
- Starting prisoner reputation.
- Starting staff trust/suspicion.
- One passive advantage.
- One meaningful disadvantage.
- Optional unique side-story flag.

Archetypes:

1. **The Fighter** — high Strength/Fighting, lower staff trust and slower academic/social gains.
2. **The Hustler** — high Persuasion/Street Smarts/Trading, physically weaker.
3. **The Veteran** — high Prison Knowledge and starting connections, higher baseline officer suspicion.
4. **The First-Timer** — weaker overall starting stats, higher staff trust, improved broad learning rate.
5. **The Athlete** — high Fitness/Stamina, decent physical base, low influence.
6. **The Thinker** — high Intelligence/Awareness, efficient work/problem-solving, physically weaker.

Character selection must change actual gameplay values, not only text.

---

# 7. PLAYER STATS AND NEEDS

Use a data-driven stats component. Avoid a survival-game nuisance where bars drain every few minutes. Needs should influence planning but not dominate the game.

## Core abilities

Physical:

- Strength
- Fitness
- Stamina
- Fighting

Mental:

- Intelligence
- Awareness
- Nerve

Social:

- Persuasion
- Intimidation
- Social Skill

Prison-life skills:

- Work Skill
- Street Smarts
- Prison Knowledge
- Game Skill (or separate chess/checkers skill if warranted)

## Dynamic conditions

- Energy
- Hygiene
- Hunger/meal state (lightweight, not punishing)
- Stress
- Health
- Current stamina

## Progression philosophy

Stats improve primarily through relevant activity:

- Strength via strength training.
- Fitness/Stamina via exercise.
- Fighting via practice/controlled combat experiences/missions.
- Intelligence via education, reading, work/minigame tasks.
- Persuasion via dialogue/social outcomes.
- Prison Knowledge via observation, conversations and time.
- Work Skill via jobs.

Use diminishing returns and sensible caps. Do not allow a single repeated action to max a stat in minutes.

Provide immediate feedback after meaningful growth without constantly interrupting play.

---

# 8. DAILY ROUTINE AND TIME

This is a foundational system.

Target one in-game day around **30–45 real minutes** at normal speed, tunable from data.

Create a `GameClock` / `RoutineManager` with scheduled blocks such as:

- Morning unlock/count.
- Breakfast/association.
- Work/education block.
- Lunch/count.
- Afternoon work/exercise.
- Evening association.
- Evening meal.
- Lock-up.
- Night.

Exact fictional timings can be tuned for gameplay and must not claim to model a real prison’s security procedures.

Required behavior:

- HUD shows time and current routine in a compact manner.
- Areas/NPC schedules react to routine.
- NPCs move to scheduled destinations.
- Player may comply or ignore routine when physically possible.
- Ignoring required activities can generate staff warnings, trust loss, sanctions or heat.
- Sleeping advances time appropriately during lock-up.
- Mission system can subscribe to time/routine events.
- NPC schedules should not all change at the exact same frame; stagger path requests.

Allow accelerated time only when appropriate (sleep, waiting, certain work/training interactions).

---

# 9. HYGIENE / SHOWER SYSTEM

Hygiene must matter socially.

Implement:

- Hygiene slowly drops over time and faster after training/fights.
- Shower interaction restores hygiene through a short non-explicit interaction/transition.
- Low hygiene causes contextual NPC comments and small relationship/social penalties.
- Very low hygiene can cause some NPCs to refuse close social interactions until improved.
- Avoid humiliating presentation; keep it as a believable simulation mechanic.
- Character appearance can use mild dirty/sweaty material state if practical.

Hygiene must feed the relationship/dialogue condition system.

---

# 10. TRAINING AND PHYSICAL PROGRESSION

Provide at least:

- Pull-up station.
- Push-up/bodyweight interaction area.
- Cardio station or yard running/training interaction.
- Optional weights if assets permit.

Training loop:

1. Approach equipment.
2. Context action.
3. Short timing/hold/repetition interaction or animation.
4. Consume energy/stamina.
5. Gain small skill XP.
6. Hygiene decreases slightly.
7. Training has cooldown/diminishing return within the same day.

Do not make progress depend on hundreds of repetitive taps.

Physical stats must affect combat calculations and some dialogue/intimidation gates.

---

# 11. JOBS

Implement at least one functioning prison job and scaffold others.

First job suggestion: **wing orderly / cleaning detail** because it can be implemented in the existing wing without a giant extra environment.

Working loop:

- Player is assigned/eligible for job.
- Job has scheduled attendance window.
- Arriving on time increases staff trust/reliability.
- Simple task objectives appear (clean marked harmless locations, move ordinary supplies, complete a timed checklist).
- Successful shift yields legitimate in-game pay and Work Skill XP.
- Missing/abandoning work reduces reliability/trust and can eventually cause job loss.
- Job performance can alter officer dialogue.

Scaffold future jobs:

- Kitchen.
- Workshop.
- Laundry.
- Library/education helper.
- Servery.

Jobs must be data-driven and mission systems should be able to test whether a player holds/attended a job.

---

# 12. ECONOMY AND INVENTORY

Implement a lightweight inventory/economy.

Currencies/resources:

- Legitimate prison account/pay balance.
- Optional abstract favor/debt values between NPCs.

Inventory item categories:

- Approved consumables.
- Cosmetic/clothing variants if used.
- Books/game items.
- Generic story items.
- **Abstract contraband tokens** only where story requires them.

Do not create realistic recipes, sourcing instructions, concealment techniques or security-evasion mechanics. A mission can say “obtain the generic package” and represent success with a story token and risk roll rather than teaching real methods.

Inventory requirements:

- Stackable/non-stackable support.
- Item definitions as ScriptableObjects or equivalent data.
- Add/remove/query API.
- Simple UI.
- Save/load.
- Mission condition integration.

---

# 13. PRISONER REPUTATION + STAFF REPUTATION

These are separate and often conflicting.

## Prisoner-facing dimensions

- Respect
- Trust
- Fear
- Influence

## Staff-facing dimensions

- Staff Trust
- Suspicion
- Heat
- Compliance/Reliability

Do not collapse these into one karma score.

Examples:

- Winning a fight can increase Fear and some Respect but raise Heat.
- Helping an NPC can increase Trust without increasing Fear.
- Consistently attending work can increase Staff Trust.
- Spending time around a heavily watched NPC can gradually increase Suspicion.
- Being overly cooperative with officers may lower trust with certain prisoners.
- High Heat can cause other prisoners to refuse risky story interactions because the player is “red hot.”

Add thresholds that change:

- Dialogue variants.
- NPC willingness to talk.
- Mission availability.
- Prices/favors.
- Officer responses.
- Search/check frequency as an abstract event system.
- Sanction likelihood.

Show player enough feedback to understand consequences without displaying every hidden variable.

---

# 14. OFFICER INTELLIGENCE / HEAT NETWORK

Create a fictional systemic model, not a realistic security simulation.

Concept:

- Officers have individual suspicion toward the player.
- Significant witnessed events generate abstract `IntelEvent`s.
- Intel events can contribute to global Heat over time.
- Repeated association with certain high-attention NPCs can contribute a small amount of Suspicion.
- Heat naturally decays when the player avoids trouble and maintains routine.
- Staff Trust can moderate some outcomes but should not erase serious events.

Possible consequences:

- Verbal warning.
- Increased observation state.
- Temporary loss of an optional privilege.
- Job review/change.
- Temporary mission lock.
- Fictional cell check event resolved abstractly.
- Segregation story state for severe repeated incidents.

Do not model ways to defeat or bypass real searches/security. The system should be probabilities, story decisions and consequences.

---

# 15. ASSOCIATION / FRIEND GROUP CONSEQUENCES

Each important NPC should expose metadata such as:

- Personal relationship with player.
- Influence.
- Officer-attention level.
- Social group/faction tags.
- Reliability.
- Hidden loyalty/betrayal tendencies.
- Current mood/stress.

Track player association history:

- Meaningful conversations.
- Time spent together during association periods.
- Help/refusal events.
- Conflicts.
- Publicly witnessed support/disputes.

Effects:

- Becoming close to one person can alter another person’s opinion.
- Some prisoners avoid someone who attracts too much officer attention.
- Some staff become more suspicious based on association patterns.
- Friend selection can later alter mission solutions.

Keep network evaluation computationally cheap. Important NPCs get deep tracking; background population can use simplified relationships.

---

# 16. NPC AI — MAKE THE WING FEEL ALIVE

At minimum implement a schedule-driven state machine for important NPCs:

States could include:

- InCell
- LeavingCell
- WalkingToRoutine
- Working
- Eating
- Exercising
- Socializing
- PlayingGame
- Waiting
- TalkingToPlayer
- Conflict
- ReturningToCell
- LockedUp

Use NavMesh or Unity AI Navigation appropriate for the chosen Unity version.

NPC requirements:

- Individual home cell/destination assignments.
- Daily schedule.
- Basic avoidance/separation.
- Context barks.
- Relationship-aware reactions.
- Player interaction interruption and return-to-schedule logic.
- Time-window availability for certain quests.
- Lightweight off-screen simulation where possible.

Do not run expensive decision trees every frame for every NPC. Use staggered ticks/events.

Background NPCs can use simpler schedules, pooled barks and less frequent thinking.

---

# 17. NPC MEMORY

This is one of the game’s signature mechanics.

Create a lightweight event-memory system for important characters.

Memory examples:

- Player helped me.
- Player refused me.
- Player embarrassed me publicly.
- Player kept a promise.
- Player broke a promise.
- Player fought me.
- Player fought my ally.
- Player spends time with my rival.
- Player beat me at a game.
- Player repeatedly misses work (officer memory).
- Player has been reliable for several days.

Each memory needs:

- Event type.
- Source/target IDs.
- Timestamp/day.
- Magnitude.
- Optional expiry/decay.
- Tags for dialogue/mission queries.

Do not store raw natural-language history for everything. Use structured events plus selective summary values.

Relationship score should be derived from base disposition + memories + group effects + current context.

---

# 18. DIALOGUE

Build a data-driven dialogue system supporting:

- NPC barks.
- Short conversations.
- Choice branches.
- Stat checks.
- Relationship checks.
- Reputation checks.
- Time/routine checks.
- Mission state checks.
- Memory flags.
- Item/job checks.
- Consequences/actions.

UI should be touch friendly.

Dialogue should not freeze the entire world unless required. For important conversations, nearby simulation can slow/pause safely, but avoid weird NPC collisions.

Provide reusable nodes/actions rather than hardcoding every conversation into MonoBehaviours.

---

# 19. MINIGAMES

At least one minigame must be genuinely playable. Prefer implementing **checkers or simplified chess** first because it strongly supports the social-gate idea.

Desired long-term set:

- Chess.
- Checkers.
- Fictional card-table game or simplified poker/blackjack-style minigames using only fictional in-game points, with no real-money gambling, purchases or gambling monetization.
- Optional darts/table game depending on art scope.

Minigame integration:

- NPC can require a match before deeper conversation.
- Wins/losses modify relationship/memory.
- Some NPCs have skill levels.
- Player Game Skill can influence AI difficulty only subtly; do not auto-win.
- Mission conditions can query match result.

If full chess AI is too expensive for first pass, implement legal board play plus a simple AI/search depth adequate for mobile, or implement checkers first and scaffold chess cleanly.

---

# 20. COMBAT

Combat is part of prison drama, not the whole game.

Implement:

- Unarmed third-person combat.
- Health and stamina.
- Light/heavy attacks.
- Block/dodge.
- Short hit stun.
- Knockdown/end state.
- AI attack windows.
- Cooldown to avoid attack spam.
- Stat influence: Strength, Fighting, Fitness/Stamina.
- NPC difficulty profiles.
- Fight consequences: relationship, Respect/Fear, Heat, temporary condition penalties.
- Officer intervention trigger when appropriate.

Use non-graphic feedback:

- Impact animation.
- Sound.
- Camera shake kept subtle.
- Vignette/flash if needed.
- Temporary “bruised/sore” status icon, not detailed wounds.

Some fights should be unwinnable or extremely difficult early because the player has not trained enough. Communicate risk without arbitrary invisible cheating.

---

# 21. MISSION SYSTEM

Build a generic mission framework that can support the 30-mission campaign and side missions described in `NPCS_AND_MISSIONS.md`.

A mission should contain:

- ID.
- Title.
- Description/journal text.
- Act.
- Prerequisites.
- Start conditions.
- Ordered/unordered objectives.
- Optional objectives.
- Fail/temporary lock conditions.
- Rewards.
- Relationship consequences.
- Stat/reputation consequences.
- Dialogue hooks.
- Time windows.
- Required NPCs.
- World state changes.

Objective types:

- Talk to NPC.
- Go to zone.
- Attend routine.
- Complete job shift.
- Train to threshold.
- Win minigame.
- Improve relationship.
- Possess generic story item.
- Make dialogue choice.
- Wait until routine/time.
- Resolve conflict.
- Maintain low/high Heat threshold for a period.
- Choose ally.

Avoid mission-marker overload. Support:

- Discovered opportunities.
- Journal tracking.
- Optional world indicator only when the player reasonably knows where to go.
- NPC approach/bark triggers.

Implement the framework first, then fully author as many early missions as time allows. The entire 30-mission outline should exist as data/scaffolding even if later acts are not fully cinematic yet.

---

# 22. SIDE MISSIONS SHOULD FEED MAIN MISSIONS

Important design rule:

A side story is not merely “+100 coins.” It can provide:

- A trustworthy ally.
- A new relationship.
- A skill boost opportunity.
- Access to a location during a routine.
- Information/story clue.
- Lowered Heat through improved routine.
- A rival.
- A future favor/debt.
- A character who may support or betray the player later.

Some main mission branches should become available or easier based on completed side stories. Do not hard-lock the entire campaign behind obscure optional content without alternative routes.

---

# 23. “BOSS OF THE WING” MUST EMERGE, NOT BE HANDED OUT

Do not create a single mission titled “Become Boss” that instantly changes a bool.

Influence should emerge from:

- Respect.
- Trust.
- Fear.
- Influence/favors.
- Relationships with key characters.
- Physical reputation.
- Reliability/leadership decisions.

At high influence:

- NPCs approach player more often.
- Dialogue acknowledges status.
- Some conflicts can be resolved socially.
- Side-mission request quality changes.
- Rivals react.
- Officers may pay more attention.

Different builds can become influential differently. A physically weak but socially connected character can still become important.

---

# 24. STORY ENDINGS

Do not require the full final campaign to be implemented before the vertical slice is playable, but design save/world flags for multiple endings.

Potential fictional endings:

1. **Escape ending** — culmination of an abstract fictional storyline; do not simulate real escape methods.
2. **Release/parole-style ending** — player abandons the risky plan and progresses through legitimate story choices.
3. **Transfer ending** — choices result in a high-security or different-prison transfer, potentially setting up sequel/NG+.
4. **Influence ending** — player stays but becomes a major social power within the fictional prison system.
5. **Collapse/betrayal ending** — poor trust decisions and high Heat destroy the plan.

Earlier relationships should determine which versions are available.

---

# 25. UI / UX

Keep HUD minimal.

Persistent or near-persistent:

- Current time/routine.
- Small context objective if tracking a mission.
- Interaction button.
- Movement control.
- Camera touch area invisible.
- Health/stamina only when relevant.

Menus:

- Pause.
- Journal/Missions.
- Character/Skills.
- Relationships.
- Inventory.
- Routine/Calendar.
- Settings.

Relationships screen should show only information the player has reasonably learned, not hidden loyalty/betrayal values.

Character screen should clearly show:

- Abilities.
- XP/progress.
- Dynamic conditions.
- Prisoner reputation.
- Staff standing/Heat.

Use readable type and large touch targets. No tiny desktop UI.

---

# 26. SAVE / LOAD

Implement robust local save system.

Save:

- Selected character.
- Player transform/location safely.
- Game day/time/routine.
- Stats/needs.
- Money/inventory.
- Jobs.
- Mission states.
- NPC relationship/memory summaries.
- Reputation/heat.
- World flags.
- Minigame outcomes relevant to story.
- Accessibility/settings.

Requirements:

- Autosave at meaningful safe points.
- Manual save slots if practical.
- Version field/migration strategy.
- Atomic write or backup approach to reduce corruption risk.
- Never save player embedded inside a door/wall after scene transitions.

---

# 27. AUDIO

Even placeholder audio must be structured by category.

Need hooks for:

- Footsteps by material if feasible.
- Metal doors.
- Cell door ambience.
- Distant wing chatter.
- TV/radio murmur.
- PA ambience.
- Yard wind/rain.
- Training impacts.
- UI feedback.
- Combat impacts (non-graphic).

Use free/placeholder audio only if licensing allows repository redistribution. Otherwise use silent hooks and document asset needs rather than copying unlicensed media.

---

# 28. ART / LIGHTING / PERFORMANCE

Aim for gritty realism within mobile constraints.

Recommended approach:

- URP.
- Mostly baked lighting/static lightmaps once environment stabilizes.
- Limited dynamic lights.
- Reflection probes used sparingly.
- Occlusion culling where useful.
- LODGroups for environment/characters.
- GPU instancing for repeated props/materials.
- Modular cell pieces.
- Texture atlases when useful.
- 1K textures default for environment prototypes; higher only for hero assets where justified.
- Conservative shadow distance.
- Mobile-friendly SSAO/post FX only on higher preset.
- Avoid transparent overdraw-heavy effects.

Quality presets:

- Performance.
- Balanced.
- High.

Performance mode should prioritize stable framerate over pretty shadows.

---

# 29. ACCESSIBILITY / SETTINGS

Include:

- Camera sensitivity.
- Y-axis invert toggle.
- Master/music/SFX volume.
- Subtitle toggle/size if dialogue audio appears.
- Vibration toggle if used.
- Quality preset.
- Target FPS option if feasible.
- Button scale option or at least large defaults.
- Reduced camera shake.
- Color should never be the only way to communicate status.

---

# 30. PROJECT ARCHITECTURE

Follow `TECHNICAL_SPEC.md`, but the expected broad separation is:

- Core/bootstrap.
- Input.
- Player.
- Camera.
- Interaction.
- Stats.
- Time/routine.
- NPC AI.
- Relationships/memory.
- Reputation/heat.
- Dialogue.
- Missions.
- Jobs.
- Training.
- Minigames.
- Combat.
- Inventory/economy.
- Save.
- UI.
- Audio.
- World/environment.
- Editor/tools.
- Tests.

Prefer ScriptableObjects/data assets for definitions and runtime state objects for mutable state. Avoid `FindObjectOfType` everywhere. Use clear dependency wiring/bootstrap/service registration appropriate for project scale without adding a heavyweight paid framework.

Use assemblies if they genuinely improve compile/test boundaries, but do not spend the entire run building framework infrastructure.

---

# 31. REPOSITORY STRUCTURE

A sensible target:

```text
/
  Assets/
    _OnTheWing/
      Art/
      Audio/
      Materials/
      Prefabs/
        Characters/
        Environment/
        Interactables/
        UI/
      Scenes/
        Bootstrap.unity
        MainMenu.unity
        CharacterSelect.unity
        Wing_A.unity
      Scripts/
        Core/
        Input/
        Player/
        Camera/
        Interaction/
        Stats/
        Time/
        AI/
        Relationships/
        Reputation/
        Dialogue/
        Missions/
        Jobs/
        Training/
        Minigames/
        Combat/
        Inventory/
        Save/
        UI/
        Audio/
        World/
      Data/
        Characters/
        NPCs/
        Items/
        Missions/
        Dialogue/
        Jobs/
        Routine/
      Tests/
        EditMode/
        PlayMode/
  Packages/
  ProjectSettings/
  .github/workflows/
  README.md
  MASTER_BUILD_PROMPT.md
  GAME_DESIGN_SPEC.md
  TECHNICAL_SPEC.md
  NPCS_AND_MISSIONS.md
  ACCEPTANCE_AND_SCORECARD.md
  BUILD_STATUS.md
```

Adapt if Unity’s generated structure requires changes.

---

# 32. TESTING

Add automated tests for pure logic wherever practical:

- Stat XP/level calculations.
- Relationship memory weighting/decay.
- Heat changes/decay.
- Routine time transitions.
- Mission objective completion.
- Inventory add/remove.
- Save serialization round-trip.
- Character archetype modifiers.

Add play-mode smoke tests if reliable:

- Bootstrap scene loads.
- Player prefab spawns.
- Wing scene contains required manager references.

Also create an in-game developer/debug menu disabled or hidden in release builds that can:

- Advance time.
- Set Heat.
- Add money.
- Set stats.
- Teleport to named test zones.
- Start early mission.
- Toggle NPC debug labels.

This dramatically improves future iteration.

---

# 33. GITHUB ACTIONS / APK DELIVERY

The owner is phone-first, so repository automation matters.

Create an Android build workflow using a reputable Unity CI approach such as GameCI where compatible with the pinned Unity version.

Workflow goals:

- Manual `workflow_dispatch` trigger.
- Build on relevant branch pushes if build minutes are acceptable.
- Cache Unity Library appropriately.
- Produce `.apk` artifact.
- Clear artifact name such as `OnTheWing-Android`.
- Optionally create a GitHub Release on version tags.
- Do not commit secrets.

Unity Personal activation may require repository secrets/license material that only the owner can supply. Configure the workflow and document exact required secret names and how to obtain them at a high level. Never invent credentials.

If CI cannot be fully executed because license secrets are absent, this is not permission to stop game development. Continue implementing the project and mark CI as configured-but-awaiting-license in `BUILD_STATUS.md`.

---

# 34. FREE-COST RULE

Core prototype must not require paid assets, subscriptions or cloud services.

Allowed:

- Unity Personal under its applicable eligibility terms.
- GitHub repository/workflows subject to account limits.
- Free/open licensed assets if redistribution license is verified.
- Original procedural/primitive placeholder geometry.

Avoid:

- Paid Asset Store dependencies.
- Paid backend services.
- Mandatory AI APIs.
- Paid analytics.
- DRM/account systems.

Keep third-party dependencies minimal and document licenses.

---

# 35. IMPLEMENTATION PRIORITY — DO NOT STOP AT PHASE 1

Work in this order, but continue as far as possible:

## P0 — Project boots

- Unity project.
- URP.
- scenes.
- bootstrap.
- menu.
- Android settings.

## P1 — Player can walk the wing

- UK-style wing greybox.
- player controller.
- mobile joystick.
- swipe camera.
- interaction system.
- player cell.

## P2 — Prison day exists

- clock.
- routine blocks.
- unlock/lock state.
- NPC schedule system.
- 8–15 important NPC placeholders.
- officer placeholders.

## P3 — Life simulation works

- stats.
- hygiene/showers.
- training.
- job attendance.
- money.
- basic inventory.

## P4 — Social simulation works

- relationships.
- memory.
- prisoner reputation.
- staff trust/suspicion/heat.
- dialogue.
- association effects.

## P5 — Game-like content

- character selection.
- first 3 main missions fully playable.
- at least 5 side opportunities if time.
- one playable minigame.
- non-graphic combat encounter.

## P6 — Breadth

- more main missions authored.
- more side missions.
- more enterable cells/areas.
- additional jobs/training.
- richer NPC schedules.
- more minigames.

## P7 — Polish

- materials/lighting.
- audio.
- animation improvements.
- UI polish.
- performance profiling.
- quality settings.

## P8 — Delivery

- save/load verification.
- tests.
- GitHub Actions Android build.
- documentation.
- `BUILD_STATUS.md`.

A model that completes P0–P5 with real working code is better than one that creates 100 files of empty abstractions. A model that can proceed through P6–P8 should do so.

---

# 36. FIRST THREE FULLY PLAYABLE MISSIONS

Use the detailed story document, but ensure these early experiences exist even if later content is scaffolded.

## Mission 1 — First Morning

Purpose: teach movement, routine and interaction naturally.

- Start in cell.
- Morning unlock.
- Learn movement/camera.
- Exit cell.
- Speak to assigned nearby NPC.
- Attend required morning point/routine.
- Player may briefly deviate; officer warning system introduced.
- End with journal unlocked.

## Mission 2 — Find Your Feet

Purpose: introduce prison-life systems.

Objectives can include a selection of:

- Shower.
- Attend/accept first job assignment.
- Use a training station.
- Speak to 2–3 distinct NPC personalities.
- Learn that people have schedules.

Do not force every tutorial into one linear corridor. Let objectives be completed in flexible order.

## Mission 3 — Who You Sit With

Purpose: introduce social consequences.

- Player receives competing invitations or requests from two incompatible NPCs/groups.
- Choice changes relationship values.
- Association is witnessed by at least one other NPC/officer.
- Small prisoner/staff reputation consequence.
- Opens two different side mission possibilities.

No dangerous real-world methods are needed.

---

# 37. CONTENT DENSITY TARGET

Even if many NPCs use placeholder models, the first wing should not feel empty.

Target initial simulation:

- 6 playable character definitions.
- 15 named important inmates.
- 5 named officers.
- 10–20 simplified background inmates if performance permits.
- 3 landings.
- 1 yard.
- 1 shower area.
- 1 training/gym area.
- 1 job activity.
- 1 minigame table.
- 3 fully playable main missions minimum.
- 30 main mission data entries/scaffold.
- 10+ side-mission data entries/scaffold.

If runtime performance is poor, reduce active visual NPC count and use schedule-based pooling/off-screen state rather than deleting character data.

---

# 38. FAILURE/CONSEQUENCE PHILOSOPHY

Avoid constant hard Game Over screens.

Most failures should become new state:

- Miss work → warning/trust loss/job risk.
- Lose fight → health/energy penalty, reputation/memory changes, story branch.
- Anger NPC → alternative route becomes necessary.
- High Heat → risky NPCs avoid player, privileges reduced.
- Fail minigame → rematch later or find another way.

Reserve hard failure for exceptional story moments.

This lets the prison simulation create stories rather than forcing reloads.

---

# 39. DESIGN QUALITY BARS

Do not ship these anti-patterns if avoidable:

- Giant HUD full of bars.
- NPCs frozen in place with quest icons forever.
- Every quest being “walk to marker and press E.”
- Stats that do not affect anything.
- Reputation as one generic number.
- Prison routine that is only text and does not move NPCs.
- Six character cards that all produce identical gameplay.
- Minigames that are fake progress bars.
- A world with 50 cell doors but no enterable/social spaces.
- Mission system hardcoded entirely in scene scripts.
- Mobile controls that require three fingers constantly.
- Photorealistic asset choices that destroy mobile framerate.
- One enormous `GameManager.cs` containing everything.

---

# 40. AUTONOMOUS DECISION POLICY

When the documents leave a gap, make a sensible decision and record it in `BUILD_STATUS.md` rather than stopping to ask.

Only require owner input for things you truly cannot do, such as:

- Missing GitHub/Unity credentials.
- License acceptance/activation requiring the owner.
- A final art direction choice that cannot be represented with placeholders and does not block coding.

For ordinary implementation choices, decide and build.

---

# 41. END-OF-RUN CHECKLIST

Before you finish your run:

1. Ensure the project structure is valid Unity.
2. Remove compile errors.
3. Ensure scenes referenced in build settings exist.
4. Check mobile UI references are wired.
5. Check player spawns and can move.
6. Check at least one NPC schedule runs.
7. Check clock/routine advances.
8. Check shower changes Hygiene.
9. Check training changes a stat/XP and costs energy.
10. Check job attendance changes pay/trust.
11. Check relationship interaction changes memory/score.
12. Check Heat can rise and decay.
13. Check at least one minigame is playable.
14. Check at least one combat encounter works non-graphically.
15. Check first three missions can progress.
16. Check save/load round-trip.
17. Check no required paid service is introduced.
18. Check Android build configuration.
19. Add/update tests.
20. Write `BUILD_STATUS.md` truthfully.
21. Commit/push the implementation if your environment permits.

---

# 42. WHAT “DONE” MEANS FOR THIS COMPARISON

The repository owner is comparing models. Your output will be judged primarily by what can be **played**, not how much prose you produce.

A strong result lets the owner:

- Download an APK from GitHub Actions once any required Unity license secret is provided.
- Install it on Android.
- Select a meaningfully different character.
- Walk freely around the wing with good touch controls.
- See NPCs living by a routine.
- Talk to people and have them remember important interactions.
- Shower because Hygiene matters.
- Train because Strength/Fitness matter.
- Work because attendance/pay/staff trust matter.
- Build prisoner reputation and staff suspicion separately.
- Become “red hot” and see NPC behavior change.
- Play a social minigame.
- Experience a fight whose result depends partly on training.
- Progress through real early missions.
- Save and continue.

Everything beyond that is additional value. Continue building until you have exhausted the productive time available.

**Do not stop after explaining how you would build On The Wing. Build On The Wing.**
