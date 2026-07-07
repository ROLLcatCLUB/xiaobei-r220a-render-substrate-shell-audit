# 1013R R220A Render Substrate And Shell Layer Audit

Date: 2026-07-08

Repository root: `D:\Documents\SmartEdu\xiaobei-core`

## Result

PASS_WITH_NOTES.

The local render substrate exists and is usable. It should be treated as layered infrastructure, not as one standalone renderer.

The current implementation target should be:

`outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013R_R97B_TEACHER_SHELL_EXPERIENCE_POLISH_AND_STALE_CONTENT_CLEANUP/r97b_clean_shell_context_preview.html`

R36 and M1 remain historical baselines. R100-P1 is legacy preview material and must not become the current shell again.

## Layer Map

### Layer 0: App Shell

Evidence:

- `backend/xiaobei_ai/prep_room_render_shell_registry_1013L_R0.py`
- `outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013L_M1_canonical_main_shell_milestone/1013L_M1_report.md`

Role:

- Defines persistent top shell, dynamic RenderStage, and persistent bottom Agent composer.
- Treats existing pages as RenderStage states instead of disconnected pages.
- Keeps standalone static pages as review or rollback artifacts only.

Status:

- Contract exists.
- Routes are registered in `backend/xiaobei_ai/routes.py`.
- Formal frontend binding is not the current R220A target.

### Layer 1: Prep Room Workspace Shell

Evidence:

- R97B working shell.
- R36 static patch consolidation report.
- R108 handoff.

Role:

- Owns prep-room notebook workspace, binder/panel/workspace/right rail layout, bottom Xiaojiao context, import drawer, and teacher-visible shell context.
- Reuses R36 interaction ideas such as right rail selection, pointed edit bubble, and independent scrolling.

Status:

- Current working shell is R97B.
- R36 is a reference baseline only.
- R100-P1 is legacy and should not be used as the active shell.

### Layer 2: Render Surface / Canvas

Evidence:

- `docs/prep-room-render-surface-map.md`
- `backend/xiaobei_ai/prep_room_unified_viewmodel_1013R_R15.py`
- `backend/xiaobei_ai/prep_room_render_blocks_protocol_1013R_R17.py`
- `backend/xiaobei_ai/prep_room_render_block_component_boundary_1013R_R24.py`
- `docs/1013R_R30_visible_frame_connector.md`

Role:

- Defines stable render slots and visible frame mapping.
- Important slots include `lesson_body`, `teaching_process`, `courseware_script`, `classroom_display_screen`, `worksheet`, `assessment_rubric`, `source_evidence`, `confirm_actions`, and `bottom_composer`.

Status:

- Contract substrate exists.
- It should stay readonly during R220A.
- The shell layer should expose and verify slot ownership before any field rendering.

### Layer 3: Lesson Content Renderer

Evidence:

- R97B `applyBackendPayload(payload, endpoint)`.
- R97B `renderSingleLessonTemplateEpisodes(template, payload)`.
- R97B `renderUnifiedLessonProcessStep(episode, renderMode)`.
- R97B `updateRightRailFromBackend(payload, steps, current)`.
- R97B `updateBottomXiaojiaoFromBackend(steps, current, payload)`.

Role:

- Receives backend uploaded-lesson preview payloads.
- Updates hero, section content, teaching-process episodes, right rail assistant state, bottom Xiaojiao summary, provenance ledger, and stale-static cleanup.

Status:

- The existing R97B shell already routes uploaded `.docx` / `.pdf` preview through `/api/prep-room/uploaded-lesson-document-preview`.
- `single_lesson_template.process_episodes` is already preferred over legacy `process_steps` when available.
- Non-process sections still depend mainly on `current.sections` and `updateSectionFromViewModel`.
- Right rail currently behaves as current-episode assistant/status context, not a full shell-layer slot contract.
- Bottom Xiaojiao currently shows upload-preview context, not a precise selected-field or selected-slot contract.

## Backend Contract Evidence

`backend/xiaobei_ai/routes.py` registers:

- `prep_room_render_shell_registry_1013L_R0.register_routes(...)`
- `prep_room_main_shell_fetch_adapter_1013L_R5.register_routes(...)`

R0 exposes:

- `/api/prep-room/render-shell/registry`
- `/api/prep-room/render-shell/state/<state_id>`

R5 exposes:

- `/api/prep-room/main-shell/viewmodel`
- `/api/prep-room/main-shell/viewmodel/state/<state_id>`

R97B uses:

- `/api/prep-room/uploaded-lesson-document-preview`

## Recommended Next Landing Plan

Keep R220A as readonly audit and do not mutate the shell yet.

Then open the next shell-layer implementation as one main code line:

```text
1013R_R220B_R97B_SHELL_LAYER_SLOT_OWNERSHIP_BINDING
```

Main code line target:

- R97B working shell only.

Implementation goal:

- Add or normalize shell-layer ownership markers and resolver functions on existing R97B DOM surfaces.
- Prove that App Shell, Workspace Shell, Render Surface, Lesson Content Renderer, Right Rail, and Bottom Xiaojiao can be addressed without field rendering.
- Preserve the existing backend preview entry and `applyBackendPayload()` behavior.

Expected minimal additions:

- A shell-slot inventory object such as `window.__R220_SHELL_LAYER_SLOT_OWNERSHIP__`.
- Readonly DOM markers for existing shell regions, for example app shell, workspace shell, render surface, lesson content region, right rail, and bottom Xiaojiao.
- A tiny smoke script or validator that checks markers and confirms the upload-preview route remains unchanged.

Forbidden in R220B:

- No new renderer.
- No new HTML copy.
- No field rendering.
- No save/export/formal apply.
- No provider/model call.
- No R21/R36/R100-P1 modifications.

## Review Questions For GPT

1. Is R97B correctly identified as the only current main-code shell target?
2. Are R0/R5/R13/R15/R17/R24/R30 correctly scoped as readonly contract lines?
3. Should R220B start with shell-layer slot ownership markers and resolver checks before field rendering?
4. Are right rail and bottom Xiaojiao correctly identified as existing surfaces whose exact slot contracts are still incomplete?
5. Are any old pages being accidentally promoted back into the current shell line?

