# Trying to use Remix with Prettier 3

Because the `@remix-run/dev` package depends on Prettier 2, it is awkward to make use of a shared ESLint config that has a dependency on Prettier 3.  In this case, ESLint fails to find the `eslint-plugin-prettier` package.

To reproduce the issue, clone this project and then install the dependencies.

```shell
npm install
```

After that, you should see something like this listed for the `prettier` and `eslint-plugin-prettier` packages:

```shell
npm ls prettier
remix-prettier-issue@ /Users/tim/projects/remix-prettier-issue
├─┬ @remix-run/dev@2.9.2
│ └── prettier@2.8.8
└─┬ eslint-config-planet@22.1.0
  ├─┬ eslint-plugin-prettier@5.1.3
  │ └── prettier@3.3.1 deduped
  └── prettier@3.3.1
```

```shell
npm ls eslint-plugin-prettier
remix-prettier-issue@ /Users/tim/projects/remix-prettier-issue
└─┬ eslint-config-planet@22.1.0
  └── eslint-plugin-prettier@5.1.3
```

Then, when you try to run ESLint, you can see this failure:

```shell
npm test

> test
> eslint vite.config.js


Oops! Something went wrong! :(

ESLint: 8.57.0

ESLint couldn't find the plugin "eslint-plugin-prettier".

(The package "eslint-plugin-prettier" was not found when loaded as a Node module from the directory "/Users/tim/projects/remix-prettier-issue".)

It's likely that the plugin isn't installed correctly. Try reinstalling by running the following:

    npm install eslint-plugin-prettier@latest --save-dev

The plugin "eslint-plugin-prettier" was referenced from the config file in "package.json » eslint-config-planet".

If you still can't figure out the problem, please stop by https://eslint.org/chat/help to chat with the team.
```