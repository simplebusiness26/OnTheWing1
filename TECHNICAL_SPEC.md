# TECHNICAL SPEC — ON THE WING

This document defines the preferred implementation architecture for the first playable version of **On The Wing**. It is intentionally practical: the coding model should use it to build a working game, not to create an over-engineered framework.

---

# 1. Engine and project settings

## Engine

- Unity 6 LTS family.
- C#.
- Universal Render Pipeline.
- Android first.
- Landscape orientation.

Pin the exact Unity version in `ProjectSettings/ProjectVersion.txt` after project creation.

Avoid experimental packages unless required.

## Recommended packages

Use official Unity packages where practical:

- Input System.
- AI Navigation / NavMesh package appropriate to pinned Unity version.
- TextMeshPro if not already integrated.
- Cinemachine only if it materially helps and is stable for the pinned version; a custom lightweight camera is also acceptable.
- Unity Test Framework.

Avoid a large dependency stack. Do not use paid frameworks.

---

# 2. Quality target

Primary device class: mid-range Android handset.

Initial target:

- 30 FPS stable on Balanced.
- 60 FPS optional on capable devices.
- Landscape.
- Conservative memory usage.
- Short boot time.
- No network requirement.

Suggested build profiles:

### Performance

- 30 or 60 target selectable.
- Low shadow distance.
- Minimal post processing.
- Lower render scale.
- Reduced active background NPC visual count if necessary.

### Balanced

- 30 FPS target.
- Moderate shadows.
- Basic post effects.
- Standard render scale.

### High

- Optional stronger shadows/post effects.
- Higher render scale.

Do not tie game simulation rate to frame rate.

---

# 3. Scene architecture

Recommended scenes:

1. `Bootstrap`
2. `MainMenu`
3. `CharacterSelect`
4. `Wing_A`
5. Optional additive spaces later: `Yard_A`, `Gym_A`, etc.

For the first build, keeping wing + attached small areas in a single scene is acceptable if simpler and faster.

## Bootstrap responsibilities

Create persistent services/state:

- Save service.
- Game state/session.
- Settings.
- Audio manager.
- Scene transition service.
- Optional event bus.

Do not place every gameplay system in DontDestroyOnLoad. World-specific managers belong in the world scene.

---

# 4. Suggested folder layout

```text
Assets/_OnTheWing/
  Art/
    Characters/
    Environment/
    Props/
    UI/
  Audio/
  Materials/
  Prefabs/
    Characters/
    Environment/
    Interaction/
    Systems/
    UI/
  Scenes/
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
    Editor/
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
```

Namespaces should be consistent, e.g. `OnTheWing.Player`, `OnTheWing.AI`, etc.

---

# 5. Data versus runtime state

Use ScriptableObjects for immutable definitions and serializable plain classes/structs for mutable save/runtime state.

Example:

`PlayableCharacterDefinition : ScriptableObject`

contains:

- ID
- display name
- bio
- base stats
- growth modifiers
- passive trait IDs
- starting reputation
- starting staff standing
- prefab/avatar reference

Runtime:

`PlayerProgressState`

contains:

- selected character ID
- current stats/XP
- conditions
- reputation
- inventory
- job state
- mission state

Never mutate the ScriptableObject definition as player save state.

---

# 6. IDs

Every persistent content object should have a stable string ID.

Examples:

- `char_fighter_mack`
- `npc_malcolm_reed`
- `mission_main_001`
- `item_book_basic`
- `job_wing_orderly`
- `zone_yard_main`

IDs must not depend on Unity instance IDs.

Provide duplicate-ID validation in editor or runtime development build.

---

# 7. Input architecture

Define a unified input abstraction so touch and editor controls drive the same player logic.

Suggested interface/state:

```csharp
public interface IPlayerInputSource
{
    Vector2 Move { get; }
    Vector2 LookDelta { get; }
    bool SprintHeld { get; }
    bool InteractPressed { get; }
    bool LightAttackPressed { get; }
    bool HeavyAttackPressed { get; }
    bool DefendHeld { get; }
    bool PausePressed { get; }
}
```

Touch UI updates a mobile input state.

Keyboard/mouse adapter updates the same logical input state in editor/desktop testing.

Do not have player movement directly query random UI components.

---

# 8. Floating joystick

Requirements:

