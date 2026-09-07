# GAME DESIGN SPEC — ON THE WING

## 1. High concept

**On The Wing** is a third-person, mobile-first, open-world prison-life drama game set inside a fictional British prison. The player chooses one of six adult inmates with different histories, builds and abilities, enters the same prison as a nobody, and then lives through an evolving mixture of daily routine, friendship, rivalry, work, training, games, reputation, officer attention and a long branching story.

The key difference from a normal mission game is that the prison is not simply a background. It is the game.

The player should be able to spend multiple in-game days ignoring the main campaign and still have meaningful progression through everyday life. Showers matter. Work matters. Training matters. Who the player sits with matters. Missing routine matters. Beating someone at checkers can matter. Becoming friendly with the wrong person can make officers pay more attention. Becoming too friendly with officers can make some inmates distrust the player.

The game should feel gritty, serious and dramatic, while still containing funny, strange and memorable characters and situations. It should never become relentlessly grim.

The central long-term story can involve a fictional escape plan and other possible endings, but any illegal activity is represented as abstract narrative/gameplay logic rather than realistic instruction.

---

# 2. Design pillars

## Pillar A — Live there

The wing should feel like somewhere the player inhabits rather than a level the player completes.

The game world continues to operate when the player is not pursuing a mission. NPCs have cells, destinations, schedules and relationships. Morning feels different from evening. The exercise yard exists for more than one cutscene. A job exists after its tutorial mission.

## Pillar B — Ordinary actions have consequences

Basic life systems are connected to social and story systems.

Examples:

- Poor Hygiene causes comments and social penalties.
- Training increases physical capability.
- Missing work affects Staff Trust and reliability.
- Being repeatedly seen around a highly watched prisoner raises Suspicion.
- Winning at a board game can unlock another conversation.
- Keeping a promise creates a positive memory.
- Breaking one can close a route much later.

## Pillar C — Reputation is multidimensional

There is no single “good/bad” meter.

Prisoner-facing:

- Respect
- Trust
- Fear
- Influence

Staff-facing:

- Staff Trust
- Suspicion
- Heat
- Compliance/Reliability

A player can be respected and watched, feared and disliked, trusted but physically weak, or compliant but socially isolated.

## Pillar D — People remember

Important NPCs should carry structured memories of meaningful player actions. The game should reference those memories in later dialogue and mission logic.

## Pillar E — Build your own route

Different player characters and different relationships should make the same campaign feel different. Physical power is one route, not the route.

## Pillar F — Mobile without feeling like a small game

The phone interface should disappear into the experience. One movement joystick, camera swipe, context button and temporary situational buttons are preferable to a screen full of virtual controls.

---

# 3. Camera and movement feel

The default camera is third-person behind the character, similar in broad feel to console open-world games but simplified for touch.

Desired feel:

- Player can move freely through cells, landings, stairs, communal spaces and yard.
- Camera remains close enough to feel intimate indoors.
- Camera automatically pulls slightly back in yard/large spaces if useful.
- Swipe anywhere across the right-side look zone.
- Camera collision is reliable in narrow cells.
- Character does not feel glued to cardinal directions.
- Movement speed changes smoothly based on analog joystick magnitude.
- Sprint is limited by stamina.
- Short contextual animation transitions are acceptable for sitting, showering, training and minigames.

Avoid tank controls and avoid forcing the player to stop before rotating.

---

# 4. The first prison wing

The first playable prison wing is a long rectangular atrium inspired by the visual language of traditional UK cellular wings.

## Shape

- Cells line both long sides of the rectangle.
- Opposing rows face one another across a central void.
- Three residential levels in the first build.
- Upper cells open onto narrow landings.
- Railings line the landings.
- Stairs connect levels.
- A safety net/mesh catches the eye across part of the central void.
- Ground floor contains communal movement space.
- Short ends are used for stairs, gates, offices, service spaces and circulation, rather than normal full rows of cells.

## Why this matters for gameplay

The architecture creates natural visibility and social tension.

- Someone can shout across from the opposite landing.
- An officer below can notice a gathering upstairs.
- The player can see a rival without being able to immediately reach them.
- NPC life is visible across multiple levels.
- Arguments and conversations can attract attention.
- Returning to the cell has a strong visual identity.

