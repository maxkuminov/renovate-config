# renovate-config

Shared Renovate policy for every `maxkuminov` repo the Renovate app is installed on.

`org-inherited-config.json` is picked up automatically by the Mend-hosted Renovate app
(inherited config) — repos do not need their own `renovate.json`. Add one only to
override something for that repo (e.g. `"baseBranchPatterns": ["dev"]`).

No onboarding PRs: `onboarding: false` + `requireConfig: "optional"` mean a newly installed repo
starts getting update PRs on this policy right away. To opt a repo out, uninstall the app there,
archive the repo, or give it a `renovate.json` with `"enabled": false`.

Policy: weekly (Monday before 6am ET), rebase only on conflict, max 5 open PRs,
minor/patch grouped into one PR and automerged when all checks pass (not 0.x minors),
majors one PR each, with vite* and openai+zod majors grouped. Security alerts ignore the schedule.
