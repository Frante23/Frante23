# GitHub Profile V2 — Setup

This package is intended for the public profile repository:

Frante23/Frante23

The README expects the GitHub Actions workflow to generate the SVG files inside `profile/`.

## 1. Enable private contribution visibility

On your GitHub profile, open the contribution graph settings and enable private contributions. GitHub shows private activity anonymously; it does not reveal private repository names or content.

## 2. Create a Personal Access Token

The workflow uses `stats-organization/github-readme-stats-action@v2`.

Its documentation currently specifies a Personal Access Token with the classic scopes:

- `repo`
- `read:user`

Because the `repo` scope is broad, treat this token as a password. Never paste it into README.md or into the workflow file.

## 3. Save the token as a repository secret

Open:

Frante23/Frante23 → Settings → Secrets and variables → Actions → New repository secret

Use this exact name:

GH_STATS_TOKEN

Paste the Personal Access Token as the value.

## 4. Upload the files

Your profile repository should contain:

README.md
.github/workflows/stats.yml
profile/

The `profile/` folder may start empty.

## 5. Run it manually once

Open:

Actions → Update GitHub Profile Stats → Run workflow

After the workflow finishes, it should create:

profile/stats.svg
profile/top-langs.svg
profile/pin-mate1133.svg
profile/pin-tutorial-epico.svg

The workflow will then refresh the cards automatically once per day.

## 6. Featured projects

The current public repositories are limited. The V2 temporarily features:

mate1133-inscripcionepica
tutorial-epico

Replace these cards later with stronger portfolio-ready repositories. To replace one, change both the `repo=` value and output `path` in `.github/workflows/stats.yml`, then update the matching image and link in README.md.
