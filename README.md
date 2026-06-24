# .github — infraspecdev org defaults & README template

This repo holds infraspecdev's **org-wide community health files** (which GitHub auto-cascades to every repo) and a single **README template** any repo can copy.

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

## Keep reference sections auto-generated

- **Terraform modules:** `terraform-docs markdown table --output-file README.md --output-mode inject .` between the `<!-- BEGIN_TF_DOCS -->` / `<!-- END_TF_DOCS -->` markers.
- **GitHub Actions:** generate the inputs/outputs tables from `action.yml` (e.g. `action-docs`).
