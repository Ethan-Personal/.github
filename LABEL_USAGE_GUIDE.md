# Using Organization Labels in Other Repositories

This guide explains how to use the labels defined in this organization's `.github` repository in your other projects and repositories within the same organization.

## Overview

The `.github/labels.yml` file in this repository contains organization-wide label definitions that can be applied to any repository in the organization. These labels are designed to provide consistency across all projects.

## Available Labels

The organization currently defines the following labels:

### Type Labels (categorize the kind of work)
- `type:bug` - Something is broken or incorrect
- `type:feature` - Parent feature / epic
- `type:task` - Implementation task
- `type:research` - Research or investigation task

### Status Labels (track feature/task lifecycle)
- `status:backlog` - Feature exists but not currently active
- `status:feature-in-progress` - Currently active feature
- `status:done` - Completed (feature or task)
- `status:blocked` - Blocked by unmet dependencies
- `status:ready` - Unblocked and ready to start
- `status:in-progress` - Actively being worked on

### State Labels (archival and visibility)
- `state:archived` - Hidden from active boards but still accessible

## How to Use These Labels in Your Repository

### Method 1: Manual Label Creation via GitHub UI (Simplest)

This is the easiest method and doesn't require any tools or workflows.

1. **Navigate to your target repository** (e.g., FB-Yahoo)
   - Go to `https://github.com/ethankook/FB-Yahoo` (or your repository URL)

2. **Go to the Labels page**
   - Click on "Issues" tab
   - Click on "Labels" button (next to Milestones)
   - Or directly navigate to: `https://github.com/ethankook/FB-Yahoo/labels`

