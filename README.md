# gclone

A zsh script for efficiently cloning your GitHub repositories with smart handling of conflicts and directory management.

## Introduction

`gclone` simplifies the process of cloning your own GitHub repositories while enforcing a consistent directory structure. The script:

- Verifies you're in the proper directory structure (`/<path>/github/<your-username>/`)
- Uses your current directory name as your GitHub username
- Validates repository existence before attempting to clone
- Intelligently handles existing directories by offering to:
  - Move them to trash (if [trash](https://hasseg.org/trash/) command is available)
  - Delete them permanently (if trash is unavailable)
  - Rename them with a timestamp, appends: `YYYYMMDD.HHMMSS`
- Provides clear error messages and usage information

## Installation

1. Download the script:
   ```bash
   curl -LO https://raw.githubusercontent.com/jftuga/gclone/main/gclone
   ```

2. Make it executable:
   ```bash
   chmod 755 gclone
   ```

3. Place it in your PATH (e.g., `/usr/local/bin/` or `~/bin/`):
   ```bash
   mv gclone ~/bin/
   ```

## Usage Output

```
Usage: gclone [repo-name]
This will then clone: https://github.com/<your-username>/repo-name
```

## Example

```bash
# First, navigate to your GitHub username directory
cd ~/github/jftuga/

# Clone one of your repositories
gclone awesome-project
```

## Directory Structure

`gclone` expects a specific directory structure:

```
/<path>/github/<your-github-username>/
```

For example:
```
/home/john/github/jftuga/
```

The script uses your current directory name (`jftuga` in this example) as your GitHub username when forming the clone URL.

## Demo Shell Session

```bash
$ cd ~/github/jftuga/
$ gclone gclone

# If the directory already exists
Folder already exists: gclone

Move to trash? (y/N) n
Skipped removal.
Rename to gclone--20250307.143010? (y/N) y
Renamed to: gclone--20250307.143010

git clone https://github.com/jftuga/gclone
Cloning into 'gclone'...
remote: Enumerating objects: 15, done.
remote: Counting objects: 100% (15/15), done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 15 (delta 2), reused 15 (delta 2), pack-reused 0
Receiving objects: 100% (15/15), done.
Resolving deltas: 100% (2/2), done.
```

## Features

- **Smart Conflict Resolution**: Offers to trash, delete, or rename existing directories
- **Repository Validation**: Checks if repositories exist before attempting to clone
- **Platform Compatibility**: Works on both macOS and Linux
- **Trash Integration**: Uses the [trash](https://formulae.brew.sh/formula/trash) command if available instead of permanent deletion
- **Safe Defaults**: Requires explicit confirmation for potentially destructive operations

## Requirements

- zsh shell
- git
- curl (for repository existence verification)
- Optional: `trash` command for safer directory removal

## Customization

You can modify the `GITHUB_CONTAINER_PATH` variable in the script if your GitHub projects are organized under a different directory name than "github".

```bash
# Change this to match your directory structure preference
GITHUB_CONTAINER_PATH="github"
```
