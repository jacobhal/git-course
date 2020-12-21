# Git Hooks

Git Hooks are executable scripts that can be executed before or after certain Git events. For instance, before creation of a commit message, or before pushing to remote etc.

> Git Hooks reference: https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks

## Git Hooks in practice

These are some ways that Git Hooks can be used:

- Verify commit message format or edit the commit messages
- Run application tests before each commit or before pushing to remote
- Verify and potentially fix code syntax mistakes using linters like ESLint, Pylint
- Generate notifications after successfully committing
- Deploy updated application to production on the server

## How to create Git Hooks

There are some default samples of Git Hooks whenever you create a Git repository. These can be found in the .git/hooks folder. However, they are all disabled by default.

> In order to enable any of the git hooks samples (or create your own), simply remove the ".sample" file extension.

NOTE: Make sure that any Git hooks have executable permissions "x" when you type `la -la .git/hooks` in the terminal. This includes users, group users and users from other groups.

> The Git hooks samples are executed by sh-shell but can be modified by changing the first line.

## The pre-commit library

There are several libraries that share already created Git Hooks. One very popular Git repository is the pre-commit repository.

Using some of the already defined hooks there can increase productivity and will not affect anyone else on your team since those are only local.

Documentation: https://github.com/pre-commit/pre-commit-hooks

> Adding the pre-commit npm package as a dev dependency allows you to share Git hooks settings for the entire team. For instance, you could specify a set of tests to run in your package.json file.

## The Husky library

This is one of the most popular npm packages for predefined Git hooks that you can use.

It works similar to the pre-commit library but has much more features.

Documentation: https://typicode.github.io/husky/#/

Here is an example of using Husky to run linting and jest tests before accepting a commit:

```JSON
"scripts": {
    "test": "jest",
    "lint": "eslint src/**"
},
"husky": {
    "hooks": {
        "pre-commit": "npm run lint && npm test"
    }
}
```

> `npm test` is a shorthand version for `npm run test`.

## The lint-staged library

This is another popular npm package for predefined hooks. This one specializes on running linting on only staged files and allows you to do extra things like running prettier on the files that fail.

Documentation: https://github.com/okonet/lint-staged

Here is an example of using lint-staged with Husky to run linting and jest tests + prettier on changed files only before accepting a commit:

```JSON
"scripts": {
    "test": "jest",
    "lint": "eslint src/**",
    "lint-fix": "eslint src/** --fix"
},
"husky": {
    "hooks": {
        "pre-commit": "lint-staged"
    }
},
"lint-staged": {
    "*.js": [
        "eslint",
        "jest -findRelatedTests",
        "prettier --write"
    ]
}
```

> `eslint --fix` tries to correct linting errors automatically.

## The commitlint library

If you want to have rules for commits, the commitlint library is a great option.

Documenation: https://github.com/conventional-changelog/commitlint

## Client-Side Hooks

Most Git hooks are local to your repository, called client-side hooks.

### Committing-Workflow Hooks

#### pre-commit hook

This is a simple hook that runs python unit tests before committing.

```sh
#!/bin/sh
current_branch=`git branch | grep '*' | sed 's/* //'`

if [ "$current_branch" = "master" ]; then
    echo "You are about to commit on master. I will run your tests first..."
    python -m unittest discover tests
    if [ $? -eq 0 ]; then
        # tests passed, proceed to prepare commit message
        exit 0
    else
        # some tests failed, prevent from committing broken code on master
        echo "Some tests failed. You are not allowed to commit broken code on master! Aborting the commit."
        echo "Note: you can still commit broken code on feature branches"
        exit 1
    fi
fi
```

NOTE: The hook can be skipped if you include the `--no-verify` option with the commit command.

#### prepare-commit-msg hook

TODO

#### commit-msg hook

TODO

#### post-commit hook

TODO

### Other Client Hooks

## pre-rebase hook

TODO

## Server-Side Hooks

TODO

Some hooks can also be created server-side and will be shared for everyone working in the repository.

### pre-receive hook

TODO

### update hook

TODO

### post-receive hook

TODO
