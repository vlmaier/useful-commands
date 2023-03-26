# Useful commands

List of useful commands I looked for, found and figured I'll definitely need them again later.

## Shell

### Image processing

#### Resize PNG image and convert it to base64 format for HTML

```shell
FILE="YOUR_FILE.png" && sips -Z 32 $FILE && echo "data:image/png;base64,$(cat $FILE | base64)" | pbcopy
```

## Git

### Daily Work

#### View changes about to be committed

```shell
git diff --cached
```

* w/o `--cached` the diff of **ANY** changes is shown

#### Show incoming changes w/o creating a merge conflict

```shell
git log -p HEAD..FETCH_HEAD
```

### Statistics

#### Top 10 touched files in a git repository (by a specific author)

```shell
git log --author="vlmaier" --pretty=format: --name-only | sort | uniq -c | sort -rg | head -10
```

### Refactoring

#### Replace author email in commits

```shell
git filter-branch --env-filter '
WRONG_EMAIL="..."
NEW_NAME="..."
NEW_EMAIL="..."

if [ "$GIT_COMMITTER_EMAIL" = "$WRONG_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$NEW_NAME"
    export GIT_COMMITTER_EMAIL="$NEW_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$WRONG_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$NEW_NAME"
    export GIT_AUTHOR_EMAIL="$NEW_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```

### Forensics

#### View project history w/ diffs at each step

```shell
git log -p
```

#### Search for all occurrences of "..." in any files

```shell
git grep "..."
```

* specify a commit hash after "..." to be more specific

#### Browse any commits from the last 2 weeks modified files under the . directory

```shell
git log --since="2 weeks ago" .
```

#### Show file for a particular version

```shell
git show [commit|tag]:filename
```

#### Show all commits since a specific commit | tag

```shell
git log [commit|tag]..
```

#### Show any changes matching the string "..."

```shell
git log -p -S '...'
```

#### Get set of patches between two versions

```shell
git format-patch main..feature/test
```

#### Show number of commits since it diverged from origin

```shell
git log origin..origin/feature/test | wc -l
```

#### Show reflog entries for a branch

```shell
git log --walk-reflogs branch
```

* reflog history is only available for the **LOCAL** repository

## Maven

#### Check for new dependency updates

```shell
mvn versions:display-dependency-updates  
```
