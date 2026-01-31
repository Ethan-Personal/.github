# Quick Reference Card

Use this as a quick reference for creating issues with the markdown templates.

## One-Line Commands

### GitHub CLI
```bash
# Bug
gh issue create --repo OWNER/REPO --title "bug: TITLE" --body-file issue-templates-md/bug.md --label "type:bug"

# Feature  
gh issue create --repo OWNER/REPO --title "feature: TITLE" --body-file issue-templates-md/feature.md --label "type:feature"

# Research
gh issue create --repo OWNER/REPO --title "research: TITLE" --body-file issue-templates-md/research.md --label "type:research"

# Task
gh issue create --repo OWNER/REPO --title "task: TITLE" --body-file issue-templates-md/task.md --label "type:task"
```

## Copy to Clipboard (for Raycast/Manual Use)

### macOS
```bash
cat issue-templates-md/bug.md | pbcopy       # Bug
cat issue-templates-md/feature.md | pbcopy   # Feature
cat issue-templates-md/research.md | pbcopy  # Research
cat issue-templates-md/task.md | pbcopy      # Task
```

### Linux
```bash
cat issue-templates-md/bug.md | xclip -selection clipboard       # Bug
cat issue-templates-md/feature.md | xclip -selection clipboard   # Feature
cat issue-templates-md/research.md | xclip -selection clipboard  # Research
cat issue-templates-md/task.md | xclip -selection clipboard      # Task
```

### Windows (PowerShell)
```powershell
Get-Content issue-templates-md\bug.md | Set-Clipboard       # Bug
Get-Content issue-templates-md\feature.md | Set-Clipboard   # Feature
Get-Content issue-templates-md\research.md | Set-Clipboard  # Research
Get-Content issue-templates-md\task.md | Set-Clipboard      # Task
```

## Template Locations

All templates are in the `issue-templates-md/` directory:
- `bug.md` - For reporting bugs and defects
- `feature.md` - For new features (parent issues)
- `research.md` - For investigation tasks
- `task.md` - For implementation work items

## See Also

- [README.md](README.md) - Full documentation with usage instructions
- [EXAMPLES.md](EXAMPLES.md) - Detailed examples for various tools
- [../README.md](../README.md) - Information about the repository structure
