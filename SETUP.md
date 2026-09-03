# GitHub Profile — Final Setup

This package is prepared for the profile repository:

`Frante23/Frante23`

The profile is designed so that the README itself does not contain your Personal Access Token. GitHub Actions reads the token from a repository secret, generates static SVG cards and commits only those generated SVG files.

## 1. Copy the package into the profile repository

Your repository should end up with this structure:

```text
Frante23/
├── README.md
├── SETUP.md
├── assets/
│   ├── banner.svg
│   └── footer.svg
├── profile/
│   └── .gitkeep
└── .github/
    ├── dependabot.yml
    └── workflows/
        └── stats.yml
```

## 2. Enable GitHub private contribution visibility

Open your GitHub profile and enable the option to display private contributions in your contribution settings.

GitHub displays the count of private contributions on your profile without exposing the private repository names or contribution details to people who cannot access those repositories.

This native GitHub setting is separate from the README statistics workflow.

## 3. Create a classic Personal Access Token

Go to:

`GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)`

Create a new classic token.

Suggested note:

`GitHub Profile Stats`

Select the scopes required by the statistics action:

```text
repo
read:user
```

Choose an expiration period you are comfortable maintaining.

The `repo` scope is broad. Treat this PAT as a password and revoke it if you stop using the workflow.

## 4. Store the PAT as a repository secret

Open:

`Frante23/Frante23 → Settings → Secrets and variables → Actions`

Create a new repository secret.

Use exactly this name:

```text
GH_STATS_TOKEN
```

Paste the PAT into the secret value.

Do not paste the PAT into `README.md`, `stats.yml`, an issue, a commit, or a chat message.

## 5. Check workflow write permissions

Open:

`Frante23/Frante23 → Settings → Actions → General`

Under Workflow permissions, the workflow needs permission to write repository contents because it commits the generated SVG files.

The workflow itself declares:

```yaml
permissions:
  contents: write
```

If your repository-level Actions policy forces read-only access, change the repository setting so Actions can write.

## 6. Run the workflow for the first time

Open:

`Frante23/Frante23 → Actions → Update GitHub Profile Stats`

Click:

`Run workflow`

The run should generate:

```text
profile/stats.svg
profile/top-langs.svg
profile/pin-mate1133.svg
profile/pin-tutorial-epico.svg
```

The workflow commits those files back to the profile repository.

After the first successful run, the README cards will render normally.

## 7. Automatic refresh

The workflow is configured to run once per day:

```cron
17 7 * * *
```

GitHub Actions scheduled workflows use UTC.

You can also run it manually whenever you want from the Actions tab.

## 8. Security choices included in this version

The third-party statistics action is pinned to the exact commit used by release `v2.0.2` instead of using a floating `@v2` reference.

`actions/checkout` is also pinned to the exact commit for `v7.0.1`.

The statistics action's internal core is pinned to `2.1.3`.

`fail_on_error` is enabled so a failed API request does not silently replace your profile card with an error card.

The PAT is used only for the statistics-generation steps. Repository checkout and the final push use the workflow's normal GitHub token.

Dependabot is configured to check GitHub Actions dependencies weekly.

## 9. Private statistics

The statistics action documentation specifies a classic PAT with `repo` and `read:user` for private repository statistics.

There is intentionally no `count_private=true` option in this workflow. The current GitHub Stats Extended documentation does not document that option as required for authenticated private statistics. Private access comes from the PAT supplied to the action.

## 10. Featured projects

The current configuration generates cards for:

`mate1133-inscripcionepica`

and:

`tutorial-epico`

When you have stronger public portfolio repositories, replace these values in `.github/workflows/stats.yml` and update the corresponding links and SVG paths in `README.md`.

Do not use a private repository as a Featured Project unless the project has a public, sanitized portfolio version that visitors can actually open.