## First slice spaces

Required:

- Player cell.
- Several enterable inmate cells.
- Wing atrium.
- Ground-floor association zone.
- Shower room.
- Exercise yard.
- Training/gym space.
- Officer station/desk zone.
- Work/cleaning storage area.
- Board-game table.

Optional later:

- Education/library.
- Kitchen/servery.
- Workshop.
- Healthcare.
- Visits.
- Chaplaincy/multi-faith room.
- Segregation story area.
- Additional wings.

---

# 5. Art direction

Target: **gritty stylized realism**, not cartoonish and not console-photoreal at the expense of mobile performance.

Visual language:

- Cold institutional lighting.
- Muted environment surfaces.
- Worn paint and metal.
- Scuffed floors.
- Noticeboards and institutional signage.
- Rainy grey yard conditions as one weather mood.
- Warm pools of cell lighting contrasting with cold landings.
- Character faces/clothing should read clearly even with mobile-friendly detail.

The environment should look used rather than abandoned. Clutter should feel controlled and believable.

Violence should not use gore. Impact can be sold through animation, sound, particles that do not depict graphic injury, camera movement and consequences.

---

# 6. Tone

Primary tone: grounded prison drama.

Secondary tone: dark humor, personality and absurdity.

The game needs characters who are funny because of who they are, not because the game stops respecting its setting.

Examples of memorable non-story moments:

- One inmate takes checkers far too seriously.
- A harmless argument begins over who has changed the TV channel.
- Someone constantly invents terrible business ideas for after release.
- A prisoner insists he can predict everyone’s sentence outcome despite always being wrong.
- An officer has a dry sense of humor but becomes stern the moment routine is ignored.
- Two inmates maintain a long-running petty rivalry over gym equipment.

These moments keep free-roam periods enjoyable.

---

# 7. Playable characters

All playable characters are adults. Each has a distinct mechanical profile and a short fictional background. The exact conviction is narrative flavor, not a tutorial in criminal behavior.

## Character 1 — Marcus “Mack” Doyle / The Fighter

Build: broad, powerful.

Starting strengths:

- Strength: high
- Fighting: high
- Nerve: high

Weaknesses:

- Intelligence: below average
- Staff Trust: low
- Suspicion: moderately high

Passive: physical training gains a little faster.

Disadvantage: officer suspicion rises slightly faster after conflict.

Playstyle: strong early physical confidence, harder social/staff balancing.

## Character 2 — Leon Price / The Hustler

Build: lean, quick-talking.

Strengths:

- Persuasion
- Street Smarts
- Social Skill
- Trading/favor negotiation

Weaknesses:

- Strength
- Fighting

Passive: stronger outcomes from certain social checks.

Disadvantage: physical intimidation checks are harder until trained.

Playstyle: relationships and favors.

## Character 3 — Darren Cole / The Veteran

Build: average, older than most starting characters.

Strengths:

- Prison Knowledge
- Awareness
- Starting relationships

Weaknesses:

- Fitness grows more slowly.
- Baseline Suspicion higher.

Passive: learns NPC schedules/wing information faster.

Disadvantage: some officers begin wary of him.

Playstyle: information and experience.

## Character 4 — Jamie Hart / The First-Timer

Build: average.

Strengths:

- Higher Staff Trust
- Broad learning multiplier

Weaknesses:

- Low starting Prison Knowledge
- Low Respect/Fear
- Few relationships

Passive: small XP gain bonus to all skills until mid-level.

Disadvantage: certain experienced inmates initially dismiss him.

Playstyle: classic “start at zero” RPG route.

## Character 5 — Kieran Shaw / The Athlete

Build: athletic.

Strengths:

- Fitness
- Stamina
- Movement recovery

Weaknesses:

- Influence
- Prison Knowledge

Passive: lower stamina cost for sprinting/training.

Disadvantage: low initial social leverage.

Playstyle: mobility and physical development.

## Character 6 — Aaron Malik / The Thinker

Build: slight/average.

Strengths:

- Intelligence
- Awareness
- Work Skill learning
- Games/puzzles

