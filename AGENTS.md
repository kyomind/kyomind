# AGENTS.md

This repository is the special GitHub profile repository for `kyomind/kyomind`. The main artifact is the root `README.md`, which is rendered on the public GitHub profile.

## Scope

- Apply these rules to the whole repository.
- Keep this file focused on agent behavior. Keep repo orientation and profile copy in `README.md`.
- No layered `AGENTS.md` files are needed unless the repository grows directories with distinct agent rules.

## Source Of Truth

- `README.md` is the primary user-facing output of this repository.
- `.github/workflows/recent-post.yml` controls the automated latest-post update.
- The section between `<!-- BLOG-POST-LIST:START -->` and `<!-- BLOG-POST-LIST:END -->` is workflow-managed content.

## Working Rules

- Prefer minimal edits. This repo is intentionally small.
- Preserve the overall structure and tone of `README.md` unless the user asks for a profile rewrite.
- Do not manually rewrite or remove the blog post marker comments.
- If changing content inside the workflow-managed blog section, first confirm whether the user wants a manual override or a workflow change.
- When adding new profile sections, keep them compatible with GitHub profile README rendering.
- Avoid adding repository files that do not serve the profile page or its automation.

## Editing Guidance

- Check whether a requested change belongs in `README.md` or in workflow/configuration files.
- Put agent instructions, workflow constraints, and approval boundaries in `AGENTS.md`, not in `README.md`.
- If a request would add recurring automation behavior, prefer `.github/workflows/` over manual README maintenance.

## Validation

- After editing `README.md`, verify that Markdown remains readable as a GitHub profile page.
- After editing `.github/workflows/recent-post.yml`, validate YAML syntax and keep the blog marker contract intact.
- Before finishing, confirm that `README.md` still reads like a profile page rather than an implementation note.
