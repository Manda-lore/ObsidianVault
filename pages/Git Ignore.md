# How to add .gitignore after its too late
If `.obsidian` is already being tracked by Git, adding it to `.gitignore` is not enough. Remove it from the Git index while keeping it on disk:

```
git rm -r --cached .obsidian
git commit -m "Stop tracking .obsidian"
```