Weaknesses:

- Strength
- Fighting

Passive: learns mental/work skills faster and can notice some optional dialogue clues.

Disadvantage: lower damage/stagger resistance until physically trained.

Playstyle: strategic and social route.

---

# 8. Skill progression

Skills range conceptually from 0–100, but the user-facing display may use levels/bands if clearer.

## Physical

### Strength

Affects:

- Physical attack power.
- Some grapple/struggle calculations if implemented.
- Intimidation checks in combination with reputation.
- Certain training/work interactions.

### Fitness

Affects:

- Recovery.
- Running efficiency.
- Training capacity.

### Stamina

Affects:

- Sprint duration.
- Combat stamina pool.
- Exercise endurance.

### Fighting

Affects:

- Attack timing.
- Defense effectiveness.
- Counter window.
- AI/player combat calculations.

## Mental

### Intelligence

Affects:

- Work/education opportunities.
- Some dialogue options.
- Puzzle/board-game support.

### Awareness

Affects:

- Noticing optional events.
- Reading mood/relationship hints.
- Some story alternatives.

### Nerve

Affects:

- Stress resistance.
- Dialogue under pressure.
- Combat composure.

## Social

### Persuasion

Affects cooperative dialogue outcomes.

### Intimidation

Affects threat-based social outcomes, influenced by Strength/Fear.

### Social Skill

Affects rapport and relationship growth.

## Prison-life

### Work Skill

Affects job efficiency, pay/reliability opportunities.

### Prison Knowledge

Affects understanding of routine, available contextual hints and some dialogue routes.

### Street Smarts

Affects social risk assessment, negotiation and abstract story interactions.

### Game Skill

Affects optional hints/AI scaling in board/card minigames without guaranteeing victory.

---

# 9. Dynamic conditions

## Hygiene

Drops gradually and faster after strenuous activity. Low Hygiene causes comments and can reduce close-social willingness. Shower restores it.

## Energy

Reduced by training, fights and long active periods. Rest/sleep recovers it.

## Hunger/meal state

Meals provide a modest energy/recovery benefit. Missing one should not make the game unplayable.

## Stress

Rises through conflict, sanctions, relationship problems and some story events. Lowered through rest, successful social moments, routine stability and certain activities.

## Health

Combat and scripted events can temporarily reduce health. Health recovery is simplified and non-graphic.

---

# 10. Daily life loop

A normal day should create choices.

Example rhythm:

### Morning

- Unlock/count.
- Shower or delay.
- Speak to neighbors.
- Breakfast/association.
- Attend work or skip it for another opportunity.

### Midday

- Work/education.
- Meal.
- Short social window.

### Afternoon

- Work continuation or yard/exercise depending on routine.
- Training.
- NPC meetings.
- Side-story opportunity.

### Evening

- Association.
- Board games.
- Social visits between accessible cells.
- Main-story conversation.
- Job/payment updates.

### Lock-up/night

- Cell interactions.
- Journal/skills review.
- Sleep.
- Some rare scripted cell conversations/events.

The player should learn where people are likely to be without the game showing omniscient GPS icons for everyone.

---

# 11. Routine compliance

The game should treat disobedience as a system, not an instant failure.

Examples:

- Late to work: warning + reliability loss.
- Repeatedly late: pay reduction/job review.
- Ignore movement instruction: Suspicion/Heat.
- Keep missing assigned activity: Staff Trust declines.

Good compliance should create benefits too:

- Officers become less confrontational.
- Certain job roles open.
- Small Heat decay bonus.
- Some legitimate ending/story routes remain stronger.

But too much staff friendliness can be interpreted negatively by certain inmates depending on personality.

---

# 12. Work

The first functional job is wing orderly/cleaning detail.

Gameplay goals:

- Give structure to the day.
- Provide legitimate money.
- Provide Work Skill growth.
- Create officer relationships.
- Force occasional conflict between “do my job” and “meet this person now.”

A shift should take only a few real minutes and contain simple tasks rather than repetitive chores.

Potential future jobs:

- Laundry.
- Kitchen.
- Workshop.
- Library.
- Servery.
- Stores.

