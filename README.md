# ESLINT:
## Linting Your Project
`npm install eslint --save-dev`

Create .eslintrc.json, example

`
{\
  "env": {
    "browser": true
  },
  "extends": "eslint:recommended",
  "parserOptions": {
    "ecmaVersion": 2021
  },
  "rules": {
    "quotes": ["error", "double"],
    "semi": ["error", "always"]
  }
}
`


We can look at what each one of these fields in the config does:

+ env - Specifies the environment we are planning to run our code in. When we say browser ESLint will not throw an error if we try to use a DOM method like document.querySelector(). Another common env value is node.

+ extends - This option allows us to inherit from existing lists of rules. ESLint provides a list of default recommended rules. If there are any you disagree with, they can be disabled manually in the rules field on the config.

+ parserOptions - The ecmaVersion property tells ESLint which ECMA version of Javascript you are targeting. For example if you use a value fo 2015 it will throw an error if you try to use syntax like const or let instead of var. Setting it to 2016 would allow you to use them.

+ rules - This is where you manually configure any rules you would like to apply in your project, and whether you want to show a warning or throw an error. Tools can be set to listen for ESLint errors and cancel if they are encountered

## Extending Configurations (Airbnb):

`npm install eslint-config-airbnb --save-dev`

`"extends": ["eslint:recommended", "airbnb"]`


## Plugins (React):
Plugins allow to you add new rules that go beyond just the basic Javascript syntax so that you can also include rules that help write alternative syntax in the JS environment. Two popular examples of that would be React (JSX) and Typescript.

`npm install eslint-plugin-react --save-dev`
<br>
<br>

`"plugins": ["react"],`


`"extends": ["eslint:recommended", "plugin:react/recommended"],`

## Prettier:
>> Turns off all ESLint rules that have the potential to interfere with Prettier rules.

`yarn add eslint-config-prettier`

`"extends": ["other configs", "prettier"]` 

**NOTE**: "prettier" must be the last item, so it can overwrite the orthers.


Example of overwrited rules:
@typescript-eslint/eslint-plugin

@babel/eslint-plugin

eslint-plugin-babel

eslint-plugin-flowtype

eslint-plugin-react

eslint-plugin-standard

eslint-plugin-unicorn

eslint-plugin-vue

>> Turns Prettier rules into ESLINT rules:

`yarn add prettier eslint-plugin-prettier --dev`

`"extends": ["plugin:prettier/recommended"]`

**EXPLAIN **

Exactly what does plugin:prettier/recommended do? Well, this is what it expands to:

`{
  "extends": ["prettier"],
  "plugins": ["prettier"],
  "rules": {
    "prettier/prettier": "error",
    "arrow-body-style": "off",
    "prefer-arrow-callback": "off"
  }
} `

+ "extends": ["prettier"] enables the config from eslint-config-prettier, which turns off some ESLint rules that conflict with Prettier.
+ "plugins": ["prettier"] registers this plugin.
+ "prettier/prettier": "error" turns on the rule provided by this plugin, which runs Prettier from within ESLint.
+ "arrow-body-style": "off" and "prefer-arrow-callback": "off" turns off two ESLint core rules that unfortunately are problematic with this plugin – see the next section.

>> Create .prettierrc file and it will be merge into eslint-rules:

final .eslintrc.json

`
{
  "plugins": [
    "@typescript-eslint",
    "react",
    "prettier"
  ],
  "extends": [
    "next/core-web-vitals",
    "eslint:recommended",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:react/recommended",
    "plugin:prettier/recommended"
  ],
  "rules": {
    "react/react-in-jsx-scope": "off"
  }
}`
