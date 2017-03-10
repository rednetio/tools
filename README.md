# Simple git hooks to make your life easier

These simple hooks are a good addition to your project. They can be bypassed using the `--no-verify` option. (i.e. `git push --no-verify`)

### ESLint pre-commit hook

[Pre-commit](scripts/hooks/pre-commit)

```bash
#!/bin/bash

files=$(git --no-pager diff --name-status --cached | grep "\.js")
if [ ${#files} -gt 0 ]
  then
  echo "🕵  A JavaScript file has been modified. Running linter."
  npm run lint || exit 1
fi

exit 0

```

### Pre-push Github pull-request hook

[Pre-push](scripts/hooks/pre-push)

```bash
#!/bin/bash

branch=$(git rev-parse --abbrev-ref HEAD)

if [ "$branch" = "master" -o "$branch" = "develop" ]; then
  >&2 echo "Please do not push on ${branch}, create a branch then open a pull request"
  exit 1
fi

echo -e "Follow this link to create your pull request:\n"
echo -e "    https://github.com/${YOUR_ORGANIZATION}/${YOUR_REPOSITORY}/compare/develop...${branch}\n"

```