Jobs can influence which NPCs the player sees and which side stories become available.

---

# 13. Money, items and favors

Money should matter but not become the only progression system.

Legitimate pay can buy approved quality-of-life items/cosmetics/books/game items.

Favors are more interesting than a giant currency total.

A relationship can track:

- OwesPlayer
- PlayerOwes

Use favor values as story gates and social pressure, not as a realistic criminal economy simulation.

Generic contraband can exist as abstract story tokens, with categories like `RestrictedItem`, `GenericPackage`, `ForbiddenPhoneToken` if needed for fiction. Do not encode real sourcing, concealment, smuggling or evasion methods.

---

# 14. Social reputation

## Respect

“People take me seriously.”

Sources:

- Standing up for someone.
- Winning difficult challenge/fight.
- Keeping promises.
- Performing well in visible activities.

## Trust

“People believe I will do what I say.”

Sources:

- Keeping commitments.
- Helping without betraying confidence.
- Consistency.

## Fear

“People think crossing me has consequences.”

Sources:

- Physical victories.
- Intimidation choices.
- Reputation events.

Fear is not automatically good. High Fear can make friendly relationships harder.

## Influence

“People listen or owe me.”

Sources:

- Favors.
- Relationships with key NPCs.
- Resolving disputes.
- Story decisions.

---

# 15. Staff standing

## Staff Trust

Built through reliability and routine.

## Suspicion

Built through witnessed patterns and concerning associations.

## Heat

Represents how much current attention is focused on the player.

Heat should rise faster than it decays after serious incidents but eventually fall if the player lives quietly.

## Compliance/Reliability

Tracks whether the player actually turns up and does assigned tasks.

The player can therefore have high Staff Trust but temporarily high Heat after a major incident, or low Trust with low immediate Heat.

---

# 16. “Red hot” gameplay

When Heat is high, the world changes:

- Some inmates refuse risky conversations.
- A friend may tell the player to stay away for a few days.
- Officer barks become more watchful.
- Certain story opportunities pause.
- A job can be reviewed.
- Abstract check events become more common.
- Highly cautious NPCs may lower Trust merely because association is now risky.

This should never become an impossible punishment spiral. The player can reduce Heat through time, routine, good behavior and some story resolutions.

---

# 17. Relationships and memory

Each important NPC has:

- Base disposition.
- Current relationship score.
- Trust toward player.
- Fear toward player.
- Rival/allied group tags.
- Reliability trait.
- Heat sensitivity.
- Hidden loyalty tendency.
- Structured memories.

Memory events should be referenced naturally:

“You actually turned up when you said you would.”

“You left me hanging last week.”

“You’re always around him now.”

“You beat me fair and square.”

The player should feel continuity without the dialogue system needing a giant language model at runtime.

---

# 18. Social groups

Do not make every prisoner belong to a rigid faction. Use overlapping social groups.

Examples:

- Gym crowd.
- Older long-term inmates.
- Workers.
- Gamers/card-table group.
- High-attention group.
- Quiet/low-profile group.

An NPC can belong to more than one.

Association creates indirect consequences through these relationships.

---

# 19. Board games and social gates

Board games should be part minigame, part dialogue space.

Examples:

- Malcolm will not discuss serious matters with the player until they sit through a game of checkers.
- Aaron’s Thinker archetype gets better board-reading hints but still has to win legitimately.
- Beating a proud NPC creates a small memory that can improve Respect but reduce warmth.
- Deliberately losing should not be an obvious optimal exploit.

The game can pause the local interaction while keeping the broader clock behavior controlled.

---

# 20. Combat philosophy

Fights are short, tense and socially meaningful.

The player should sometimes decide **not** to fight because:

- Opponent is much stronger.
- Officers are nearby.
- Heat is already high.
- Losing would damage a relationship or mission.
- Winning would create a rival.

Training must matter. A new weak character should not be able to beat every established fighter through button mashing.

However, combat should still reward player timing and decision-making, not only stat totals.

Suggested formula blend:

- Player input skill.
- Fighting stat.
- Strength.
- Stamina.
- Opponent profile.
- Current Energy/Stress.

No gore system.

---

# 21. Consequences instead of constant game-over

