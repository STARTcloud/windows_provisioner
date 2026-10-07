# Notifications

Cross-repo notes for whoever works in this repository. An item appears
here when another repository's change needs a step in this one, names
that step and the file that settles it, and leaves when the step lands.
Read every file named in any item in full before acting on it.

## Adopt the markdown lint and format tooling

`startcloud-ui` gates documentation formatting in CI. `moonshine_roles` has
adopted the same tooling, and every `*_roles` and `*_provisioner` repository
is to follow so the estate stays convergent.

What to add, copied from `startcloud-ui`:

- `.markdownlint.json` — editor-side rules; `MD013` and `MD041` off, `MD033`
  limited to `div p em ul li a img style`.
- `.prettierrc` — printWidth 100, tabWidth 2, single quotes, `endOfLine: auto`.
- `.prettierignore` — must exclude `CHANGELOG.md`, `LICENSE.md` and every
  Ansible-owned path in the repository. Prettier reformats YAML, and that
  would fight `ansible-lint` and `yamllint`; it also rewraps the licence
  text. Only the hand-written markdown is meant to be gated here.

What to change in CI:

- Add a `format` job named `Lint & Format` to `.github/workflows/lint.yml`,
  before the existing lint job: checkout, `actions/setup-node@v7` with
  `node-version: '22'`, then `npx --yes prettier --check .`. No
  `package.json` and no `npm ci` — these repositories carry no Node manifest.

The reference implementation is `moonshine_roles`; `startcloud-ui` is the
origin of the three dotfiles.

`notifications.md` itself is never committed — add it to `.gitignore` and
delete the file once the item above has landed.
