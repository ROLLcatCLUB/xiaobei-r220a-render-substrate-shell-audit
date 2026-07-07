# R220A Render Substrate And Shell Layer Audit

This is a narrow GPT review package for the Shiwei prep-room render shell line.

## What To Review

Please review whether the next implementation should start from the existing R97B working shell instead of creating another HTML copy or starting with field rendering.

The intended parallel structure is:

```text
1 main code line + 2 readonly contract lines
```

- Main code line: the current R97B working shell only.
- Readonly contract line A: backend shell registry, fetch adapter, render slots, render block contracts.
- Readonly contract line B: historical shell lineage and handoff evidence, especially M1, R36, R97B, R100-P1, and R108.

## Primary Conclusion

The local render substrate already exists. It is not a single renderer file. It is a layered substrate composed of:

- 1013L_R0 and 1013L_R5 backend shell contracts and registered readonly routes.
- R13/R15/R17/R24/R30 render surface, ViewModel, render-block, component-boundary, and visible-frame contracts.
- R36/M1 historical shell and visual interaction baselines.
- R97B current working shell, which already wires uploaded lesson preview payloads into the existing shell.

The next shell-layer work should target the R97B shell and should not revive R100-P1 or use R36 as the current code target.

## Hard Boundary

- Do not create a new teacher static page.
- Do not treat R100-P1 as the current shell.
- Do not modify R21 or R36.
- Do not start with field rendering.
- Do not add save, export, formal apply, database writes, memory writes, Feishu writes, vector writes, provider calls, or new model calls.
- Do not push the dirty main project as a review artifact.

## Files In This Package

- `R220A_RENDER_SUBSTRATE_AND_SHELL_LAYER_AUDIT.md`: human-readable audit and landing plan.
- `R220A_RENDER_SUBSTRATE_AND_SHELL_LAYER_AUDIT.json`: structured summary.
- `GPT_REVIEW_PROMPT_R220A.md`: prompt for GPT review.
- `PACKAGE_MANIFEST.json`: package file manifest.
- `source_anchors/`: selected source excerpts and existing docs used as evidence.
- `input/R220A_UPSTREAM_BRIEF.txt`: user's upstream R220A planning brief.

