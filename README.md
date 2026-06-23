# .github — infraspecdev org defaults & README standard

This repo holds infraspecdev's **org-wide community health files** (which GitHub auto-cascades to every repo — at the repo root) and the **reusable README standard** (everything under [`readme-standard/`](./readme-standard)): one base template + per-repo-type overlays, plus a `make`-driven generator.

## Quick start — generate a README

All README tooling lives in [`readme-standard/`](./readme-standard); run `make` from there:

```bash
cd readme-standard
make readme                 # interactive: prompts for type, name, description, public?, ...
# or non-interactive:
make readme ARGS="--type go-cli --name goperf --description '...' --public --out README.md"
make list                   # show the supported repo types
# (from the repo root you can also use:  make -C readme-standard readme)
```

The generator (`readme-standard/bin/render-readme.py`) stitches the base wrapper + your type overlay, applies the `--public` transform, strips authoring annotations, and writes a ready README. See a worked output in [`readme-standard/templates/EXAMPLE-goperf.md`](./readme-standard/templates/EXAMPLE-goperf.md) (internal) and [`EXAMPLE-goperf-public.md`](./readme-standard/templates/EXAMPLE-goperf-public.md) (public).

## Repo types → overlays

| Type key | Repo type | Overlay |
|----------|-----------|---------|
| `terraform-module` | Terraform reusable module (`terraform-aws-*`) | `01-terraform-module.md` |
| `live-iac` | Live IaC / environment (state-bearing) | `02-live-iac.md` |
| `template` | Template / scaffold repo | `03-template-repo.md` |
| `go-cli` | Go service / CLI | `04-go-cli-service.md` |
| `web-app` | Web / full-stack app | `05-web-app.md` |
| `github-action` | GitHub Action / CI tool | `06-github-action.md` |
| `ml-poc` | ML / AI POC / experiment | `07-ml-poc.md` |
| `bot-utility` | Internal bot / utility / scripts | `08-bot-utility.md` |
| `config-mgmt` | Config management (decK/Ansible/Kong) | `09-config-mgmt.md` |
| `learning` | Learning / hiring assessment | `10-learning-assessment.md` |
| `plugin-lib` | Plugin / prompt / skill library | `11-plugin-prompt-lib.md` |
| `docs-content` | Docs / content / website | `12-docs-content.md` |
| _(stack on any of the above)_ | **Public / open-source delta** | `13-public-repo.md` (use `--public`) |

## Hand-copy path (no `make`)

Prefer the generator, but you can also: copy [`readme-standard/templates/README.base.md`](./readme-standard/templates/README.base.md) → `README.md`, append your overlay from [`readme-standard/templates/overlays/`](./readme-standard/templates/overlays), fill placeholders, strip the `[REQUIRED]` tags and `<!-- comments -->`. For public repos, also apply `overlays/13-public-repo.md`.

## Distribution

**README is not a default community health file** — GitHub does not auto-cascade it. So:

- The files that **do** cascade org-wide live at the root here: [`CONTRIBUTING.md`](./CONTRIBUTING.md), [`CODE_OF_CONDUCT.md`](./CODE_OF_CONDUCT.md), [`SECURITY.md`](./SECURITY.md), plus the org profile in [`profile/README.md`](./profile/README.md).
- READMEs are adopted **actively**: run `make readme` in a repo, or seed via GitHub template repositories (fold overlays into `terraform-module-template`, `golang-template`, etc.).

## Consistency without a linter

There is intentionally **no CI linter** enforcing README structure. Structure comes from the carrots, not a stick:

- Run `make readme` — the generator produces correct structure by construction.
- Seed new repos from GitHub template repositories (overlays folded into `terraform-module-template`, `golang-template`, etc.).

The real gap to watch is *missing or empty* READMEs (a structure linter wouldn't catch those anyway). If you ever want a guardrail, prefer a lightweight presence check ("README exists and is non-trivial") over heading enforcement.

## Keep reference sections auto-generated

- **Terraform modules:** `terraform-docs markdown table --output-file README.md --output-mode inject .` between the `<!-- BEGIN_TF_DOCS -->` / `<!-- END_TF_DOCS -->` markers (wire into pre-commit).
- **GitHub Actions:** generate the inputs/outputs tables from `action.yml` (e.g. `action-docs`).

---

Rationale, sources, and the org-wide README audit that produced this standard: see the Shield research doc (`docs/shield/readme-template/research.md`).
