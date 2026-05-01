# Contributing to Sphinx Stack documentation

The Sphinx Stack is a shared foundation for Sphinx documentation projects, and
contributions help improve the documentation of all its users. The Documentation
Practice team performs most of the work, but all contributors are welcome.

Common contributions include:

- Bug fixes: Build errors, broken links, configuration issues
- Improvements: Better defaults, new extensions, workflow enhancements, new or improved
  style rules
- Dependency updates: Security patches, compatibility fixes, better tooling

If you run into any problems or see room for improvement, we encourage you to open an
issue or even contribute a fix.

> This guide only covers contributions to documentation. If you're interested in
> contributing to Sphinx Stack development, refer to the [main repository's
> guide](https://github.com/canonical/sphinx-stack/blob/main/CONTRIBUTING.md).

## Review the project expectations

Review these three documents before contributing:

### Ubuntu Code of Conduct

When contributing, you must abide by the [Ubuntu Code of
Conduct](https://ubuntu.com/community/ethos/code-of-conduct). Projects governed by
Canonical expect good conduct and excellence from every member.

### Canonical Contributor License Agreement

Code contributions can only be accepted from contributors who have signed our
[Contributor License Agreement (CLA)](https://ubuntu.com/legal/contributors). Signing
the agreement grants Canonical permission to use your contributions, and you remain the
copyright owner of your work (no copyright assignment occurs).

Review the terms of the agreement before signing it or committing anything. If you agree
and choose to sign it, your work can be incorporated into the repository.

### Open source license

The Sphinx Stack is licensed under [CC-BY-SA-3.0](LICENSE).

## Report an issue or open a request

If you find a bug or feature gap in the Sphinx Stack docs, look for it in the [project's
GitHub issues](https://github.com/canonical/sphinx-stack-docs/issues) first. Add
your voice to the thread if you have fresh input.

If the bug or feature doesn't have an issue, [open
one](https://github.com/canonical/sphinx-stack-docs/issues/new/choose).

## Development setup

Create a [personal fork](https://github.com/canonical/sphinx-stack-docs/fork) of
the repository, then clone it and add the upstream remote:

With
[SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account):

```bash
git clone git@github.com:<username>/sphinx-stack-docs
cd sphinx-stack-docs
git remote add upstream git@github.com:canonical/sphinx-stack-docs
git fetch upstream
```

With
[HTTPS](https://docs.github.com/en/get-started/git-basics/about-remote-repositories#cloning-with-https-urls):

```bash
git clone https://github.com/<username>/sphinx-stack-docs
cd sphinx-stack-docs
git remote add upstream https://github.com/canonical/sphinx-stack-docs
git fetch upstream
```

Install dependencies and verify the build:

```bash
cd docs
make install
make html
```

## Contribute a change

### Research the topic

All significant work should be tied to an existing issue. Before starting, comment on
the issue to have it assigned to you.

#### Minor changes

Check [GitHub issues](https://github.com/canonical/sphinx-stack-docs/issues) for
existing reports. If none exist, [open
one](https://github.com/canonical/sphinx-stack-docs/issues/new/choose) and state
your interest in working on it.

#### Major changes

Describe your proposal in the issue thread, including page's
[Diátaxis](https://diataxis.fr) category and structure.

### Create a development branch

Sync and create a new branch:

```bash
git fetch upstream
git checkout -b <new-branch-name>
```

Name your branch `<ticket-id>-<description>` (e.g., `issue-235-add-setup-guide`),
keeping it under 80 characters.

### Make your changes

Follow these guidelines:

- Use separate commits for each logical change, and for changes to different components
- Keep the Sphinx Stack minimal by default; optional features are best implemented
  by the projects using the Sphinx Stack rather than the Sphinx Stack itself

### Commit a change

```bash
git add -A
git commit
```

Use [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) format:

```
docs: add initial setup guide
```

To determine the commit type, check the file history with `git log --oneline <filename>`.

> **Tip**
>
> If you're unsure which type to use, the commit may be doing too much, so split it into
> smaller commits instead. Select the highest-ranked type that fits:
>
> - `ci`
> - `build`
> - `feat`
> - `fix`
> - `perf`
> - `refactor`
> - `style`
> - `test`
> - `docs`
> - `chore`

### Sign your commits

All commits require cryptographic signatures ([DCO
1.1](https://developercertificate.org/)). You can sign commits by adding `-S` to the
`git commit` command from the previous section, for example:

```bash
git commit -S -m "docs: add initial setup guide"
```

Signed commits display a "Verified" badge in GitHub. Set up signing via [GitHub Docs -
About commit signature
verification](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification).

> **Tip**
>
> You can configure your Git client to sign commits by default for any local repository
> by running `git config --global commit.gpgsign true`. Once you have done this, you no
> longer need to add `-S` to your commits explicitly.
>
> See [GitHub Docs - Signing commits](https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-commits) for more information.

If you've made an unsigned commit and encounter the "Commits must have verified
signatures" error when pushing your changes to the remote:

1. Amend the most recent commit by signing it without changing the commit message, and
   push again:

   ```bash
   git commit --amend --no-edit -n -S
   git push
   ```

2. If you still encounter the same error, confirm that your GitHub account has been set
   up properly to sign commits as described in the [GitHub Docs - About commit signature
   verification](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification).

   > **Tip**
   >
   > If you use SSH keys to sign your commits, make sure to add a "Signing Key" type in
   > your GitHub account. See [GitHub Docs - Adding a new SSH key to your
   > account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
   > for more information.

### Test the change

Build and run the checks locally before submitting:

```bash
cd docs
make html
```

```bash
make spelling      # Check spelling
make linkcheck     # Validate links
make woke          # Check inclusive language
make lint-md       # Check Markdown style
make vale          # Check style guide compliance (optional)
```

To preview locally with live reload at `http://127.0.0.1:8000`, run:

```bash
make run
```

### Push the branch and open a PR

```bash
git push -u origin <branch-name>
```

Next, open a PR on GitHub. Format its title as a conventional commit (GitHub may do this
automatically for single-commit branches).

### Describing PRs

Your PR should include the following details:

- Title: Short, descriptive summary
- Description: Problem solved, features added, or bugs fixed
- Relevant issues: [Link related issues and PRs](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/autolinked-references-and-urls)

## CI/CD pipeline

The repository configures multiple automated checks. Some are conditional based on
target branch or changed files.

If a check fails, review the logs for remediation guidance. For failures unrelated to
your changes, rebase against the latest base branch.

### Checks on all PRs

These run on every PR and on pushes to `main`:

- Documentation build: Builds the documentation and checks for errors
- Spelling check: Verifies spelling using Vale
- Link check: Validates all links in the documentation
- Inclusive language check: Runs woke to check for non-inclusive language
- Python dependency build: Verifies dependencies can be built from source

### Checks on PRs to `main` only

- CLA check: Verifies you have signed the Canonical Contributor License Agreement
- Removed URLs check: Detects if any URLs were removed without redirects

#### CLA check in CI

When you open a pull request (PR) against the `main` branch, a mandatory automated check
verifies that you have signed the CLA. It uses the
[canonical/has-signed-canonical-cla](https://github.com/canonical/has-signed-canonical-cla)
GitHub Action.

If you haven't signed the CLA:
1. The check will fail with a message indicating the CLA requirement
2. Visit <https://ubuntu.com/legal/contributors> to review and sign the agreement
3. Once signed, re-run the check if you have permissions, or ask a maintainer to do so.
   Pushing a new commit also triggers re-evaluation.

The CLA check only runs on PRs to `main`. Internal team members working on other
branches should ensure they have signed the CLA before their changes are merged to
`main`.

### Optional checks (allowed to fail)

- Style guide check (`vale`): Checks compliance with the Canonical style guide
- Accessibility check (`pa11y`): Checks accessibility of generated HTML

## Review process

PRs are typically reviewed within a week.

### Responding to feedback

Push additional commits to address feedback (commit locally rather than via GitHub UI to
avoid sync conflicts).

Rebase your branch before requesting a review to keep your commits clean. Once review
has started, avoid rebasing to maintain the review history and make it easier for
reviewers to see what changed.

### Common feedback themes

Reviewers may request:

- Wording, terminology, or formatting changes
- Consistency with existing patterns
- Proper reST or MyST markup style
- Cross-references: Use proper reST or MyST syntax
- Examples: Start minimal, then show options; include verification steps
