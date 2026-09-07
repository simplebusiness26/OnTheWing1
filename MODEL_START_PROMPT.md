# ONE PROMPT TO GIVE THE CODING MODEL

Copy/paste the prompt below into the model that is building this repository, or simply tell the model to open this file and follow it.

---

You are taking full ownership of this repository for one autonomous build run. Build **On The Wing** as far as you possibly can rather than replying with another plan.

Before making implementation decisions, read every root specification file in this repository in full, especially:

- `MASTER_BUILD_PROMPT.md`
- `BUILD_PLAN.md`
- `GAME_DESIGN_SPEC.md`
- `TECHNICAL_SPEC.md`
- `NPCS_AND_MISSIONS.md`
- `ACCEPTANCE_AND_SCORECARD.md`

Then inspect the repository and immediately start implementing the game.

Your objective is to leave behind the **largest coherent, playable Android Unity build you can complete in this run**. Do not stop after creating architecture, TODOs, a design document, a title screen or one movement script. Work through the build plan in priority order and continue until genuinely blocked by a tool limit or an external credential that only I can provide.

Key requirements that must remain central:

- Unity 6 LTS family + URP + C#.
- Android/mobile first and free-to-build/test with free tooling.
- Third-person free movement.
- Floating left joystick.
- Right-side swipe camera with good indoor collision.
- Gritty stylized-realistic fictional UK prison.
- Three-level rectangular wing with opposing long rows of cells, landings, railings, central void, safety net, stairs, showers, yard, training, work area and game table.
- Six playable adult characters with genuinely different stats, weaknesses, growth and starting reputation.
- Skills that improve through doing relevant activities.
- Game clock and a living daily routine.
- NPCs with cells, schedules, routines and interruptions.
- Hygiene/showering that affects social behavior.
- Training that affects physical capability.
- A real job with attendance, pay, Work Skill and staff consequences.
- Separate prisoner Respect / Trust / Fear / Influence.
- Separate Staff Trust / Suspicion / Heat / Reliability.
- “Red hot” Heat behavior where cautious prisoners may stop dealing with the player and officers react differently.
- Important NPCs with structured memories of promises, help, disputes, game results, fights and associations.
- Data-driven dialogue and mission logic.
- At least the first three main missions fully playable, while scaffolding the full 30-mission campaign.
- Side missions that affect relationships and later routes.
- At least one **real playable board minigame**, preferably checkers, integrated into NPC memory/story.
- Unarmed non-graphic combat where training/stats matter and fights cause relationship/reputation/Heat consequences.
- Local save/load that preserves the living simulation.
- Mobile settings/performance controls.
- Development/debug tools that make time, stats, Heat, missions and teleporting easy to test.
- GitHub Actions Android APK build workflow, with any Unity Personal license secret requirements clearly documented rather than invented.

Where final character models, animations, textures or audio are unavailable, use clean coherent placeholders and KEEP BUILDING. You are explicitly authorized to make sensible implementation choices without asking me about minor details. Do not wait for final art before making the gameplay functional.

Do not implement realistic instructions for dangerous or illegal activity. Any contraband, security, prison-rule-breaking or escape content must remain fictional and abstract in mechanics/story data. Violence may be intense in gameplay but must remain non-graphic, with no gore or detailed injury depiction.

Use `ACCEPTANCE_AND_SCORECARD.md` as your QA checklist. A feature earns no credit merely because a class or document exists: it needs to be wired into gameplay where practical.

Before ending your run:

1. eliminate known compile errors;
2. make the project boot into a usable flow;
3. verify the world/player/routine systems are actually connected;
4. add automated tests where useful;
5. configure Android CI as far as possible;
6. create/update `BUILD_STATUS.md` with a truthful implementation inventory, current blockers and exact APK-testing steps;
7. commit/push the implementation if your environment permits.

If you complete the minimum vertical slice early, continue into more NPCs, missions, side stories, jobs, minigames, polish and performance. **Do not stop simply because the first milestone works.**

Do the work now. Do not respond with “here is what I would build.” Build it.