- Spawn/anchor control center near touch start inside left movement region if using floating mode.
- Clamp knob displacement to radius.
- Return normalized vector with analog magnitude.
- Release returns zero.
- Multi-touch safe.
- Does not steal right-side camera touch.
- Expose dead zone.
- Support fixed fallback layout if floating implementation proves unstable.

Use Unity EventSystem pointer interfaces or Input System EnhancedTouch, but keep implementation simple and reliable.

---

# 9. Swipe camera

Implement a right-side look zone.

Requirements:

- Track one pointer/finger assigned to camera look.
- Ignore touches that began on action buttons/menu.
- Convert pixel delta using DPI-independent sensitivity scaling where practical.
- Apply horizontal yaw and clamped pitch.
- Smooth target follow.
- Spherecast/raycast from target to desired camera point to avoid wall clipping.
- Damp camera correction to avoid jitter in cells.

Settings:

- X sensitivity.
- Y sensitivity.
- Invert Y.
- Reduced camera shake.

---

# 10. Player motor

Use either CharacterController or a carefully controlled Rigidbody. CharacterController is preferable for predictable mobile third-person locomotion unless animation/root-motion demands otherwise.

Responsibilities:

- Camera-relative movement.
- Walk/jog/sprint speeds.
- Acceleration/deceleration.
- Gravity.
- Ground detection.
- Slope handling.
- Step handling.
- Rotation smoothing.
- Movement suppression during interactions/combat states.

State model:

- Locomotion.
- Interaction.
- Dialogue.
- Minigame.
- Combat.
- Disabled/cutscene.

Avoid boolean soup. Use a simple high-level player mode/state.

---

# 11. Animation architecture

Prototype can begin with placeholders, but code should support Animator-driven movement.

Animator parameters could include:

- `Speed`
- `MoveX`
- `MoveY`
- `Grounded`
- `Combat`
- `AttackType`
- `Hit`
- `KnockedDown`
- `InteractionType`

Do not require root motion for basic navigation.

If final humanoid animations are unavailable, use simple placeholder animation clips or animator states without blocking the rest of gameplay.

---

# 12. Interaction system

Create a generic interaction interface.

```csharp
public interface IInteractable
{
    string InteractionId { get; }
    InteractionPrompt GetPrompt(PlayerContext player);
    bool CanInteract(PlayerContext player);
    void Interact(PlayerContext player);
}
```

Use an `InteractionScanner` around the player:

- Sphere/trigger candidates.
- Score by distance + facing.
- Select best candidate.
- Update context button label/icon.

Interaction implementations:

- NPC talk.
- Door.
- Shower.
- Training equipment.
- Job task.
- Bed/sleep.
- Board-game table.
- Sit point.
- Generic inspectable.

Do not hardcode interaction behavior in the UI button.

---

# 13. Doors and routine locks

Door component supports:

- Open/closed visual state.
- Locked/unlocked interaction state.
- Routine-driven state.
- Mission override.
- NPC use.

For cell doors, world routine can broadcast unlock/lock events.

Avoid complex physical hinged doors if they cause NavMesh/collision instability. Animated transform doors are acceptable.

---

# 14. Stats architecture

Define enum or IDs for stats.

```csharp
public enum StatType
{
    Strength,
    Fitness,
    Stamina,
    Fighting,
    Intelligence,
    Awareness,
    Nerve,
    Persuasion,
    Intimidation,
    SocialSkill,
    WorkSkill,
    StreetSmarts,
    PrisonKnowledge,
    GameSkill
}
```

Each stat tracks:

- Level/value.
- XP/progress.
- Growth modifier from chosen character.

Provide:

- `GetValue`
- `AddXp`
- threshold progression
- clamp/cap
- event on change

Use data/config for XP curves.

---

# 15. Conditions

`PlayerConditionState`:

- health
- stamina
- energy
- hygiene
- stress
- meal/hunger state

Conditions update at a low frequency, not every frame where unnecessary.

Example:

- Game clock minute event updates slow needs.
- Combat changes health/stamina immediately.
- Training changes energy/hygiene immediately.

Expose derived tags such as:

- `LowHygiene`
- `Exhausted`
- `HighStress`

Dialogue/AI can query tags.

---

# 16. Game clock

Use a deterministic simulated clock independent of `Time.time` representation.

Possible state:

```csharp
[Serializable]
public struct SimTime
{
    public int Day;
    public int MinuteOfDay;
}
```

`GameClock`:

- real seconds per game minute configurable.
- pause modes.
- advance by minutes.
- event on minute/hour/day.
- save/load.

