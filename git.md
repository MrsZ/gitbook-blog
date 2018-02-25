# Remove commits

```bash
git reset --hard HEAD~1
```

The HEAD~1 means the commit before head.

push时需要加`-f`强行push

# delete branch

delete remote branch

```bash
git push origin --delete <your_branch>
```

delete local branch

```bash
git branch -D <branch_name>
```

# set remote url

```bash
git remote set-url origin https://github.com/USERNAME/REPOSITORY.git
```

添加新的url

```bash
git remote set-url --add [--push] <name> <newurl>
```

{% gist id="https://gist.github.com/SamyPesse/6ceb8cb8d531ffab75f0" %}{% endgist %}





