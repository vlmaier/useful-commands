# Useful commands

List of useful commands I looked for, found and figured I'll definitely need them again later.

## Git


#### Top 10 touched files in a git repository (by a specific author)

```
git log --author="AUTHOR_NAME" --pretty=format: --name-only | sort | uniq -c | sort -rg | head -10
```