Avoid floating-point drift by using accumulated time and integer simulated minutes.

---

# 17. Routine system

`RoutineDefinition : ScriptableObject`

Contains blocks:

- ID.
- display name.
- start minute.
- end minute.
- player expected-zone/rule tags.
- door/world state instructions.

`RoutineManager` determines active block and emits change events.

NPC schedules reference routine blocks or explicit time windows.

Player compliance system subscribes and checks whether player is in an expected state/zone by a grace deadline.

Do not punish instantly at the exact routine boundary; use grace periods.

---

# 18. Zone system

Place trigger volumes with stable IDs.

Examples:

- `zone_player_cell`
- `zone_wing_ground`
- `zone_showers`
- `zone_yard`
- `zone_job_cleaning`
- `zone_games_table`

Track player current/entered zones.

Mission, routine and AI systems query zone IDs instead of world coordinates.

---

# 19. NPC definition

`NpcDefinition : ScriptableObject`:

- stable ID.
- name/nickname.
- archetype/personality tags.
- home cell zone/anchor ID.
- base relationship.
- group tags.
- influence.
- officer-attention level.
- reliability.
- loyalty tendency hidden.
- heat sensitivity.
- combat profile.
- board-game skill.
- schedule definition.
- dialogue IDs.

Runtime `NpcState`:

- relationship metrics.
- current routine state.
- memories.
- active mission flags.
- current mood.
- injuries/temporary non-graphic condition.

---

# 20. NPC scheduling

`NpcScheduleDefinition` uses entries like:

- routine/time range.
- destination anchor/zone.
- activity type.
- priority.
- allowed interruption.

NPC brain:

1. Determine active schedule entry.
2. Acquire destination.
3. Move using NavMeshAgent.
4. Enter activity state.
5. React to player/mission events.
6. Resume schedule after interruption.

Use staggered evaluation, e.g. each NPC thinks on a 0.2–1.0 second interval offset rather than every Update.

Pathfinding requests should also be staggered around routine changes.

---

# 21. NPC LOD / simulation budget

Important NPCs near player:

- full NavMesh movement.
- animation.
- reactions.
- interaction.

Important NPCs far/off-screen:

- simplified schedule state.
- teleport/snap to destination only when safe/not observed if required by performance.

Background NPCs:

- simpler schedule.
- no deep memory.
- lower tick frequency.

Do not instantiate 100 fully simulated characters for the first wing.

---

# 22. Relationship model

Use multiple values, for example:

```csharp
[Serializable]
public class RelationshipState
{
    public float Affinity;
    public float Trust;
    public float Fear;
    public int FavorsOwedToPlayer;
    public int FavorsPlayerOwes;
}
```

Do not confuse NPC-specific Trust with global prisoner Trust reputation.

Provide mutation methods that always create optional memory/event records so story logic remains auditable.

---

# 23. Memory system

Structured `MemoryEvent`:

- event ID/GUID.
- type.
- source ID.
- target ID.
- day/minute.
- magnitude.
- tags.
- decay policy.

Example enum:

- HelpedMe
- RefusedMe
- KeptPromise
- BrokePromise
- BeatMeAtGame
- LostToMeAtGame
- FoughtMe
- HelpedAlly
- HarmedAlly
- AssociatedWithRival
- ReliableWorker
- MissedWork
- PublicSupport
- PublicHumiliation

Provide query helpers:

- `HasMemory(type)`
- `GetRecentMemories(tag)`
- `GetWeightedMemoryImpact()`

Cap retained low-value memories or decay them to keep save size manageable.

---

# 24. Global reputation

`PrisonerReputationState`:

- Respect.
- Trust.
- Fear.
- Influence.

`StaffStandingState`:

- Trust.
- Suspicion.
- Heat.
- Reliability.

Clamp values, ideally 0–100 or -100–100 consistently.

Emit events on threshold crossing:

- `HeatWarm`
- `HeatHot`
- `HeatRedHot`
- `InfluenceKnown`
- etc.

Dialogue/mission availability can subscribe/query.

---

# 25. Heat system

Central `HeatService` should accept reasoned events rather than arbitrary direct writes.

```csharp
public void AddHeat(float amount, HeatReason reason, string witnessId = null)
```

Heat decay:

- periodic.
- slower at high levels after major incidents if desired.
- boosted modestly by reliable routine.

Association effect:

