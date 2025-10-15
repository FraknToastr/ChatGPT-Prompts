# Non-Regressive Code Contract (paste this at the start)

**Do not change existing functionality.** All behavior, defaults, file paths, parameters, and outputs must remain exactly as in my current code **unless I explicitly say “CHANGE:”** and specify what to change.

## Rules
1. **Additive by default:** Only add comments, explanations, tests, or separate helper utilities. Do **not** edit existing logic, names, signatures, constants, defaults, or output formats.
2. **No silent edits:** If you believe a fix is necessary, **propose** it in a short note first. Do **not** apply it unless I reply with `CHANGE: <approved>`.
3. **Exact preservation:** Keep current:
   - File paths and discovery locations  
   - Parameter names/types/order/defaults  
   - Return shapes / printed text / file names / extensions  
   - Layouts, sizes, and rendering details  
4. **Patches over rewrites:** When I do approve a change, return a **unified diff patch** against my file(s) **and** the full updated file(s). Mark your patch section with `PATCH START/END`.
5. **Compatibility:** New code must be backward-compatible and off by default (gated behind a new flag that defaults to **False**).
6. **No speculative fixes/“improvements”.** No refactors, renames, reformatting, or dependency swaps without `CHANGE:` approval.
7. **Assume constraints are intentional.** If something seems odd, ask; don’t alter it.
8. **Echo invariants:** At the top of your answer, list the invariants you are preserving (paths, grid sizes, ranges, etc.) to confirm compliance.

## Response format
- If only analysis or docs: ✅ “No code changes applied.”  
- If adding utilities/tests: provide **new files only**.  
- If a change is requested and approved:  
  - `PATCH:` (unified diff)  
  - `FULL FILE:` (final file content)  
  - `NOTES:` (why, impact, how to revert)

## Change approval protocol
Only treat lines that start with **`CHANGE:`** as authorization. Examples:
- `CHANGE: Center glyphs vertically using ascent/descent; do not alter corners/labels.`  
- `CHANGE: Do NOT scan C:\Windows\Fonts. Only use ArcGIS Pro Resources\Fonts.`

Anything not prefixed with `CHANGE:` is **not** permission to modify existing behavior.

---

### Ultra-short version (if you want a one-liner)
> “Additive-only. Do not change existing behavior, defaults, paths, parameters, or outputs unless I write `CHANGE:` and specify exactly what to alter. Otherwise propose, don’t apply. Patches > rewrites.”

If you like, I can turn your current project’s specifics (paths, grid sizes, label rules, font folders, code ranges, etc.) into a ready-made **Invariants** block you can reuse.
