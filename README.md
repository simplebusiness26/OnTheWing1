# On The Wing

**On The Wing** is a mobile-first, third-person, open-world UK-prison-life drama game concept. This repository is one of two deliberately identical model-comparison starting points.

## Model comparison rule

`OnTheWing1` and `OnTheWing2` should begin from the same specification. Give each coding model the contents of **MASTER_BUILD_PROMPT.md** (or point the model at the repository and tell it to follow that file exactly), then compare what each model actually builds.

Do not simplify the brief merely to finish quickly. The goal is to build the largest coherent, playable vertical slice possible in one autonomous run, while keeping the project maintainable and Android/mobile friendly.

## Intended player experience

The player chooses from six inmates with different starting strengths, weaknesses, histories and skill-growth profiles, then enters a gritty fictional UK prison. The prison should feel alive: timed unlocks, roll checks, work, exercise, showers, meals, relationships, officer attention, friendships, rivalries, minigames, reputation, skills, money, jobs, side stories and a long main campaign.

The player can ignore the main story for in-game days and simply live prison life. Ordinary activities matter: hygiene affects social reactions, training affects physical ability, missed work affects staff trust, associations affect officer attention, and NPCs remember meaningful interactions.

The game is fictional entertainment. Illegal or dangerous activities must be represented as abstract gameplay systems rather than realistic real-world instructions. Violence may feel intense and consequential but should remain non-graphic: no gore, dismemberment or detailed injury simulation.

## Read these first

1. `MASTER_BUILD_PROMPT.md` — the one-prompt autonomous build instruction.
2. `GAME_DESIGN_SPEC.md` — game vision, mechanics, characters, world, story and content.
3. `TECHNICAL_SPEC.md` — Unity architecture, mobile targets, systems and CI expectations.
4. `ACCEPTANCE_AND_SCORECARD.md` — definition of done and model-comparison scoring.

## Target

- Engine: Unity 6 LTS family, URP, C#.
- Platform: Android first.
- Input: left floating joystick + right-side swipe camera + context actions.
- Camera: third-person, over-the-shoulder/free-follow.
- Art direction: realistic-looking, gritty, slightly stylized for mobile performance.
- Cost target: buildable/testable using free tooling and free assets/placeholders.
- Delivery target: a GitHub Actions Android APK workflow, with clear documentation for any Unity Personal license secrets the owner must add manually.

The coding model should **build**, not merely plan. Where final art/audio is unavailable, use coherent placeholders and continue implementing gameplay rather than stopping.