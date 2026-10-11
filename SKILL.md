---
name: openmontage
description: "Produce a video with the local OpenMontage system: explainers, promos, product films, montages, clips."
---

# OpenMontage — local video production

OpenMontage (calesthio/OpenMontage, AGPLv3) is installed at `C:\Users\HH\Documents\repos\OpenMontage`. Use it when a request needs a produced video (explainer, promo, product film, montage, clip cut, subtitles, dub). For the film's story and shot design, also apply `director`.

## Setup on this machine

- Python: `.venv\Scripts\python.exe` (uv, 3.11). Never the `python` on PATH (it is Postgres's).
- Remotion: `remotion-composer/` with `node_modules` installed. Render with `npx remotion render <entry> <CompositionId> <out.mp4>` from that folder or the project folder.
- Preflight (what tools are usable right now):
  `.venv\Scripts\python.exe -c "from tools.tool_registry import registry; import json; registry.discover(); print(json.dumps(registry.provider_menu(), indent=2))"`
- Works with no keys: Remotion and HyperFrames composition, ffmpeg tools, screen capture, `pixabay_music`, `threejs_world`, subtitles, video analysis.
- Missing: every paid TTS, image and video generation provider (no FAL / OpenAI / ElevenLabs / Google keys). Do not plan on generated footage or voice; say so once at proposal. Piper TTS is installable locally but not premium.

## Method

1. Read `AGENT_GUIDE.md` (the agent contract) before producing. Its Rule Zero holds: every production goes through a pipeline in `pipeline_defs/<name>.yaml`; read each stage director in `skills/pipelines/<pipeline>/` before that stage, and the Layer-3 skill under `.agents/skills/` before calling a tool that names one.
2. A reference video ("make one like this") goes through `skills/meta/video-reference-analyst.md` first.
3. Hero work (promo, launch, brand) uses atelier mode: hand-authored Remotion composition, not the stock scene types. Route through `skills/meta/taste-direction.md` and `skills/meta/bespoke-composition.md`.
4. When both Remotion and HyperFrames are available, state both and the pick with its reason; record it in the project's decision log.
5. Projects live in `projects/<name>/`. Keep a new version in its own folder; never overwrite a rejected version's renders.

## Hercules Studio films

Prior work: `projects/hercules-studio-promo/v3/` (capture scripts: `twinlib.cjs`, `shoot3d.cjs`, `shoot_journey.cjs`, `capture_ui.cjs`, `rec_vision.cjs`, `sheet.py`) and `projects/hercules-studio-film-v4/` (v4 "Follow the signal", the accepted direction; v1–v3 rejected). Reuse these capture scripts instead of rewriting them.

- Deterministic 3D capture: `window.__studioTwin` → `capturePause(true)`, then per frame set camera, `advance(1000/30)`, `frame()`, screenshot. Exact 30 fps, no wall-clock recording.
- Rules from his rejections: sell the outcome, not a screen tour; write the value story first; name industries, never client sites; plain words, no equipment names or tags; show a module by its effect on the plant with text riding on the machines, never a form or dialog; the camera follows the data's journey (machine → plant → Hercules → decision), nothing dwells; never "predictive".

## Done

Watch the exported file itself: duration, resolution, fps, audio streams (ffprobe), and a contact sheet of start / middle / end and every transition. Run `looker` on key frames for anything he will see. Deliver the mp4 path with what is real capture and what is illustrative.
