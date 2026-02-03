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


### Pull Request Template

Located at `.github/pull_request_template.md` - Default template for all pull requests in the organization.

### Labels

Located at `.github/labels.yml` - Organization-wide label definitions that can be synced across repositories using label management tools.

**Type Labels** (categorize the kind of work):
- **type:bug** - Something is broken or incorrect
- **type:feature** - Parent feature / epic
- **type:task** - Implementation task
- **type:research** - Research or investigation task

**Status Labels** (track feature/task lifecycle):
- **status:backlog** - Feature exists but not currently active
- **status:feature-in-progress** - Currently active feature
- **status:done** - Completed (feature or task)
- **status:blocked** - Blocked by unmet dependencies
- **status:ready** - Unblocked and ready to start
- **status:in-progress** - Actively being worked on

**State Labels** (archival and visibility):
- **state:archived** - Hidden from active boards but still accessible

## Why This Structure?

GitHub's special `.github` repository requires:
1. The repository to be named `.github`
2. Templates to be in a `.github/` directory within the repository
3. This creates the appearance of nesting, but it's the expected structure

For more information, see [GitHub's documentation on creating a default community health file](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file).
