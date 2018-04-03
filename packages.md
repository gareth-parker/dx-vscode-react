# Linting and Code Quality

## eslint

.eslintrc file (extends 'react-app' for CRA projects)

```
{
  "extends": ["react-app"]
}
```

## Prettier

`yarn add --dev prettier eslint-config-prettier eslint-plugin-prettier`

.eslint config updated to:

```
{
  "extends": ["react-app", , "prettier"],
  "rules": {
    "prettier/prettier": [
      "error",
      {
        "semi": false
      }
    ]
  },
  "plugins": ["prettier"]
}
```

or:

```
{
  "extends": ["react-app", "plugin:prettier/recommended"],
  "rules": {
    "semi": ["error", "never"],
    "prettier/prettier": [
      "error",
      {
        "semi": false
      }
    ]
  }
```

### IDE Settings

We turn off javascript formatting on save because we want eslint to do that for us.

```
{
  "editor.formatOnSave": true,
    "[javascript]": {
        "editor.formatOnSave": false
    },
    "eslint.autoFixOnSave": true,
    "eslint.alwaysShowStatus": true,
    "prettier.disableLanguages": [
        "js"
    ],
    "prettier.semi": false,
}
```

### Process Optimization

Provide the means to work with githooks in scripts.

Running Prettier against staged files instead of the whole project everytime:

First, install the dependencies with
`yarn add --dev husky lint-staged`

Create scripts and config for precommit using husky to trigger prettier

```
scripts: {
  ...
  "precommit": "lint-staged",
  ...
},
...
"lint-staged": {
  "src/**/*.{js,jsx,json,css}": [
    "prettier --write",
    "git add"
    ]
  }
}
```

The `pretty-quick` npm package wraps up this configuration for you, so you can use the following instead for your script and remove the lint-staged config:

```
{
  "precommit": "pretty-quick --staged"
}
```

```sh
garethparkeradmin$ git commit -m 'Chore: Updated scss styling for Sankey'
husky > npm run -s precommit (node v9.5.0)

🔍  Finding changed files since git revision 747732e.
🎯  Found 5 changed files.
✍️  Fixing up package.json.
✅  Everything is awesome!
```

Now, if other developers do not have their IDE setup with prettier, this hook will format the files and recommit them.
