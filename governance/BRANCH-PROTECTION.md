# Branch Protection Rules

This document outlines recommended branch protection rules for the Universal Manifest repository to ensure code quality, security, and stability.

## Main Branch Protection

The `main` branch should be protected with the following rules to prevent direct commits and ensure all changes go through proper review.

### Required Settings

#### 1. Require Pull Request Reviews

- **Require pull request reviews before merging**: Enabled
- **Required number of approvals**: 1 minimum (2+ recommended for production)
- **Dismiss stale pull request approvals when new commits are pushed**: Enabled
- **Require review from Code Owners**: Enabled (if CODEOWNERS file exists)

#### 2. Require Status Checks

**Require status checks to pass before merging**: Enabled

**Required status checks** (must pass):
- `test` - Run tests from packages/universal-manifest
- `terminology` - Check terminology consistency
- `build-site` - Build documentation site

**Status checks settings**:
- **Require branches to be up to date before merging**: Enabled
  - This ensures PRs are tested against the latest main branch

#### 3. Require Conversation Resolution

- **Require conversation resolution before merging**: Enabled
  - All review comments must be resolved before merge

#### 4. Require Signed Commits (Optional but Recommended)

- **Require signed commits**: Enabled
  - Ensures commit authenticity via GPG/SSH signatures

#### 5. Additional Protection Rules

- **Require linear history**: Enabled (Optional)
  - Prevents merge commits, enforces rebase or squash

- **Do not allow bypassing the above settings**: Enabled
  - Administrators must follow the same rules

- **Restrict who can push to matching branches**: Enabled
  - Only specific users/teams can push directly (in emergency cases)

- **Allow force pushes**: Disabled
  - Prevents history rewriting on main branch

- **Allow deletions**: Disabled
  - Prevents accidental deletion of main branch

## How to Configure

### Via GitHub Web UI

1. Navigate to **Settings** → **Branches**
2. Click **Add branch protection rule**
3. Enter branch name pattern: `main`
4. Configure settings as outlined above
5. Click **Create** or **Save changes**

### Via GitHub CLI

```bash
# Requires gh CLI and appropriate permissions
gh api repos/:owner/:repo/branches/main/protection \
  --method PUT \
  --input branch-protection-config.json
```

Example `branch-protection-config.json`:

```json
{
  "required_status_checks": {
    "strict": true,
    "contexts": ["test", "terminology", "build-site"]
  },
  "enforce_admins": true,
  "required_pull_request_reviews": {
    "dismissal_restrictions": {},
    "dismiss_stale_reviews": true,
    "require_code_owner_reviews": true,
    "required_approving_review_count": 1
  },
  "restrictions": null,
  "required_signatures": true,
  "allow_force_pushes": false,
  "allow_deletions": false,
  "required_conversation_resolution": true,
  "required_linear_history": true
}
```

## CI/CD Integration

The branch protection rules are designed to work with the CI/CD pipeline defined in `.github/workflows/ci.yml`.

### Status Checks

The following jobs must complete successfully:

1. **test**: Validates the core package functionality
   - Runs `npm test` in `packages/universal-manifest/`
   - Includes build and example validation

2. **terminology**: Ensures terminology consistency
   - Runs `npm run check:terminology` in `packages/universal-manifest/`
   - Validates spec terminology usage

3. **build-site**: Verifies documentation site builds
   - Runs `npm run build:clean` in `site/`
   - Ensures all Astro content is valid

### Additional Checks (Main Branch Only)

4. **smoke-endpoints-prod**: Production endpoint verification
   - Only runs on `main` branch after merge
   - Validates live endpoints are functioning
   - Does not block merges (runs post-merge)

## Development Workflow

With these protections in place, the typical workflow is:

1. **Create feature branch** from `main`
   ```bash
   git checkout -b feature/my-feature
   ```

2. **Make changes and commit**
   ```bash
   git add .
   git commit -m "feat: add new feature"
   ```

3. **Push to GitHub**
   ```bash
   git push origin feature/my-feature
   ```

4. **Create Pull Request**
   - Use the PR template to describe changes
   - CI checks will run automatically

5. **Address review feedback**
   - Make requested changes
   - Push additional commits
   - Resolve all conversations

6. **Ensure CI passes**
   - All required status checks must be green
   - Branch must be up to date with main

7. **Merge**
   - Once approved and checks pass, merge the PR
   - Main branch protections prevent premature merges

## Emergency Procedures

In rare cases where main branch protection needs to be temporarily bypassed:

1. **Document the reason** in an issue or incident report
2. **Notify the team** before making changes
3. **Re-enable protections** immediately after the emergency fix
4. **Create a follow-up PR** to properly review the emergency changes

## Additional Resources

- [GitHub Branch Protection Documentation](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches)
- [GitHub Status Checks](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/collaborating-on-repositories-with-code-quality-features/about-status-checks)
- [Signed Commits](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification)

## Changelog

- **2026-02-27**: Initial branch protection guidelines created