- only meaningful repeated proximity/social events with high-attention NPCs.
- do not add Heat every frame merely standing near someone.

Abstract officer events should use probabilities and story rules, never realistic search-evasion logic.

---

# 26. Witness system

For important public actions:

- determine nearby NPC/officer witnesses using radius + optional line of sight.
- create memory/reputation/Heat outcomes.

Examples:

- public argument.
- fight.
- helping someone.
- social grouping event.

Keep it cheap: event-driven checks, not continuous surveillance calculations every frame.

---

# 27. Dialogue data model

A simple node graph represented as ScriptableObjects, JSON-like serializable assets, or custom serializable classes is acceptable.

Node types:

- Line.
- Choice.
- Condition branch.
- Action.
- End.

Condition examples:

- stat >= value.
- relationship >= value.
- memory exists.
- Heat <= value.
- mission state.
- inventory item.
- current routine.
- selected playable character.

Action examples:

- add relationship.
- add memory.
- start mission.
- complete objective.
- add/remove item.
- change reputation.
- set world flag.

Author early dialogue in data, not C# `if` chains.

---

# 28. Mission architecture

`MissionDefinition`:

- ID.
- title.
- act.
- journal description.
- prerequisite condition list.
- objective definitions.
- rewards/consequences.
- optional failure/lock rules.

`MissionRuntimeState`:

- status: Locked/Available/Active/Completed/Failed/Paused.
- active objective indexes.
- objective progress values.
- timestamps.
- branch choices.

Mission objective interface/base type:

- initialize.
- subscribe to relevant events.
- evaluate.
- serialize progress.
- cleanup subscriptions.

Do not poll all objectives every frame.

Event examples:

- NpcTalkedTo.
- ZoneEntered.
- RoutineAttended.
- JobShiftCompleted.
- StatChanged.
- MinigameCompleted.
- RelationshipChanged.
- ItemAdded.
- DialogueChoiceMade.
- HeatThresholdChanged.

---

# 29. World flags

Create a central save-backed flag store for story state.

Examples:

- `met_malcolm`
- `joined_evening_game`
- `job_orderly_active`
- `chose_reece_over_vince`

Support bool/int/string where needed but prefer strongly typed APIs around important systems.

Avoid using PlayerPrefs for major game state.

---

# 30. Job system

`JobDefinition`:

- ID.
- display name.
- schedule window.
- pay.
- required conditions.
- task list generator.
- reliability gain/loss.

`JobState`:

- assigned job ID.
- attendance streak.
- missed shifts.
- completed shifts.
- performance.

First shift tasks can be interactable checkpoints:

- wipe/clean marked area via short progress interaction.
- collect ordinary cleaning supply.
- return item.

Keep tasks intentionally generic and harmless.

---

# 31. Training system

`TrainingStation` definition:

- stat XP targets.
- energy cost.
- hygiene cost.
- cooldown/diminishing return tag.
- animation/interaction duration.

Training should emit an event so missions can track it.

Use daily diminishing returns table rather than permanent hard cooldown.

---

# 32. Inventory

`ItemDefinition : ScriptableObject`:

- ID.
- display name.
- icon.
- category.
- max stack.
- value if applicable.
- tags.

`InventoryState` stores item ID + quantity, not direct Unity object references.

Provide:

- add.
- remove.
- contains.
- count.
- capacity if used.

Keep first inventory small and clear.

---

# 33. Economy

Store legitimate money as integer minor units or simple integer credits/pounds-like fictional balance.

Never use floating point for currency.

Favor/debt values are separate from money.

No real-money purchases.

---

# 34. Minigame framework

Create `IMinigame` or a common result model:

```csharp
public struct MinigameResult
{
    public string GameId;
    public string OpponentId;
    public bool Won;
    public int Score;
}
```

At minimum implement checkers if possible.

Checkers requirements:

- board state.
- legal move generation.
- captures.
- turn flow.
- win/lose detection.
- simple AI.
- touch piece selection.
- exit/forfeit behavior.
- result event to relationships/missions.

If chess is implemented later, share UI shell/result plumbing but not rules logic.

Card-style games must use fictional in-game points only, no real-money gambling systems.

---

# 35. Combat architecture

Components:

- `Combatant` for stats/health/stamina.
- `PlayerCombatController`.
- `NpcCombatController`.
- hitbox/hurtbox or short-range overlap query.
- target selector.
- combat state machine.

Attack definition:

