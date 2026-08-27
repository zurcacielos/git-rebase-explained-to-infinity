# Rebase Workflow Full Lifecycle

This document outlines the complete lifecycle of a feature branch in a rebase-based workflow, from creation to merging. 

For the specific details on how to safely force-push a branch after a rebase, refer to the [Unified Force-Push Workflow](unified-force-push-workflow.md) guide.

## Feature Branch Lifecycle

```mermaid
flowchart TD
    Start((Start)) --> Checkout["Create new branch from development<br>git fetch origin<br>git checkout -b feature-local origin/development"]
    Checkout --> Commit[Make changes and commit<br>git commit]
    Commit --> InitialPush[Initial push to remote<br>git push -u origin feature-local]
    InitialPush --> PR[Open Pull Request for Code Review]
    PR --> Review{Code Review Decision}
    
    Review -- Approved --> Merge[Merge or Rebase into development]
    Merge --> End((End))
    
    Review -- Changes Requested --> MoreCommits[Make requested changes locally<br>git commit]
    MoreCommits --> Fetch[Fetch latest development updates<br>git fetch origin]
    Fetch --> Rebase[Rebase local feature branch<br>git rebase origin/development]
    Rebase --> ForcePush[[Update PR with Force Push<br>🔗 Click here for detailed workflow]]
    ForcePush --> PR
    
    click ForcePush "unified-force-push-workflow.md" "View detailed force-push workflow"
    style ForcePush stroke:#0969da,stroke-width:2px,color:#0969da
```

This diagram provides a high-level view of the process. The most complex step is updating the Pull Request after a rebase (the **Update PR with Force Push** step), because your local history has diverged from the remote history. 

To handle that specific step safely without overwriting your teammates' work, strictly follow the [Unified Force-Push Workflow](unified-force-push-workflow.md).