Most failures should redirect rather than end the game.

Lose a fight:

- Wake/recover at a safe point.
- Temporary stat condition.
- Relationship consequences.
- Reputation consequences.

Miss a mission window:

- Reschedule, alternate route or temporary lock.

Lose a board game:

- NPC remembers it.
- Rematch later or use another route.

Lose a job:

- New storyline around getting another job or rebuilding reliability.

This makes each save feel personal.

---

# 22. Main campaign structure

Thirty main missions in five acts.

Act I — **Fresh Reception** (1–6)

Learn the wing, meet the power structure, discover that ordinary choices are being noticed.

Act II — **Finding Your Place** (7–12)

Build capability, work, money and relationships. The player begins choosing who matters.

Act III — **Something Bigger** (13–18)

A larger fictional plan emerges. Allies, favors and story items begin linking together.

Act IV — **Pressure** (19–24)

Heat, betrayal, loyalty and staff attention put earlier choices under stress.

Act V — **The Endgame** (25–30)

The world-state created across the campaign determines available endings.

Detailed missions are in `NPCS_AND_MISSIONS.md`.

---

# 23. Main-story design rule

The player should never be collecting thirty meaningless “escape components.”

Instead, the long-term plan is assembled from **relationships, leverage, trust, access, information and abstract story tokens**.

Examples of safe abstract story progress:

- Earn the confidence of a person who knows something important.
- Secure an ally’s commitment.
- Obtain a fictional coded document token.
- Reduce Heat enough for a meeting to happen.
- Decide between two conflicting allies.
- Complete a work/relationship branch that changes access.

Never turn this into real-world prison escape instruction.

---

# 24. Side missions

Side missions should have persistent meaning.

Categories:

- Friendship stories.
- Rivalry stories.
- Work stories.
- Gym stories.
- Game-table stories.
- Officer relationship stories.
- Family/visits stories when that area exists.
- Personal character stories.
- Reputation stories.
- Humor/odd-character stories.

Rewards can include:

- Memory/relationship.
- Favor.
- Stat growth.
- Alternate mission route.
- New schedule knowledge.
- New safe social introduction.
- Reduced conflict.

Avoid endless generic fetch quests.

---

# 25. Becoming influential

There is no “Boss Level” stat.

The game internally evaluates a combination of:

- Respect.
- Influence.
- Relationships with key people.
- Favors owed.
- Fear.
- Story flags.

As the player becomes influential:

- NPCs start approaching the player.
- The player is asked to mediate disputes.
- New dialogue acknowledges status.
- Some weaker rivals back down.
- Strong rivals become more interested.
- Staff may monitor the player more closely.

The player should notice this transformation organically.

---

# 26. Endings

Five broad ending families should be supported by world flags.

## A. Escape ending

A fictional narrative outcome unlocked by strong preparation/relationships and low-enough failure conditions. The execution itself remains cinematic/abstract rather than operationally realistic.

## B. Legitimate release ending

The player gradually abandons the risky plan and pursues legitimate progression, with relationships changing accordingly.

## C. Transfer ending

The player’s actions produce a transfer to another fictional facility. This can be positive, negative or sequel-bait depending on state.

## D. Influence ending

The player remains inside but has become a major social power. It should not necessarily be framed as purely positive.

## E. Betrayal/collapse ending

High Heat, poor judgment or broken relationships cause the plan to fail and leave the player facing a new reality.

The final mission should read the whole save rather than ask one simplistic final choice.

---

# 27. Difficulty

Do not begin with a standard Easy/Medium/Hard selection.

Difficulty emerges from:

- Character selection.
- Stat build.
- Relationships.
- Decisions.
- Routine discipline.
- Combat choices.

Accessibility settings should still allow reduced combat timing difficulty or aim/camera assistance later if needed.

---

# 28. UI philosophy

The player should mostly look at the prison, not the HUD.

HUD:

- Small time/routine indicator.
- Current tracked objective.
- Context interaction button.
- Touch movement.
- Temporary health/stamina when relevant.

Do not permanently show Hygiene, Hunger, Heat, Respect, Trust, Fear, Influence, Energy and Stress as ten bars.

