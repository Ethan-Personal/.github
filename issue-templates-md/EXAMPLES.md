# Usage Examples for Issue Templates

This file provides practical examples of how to use the markdown issue templates with various tools.

## 1. GitHub CLI (gh)

### Create an issue directly from template
```bash
# Bug report
gh issue create \
  --repo owner/repo \
  --title "bug: API returns 500 error on invalid input" \
  --body-file issue-templates-md/bug.md \
  --label "type:bug"

# Feature request
gh issue create \
  --repo owner/repo \
  --title "feature: Add dark mode support" \
  --body-file issue-templates-md/feature.md \
  --label "type:feature"

# Task
gh issue create \
  --repo owner/repo \
  --title "task: Implement user authentication" \
  --body-file issue-templates-md/task.md \
  --label "type:task"

# Research
gh issue create \
  --repo owner/repo \
  --title "research: Evaluate database options" \
  --body-file issue-templates-md/research.md \
  --label "type:research"
```

### Interactive mode with template
```bash
# Copy template and edit before creating
cp issue-templates-md/bug.md /tmp/my-bug.md
# Edit /tmp/my-bug.md with your details
gh issue create --repo owner/repo --body-file /tmp/my-bug.md
```

## 2. GitHub API (curl)

### Create a bug report
```bash
curl -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: token YOUR_GITHUB_TOKEN" \
  https://api.github.com/repos/owner/repo/issues \
  -d '{
    "title": "bug: Database connection timeout",
    "body": "'"$(cat issue-templates-md/bug.md)"'",
    "labels": ["type:bug"]
  }'
```

### Create a feature request
```bash
FEATURE_BODY=$(cat issue-templates-md/feature.md)
curl -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: token YOUR_GITHUB_TOKEN" \
  https://api.github.com/repos/owner/repo/issues \
  -d @- <<EOF
{
  "title": "feature: Add OAuth support",
  "body": "$FEATURE_BODY",
  "labels": ["type:feature"]
}
EOF
```

## 3. Raycast (GitHub Extension)

1. Open Raycast (⌘ + Space)
2. Type "Create GitHub Issue"
3. Select your repository
4. Copy the content from one of the markdown templates:
   ```bash
   cat issue-templates-md/bug.md | pbcopy  # macOS
   ```
5. Paste into the issue body field
6. Fill in the sections with your details
7. Submit

## 4. Python Script

```python
import requests
import os

def create_issue(repo, title, template_path, token):
    with open(template_path, 'r') as f:
        body = f.read()
    
    url = f'https://api.github.com/repos/{repo}/issues'
    headers = {
        'Authorization': f'token {token}',
        'Accept': 'application/vnd.github.v3+json'
    }
    data = {
        'title': title,
        'body': body,
        'labels': ['type:bug']
    }
    
    response = requests.post(url, headers=headers, json=data)
    return response.json()

# Usage
token = os.environ['GITHUB_TOKEN']
issue = create_issue(
    'owner/repo',
    'bug: Login page not responsive',
    'issue-templates-md/bug.md',
    token
)
print(f"Created issue #{issue['number']}")
```

## 5. Node.js Script

```javascript
const { Octokit } = require("@octokit/rest");
const fs = require('fs');

async function createIssue(repo, title, templatePath) {
  const octokit = new Octokit({
    auth: process.env.GITHUB_TOKEN
  });
  
  const body = fs.readFileSync(templatePath, 'utf8');
  
  const [owner, repoName] = repo.split('/');
  
  const { data } = await octokit.issues.create({
    owner,
    repo: repoName,
    title,
    body,
    labels: ['type:bug']
  });
  
  return data;
}

// Usage
createIssue('owner/repo', 'bug: Memory leak in worker', 'issue-templates-md/bug.md')
  .then(issue => console.log(`Created issue #${issue.number}`))
  .catch(error => console.error(error));
```

## 6. Bash Script Helper

Create a reusable script:

```bash
#!/bin/bash
# create-issue.sh

REPO=$1
TYPE=$2
TITLE=$3
TEMPLATE_DIR="issue-templates-md"

if [ -z "$REPO" ] || [ -z "$TYPE" ] || [ -z "$TITLE" ]; then
  echo "Usage: ./create-issue.sh owner/repo <bug|feature|task|research> 'Issue title'"
  exit 1
fi

TEMPLATE_FILE="$TEMPLATE_DIR/$TYPE.md"

if [ ! -f "$TEMPLATE_FILE" ]; then
  echo "Error: Template $TEMPLATE_FILE not found"
  exit 1
fi

gh issue create \
  --repo "$REPO" \
  --title "$TYPE: $TITLE" \
  --body-file "$TEMPLATE_FILE" \
  --label "type:$TYPE"
```

Usage:
```bash
chmod +x create-issue.sh
./create-issue.sh owner/repo bug "Login fails with special characters"
./create-issue.sh owner/repo feature "Add export to PDF"
```

## Tips

1. **Fill out templates locally first**: Copy the template, fill it out in your editor, then create the issue
2. **Use environment variables**: Store your GitHub token in `GITHUB_TOKEN` environment variable
3. **Customize labels**: Adjust the labels in the commands to match your repository's label scheme
4. **Batch creation**: Loop through templates to create multiple issues at once
5. **Version control templates**: Keep these templates in a shared location for your team

## Template Front Matter

Each markdown template includes front matter (the section between `---`):
- `name`: Display name of the template
- `about`: Description of when to use it
- `title`: Prefix for the issue title
- `labels`: Default labels to apply

These can be parsed programmatically or used as reference when creating issues manually.