- windup.
- active window.
- recovery.
- stamina cost.
- base impact.
- animation ID.

Damage/impact formula should combine base + Strength/Fighting and mitigation without becoming overly complex.

Do not include weapon crafting or dangerous-realism systems in the prototype.

Fight end:

- defeat/knockdown.
- relationship/reputation event.
- Heat/witness event if public.
- temporary `Sore`/recovery condition.

---

# 36. Officer intervention

For first version:

- If a fight occurs within an officer-observed zone or witness check succeeds, broadcast intervention after short delay.
- Combatants disengage through state change.
- Player receives Heat/reputation consequence.
- Optional transition to consequence screen/state.

Do not build tactical evasion of staff/security.

---

# 37. Save architecture

Use JSON or another simple local serialization format suitable for Unity and Android.

Recommended:

`SaveGameData` contains plain serializable state only.

Fields:

- save version.
- selected character ID.
- day/time.
- safe player spawn ID and transform.
- player progress.
- conditions.
- inventory/economy.
- reputation.
- jobs.
- missions.
- NPC runtime states.
- world flags.
- settings references where appropriate.

Write path:

`Application.persistentDataPath`.

Reliability:

1. Serialize to temp file.
2. Validate serialization succeeded.
3. Replace primary.
4. Keep one backup if easy.

Provide migration hook:

```csharp
ISaveMigration
```

Even if only version 1 exists now.

Autosave moments:

- new day.
- mission completion.
- job completion.
- major relationship choice.
- pause/menu manual save.

Avoid autosaving during unstable animation/transitions.

---

# 38. Spawn/checkpoint system

Save named safe spawn anchors rather than relying only on raw world position.

Examples:

- PlayerCellBed.
- WingGroundSafe.
- YardEntry.

On load:

- try saved transform if valid.
- fallback to named safe spawn.

This prevents reloading inside moving doors/invalid areas.

---

# 39. UI architecture

Use Canvas + safe area fitter.

Screens/panels:

- Main Menu.
- Character Select.
- Gameplay HUD.
- Pause.
- Journal.
- Skills/Character.
- Relationships.
- Inventory.
- Settings.
- Dialogue.
- Minigame.

Use one UI root/presenter structure, not dozens of independent canvases if avoidable.

Text must remain readable on phone.

Use icons plus labels for critical interactions.

---

# 40. Safe area

Implement safe area support based on `Screen.safeArea`.

Ensure:

- joystick not under rounded corner/cutout.
- action buttons not against edge.
- top HUD avoids camera notch.

Update when orientation/resolution changes even though landscape is fixed.

---

# 41. Settings

Persistent settings:

- quality preset.
- target FPS.
- camera sensitivity.
- invert Y.
- master volume.
- SFX volume.
- music volume.
- vibration.
- reduced camera shake.

PlayerPrefs is acceptable for non-critical local settings; do not use it for main game state.

---

# 42. Audio manager

Simple categorized mixer:

- Master.
- SFX.
- Ambience.
- Music.
- Dialogue if later used.

Use AudioMixer if available.

Pool repeated one-shot sources where practical.

Ambient zones can crossfade wing/yard ambience.

---

# 43. Wing procedural/editor builder

Because the repository starts without final 3D art, an editor script that generates the first wing from modular primitives can massively accelerate the build.

Suggested `WingGreyboxBuilder` editor tool:

Parameters:

- cell count per side per level.
- number of levels.
- cell width/depth/height.
- atrium width/length.
- landing width.
- stair locations.

Generate:

- floor.
- side walls.
- cell shells.
- cell doors.
- landings.
- railings.
- stair blocks/ramps.
- safety-net visual plane/mesh.
- officer desk placeholder.
- shower room.
- yard connection.

The result should be editable after generation.

This is preferable to manually writing a huge Unity scene YAML file if editor automation can build it safely.

---

# 44. Runtime fallback world builder

If the coding environment cannot run Unity Editor to generate scene assets, it is acceptable to temporarily create a runtime `PrototypeWorldBuilder` that instantiates primitives from code for the first playable build.

However:

- keep it modular.
- do not permanently couple game rules to generated primitive names.
- later allow replacement with authored prefabs.

This fallback is far better than leaving the world absent.

---

# 45. Materials

Create a small mobile-friendly material palette:

- painted wall.
- concrete floor.
- dark metal railing.
- cell door metal.
- institutional accent paint.
- yard concrete.
- safety net.

