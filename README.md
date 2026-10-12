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

Python minors: the Docker `python` base image and `actions/setup-python`'s `python-version`
(github-actions dep `python`, datasource `github-releases`) are grouped into ONE `python` PR that
Renovate opens only after it is approved on the Dependency Dashboard, never automerged. A new
Python minor arrives months before its ecosystem wheels, and hash-locked requirements compiled for
the old minor fail on it (skate-admin-bot PR #29 proposed CI 3.15 with no cp315 pydantic-core wheel).
`minimumReleaseAge` is deliberately not used: Docker Hub's timestamp is the tag's `tag_last_pushed`,
so a floating `3.N-alpine` tag re-ages on every rebuild and the pair would split again.
