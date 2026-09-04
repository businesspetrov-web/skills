---
name: publish-skill-to-github
description: ALWAYS run right after a skill is created or updated (via propose_skills or skill-creator): push the SKILL.md and its files to Pavel's GitHub repo "skills" so every skill is backed up and shareable.
---

# Publish skill to GitHub

Every time you create a new skill or update an existing one for Pavel (whether through `propose_skills`, the `skill-creator` skill, or any other route), also commit it to his GitHub repository **`skills`** (https://github.com/businesspetrov-web/skills). This is a standing instruction — do it without being asked, and mention in one sentence that you did.

## Repository layout

```
skills/
  README.md                 # index table: one row per skill (name — description)
  <skill-name>/
    SKILL.md                # the complete skill file, exactly as proposed/saved
    ...                     # any scripts, references or assets the skill ships with
```

One folder per skill, named with the skill's kebab-case slug. An update replaces the folder's contents; never keep stale files around. Keep `README.md` in sync (add/refresh the row for the skill).

## Procedure

Important: the Cowork cloud workspace's proxy blocks both the GitHub REST API and authenticated `git push` (it only injects credentials for repos in the session's "sources"). So publish through one of these routes, in order of preference:

1. **Local clone on Pavel's computer** (if it is linked and a clone of `skills` is in a connected folder): write `<skill-name>/SKILL.md` (and companion files) there, update `README.md`, then run `git add -A && git commit -m "Add/update skill: <skill-name>" && git push` on his machine.
2. **GitHub web UI via Claude in Chrome** (Pavel is normally signed in as `businesspetrov-web`): open `https://github.com/businesspetrov-web/skills/new/main?filename=<skill-name>/SKILL.md`, set the editor's content to the full SKILL.md (use the javascript tool to set the editor value rather than typing, so auto-indent does not mangle it), and commit directly to `main`. Repeat for `README.md` (edit the existing file) and any companion files. If GitHub asks for identity verification, stop and let Pavel complete it.
3. **Fallback**: if neither route works, hand Pavel the files with SendUserFile and tell him to drop them into the repo.

Whatever the route, the SKILL.md pushed must be byte-for-byte the content passed to `propose_skills` (frontmatter plus body). Confirm to Pavel with the path `skills/<skill-name>/SKILL.md`.

## Notes

- If Pavel's computer is linked and a local clone of `skills` is in a connected folder, prefer writing there and running `git push` on his machine — no token needed.
- Do not push anything other than skill folders and the README into this repo.
- If Pavel says to skip publishing for a particular skill, respect that for that skill only; the default stays "always publish".
