# Contributing

Thanks for your interest in contributing to wagmi! Please take a moment to review this document **before submitting a pull request.**

If you want to contribute, but aren't sure where to start, you can create a [new discussion](https://github.com/wagmi-dev/wagmi/discussions).

> **Note** **Please ask first before starting work on any significant new features. This includes things like adding new hooks, actions, etc.**
>
> It's never a fun experience to have your pull request declined after investing time and effort into a new feature. To avoid this from happening, we request that contributors create a [feature request](https://github.com/wagmi-dev/wagmi/discussions/new?category=ideas) to first discuss any API changes or significant new ideas.

<br>

## Basic guide

This guide is intended to help you get started with contributing. By following these steps, you will understand the development process and workflow.

1. [Cloning the repository](#cloning-the-repository)
2. [Installing Node.js and pnpm](#installing-nodejs-and-pnpm)
3. [Installing dependencies](#installing-dependencies)
4. [Starting the development playgrounds](#starting-the-development-playgrounds)
5. [Running the test suite](#running-the-test-suite)
6. [Writing documentation](#writing-documentation)
7. [Submitting a pull request](#submitting-a-pull-request)

## Advanced guide

This guide covers more advanced topics. Pick the topics based on your needs.

8. [Versioning](#versioning)

<br>

---

<br>

## Cloning the repository

To start contributing to the project, clone it to your local machine using git:

```bash
git clone https://github.com/wagmi-dev/wagmi.git --recurse-submodules
```

Or the [GitHub CLI](https://cli.github.com):

```bash
gh repo clone wagmi-dev/wagmi -- --recurse-submodules
```

<div align="right">
  <a href="#basic-guide">&uarr; back to top</a></b>
</div>

## Installing Node.js and pnpm

wagmi uses [pnpm workspaces](https://pnpm.io/workspaces) to manage multiple projects. You need to install **Node.js v16 or higher** and **pnpm v7 or higher**.

You can run the following commands in your terminal to check your local Node.js and npm versions:

```bash
node -v
pnpm -v
```

If the versions are not correct or you don't have Node.js or pnpm installed, download and follow their setup instructions:

- Install Node.js using [fnm](https://github.com/Schniz/fnm) or from the [official website](https://nodejs.org)
- Install [pnpm](https://pnpm.io/installation)

<div align="right">
  <a href="#basic-guide">&uarr; back to top</a></b>
</div>

## Installing dependencies

Once in the project's root directory, run the following command to install the project's dependencies:

```bash
pnpm install
```

After the install completes, pnpm links packages across the project for development and [git hooks](https://github.com/toplenboren/simple-git-hooks) are set up.

<div align="right">
  <a href="#basic-guide">&uarr; back to top</a></b>
</div>

## Starting the development playgrounds

To start the local development playgrounds, run one of the following commands. This will run a [Vite](https://vitejs.dev) app (located at [`playground`](../playgrounds)) that is set up for playing around with code while making changes.

```bash
pnpm dev      # `wagmi` playground
pnpm dev:core # `@wagmi/core` playground
```

Once the dev server is running, you can make changes to any of the package source files (e.g. `packages/react`) and it will automatically update the playground.

<div align="right">
  <a href="#basic-guide">&uarr; back to top</a></b>
</div>

## Running the test suite

wagmi uses [Vitest](https://vitest.dev) to run tests and [anvil.js](https://github.com/wagmi-dev/anvil.js) to execute tests against a local Ethereum node. First, install [Anvil](https://github.com/foundry-rs/foundry/tree/master/anvil) via [Foundry](https://book.getfoundry.sh/getting-started/installation).

Next, copy over the environment variables from `.env.example` to `.env`, and fill them out. Now you are ready to run the tests! You have the following options for running tests:

- `pnpm test [package?]` — runs tests in watch mode
- `pnpm test:cov` — runs tests and reports coverage
- `pnpm test:ui` — runs tests in the [Vitest UI](https://vitest.dev/guide/ui.html)

When adding new features or fixing bugs, it's important to add test cases to cover the new or updated behavior. If snapshot tests fail, you can run the `test:update` command to update the snapshots.

<div align="right">
  <a href="#basic-guide">&uarr; back to top</a></b>
</div>

## Writing documentation

Documentation is crucial to helping developers of all experience levels use wagmi. wagmi uses [VitePress](https://vitepress.dev) for the documentation site (located at [`site`](../site)). To start the site in dev mode, run:

```bash
pnpm site
```

Try to keep documentation brief and use plain language so folks of all experience levels can understand. If you think something is unclear or could be explained better, you are welcome to open a pull request.

<div align="right">
  <a href="#basic-guide">&uarr; back to top</a></b>
</div>

## Submitting a pull request

When you're ready to submit a pull request, you can follow these naming conventions:

- Pull request titles use the [Imperative Mood](https://en.wikipedia.org/wiki/Imperative_mood) (e.g., `Add something`, `Fix something`).
- [Changesets](#versioning) use past tense verbs (e.g., `Added something`, `Fixed something`).

When you submit a pull request, GitHub will automatically lint, build, and test your changes. If you see an ❌, it's most likely a bug in your code. Please, inspect the logs through the GitHub UI to find the cause.

<div align="right">
  <a href="#basic-guide">&uarr; back to top</a></b>
</div>

<br>

---

<div align="center">
  ✅ Now you're ready to contribute to wagmi! Follow the next steps if you need more advanced instructions.
</div>

---

<br>

## Versioning

When adding new features or fixing bugs, we'll need to bump the package versions. We use [Changesets](https://github.com/changesets/changesets) to do this.

> **Note**
>
> Only changes to the codebase that affect the public API or existing behavior (e.g. bugs) need changesets.

Each changeset defines which packages should be published and whether the change should be a major/minor/patch release, as well as providing release notes that will be added to the changelog upon release.

To create a new changeset, run `pnpm changeset`. This will run the Changesets CLI, prompting you for details about the change. You’ll be able to edit the file after it’s created — don’t worry about getting everything perfect up front.

Even though you can technically use any markdown formatting you like, headings should be avoided since each changeset will ultimately be nested within a bullet list. Instead, bold text should be used as section headings.

If your PR is making changes to an area that already has a changeset (e.g. there’s an existing changeset covering theme API changes but you’re making further changes to the same API), you should update the existing changeset in your PR rather than creating a new one.

### Releasing

The first time a PR with a changeset is merged after a release, a new PR will automatically be created called `chore: version packages`. Any subsequent PRs with changesets will automatically update this existing version packages PR. Merging this PR triggers the release process by publishing to npm and cleaning up the changeset files.

### Creating a snapshot release

If a PR has changesets, you can create a [snapshot release](https://github.com/changesets/changesets/blob/main/docs/snapshot-releases.md) by [manually dispatching](https://github.com/wagmi-dev/wagmi/actions/workflows/snapshot.yml) the Snapshot workflow. This publishes a tagged version to npm with the PR branch name and timestamp.

<div align="right">
  <a href="#advanced-guide">&uarr; back to top</a></b>
</div>