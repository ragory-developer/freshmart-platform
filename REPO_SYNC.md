# Freshmart Multi-Repo Sync

This project is split into two independent repos:

- `freshmart-api` -> `https://github.com/ragory-developer/freshmart-api.git`
- `freshmart-web` -> `https://github.com/ragory-developer/freshmart-web.git`

The parent folder tracks both repos as submodules. Each child repo keeps its own
history, and the parent repo records which API commit and web commit belong
together.

## First-Time Setup

The two child repos currently need an initial commit before the parent can track
their exact commit pointers.

From this folder:

```powershell
.\push-all.ps1 -Message "Initial Freshmart project"
```

If this parent folder is not a Git repo yet, the script will push the child repos
and then print the parent setup commands.

## Daily Workflow

Make changes in `freshmart-api`, `freshmart-web`, or both, then run:

```powershell
.\push-all.ps1 -Message "Describe your update"
```

The script will:

1. Commit and push changed files in `freshmart-api`.
2. Commit and push changed files in `freshmart-web`.
3. If the parent folder is a Git repo, commit and push the updated submodule
   pointers.

## Clone Later

Clone the parent project with:

```powershell
git clone --recurse-submodules <your-parent-repo-url>
```

If you already cloned it without submodules:

```powershell
git submodule update --init --recursive
```
