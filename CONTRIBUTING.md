# Contributing

This document shows the development setup and how to start contributing
_(developing)_ for this project.

## 🔗 Table of Content

-   [Coding style guidelines](#coding-style-guidelines)
-   [Developing steps](#developing-steps)
-   [Git setup](#git-setup)
    -   [Git commits convention](#git-commits-convention)
    -   [Writing commit messages](#writing-commit-messages)
    -   [Git hooks](#git-hooks)
-   [Coding style guidelines](#coding-style-guidelines)
-   [Developing steps](#developing-steps)
-   [Git setup](#git-setup)
-   [Scripts](#scripts)

---

## 📔 Coding style guidelines

1. **Please don't write short syntax and abbreviations**.\
   Make the code easy to read, understandable, and very communicative, even if
   that will be more verbose and take more time/effort to write. Put yourself
   in the shoes of other contributors, especially when they just began their
   journey as a developer.

    - **It also regards to file(s) and directory(ies) naming!**

1. **Write functions with declarative names** _(non-anonymous)_.\
   If your function is complex, then instead of arrow functions _(unless you
   need to use lexical `this` or have other good reason)_, declare it as
   a standard function with a descriptive name.

1. **Try to follow the good practices of the JavaScript naming conventions.**\
   Credits to [the article about the naming convention best practices].

    - **Constants** - Capital letters _(UPPERCASE)_

    ```js
    const SECONDS = 60;
    const MINUTES = 60;
    const HOURS = 24;
    const DAY = SECONDS * MINUTES * HOURS;
    ```

    - **Variable** - camelCase

    ```js
    const firstName = "Matt";
    ```

    - **Boolean** - camelCase and with one of the following prefix: `is`,
      `are`, `has`

    ```js
    const isVisible = true;
    const areEqual = false;
    const hasEncryption = true;
    ```

    - **Function** - camelCase

    ```js
    function getName(firstName, lastName) {
    	return `${firstName} ${lastName}`;
    }
    ```

    - **Class** - PascalCase

    ```js
    class SoftwareDeveloper {
    	constructor(firstName, lastName) {
    		this.firstName = firstName;
    		this.lastName = lastName;
    	}
    }
    ```

    - **Methods** - camelCase

    ```js
     class SoftwareDeveloper {
         getName() {
             return ( ... );
         };
     }
    ```

    - **Private** - camelCase and with an underscore (`_`) prefix

    ```js
     class SoftwareDeveloper {
         constructor(firstName, lastName) {
             this.name = _getName(firstName, lastName);
         }

         _getName(firstName, lastName) {
             return `${firstName ${lastName}`;
         }
     }
    ```

    - **Components** _(in any framework)_ - PascalCase

    ```js
     const UserProfile = (props) {
         return ( ... );
     }
    ```

1. **Make your commit messages descriptive and ordered.**\
   Don't be afraid to edit the commit history during the Pull Request.
   Please ensure it's explaining pretty straightforward with what's going on
   and the changes it relates to.

    - It is preferable to see changes be split into small commits, so they
      explain step by step. Quantity is not essential, but the quality of
      communication and educating/informing contributors will help a lot.

1. **Organize imported modules in the code.**\
   This way, we can visually see which modules are ours from this project and
   which one has been imported from `node_modules` or Node.js packages /
   built-in modules.

[the article about the naming convention best practices]: https://javascript.plainenglish.io/javascript-naming-convention-best-practices-b2065694b7d

---

## 👣 Developing steps

1. **Create a new branch - off from the `develop` branch** for your work with
   the following git command:

    ```sh
    git checkout -b feature/#<short_name>
    ```

    where you replace the tag `#<short_name>` with the name of the feature, or
    with a unique id if you use any advanced Git flow integrations _(e.g.
    [Jira] or [GitHub])_.

1. **Start the development server**, with the following command:

    ```js
    pnpm dev
    ```

    More information about this script is in the [`pnpm dev`](#pnpm-dev)
    section.

1. **Code your modifications/new features**, and commit them along the way.
   Please read more about set [Git commits
   convention](#git-commits-convention), and [writing commit
   messages](writing-commit-messages).

1. Start the available tests, with the following command:

    ```sh
    pnpm test:watch
    ```

    More information about this script is in the [`pnpm test:watch`](#pnpm-testwatch) section.

1. **Analyze** _(use linters)_ **the changes using available commands**, such
   as:

    ```sh
    pnpm lint
    ```

    Read more about this script in the [`pnpm lint`](#pnpm-lint) section.

1. **Format the code** if your IDE _(Integrated Development Environment)_ - a
   code editor didn't do it already, using the following command:

    ```sh
    pnpm format
    ```

    Read more about this script in the [`pnpm format`](#pnpm-format) section.

1. When your changes are ready, **push the branch to a remote repo** with the
   following git command:

    ```sh
    git push origin feature/#<short_name>
    ```

1. **Merge it to `develop` branch**, whenever you decide during your process.

1. Lastly, **merge it to the production branch - `main`**, when you are sure that
   your code is ready and has no bugs. Writing tests helps to build confidence.

[jira]: https://www.atlassian.com/software/jira
[github]: https://github.com/

---

## 🛠️ Git setup

This section explains the configured Git flow for this project.

### Git commits convention

[![Conventional Commits shield]][conventional commits] [![Gitmoji shield]][gitmoji]

**This project uses [Conventional Commits], and [Gitmoji] commits
conventions.**

[conventional commits shield]: https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg?style=for-the-badge
[conventional commits]: https://conventionalcommits.org "Conventional commits convention"
[gitmoji shield]: https://img.shields.io/badge/gitmoji-%20😜%20😍-FFDD67.svg?style=for-the-badge
[gitmoji]: https://gitmoji.dev "Gitmoji convention"

### Writing commit messages

The currently recommended CLI _(Command Line Interface)_ tool to use them both
is the [gacp] Node.js package. The local config for this tool is set in the
[`.gacprc.js`](./.gacprc.js) file.

**You can either use:**

```sh
pnpm commit
```

**or install [gacp] globally on your device.**

More information about this script is in the [pnpm commit](#pnpm-commit)
section.

[gacp]: https://github.com/vivaxy/gacp

### Git hooks

There are Git hooks configured with the [Husky] tool.\
They should be installed automatically during the `pnpm install` process. In
case they didn't, use the following command:

```sh
pnpm prepare
```

Existing hooks:

-   **pre-commit** - will analyze all of staged file _(code)_ changes with the
    [`pnpm lint:staged`](#pnpm-lintstaged) script.
-   **commit-msg** - will ensure the provided commit message follows the set [Git
    commits convention](#git-commits-convention).

[husky]: https://typicode.github.io/husky

---

## 🧰 Scripts

👉 **REMINDER:** This project uses [`pnpm`] as [Node.js] package manager.

[`pnpm`]: https://pnpm.io/
[node.js]: https://nodejs.org/en/

The following scripts are available for this project:

-   [`pnpm browsers`](#pnpm-browsers)
-   [`pnpm build`](#pnpm-build)
-   [`pnpm clean`](#pnpm-clean)
-   [`pnpm commit`](#pnpm-commit)
-   [`pnpm dev`](#pnpm-dev)
-   [`pnpm format`](#pnpm-format)
-   [`pnpm lint`](#pnpm-lint)
    -   [`pnpm lint:commits`](#pnpm-lintcommits)
    -   [`pnpm lint:css`](#pnpm-lintcss)
    -   [`pnpm lint:js`](#pnpm-lintjs)
    -   [`pnpm lint:ls`](#pnpm-lintls)
    -   [`pnpm lint:md`](#pnpm-lintmd)
    -   [`pnpm lint:staged`](#pnpm-lintstaged)
    -   [`pnpm lint:ts`](#pnpm-lintts)
-   [`pnpm prepare`](#pnpm-prepare)
-   [`pnpm preview`](#pnpm-preview)
-   [`pnpm start`](#pnpm-start)
-   [`pnpm test`](#pnpm-test)
    -   [`pnpm test:coverage`](#pnpm-testcoverage)
    -   [`pnpm test:watch`](#pnpm-testwatch)

### `pnpm browsers`

**Outputs the list of supported browsers** by the project using the
[browserslist] Node.js package.

The [browserslist] configuration is in the [.browserslistrc](./.browserslistrc)
file.

[browserslist]: https://browserslist.dev/

### `pnpm build`

**Builds the output for the production** into [`dist/`](./dist) directory using
[Vite].\
📝 **NOTE:** There must be no errors with [TypeScript] compilation to prevent
possible bugs from being passed into production.

The [Vite] configuration is in the [vite.config.js](./vite.config.js) file.

[vite]: https://vitejs.dev/

### `pnpm clean`

**Cleans the built outputs**. It removes these directories:

-   `dist/` _(output from the production environment)_
-   `.cache/` _(output from the development environment)_

It uses the [rimraf] Node.js package to prevent cross-platform issues.

[rimraf]: https://github.com/isaacs/rimraf

### `pnpm commit`

**Runs a commit message generator for the staged files** using the [gacp]
Node.js package.

The [gacp] configuration is in the [.gacprc.js](./.gacprc.js) file.

### `pnpm dev`

**Starts the development server** with [Vite]. It will also enable hosting
_(it makes the server available for the other devices on your network)_.

The [Vite] configuration is in the [vite.config.js](./vite.config.js) file.

### `pnpm format`

**Formats the source code files** using [Prettier] formatter.

The [Prettier] configuration is in the [.prettierrc.js](./.prettierrc.js) file.

[prettier]: https://prettier.io/

### `pnpm lint`

**Runs all of the set linting scripts in parallel**.\
It uses the [npm-run-all] Node.js package.

[npm-run-all]: https://github.com/mysticatea/npm-run-all

#### `pnpm lint:commits`

**Analyzes the latest commit messages from the develop branch to latest**, in
order to adhere to set commit convention with [commitlint].

The [commitlint] configuration is in the [.commitlintrc.js](./.commitlintrc.js)
file.

[commitlint]: https://commitlint.js.org/#/

#### `pnpm lint:css`

Statically **analyzes the [CSS] source code** with [Stylelint] to quickly find
problems.\
It includes [Sass] _(`*.scss` files)_ as well.

The [Stylelint] configuration is in the [.stylelintrc.js](./.stylelintrc.js)
file.

[css]: https://developer.mozilla.org/en-US/docs/Web/CSS
[stylelint]: https://stylelint.io/
[sass]: https://sass-lang.com/

#### `pnpm lint:js`

Statically **analyzes the [JavaScript]/[TypeScript] source code** with
[ESLint] to quickly find problems.\
It includes as well code files for these frameworks:

-   [React] _(`*.jsx` or `*.tsx` files)_,
-   [Svelte] _(`*.svelte` files)_,
-   [Vue] _(`*.vue` files)_.

The [ESLint] configuration is in the [.eslintrc.js](./.eslintrc.js) file.

[javascript]: https://developer.mozilla.org/en-US/docs/Web/javascript
[typescript]: https://www.typescriptlang.org/
[eslint]: https://eslint.org/
[react]: https://reactjs.org/
[svelte]: https://svelte.dev/
[vue]: https://v3.vuejs.org/

#### `pnpm lint:ls`

**Checks the file names** in the project based on their parent folder and file
extension with [ls-lint].

The [ls-lint] configuration is in the [.ls-lint.yml](./.ls-lint.yml) file.

[ls-lint]: https://ls-lint.org/

#### `pnpm lint:md`

**Analyzes the markdown files** to find issues, including styling with
[markdownlint].

The [markdownlint] configuration is in the
[.markdownlint.json](./.markdownlint.json) file.

[markdownlint]: https://github.com/DavidAnson/markdownlint

#### `pnpm lint:staged`

**Runs the linters on the files in the Git staging area** with a [lint-staged]
Node.js package.

The [lint-staged] configuration is in the
[.lintstagedrc.js](./.lintstagedrc.js) file.

[lint-staged]: https://github.com/okonet/lint-staged

#### `pnpm lint:ts`

**Starts type checking all kinds of JavaScript code files** with [TypeScript]
compiler.

The [TypeScript] configuration is in the [tsconfig.json](./tsconfig.json) file.

### `pnpm prepare`

**Installs the Git hooks** with [Husky]. Should be run only once, when cloning
the project and developing.

This script should run automatically only once - during the `pnpm install`.
After that, there's no need to use it.

The [Husky] hooks are configured in the [.husky/](./.husky) directory.

### `pnpm preview`

**Starts the production server** for the built output with [Vite]. It will also
enable hosting to make the project available for the other devices on your
network.

The [Vite] configuration is in the [vite.config.js](./vite.config.js) file.

### `pnpm start`

**Starts the project locally** by running [`pnpm build`](#pnpm-build) and
[`pnpm preview`](#pnpm-preview) in series. It uses the [npm-run-all] Node.js
package.

The [Vite] configuration is in the [vite.config.js](./vite.config.js) file.

### `pnpm test`

**Runs all of the written (coded) tests** in the project with [Jest] - a
JavaScript testing framework. [Testing Library] utilizes it for good testing
practices.

The [Jest] configuration is in the [jest.config.js](./jest.config.js) file.\
The [Jest] setup is in the [jest.setup.js](./jest.setup.js) file.

[jest]: https://jestjs.io/
[testing library]: https://testing-library.com/

#### `pnpm test:coverage`

**Generates a current testing coverage of the project report** to the
[.coverage](./.coverage) directory. Made by [Jest], which uses a [istanbul] tool
internally.

The [Jest] configuration is in the [jest.config.js](./jest.config.js) file.\
The [Jest] setup is in the [jest.setup.js](./jest.setup.js) file.

[istanbul]: https://istanbul.js.org/

#### `pnpm test:watch`

**Starts the tests with watch mode** for development purposes. Inside the
running process, you can configure file(s) watching conditions.

The [Jest] configuration is in the [jest.config.js](./jest.config.js) file.\
The [Jest] setup is in the [jest.setup.js](./jest.setup.js) file.