Use tiling and material reuse.

Final texture work can come later.

---

# 46. Lighting

Prototype:

- one main directional/environment light if needed.
- repeated low-cost fluorescent fixtures represented visually.
- limited actual real-time lights.

Later:

- baked lightmaps.
- mixed lights only where necessary.
- reflection probes.

Do not use dozens of shadow-casting point lights down the wing.

---

# 47. NavMesh

Bake/wire navigation for:

- landings.
- ground floor.
- stairs.
- enterable cells.
- yard.

Agent settings must handle narrow landings without constant blockage.

If stair geometry causes navigation failure, use navigation links or simplified collision/navigation ramps while preserving visual stairs.

Test multiple NPCs passing each other.

---

# 48. Crowd behavior

Basic local avoidance is enough.

Optional:

- simple destination offsets around social points.
- occupancy slots for tables/gym areas.
- queue slots for job/meal areas.

Use reservable `ActivitySlot` components so 10 NPCs do not stand in exactly the same point.

---

# 49. Activity points

Generic `ActivityPoint`:

- ID.
- activity type.
- transform.
- capacity/slots.
- routine availability.

NPC scheduler requests slots.

Types:

- Socialize.
- Exercise.
- Sit.
- GameTable.
- Work.
- Meal.
- CellIdle.

---

# 50. Event architecture

A lightweight typed event system is useful because many systems react to the same action.

Examples:

- `GameMinuteAdvanced`
- `RoutineChanged`
- `PlayerEnteredZone`
- `NpcConversationCompleted`
- `RelationshipChanged`
- `MemoryAdded`
- `HeatChanged`
- `JobShiftCompleted`
- `TrainingCompleted`
- `MinigameCompleted`
- `CombatEnded`
- `MissionObjectiveCompleted`

Use C# events/interfaces or a simple event bus. Do not import a huge reactive framework.

---

# 51. Dependency management

Acceptable approaches:

- serialized references + bootstrap wiring.
- small service registry.
- constructor injection for pure C# classes.

Avoid:

- pervasive static singletons.
- `GameObject.Find` every frame.
- expensive scene searches inside gameplay loops.

---

# 52. Debug tooling

Create a developer overlay enabled by development flag/key/button combination.

Functions:

- advance 10 minutes / 1 hour.
- set routine.
- teleport to known zones.
- add money.
- set Hygiene.
- add XP/stat.
- set Heat.
- show NPC state labels.
- force NPC schedule reevaluation.
- start/complete early missions.
- save/load test.

Mobile-accessible debug trigger can be hidden behind e.g. five taps on a version label in development build.

Do not expose debug panel in final production release unless disabled by build define.

---

# 53. Logging

Use clear categories/prefixes.

Log:

- save failures.
- missing IDs.
- missing mission references.
- invalid schedule destinations.
- NavMesh failures in development.

Do not spam logs every frame.

---

# 54. Validation tools

Add editor validation where possible:

- duplicate IDs.
- missing NPC home cell.
- mission references missing NPC/item.
- schedule destination missing.
- playable character missing stats.
- build scene missing.

A menu item such as `Tools > On The Wing > Validate Project` is useful.

---

# 55. Automated tests

## EditMode

Prioritize pure logic tests:

### Stats

- XP increases expected stat.
- growth modifier applies.
- cap works.

### Time

- clock rolls into next day.
- routine lookup at boundaries.

### Heat

- addition clamps.
- decay works.
- thresholds fire once appropriately.

### Relationships

- memory affects score.
- decay/expiry works.

### Inventory

- add/remove/query.
- stack cap if used.

### Missions

- objective event advances.
- prerequisites block correctly.

### Save

- serialize/deserialize round-trip.
- unknown/missing optional fields use safe defaults.

## PlayMode

If stable:

- bootstrap loads.
- Wing_A player spawn exists.
- interaction scanner detects known dummy interactable.

---

# 56. Android player settings

Configure:

- landscape orientation.
- IL2CPP if build pipeline supports it reliably; Mono acceptable for faster dev builds if needed.
- ARM64 at minimum for modern Android release; development APK can include required architecture based on CI practicality.
- package identifier such as `com.simplebusiness.onthewing` (or repository-specific suffix only if needed during model comparison).
- version code/version string.
- internet permission should not be required by game code.

Do not enable unnecessary Android permissions.

---

# 57. GitHub Actions

Target `.github/workflows/android-build.yml`.

