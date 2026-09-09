---
description: Create an issue in the backlog platform (GitHub, Azure DevOps, Jira) from a description.
---

Backlog platform is set in `.opencode/harness.json` → `platform.backlog`. The platform-specific content below is injected by the CLI during onboarding.

Input: `$ARGUMENTS` (the issue title/description)

<!-- PC-PLATFORM-BACKLOG-START -->
GitHub data comes from the `gh` CLI; a page fetch of github.com is denied (pc-system-reminders). If `gh` is unavailable, report it as a blocker.
Always pass `--repo {owner}/{repo}` explicitly, never rely on git context to resolve the repo.

---

### Step 1: Parse input

`$ARGUMENTS` is the issue title/description. If it contains a title and body separated by a newline or `---`, split them. Otherwise use the full text as the title with an empty body.

### Step 2: Create issue

```bash
gh issue create \
  --repo {owner}/{repo} \
  --title "{title}" \
  --body "{body}"
```

### Step 3: Report

```text
Issue created
  URL: {issue-url}
  Number: #{number}
  Title: {title}
```

Tell the user: "Use `/plan-propose {issue-url}` to turn this into a plan."

---
<!-- PC-PLATFORM-BACKLOG-END -->
