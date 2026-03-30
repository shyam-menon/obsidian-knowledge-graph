---
name: kg-note
description: Apply linking discipline to an Obsidian knowledge graph note. Checks for missing domain tag, missing up-link to MOC, broken links, and thin sibling links. Fixes all issues and updates the MOC. Use when creating or editing a note.
argument-hint: [note title]
allowed-tools: Read, Edit, Bash, Grep
---

# Knowledge Graph Note Check

## Live vault state
Existing notes:
!`ls "notes/" 2>/dev/null || echo "Run from vault root"`

Existing MOCs:
!`ls "moc/" 2>/dev/null`

## Taxonomy reference
Read the file at `${CLAUDE_SKILL_DIR}/taxonomy.md` to understand the domain taxonomy, tag mapping, MOC mapping, and cluster membership for sibling link expectations.

## Your task

The note to check is: **$ARGUMENTS**

If no argument was given, ask the user which note they want to check before proceeding.

Work through the following rules in order. Fix each issue silently (don't ask for confirmation per fix — just do it), then report a summary of what you changed at the end.

---

### Rule 1 — Domain tag
Read the note. Check whether it contains one of: `#ai`, `#security`, `#api`, `#frontend`, `#observability`.

- If missing: use taxonomy.md to determine the correct tag based on the note's subject matter, then append a `## Tags` section with the tag.
- If the note spans two domains (e.g. an AI note that touches security), add both tags.

---

### Rule 2 — Up-link to MOC
Check whether the note contains `Up: [[` pointing to a MOC.

- Use taxonomy.md to find the correct MOC for this note's domain.
- If the up-link is missing, add `Up: [[MOC name]]` before the Tags section.
- If it points to the wrong MOC, correct it.

---

### Rule 3 — Broken links
Extract every `[[link]]` in the note. Compare each against the live note list injected above.

- A link is broken if no file in `notes/` matches the link text (Obsidian matching is case-insensitive, ignores extension).
- For each broken link: if the intent is clear, fix the filename to match an existing note. If the intent is unclear, remove the link and note it in your summary.
- Do not create placeholder links to notes that don't exist.

---

### Rule 4 — Sibling links
Look up which cluster this note belongs to in taxonomy.md. Check that the note links to the other notes in its cluster.

- Add links to cluster siblings that are missing from the note's connections section.
- Do not add links to every note in the vault — only to notes in the same cluster that are genuinely related.
- If the note has no connections section yet, create one before the Tags section.

---

### Rule 5 — Update the MOC
Read the MOC file for this note's domain (from taxonomy.md). Check whether this note already appears in it.

- If missing: add it to the correct section of the MOC.
- If the MOC has no matching section for this note's cluster, add it to the most appropriate existing section.

---

## Summary report
After making all fixes, report concisely:
- Which rules had violations and what was fixed
- Any broken links that were ambiguous (removed rather than fixed)
- Whether the MOC was updated

Then ask: "Commit these changes to git?"
If yes, run:
```
git add notes/ moc/ && git commit -m "Apply linking discipline: [note title]

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
git push
```