3. **Create each label manually**
   - Click "New label" button
   - Copy the label information from the table above:
     - **Name**: Enter the exact label name (e.g., `type:bug`)
     - **Description**: Enter the label description
     - **Color**: Enter the hex color code (without #)
   - Click "Create label"
   - Repeat for all labels you want to use

**Example for creating the `type:bug` label:**
- Name: `type:bug`
- Description: `Something is broken or incorrect`
- Color: `d73a4a`

### Method 2: Using GitHub CLI (gh)

If you have the GitHub CLI installed, you can create labels more efficiently:

```bash
# Install GitHub CLI if needed
# See: https://cli.github.com/

# Navigate to your target repository directory
cd /path/to/your/FB-Yahoo

# Create labels using gh cli
gh label create "type:bug" --description "Something is broken or incorrect" --color d73a4a
gh label create "type:feature" --description "Parent feature / epic" --color 5319e7
gh label create "type:task" --description "Implementation task" --color 1d76db
gh label create "type:research" --description "Research or investigation task" --color fbca04

gh label create "status:backlog" --description "Feature exists but not currently active" --color cfd3d7
gh label create "status:feature-in-progress" --description "Currently active feature" --color 0052cc
gh label create "status:done" --description "Completed (feature or task)" --color 000000
gh label create "status:blocked" --description "Blocked by unmet dependencies" --color d73a4a
gh label create "status:ready" --description "Unblocked and ready to start" --color 0e8a16
gh label create "status:in-progress" --description "Actively being worked on" --color 0052cc

gh label create "state:archived" --description "Hidden from active boards but still accessible" --color ededed
```

### Method 3: Using GitHub API

You can also use the GitHub REST API to create labels programmatically:

```bash
# Set your variables
GITHUB_TOKEN="your_personal_access_token"
OWNER="ethankook"
REPO="FB-Yahoo"

# Create a label using curl
curl -X POST \
  -H "Authorization: token $GITHUB_TOKEN" \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/repos/$OWNER/$REPO/labels \
  -d '{"name":"type:bug","description":"Something is broken or incorrect","color":"d73a4a"}'
```

### Method 4: Using Label Sync Tools (Advanced)

For managing labels across multiple repositories, you can use label synchronization tools:

#### Option A: github-label-sync (npm package)

```bash
# Install the tool
npm install -g github-label-sync

# Create a labels.json file (converted from labels.yml)
# Or use the labels.yml directly with a converter

# Sync labels to your repository
github-label-sync --access-token $GITHUB_TOKEN --labels .github/labels.yml ethankook/FB-Yahoo
```

#### Option B: git-labelmaker (Ruby gem)

```bash
# Install the tool
gem install git-labelmaker

# Use it to sync labels from the YAML file
git-labelmaker -t $GITHUB_TOKEN -r ethankook/FB-Yahoo .github/labels.yml
```

## Example: Setting Up Labels for FB-Yahoo Repository

Here's a complete step-by-step example for your FB-Yahoo repository:

### Quick Setup (GitHub CLI Method)

```bash
# 1. Clone your FB-Yahoo repository (if not already cloned)
git clone https://github.com/ethankook/FB-Yahoo.git
cd FB-Yahoo

# 2. Run these commands to create all organization labels
gh label create "type:bug" --description "Something is broken or incorrect" --color d73a4a --force
gh label create "type:feature" --description "Parent feature / epic" --color 5319e7 --force
gh label create "type:task" --description "Implementation task" --color 1d76db --force
gh label create "type:research" --description "Research or investigation task" --color fbca04 --force
gh label create "status:backlog" --description "Feature exists but not currently active" --color cfd3d7 --force
gh label create "status:feature-in-progress" --description "Currently active feature" --color 0052cc --force
gh label create "status:done" --description "Completed (feature or task)" --color 000000 --force
gh label create "status:blocked" --description "Blocked by unmet dependencies" --color d73a4a --force
gh label create "status:ready" --description "Unblocked and ready to start" --color 0e8a16 --force
gh label create "status:in-progress" --description "Actively being worked on" --color 0052cc --force
gh label create "state:archived" --description "Hidden from active boards but still accessible" --color ededed --force

# 3. Verify labels were created
gh label list
```

The `--force` flag will update existing labels if they already exist with that name.

## Label Reference Table

For easy copy-paste, here's the complete label information:

| Name | Description | Color Code |
|------|-------------|------------|
| type:bug | Something is broken or incorrect | d73a4a |
| type:feature | Parent feature / epic | 5319e7 |
| type:task | Implementation task | 1d76db |
| type:research | Research or investigation task | fbca04 |
| status:backlog | Feature exists but not currently active | cfd3d7 |
| status:feature-in-progress | Currently active feature | 0052cc |
| status:done | Completed (feature or task) | 000000 |
| status:blocked | Blocked by unmet dependencies | d73a4a |
| status:ready | Unblocked and ready to start | 0e8a16 |
| status:in-progress | Actively being worked on | 0052cc |
| state:archived | Hidden from active boards but still accessible | ededed |

## Best Practices

1. **Consistency**: Use the same label names and colors across all repositories in the organization
2. **Documentation**: Keep this `.github` repository as the source of truth for label definitions
3. **Updates**: When labels change in this repository, manually update them in your other repositories
4. **Default Labels**: Consider deleting GitHub's default labels that don't match your organization's label schema
5. **Automation**: For organizations with many repositories, consider setting up a GitHub Action to automatically sync labels (you can add this later if needed)

## Troubleshooting

### Label Already Exists
If a label with the same name already exists, you can either:
- Delete the old label first
- Use the `--force` flag with GitHub CLI to update it
- Manually edit the existing label in the GitHub UI

### Permission Issues
Make sure you have admin or write access to the repository where you're trying to create labels.

### API Rate Limits
If using the API or CLI tools heavily, be aware of GitHub's rate limits. Authenticated requests have higher limits.

## Additional Resources

- [GitHub Labels Documentation](https://docs.github.com/en/issues/using-labels-and-milestones-to-track-work/managing-labels)
- [GitHub CLI Documentation](https://cli.github.com/manual/gh_label)
- [GitHub REST API - Labels](https://docs.github.com/en/rest/issues/labels)

## Need Help?

If you encounter issues or need help setting up labels in your repository, please open an issue in this `.github` repository.
