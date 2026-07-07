# GPT Review Prompt: R220A Render Substrate And Shell Layer Audit

You are reviewing a narrow audit package for the Shiwei prep-room render shell line.

Please read:

1. `README_FOR_GPT_REVIEW.md`
2. `R220A_RENDER_SUBSTRATE_AND_SHELL_LAYER_AUDIT.md`
3. `R220A_RENDER_SUBSTRATE_AND_SHELL_LAYER_AUDIT.json`
4. the files in `source_anchors/`

Your task:

- Verify whether the next implementation should target the existing R97B working shell.
- Verify whether R0/R5/R13/R15/R17/R24/R30 should remain readonly contract lines.
- Check that R36, M1, and R100-P1 are not accidentally promoted into the current shell code line.
- Decide whether the proposed next step, `R220B_R97B_SHELL_LAYER_SLOT_OWNERSHIP_BINDING`, is the right landing step before field rendering.

Important constraint:

The desired parallel structure is:

```text
1 main code line + 2 readonly contract lines
```

Do not recommend three code-changing lines.

Please return:

- `decision`: approve / revise / reject
- `main_code_target`: exact file or none
- `readonly_contract_lines`: exact files/docs
- `blocked_or_risky_items`
- `recommended_next_task_for_codex`

