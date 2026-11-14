# Operations & maintenance

## Routine checks

1. Open the [profile](https://github.com/valeriandecarvalho) and verify both language versions and the toolbox animation.
2. Open GitHub [`output`](https://github.com/valeriandecarvalho/valeriandecarvalho/tree/output) and check both snake SVG files exist and display correctly.
3. Open [GitHub Actions](https://github.com/valeriandecarvalho/valeriandecarvalho/actions) and check whether the scheduled snake workflow succeeds. If GitHub billing restrictions still block it, the GitLab fallback must be healthy.
4. In [GitLab pipelines](https://gitlab.com/valeriandecarvalho1/github-snake-automation/-/pipelines), check scheduled jobs. A green job that *skipped* regeneration because both SVGs are recent is expected.
5. In GitLab Pipeline schedules, confirm the `main` schedule is active at **08:00 Europe/Paris**.

## When to update each branch

| Change | GitHub `main` | GitHub `output` | GitLab `main` |
| --- | --- | --- | --- |
| Profile wording, banner, contact, toolbox | Replace one root commit | Leave alone | Leave alone |
| Snake color palette | Update workflow; replace one root commit | Updated by next successful generator | Update generator script; replace one root commit |
| Fallback logic or test | Leave alone | Leave alone | Update scripts; replace one root commit |
| Daily snake update | Leave alone | Automatic one-root snapshot | Leave alone |

The installation package updates both `main` branches (to keep the matching palette), but intentionally **does not overwrite `output`**. Force one manual GitLab pipeline afterward to generate the new sage-color versions.

## Manual GitLab regeneration

1. GitLab → Build / Compilation → Pipelines → New pipeline.
2. Select `main`, run a web pipeline. The current rules set `FORCE_REGENERATE=1` for manual runs.
3. Check the job `snake_fallback`: verify both SVGs were regenerated and the publish log contains `Updated ... @output in one root commit`.
4. Confirm the GitHub `output` branch still has exactly one commit.

## Update the profile while keeping one root commit

Rewriting source-branch history is intentional project policy, **not a recommended general Git workflow**. Before any update:

- Back up both repositories with `git clone --mirror`.
- Prepare changes in new clones; do not delete your working folders.
- Review all files and the two remote URLs.
- Use an explicit, SHA-bound `--force-with-lease` for `main` only. A protected branch may reject the push; temporarily change the rule **only if you are authorized**, then restore it.
- Keep output untouched unless specifically regenerating the snake.
- Verify `git rev-list --count origin/main` equals `1` for both source repos.

The installation script under the deployment pack does this, but **never** run it casually for unrelated repositories.

## Failure guide

| Symptom | Likely cause / first step |
| --- | --- |
| GitLab pipeline succeeds but `output` unchanged | Check logs for `Both SVGs are fresh` / skip; normal with 20-hour threshold |
| GitLab pipeline fails with HTTP 401/403 | Check `GITHUB_TOKEN` validity, expiry, repository permission and protected variable settings |
| GitHub workflow cannot start | Open Actions and inspect account-level billing/usage block; GitLab remains backup |
| GitLab YAML invalid | Check `script:` entries with colon characters are quoted or use a multiline `|` block |
| `pre-receive hook declined` on GitLab | Branch rules may block source-branch history rewrite; restore protection afterward |
| README shows missing icons | Rebuild official toolbox GIFs before pushing; do not deploy demo graphics |
| Email link fails | Create the mailbox/forwarding alias, then test receiving mail |
