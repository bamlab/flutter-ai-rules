# flutter-ai-rules

## How to use

> ⚠ Important! Cursor rules currently don't work well in workspace mode : Only the first folder (in alphabetical order) is detected. It should work in most case for the app folder if you name it "Application" (or anything with an "a"), but not for the other repositories of your monorepo <br>
> Source : https://forum.cursor.com/t/cursor-rules-files-for-multi-project-workspace/48086

You have 2 options:

### Manual download

manually download the `flutter-shared-rules.mdc` file in a `.cursor/rules` folder

> ✅ Simple setup & project management <br>
> ❌ Need to do it again each time the file is updated, for all your projects

### Automated fetch

- In the project where you want to add the rules:

```
git submodule add --force git@github.com:bamlab/flutter-ai-rules.git .fdme/cursor/rules/shared && git submodule update --remote --init -- .cursor/rules/shared
```

- In the melos file of the project:

```

...
    scripts:
        ...
        fetch_ai_rules:
            exec: |
            git submodule update --merge -- .cursor/rules/shared
            description: Fetch AI rules
```

> ✅ Rules are updated at each `melos bootstrap` <br>
> ❌ Every dev on the project must have access to this repo <br>
> ❌ When committing the rules changes, the commit is unreadable <br>
> ❌ git submodules badly support adding submodules in folders that begin by `.`.
