You’re right—I messed that up. I’m sorry.

If you want to keep me on a very tight leash, use a **“Surgical Patch”** prompt. It hard-limits scope, forces a diff-only reply, and defers any full-file output until you say **FS**.

---

# Copy-paste prompt (short)

**Surgical Patch Mode**  
- **Task:** Apply only the minimal edits required to fix: `<describe the one issue>`.  
- **Scope guardrails:** Do **not** reformat, reorder, rename, compress, “clean up,” or change anything unrelated. Preserve whitespace and comments.  
- **Output format:** Return a **unified diff (git format)** only. No full file, no extra prose.  
- **File context:** This patch applies to `Events_Dashboard.html` exactly as I sent it.  
- **Diff rules:** Keep path as `a/Events_Dashboard.html` → `b/Events_Dashboard.html`. Use correct line numbers.  
- **No extras:** No stylistic changes, no “helpful” improvements, no dependency bumps.  
- I’ll reply **FS** if I want the full updated file.

---

# Contract prompt (strict)

**Objective**  
Fix exactly one thing: `<state the specific bug/fix, e.g., “Leaflet map not rendering due to zero-height container on first paint.”>`

**Invariants (must not change)**  
- Do **not** modify any code unrelated to the fix.  
- Do **not** reflow, minify, prettify, or reorder code/attributes/imports.  
- Preserve all whitespace, comments, and formatting that are not directly required by the fix.  
- Do **not** rename variables, functions, CSS classes, or IDs.  
- Do **not** alter logic, timing, or UI outside the fix.  
- Do **not** add or remove libraries, HTML nodes, or attributes unless strictly required for the fix.  
- Do **not** touch text copy or strings outside the changed lines.  
- Keep the file size and structure effectively unchanged except for the minimal diff.

**Allowed edits (only)**  
- Insert the minimal lines needed to implement the fix.  
- If needed, adjust at most **one** nearby line for integration (imports, variable, or call site) — explain in diff hunk comment.

**Deliverable**  
- Output **only** a **unified diff (git)** against `Events_Dashboard.html`.  
- No prose before/after the diff.  
- No full file unless I later reply **FS**.  
- Use hunks with correct line numbers; include only changed context.  
- Example header:
  ```
  --- a/Events_Dashboard.html
  +++ b/Events_Dashboard.html
  @@ -<start>,<len> +<start>,<len> @@
  ```
- Add a short `// FIX:` comment on the changed line(s) to mark intent.

**Verification you must do before returning**  
- Confirm the diff compiles/runs with the original file content + your patch.  
- Confirm the fix works in the described scenario and doesn’t alter unrelated behavior.  
- Confirm no unrelated lines are changed (no trimming, spacing, attribute reordering).

**If ambiguous**  
- Assume the narrowest interpretation that touches the fewest lines.  
- If you must choose, prefer a 1–3 line patch and note why in an inline `// FIX:` comment.

---

## Example “map fix” ask (filled in)

> **Objective:** Ensure the Leaflet map renders when its flex container computes zero height at first paint.  
> **Allowed edit:** Insert a `setTimeout(..., 0)` block right after map init that sets `#map` height to its parent’s computed height if `offsetHeight === 0`, then calls `map.invalidateSize()`.  
> **Everything else:** off-limits.  
> **Output:** unified diff only. I’ll say **FS** for the full file.

---

## Quick checklist you can paste above any task

- [ ] Minimal lines changed  
- [ ] No formatting changes  
- [ ] No unrelated code touched  
- [ ] Unified diff only  
- [ ] `// FIX:` comment on edited lines  
- [ ] Wait for **FS** before posting the full file

---

If you use one of those prompts, I’ll stick to the patch and nothing else. If I ever drift, call it out and I’ll re-issue a **smaller diff**.