Requirements:

- `workflow_dispatch`.
- checkout.
- Unity build action compatible with pinned version.
- cache.
- Android target.
- upload artifact.
- clear failures.

Likely Unity Personal CI secrets may include variables defined by the chosen GameCI flow. Document exact names in `BUILD_STATUS.md`/`CI_SETUP.md` based on the actual workflow used.

Never commit Unity license files containing private data.

If license automation cannot be completed autonomously, the workflow should still be structurally ready.

---

# 58. Model comparison fairness

Do not modify the design documents merely to reduce scope unless correcting an actual contradiction or documenting an implementation decision.

The comparison should remain fair:

- same game target.
- same systems.
- same acceptance rubric.

Repository-specific package identifier differences are acceptable only where Android install side-by-side testing benefits from it.

If using different app IDs:

- OnTheWing1: `com.simplebusiness.onthewing.one`
- OnTheWing2: `com.simplebusiness.onthewing.two`

This would allow both APKs to be installed simultaneously for comparison. Prefer doing this if simple.

The visible game title should remain `On The Wing` with a small `Build 1` or `Build 2` label only if the repository identity can be detected/configured without changing gameplay.

---

# 59. Performance budgets

First-pass practical budgets, not strict certification:

- Keep active important NPCs around player manageable (~15).
- Background active visual NPCs scale by quality preset.
- Avoid hundreds of rigidbodies.
- Avoid per-frame allocations in AI loops.
- Avoid LINQ in high-frequency Update paths.
- Pool repeated temporary effects/UI notifications where useful.
- Use shared materials.
- Use texture compression appropriate for Android.
- Keep shadow casters limited.

Profile before adding visual complexity.

---

# 60. Memory/save budget

NPC memory can grow forever if unmanaged.

Policy:

- Permanent important memories remain.
- Low-value routine memories decay/remove after a configured number of days.
- Aggregate repeated events where possible, e.g. `MissedWorkCount` plus a recent memory.

Save should remain small enough for instant local writes.

---

# 61. Content authoring strategy

Use data files/assets so later missions/NPCs can be added without rewriting managers.

For a coding model unable to create `.asset` ScriptableObjects through Unity Editor, acceptable alternatives:

1. Runtime content bootstrap creates definitions in code temporarily.
2. JSON under `StreamingAssets`/Resources for definitions.
3. Editor generation scripts create assets when Unity imports the project.

Best outcome: generation script + clean data architecture.

Do not let inability to click Unity Inspector block the entire implementation.

---

# 62. Placeholder character strategy

If no licensed humanoid models are present:

- use Capsule/primitive prototype characters with distinct colors/scale and floating name labels in development only.
- structure prefab code so model/Animator can be swapped later.
- do not wait for art.

If free assets are added, include license information and verify redistribution is permitted.

---

# 63. Placeholder audio strategy

If there is no legally redistributable audio:

- create AudioClip fields and mixer routing.
- leave clips empty.
- use UI visual feedback.
- document required audio assets.

Do not copy copyrighted game/movie audio.

---

# 64. Runtime-generated prototype content

A powerful implementation strategy for autonomous coding is a `PrototypeBootstrapper` that, when no authored scene objects are found, can generate:

- wing geometry.
- player.
- camera.
- UI.
- NPCs.
- activity points.
- shower.
- training station.
- game table.
- job points.

This can make the project immediately playable even before editor-authored prefabs exist.

The generated systems should still use the same production-facing components and IDs so the world can later transition to authored scenes without game-logic rewrite.

---

# 65. First vertical-slice technical definition of done

The build is not considered a successful vertical slice unless:

- Unity compiles without errors.
- Android scene list is valid.
- Main menu opens.
- New game leads to character select.
- Character selection affects stats.
- Wing loads.
- Touch controls exist.
- Player can freely move on the wing.
- Camera swipe/orbit works.
- At least 8 NPCs visibly follow routines.
- Current routine/time changes.
- Player can talk to an NPC.
- Relationship changes persist.
- Hygiene changes and shower restores it.
- Training grants stat XP.
- Work shift grants pay/trust and missing it causes consequence.
- Heat can rise and visibly affect at least one NPC behavior.
- One board minigame works.
- One non-graphic fight works.
- Three early missions can complete.
- Save/load works.
- Android CI is configured, with any owner-only secret requirement clearly documented.

Everything above this bar should be expanded rather than rebuilding the foundation.
