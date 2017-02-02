# Salsa Collection
## Table of Contents
- [Features](#features)
- [Installation & Configuration](#installation)
    - [Pre-Install Commands](#pre-install)
    - [NPM scripts commands](#npm-scripts)
    - [Gitlab CI Configuration](#gitlab-ci)
- [Tips](#tips)
    - [Useful Links](#links)
    - [Ionic & Cordova](#ionic-cordova)
    - [Webstorm](#webstorm)
    - [Docs](#docs)

## <a name="features"></a>Features
- Ionic RC4
- [Yarn](https://github.com/yarnpkg/yarn) for fast, reliable, and secure dependency management.
- [BetterScripts](https://github.com/benoror/better-npm-run) for better NPM scripts.
- ENV variables from package.json injected automatically.
- Documentation with [Typedoc](https://github.com/TypeStrong/typedoc/).
- Continuous Integration with Gitlab CI [see here for info](#gitlab-ci).
    - Automatic apk only when pushing to release branch.
    - Automatic ipa through ionic package only when pushing to release branch.
    - A [Docker image](https://github.com/marcoturi/ionic-docker).
- Tests
    - Unit tests with Karma.
    - E2E tests with Protractor.
    - Screenshot reporter for Protractor.
- Linting
    - [SCSS Lint](https://github.com/HugoGiraudel/sass-boilerplate) following Sass Guidelines.
    - TSlint with [Codelyzer](https://github.com/mgechev/codelyzer).
- GIT 
    - Automatic alignment of app version in config.xml from package.json through cordova hook.

## <a name="installation"></a>Installation & Configuration
### <a name="pre-install"></a>Pre-Install Commands
```
# Required dependencies (on Mac also install ios-sim and ios-deploy)
npm i –g cordova ionic yarn
gem install scss-lint
# Clone the repo –depth 1 removes all but one .git commit history
git clone –depth 1 <<path/to/gitrepo.git>>
# Change directory
cd ionic2-boilerplate
# Install project dependencies
yarn
npm run post-install

```
Note: you should have ruby 2 installed to run scss-lint.

### <a name="npm-scripts"></a>NPM scripts commands
| Task                      | Description                                              |
|---------------------------|----------------------------------------------------------|
| `dev`                     | run ionic serve                                          |
| `build`                   | Full production build. Use `--dev` flag for dev build.   |
| `release`                 | generate changelog based on commits                      |
| `push`                    | shortcut for git push origin master --follow-tags        |
| `lint`                    | lint with tslint                                         |
| `scss-lint`               | lint scss                                                |
| `test`                    | runs Karma test                                          |
| `test:watch`              | runs Karma test watching for edits (usefull for TDD)     |
| `e2e`                     | runs e2e protractor tests                                |
| `e2e:interactive`         | runs e2e protractor tests in interactive mode            |
| `outdated`                | search npm packages for outdated dependencies            |
| `ios:dev`                 | build .ipa using dev environment vars                    |
| `ios:release`             | build .ipa with production environment vars              |
| `android:dev`             | build .apk using dev environment vars                    |
| `android:devworeload`     | build .apk using dev environment vars without livereload |
| `android:release`         | build .apk with production environment vars              |

### <a name="gitlab-ci"></a>Gitlab CI Configuration
- To get the automatic .ipa from ionic package first setup a ionic.io profile with certificates for ios. Secondly add the following Secret variables in Gitlab. N.B. Be sure to don't show Build results (edit project settings) for your repo otherwise those vars could be exposed.

| Key                            | Description                                                                                                      |
|--------------------------------|------------------------------------------------------------------------------------------------------------------|
| `IONIC_LOGIN_EMAIL`            | Your ionic.io email                                                                                              |
| `IONIC_LOGIN_PASSWORD`         | Your ionic.io password                                                                                           |
| `IONIC_PACKAGE_BUILD_RELEASE`  | (Optional) Indicate whether this is a release build. Possible values are `true` or `false`. Defaults to `false`. |
| `IONIC_PACKAGE_BUILD_PROFILE`  | Security profile to use for the build, as defined in Ionic.io console.                                           |

## <a name="tips"></a>Tips
### <a name="links"></a>Useful Links
- [Search engine for find typescript typings](http://microsoft.github.io/TypeSearch/)
- [Cordova-xcode 8](https://dpogue.ca/articles/cordova-xcode8.html)
- [Ionic package setup](https://docs.ionic.io/services/package/)
- [Useful Hooks](https://github.com/driftyco/ionic-package-hooks)

### <a name="ionic-cordova"></a>Ionic & Cordova
- Avoid the use of ionic state commands and also ionic plugin/platform. Use directly cordova prepare (or cordova plugin/platform). Also save your plugin/platform only inside config.xml, not package.json to avoid confusion. See [this](https://github.com/driftyco/ionic-cli/issues/1324) for further informations. 

### <a name="webstorm"></a>Webstorm
- Set code style for typesript:
    - {import} -> { import }
    - import * from "lodash" -> import * from 'lodash'
- Set typescript settings to be used with the version inside node_modules instead of the bundled one (1.8)
- [Don't activate typescript compiler.](https://github.com/driftyco/ionic/issues/8303)
- Enable tslint in settings
- Download scss lint plugin and enable it

### <a name="docs"></a>Docs
To generate docs tsconfig.json has to be appended
``"target": "es6"`` instead of ``"target": "es5"``. Do not forget to change it back afterwards.
With this typedocs recognizes es6 constructs.
