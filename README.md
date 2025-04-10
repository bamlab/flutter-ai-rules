# flutter-ai-rules

**Disclamer:** This is an experimentation for sharing cursor rules between several flutter projects. <br>
We are currently using this repository to iterate on the sharing system and on the rules themselves.

> ⚠ **Important!** Cursor rules currently don't work well in workspace mode : Only the first folder (in alphabetical order) is detected. It should work in most case for the app folder if you name it "Application" (or anything with an "a"), but not for the other repositories of your monorepo <br>
> Source : https://forum.cursor.com/t/cursor-rules-files-for-multi-project-workspace/48086

You have 2 options for fetching the rules in your project:

## Manual download

manually download the `flutter-shared-rules.mdc` file in a `.cursor/rules` folder

> ✅ Simple setup & project management. <br>
> ❌ Need to do it again each time the file is updated, for all your projects.

## Automated fetch

- In the `melos.yaml` file of the project (replace `<app folder>` by your app folder's name):

```
    bootstrap:
        [...]
        hooks:
            post: melos fetch_ai_rules
    [...]
    scripts:
        [...]
        fetch_ai_rules:
            run: |
            curl -L -s https://raw.githubusercontent.com/bamlab/flutter-ai-rules/refs/heads/main/flutter-shared-rules.mdc -o <app folder>/.cursor/rules/shared/flutter-shared-rules.mdc
            description: Fetch AI rules
```

> ✅ Simple setup & project management. <br>
> ✅ Rules are updated at each `melos bootstrap`. <br>

<br>
<br>

---

deprecated

<details>
<summary>
 Automated fetch - if this repository is private
</summary>

- In the project where you want to add the rules (replace `<app folder>` by your app folder's name):

```
git submodule add git@github.com:bamlab/flutter-ai-rules.git <app folder>/.cursor/rules/shared && git submodule update --remote --init -- <app folder>/.cursor/rules/shared && git commit -m "devx(cursor) create cursor rules submodule"
```

- In the `melos.yaml` file of the project (replace `<app folder>` by your app folder's name):

```
    bootstrap:
        [...]
        hooks:
            post: melos fetch_ai_rules
    [...]
    scripts:
        [...]
        fetch_ai_rules:
            run: |
            git submodule update --remote --merge -- <app folder>/.cursor/rules/shared
            description: Fetch AI rules
```

> ✅ Rules are updated at each `melos bootstrap`. <br>
> ❌ Every dev on the project must have access to this repo, or will see some error after running `melos bootstrap`. <br>
> 🟠 When committing the rules changes on the project, the commit is unreadable. Nevertheless, this change has already been reviewed on this repository<br>

> 💡 If you want to interact manually with the submodule, be aware that git submodules badly support adding submodules in folders that begin by `.`. If you do so, you must always specify `-- <submodule path>` in your `git submodule` commands. You can also run `cd <submodule path>` and use regular git commands, it will work well. Don't push anything on this rules repository though<br>

> 💡 If you use the "source control" view of vscode, you can see a new section after adding the submodule. You can easily close it with a right click on its header.

### clean this installation

at the root of your project:

- remove the submodule from `.gitmodules`
- remove the submodule from `.git/modules`
  - by default, `.git` is not visible in vscode: open finder and show hidden files (`cmd`+`shift`+`.`)
  </details>
