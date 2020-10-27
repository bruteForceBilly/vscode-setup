# Visual Studio Code CSS linting & formatting

Hello! I have created this repo as an example of how you can set up CSS linting and code formatting for Visual Studio Code with [Prettier](https://prettier.io/) and [Stylelint](https://stylelint.io/).  You can clone this repo to see how I have set up the tools for linting and formatting. I have also written a short guide how to set up a repo like this one here in the read me

### What is linting? 
**lint**, or a **linter**, is a [static code analysis](https://en.wikipedia.org/wiki/Static_program_analysis "Static program analysis") tool used to flag programming errors, [bugs](https://en.wikipedia.org/wiki/Software_bug "Software bug"), stylistic errors,  etc. [[1]](https://en.wikipedia.org/wiki/Lint_(software)#cite_note-1)

### What is code formatting?
A code formatter is a development tool that will format your code after given rules. These rules can be given by a linter or set in a config file for the formatter. 

### Why should I care about this?
Besides catching bugs, linters help you ensure you follow best practice. Used together with a code formatter its a powerful combination that will save you time by fixing mistakes in your code that sometimes can be very tedious to correct (i.e spelling errors, non closing brackets etc). It's kind of like writing text messages on your phone with auto correct. 


## Guide for setting up your project like this one 

This repo uses uses prettier as a code formatter and stylelint as a linter for css together with Visual Studio Code. To set up a project in the same manner as this repo, follow these steps:

### 1) Install VS Code extensions

Navigate here and click install Stylelint
https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint

Navigate here and click install Prettier
https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode

### 2) Install Package dependencies

#### prettier-stylelint  

prettier-stylelint attempts to create a prettier config based on the stylelint config, then format with prettier followed by stylelint --fix. So after that you should end up with formatted code with no linting errors.

#### stylelint-config-standard

Turns on additional rules to enforce the common stylistic conventions found within a handful of CSS styleguides.

#### stylelint-config-prettier

Turns off all rules that are unnecessary or might conflict with Prettier. This lets you use your favorite shareable config without letting its stylistic choices get in the way when using Prettier.

#### stylelint-csstree-validator

CSS syntax validator based on csstree as plugin for stylelint. Currently it's only checking declaration values to match W3C specs and browsers extensions. (Note: At the moment it seems like I can't make prettier to format after this plugin, looking into it. )

To install all these package dependencies enter this in terminal: 

    npm install prettier prettier-stylelint stylelint stylelint-config-standard stylelint-config-prettier stylelint-csstree-validator stylelint-prettier --save-dev

### 3) Create workspace settings file

There are two ways to configure Visual Studio Codes settings, globally / user or on project basis / workspace. Almost always prefer to set settings in your workspace settings file to avoid conflict rule conflicts with other projects. 

In your project folder in terminal enter

    touch .vscode/settings.json

This will create a settings config json file for your project. Open, edit and save this file so it looks like this: 

     {
    	"[css]": {
    		"editor.defaultFormatter": "esbenp.prettier-vscode",
    		"editor.codeActionsOnSave": {
    		"source.fixAll": true,
    	},
    	},
    	"editor.formatOnSave": false,
    	"css.validate": false,
    	"stylelint.enable": true,
    }
             
Here you are telling visual studio code that for css file we want to use prettier as a default formatter, we want to run prettier on save and we want to fix all fixable linting errors any linter give us. Further we are disabling vs codes default css validator and format on save and enabling stylelint. 


### 4) Create config files for stylelint
In terminal in your project folder

    touch .stylelintrc

Now you can open and edit this file to add rules you want your linter to follow or not follow. This is an example that follows Airbnb's style guide :

    {
      "rules": {
        "selector-no-id": true,
        "indentation": 2,
        "selector-list-comma-newline-after": "always",
        "declaration-colon-space-after": "always",
        "declaration-colon-space-before": "never",
        "block-opening-brace-space-before": "always",
        "declaration-block-single-line-max-declarations": 1,
        "rule-empty-line-before": ["always", {
            "ignore": ["after-comment"]
        }],
        "comment-empty-line-before": ["always", {
          "ignore": ["stylelint-commands"]
        }],
        "declaration-property-value-blacklist": {
          "/^border/": ["none"]
        },
        "at-rule-blacklist": ["extend"],
        "max-nesting-depth": 3,
        "declaration-no-important": true,
        "selector-max-compound-selectors": 3,
        "selector-no-qualifying-type": true,
        "no-duplicate-selectors": true,
        "block-no-empty": true,
        "at-rule-empty-line-before": [
            "always", {
                "ignoreAtRules": ["import", "first-nested"]
            }
        ],
        "at-rule-name-case": "lower",
        "color-hex-case": "lower",
        "color-hex-length": "long",
        "color-no-invalid-hex": true,
        "string-quotes": "single",
        "value-no-vendor-prefix": true,
        "value-list-comma-space-after": "always-single-line",
        "shorthand-property-no-redundant-values": true,
        "comment-whitespace-inside": "always",
        "function-comma-space-after": "always-single-line",
        "function-comma-space-before": "never",
        "length-zero-no-unit": true,
        "number-no-trailing-zeros": true,
        "declaration-block-trailing-semicolon": "always",
        "declaration-block-no-duplicate-properties": true,
        "declaration-block-semicolon-newline-after": "always",
        "block-closing-brace-empty-line-before": "never",
        "block-closing-brace-newline-before": "always"
      }
    }


