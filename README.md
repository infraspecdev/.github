# .github — infraspecdev org defaults & README template

This repo holds infraspecdev's **org-wide community health files** (which GitHub auto-cascades to every repo), a single **README template** any repo can copy, and **workflow templates** that run on the org's self-hosted runner.

## Use the README template

1. Copy [`README.template.md`](./README.template.md) into your repo as `README.md`.
2. Replace the `<PLACEHOLDERS>` and fill each section.
3. Delete the **Configuration** section if there's nothing to configure.
4. Remove the instructional `<!-- comments -->` as you go.

The template is seven universal sections — **Overview, Getting Started, Usage, Local Development, Configuration, Contributing, License** — that fit any project. Keep the headings as-is so READMEs look consistent across the org. No tooling to install.

## What auto-cascades vs. what you copy

| File | How it reaches your repo |
|------|--------------------------|
| `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md`, `profile/README.md` | **Automatic** — GitHub shows these org-wide for any repo without its own copy (they must live at this repo's root) |
| `README.template.md` | **You copy it** — README is not an auto-cascaded file, so adopt it per repo |
| `workflow-templates/` | **You pick it** — offered under **Actions → New workflow → By infraspecdev**; the copy does not track later changes |

## Run workflows on the org runner

Workflows choose their runner from the `RUNS_ON` org variable, so moving repos between self-hosted and GitHub-hosted runners is one settings change, not an edit in every repo.

```yaml
runs-on: ${{ fromJSON(vars.RUNS_ON || '["ubuntu-latest"]') }}
```

**New workflows:** start from **Actions → New workflow → By infraspecdev → CI (org runner)** ([`workflow-templates/ci.yml`](./workflow-templates/ci.yml)).

**Existing workflows:** replace `runs-on: ubuntu-latest` with the line above.

**Org settings** (an org admin sets these once):

1. **Runner group** (*Settings → Actions → Runner groups*) — leave **Allow public repositories** off and give access to selected private repos only. A fork PR on a public repo could otherwise run arbitrary code on the runner.
2. **`RUNS_ON` variable** (*Settings → Secrets and variables → Actions → Variables*) — a JSON array of the runner's labels, e.g. `["self-hosted","linux"]`. Set **Repository access** to *Private repositories*.

Public repos don't see the variable, so they fall back to `ubuntu-latest`. GitHub-hosted minutes are free for public repos, so nothing is lost.

**Opt a repo out:** set a repo-level `RUNS_ON` variable (e.g. `["ubuntu-latest"]`). Repo variables override org variables of the same name.

**Runner requirements:** the runner needs whatever the jobs use — Docker and buildx for image builds, QEMU for multi-arch — and must not leak state between jobs (ephemeral runners, or clean the workspace).

## Keep reference sections auto-generated

- **Terraform modules:** `terraform-docs markdown table --output-file README.md --output-mode inject .` between the `<!-- BEGIN_TF_DOCS -->` / `<!-- END_TF_DOCS -->` markers.
- **GitHub Actions:** generate the inputs/outputs tables from `action.yml` (e.g. `action-docs`).
