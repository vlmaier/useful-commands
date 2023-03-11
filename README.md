# Useful commands

List of useful commands I looked for, found and figured I'll definitely need them again later.

## Git


#### Top 10 touched files in a git repository (by a specific author)

```shell
git log --author="vlmaier" --pretty=format: --name-only | sort | uniq -c | sort -rg | head -10
```

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

## Maven

#### Check for new dependency updates

```shell
mvn versions:display-dependency-updates  
```
