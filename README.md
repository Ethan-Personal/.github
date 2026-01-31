# .github

This is a special GitHub repository that provides organization-wide defaults for issue templates, pull request templates, and other GitHub configurations.

## Repository Structure

This repository is named `.github` (the repository name itself), and it contains a `.github` directory inside it. This might seem like a nested structure, but it's actually the correct setup:

- **Repository name**: `.github` (special GitHub repository for org-wide defaults)
- **Directory inside**: `.github/` (required directory for GitHub templates and configurations)

This is how GitHub expects organization-wide defaults to be structured. When you create a repository named `.github` in your organization, GitHub automatically uses the templates defined in the `.github/` directory within it as defaults for all repositories in the organization.

## Contents

### Issue Templates

Located in `.github/ISSUE_TEMPLATE/`:

**Web UI Issue Forms (YAML):**
- **bug.yml** - Bug report form
- **feature.yml** - Feature request form  
- **research.yml** - Research task form
- **task.yml** - Implementation task form
- **config.yml** - Issue template chooser configuration

**Markdown Templates (for CLI/Raycast/API):**
- **bug.md** - Bug report template
- **feature.md** - Feature request template
- **research.md** - Research task template
- **task.md** - Implementation task template

The markdown versions are designed for use with GitHub CLI, API, Raycast, and other third-party tools that don't support YAML issue forms.

**Usage Example (GitHub CLI):**
```bash
gh issue create --repo owner/repo --title "bug: Issue title" --body-file .github/ISSUE_TEMPLATE/bug.md --label "type:bug"
```

### Pull Request Template

Located at `.github/pull_request_template.md` - Default template for all pull requests in the organization.

## Why This Structure?

GitHub's special `.github` repository requires:
1. The repository to be named `.github`
2. Templates to be in a `.github/` directory within the repository
3. This creates the appearance of nesting, but it's the expected structure

For more information, see [GitHub's documentation on creating a default community health file](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file).