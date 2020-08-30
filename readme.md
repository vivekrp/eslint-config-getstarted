# Lint & Format (eslint-config-getstarted)

## Automatically setup the best and future-proofed linting and formatting config for your project with or without VS Code

![Node.js Package](https://github.com/vivekrp/eslint-config-getstarted/workflows/Node.js%20Package/badge.svg?style=flat-square) [![linting: eslint](https://img.shields.io/badge/linting-eslint-%238081f3)](https://github.com/eslint/eslint)
[![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg)](https://github.com/prettier/prettier) [![Node version](https://img.shields.io/node/v/eslint-config-getstarted.svg?style=flat)](http://nodejs.org/download/) [![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/vivekrp/eslint-config-getstarted/issues)

[![https://nodei.co/npm/eslint-config-getstarted.png?downloads=true&downloadRank=true&stars=true](https://nodei.co/npm/eslint-config-getstarted.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/eslint-config-getstarted)

Uses ESLint, Prettier, eslint-config-airbnb, babel-eslint, eslint-config-prettier, eslint-plugin-html, eslint-plugin-import, eslint-plugin-jsx-a11y, eslint-config-wesbos, eslint-plugin-prettier, eslint-plugin-react, eslint-plugin-react-hooks under the hood.

[![Lint-Format Poster](https://repository-images.githubusercontent.com/291339752/35966f00-ea61-11ea-8e02-52f0177aa178)](https://github.com/vivekrp/eslint-config-getstarted)

These are opinionated settings for ESLint and Prettier. You might like them - or you might not. Don't worry, you can always change them.

## What it does

- Lints JavaScript based on the latest standards
- Fixes issues and formatting errors with Prettier
- Lints + Fixes inside of HTML script tags
- Lints + Fixes React via eslint-config-airbnb
- You can see all the [rules here](https://github.com/vivekrp/eslint-config-getstarted/blob/master/.eslintrc.js) - You are very welcome to overwrite any of these settings, or just fork the entire thing to create your own.

## Installing

You can use ESLint globally and/or locally per project.

It's usually best to install this locally once per project, that way you can have project-specific settings as well as sync those settings with others working on your project via git.

You can also install globally so that any project or rogue JS file you write will have linting and formatting applied without having to go through the setup. You might disagree and that is okay, just don't do it then 😃.

## Local / Per Project Install

1. If you don't already have a `package.json` file, create one with `npm init`.

2. Then we need to install everything needed by the config:

```bash
npx install-peerdeps --dev eslint-config-getstarted
```

(**note:** npx is not a spelling mistake of **npm**. `npx` comes with when `node` and `npm` are installed and makes script running easier 😃)

3. You can see in your package.json there are now a big list of devDependencies.

4. Create a `.eslintrc` file in the root of your project's directory (it should live where package.json does). Your `.eslintrc` file should look like this:

```json
{
  "extends": ["eslint-config-getstarted"]
}
```

Tip: You can alternatively put this object in your `package.json` under the property `"eslintConfig":`. This makes one less file in your project.

5. You can add two scripts to your package.json to lint and/or fix:

```json
"scripts": {
  "lint": "eslint .",
  "lint:fix": "eslint . --fix"
},
```

6. Now you can manually lint your code by running `npm run lint` and fix all fixable issues with `npm run lint:fix`. You probably want your editor to do this though.

## Settings

If you'd like to overwrite eslint or prettier settings, you can add the rules in your `.eslintrc` file. The [ESLint rules](https://eslint.org/docs/rules/) go directly under `"rules"` while [prettier options](https://prettier.io/docs/en/options.html) go under `"prettier/prettier"`. Note that prettier rules overwrite anything in my config (trailing comma, and single quote), so you'll need to include those as well.

```json
{
  "extends": ["eslint-config-getstarted"],
  "rules": {
    "no-console": 2,
    "prettier/prettier": [
      "error",
      {
        "trailingComma": "es5",
        "singleQuote": true,
        "printWidth": 120,
        "tabWidth": 8
      }
    ]
  }
}
```

## With VS Code

You should read this entire thing. Serious!

Once you have done one, or both, of the above installs. You probably want your editor to automatically lint and fix for you. Here are the instructions for the VS Code:

1. Install the [ESLint package](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
2. Now we need to setup some VS Code settings via `Code/File` → `Preferences` → `Settings`. It's easier to enter these settings while editing the `settings.json` file, so click the ![Settings JSON](https://user-images.githubusercontent.com/13339456/79318309-17433300-7f07-11ea-9459-b27ee8dcf46c.png) icon in the top right corner or open Command Pallet by pressing Ctrl/CMD+Shift+P and then type Preferences: Open Settings (JSON):

```json
  // These are all my auto-save configs
"editor.formatOnSave": true,
// turn it off for JS and JSX, we will do this via eslint
"[javascript]": {
  "editor.formatOnSave": false
},
"[javascriptreact]": {
  "editor.formatOnSave": false
},
// tell the ESLint plugin to run on save
"editor.codeActionsOnSave": {
  "source.fixAll": true
},
// Optional BUT IMPORTANT: If you have the prettier extension enabled for other languages like CSS and HTML, turn it off for JS since we are doing it through Eslint already
"prettier.disableLanguages": ["javascript", "javascriptreact"],
```

## With Create React App

1. You gotta eject first `npm run eject` or `yarn eject`
1. Run `npx install-peerdeps --dev eslint-config-getstarted`
1. Crack open your `package.json` and replace `"extends": "react-app"` with `"extends": "eslint-config-getstarted"`

## 🤬🤬🤬🤬 IT'S NOT WORKING

Start fresh. Sometimes global modules can goof you up. This will remove them all:

```bash
npm remove --global eslint-config-getstarted babel-eslint eslint eslint-config-prettier eslint-config-airbnb eslint-plugin-html eslint-plugin-prettier eslint-plugin-import eslint-config-wesbos lint-format eslint-plugin-jsx-a11y eslint-plugin-react prettier eslint-plugin-react-hooks
```

To do the above for local, omit the `--global` flag.

Then if you are using a local install, remove your `package-lock.json` file and delete the `node_modules/` directory.

Then follow the above instructions again.