Use:

- subtle icons/warnings,
- menu screens,
- contextual messages,
- character animation/appearance,
- NPC dialogue.

The player must be able to understand cause/effect without drowning in meters.

---

# 29. Journal

The Journal is the central player-facing information system.

Tabs:

- Main Story.
- Side Stories.
- People.
- Routine.
- Notes/Discoveries.

A person entry grows as the player learns things. Do not show hidden betrayal/reliability stats directly.

Mission entries should say what the player knows, not omniscient developer instructions.

---

# 30. Relationship screen

Show:

- Known NPC portrait/icon.
- Name/nickname.
- General relationship description.
- Known social group.
- Notable player memories in plain-language summaries where appropriate.

Examples:

- “Seems to trust you.”
- “Still annoyed about the gym argument.”
- “Often around the games table in the evening.”

Do not expose exact hidden loyalty percentage.

---

# 31. Free-roam events

Small events make the wing feel alive.

Possible safe events:

- Two NPCs argue and the player can ignore or mediate.
- Officer requests everyone move along.
- Someone starts a board-game challenge.
- Gym equipment becomes the focus of a petty dispute.
- An inmate asks the player to pass on an ordinary message.
- Someone is celebrating a family update.
- A prisoner is angry about losing a job.
- TV choice creates humorous friction.
- An officer unexpectedly compliments reliable work.

These events should be short and reusable with condition variants.

---

# 32. Weather and atmosphere

The first build only needs a small number of moods.

Indoor:

- Morning fluorescent/cold.
- Day neutral.
- Evening warmer cell lighting.
- Night dim/locked.

Yard:

- Overcast.
- Light rain variant if performance permits.

Weather should not require a complex simulation at first.

---

# 33. Character visual feedback

Where practical:

- Low energy changes idle posture subtly.
- Training causes temporary sweat/dirty state.
- Shower clears it.
- Fight loss can use temporary mild bruised status/animation without graphic detail.
- Different archetypes can use different body proportions/placeholder mesh scale carefully.

Do not make Hygiene a body-shaming mechanic. It is a routine/social system.

---

# 34. Audio identity

The prison should be recognizable with eyes closed.

Important sound layers:

- Metal door clanks.
- Footsteps on hard landings.
- Distant voices bouncing through the atrium.
- TV murmur.
- Keys/doors from officer zone.
- Yard wind.
- Rain.
- PA ambience.

Music should be sparse. Free-roam atmosphere should mostly come from environment.

---

# 35. Replayability

Replay value comes from:

- Six starting characters.
- Different skill strengths.
- Different early staff/prisoner standing.
- Relationship branches.
- Side-mission dependencies.
- Different allies.
- Multiple endings.
- Different approaches to influence.

A second playthrough should reveal conversations and routes not seen the first time.

---

# 36. Monetization stance for prototype

No monetization is required for the prototype.

Do not introduce ads, stamina purchases, loot boxes, real-money gambling, paid stat boosts or pay-to-skip routine.

The first priority is to make a genuinely good game.

---

# 37. Scope discipline

The dream game can eventually include a large prison, visits, multiple wings, healthcare, education, workshops, segregation, transfers and external story scenes.

The first version should become fun inside one wing before expanding.

Vertical-slice success criteria:

- One memorable wing.
- One full day loop.
- Multiple NPC personalities.
- Basic life systems.
- Relationships/memory.
- Heat/staff consequences.
- At least one job.
- At least one board game.
- Combat.
- Early missions.
- Save/load.

Once these systems create stories on their own, more map space becomes valuable. Before that, more corridors do not.

---

# 38. Ultimate experience goal

A player should be able to tell a story like:

> “I was meant to go to work, but I skipped it because Malcolm only plays checkers in the afternoon and I needed him to trust me. I finally beat him, but one of the officers saw me hanging around with his group and my Heat went up. Then Leon stopped talking to me because he thought I was attracting too much attention. I spent the next day actually doing my job and keeping my head down, trained in the evening, and when Darren challenged me later I was finally strong enough not to get flattened.”

That kind of unscripted chain is the target.

The mission campaign should sit on top of that living simulation rather than replacing it.
