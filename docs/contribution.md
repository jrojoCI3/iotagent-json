# Contribution Guidelines

==================

## Overview

Being an Open Source project, everyone can contribute, provided that it respect the following points:

-   Before contributing any code, the author must make sure all the tests work (see below how to launch the tests).
-   Developed code must adhere to the syntax guidelines enforced by the linters.
-   Code must be developed following the branching model and change log policies defined below.
-   For any new feature added, unit tests must be provided, following the example of the ones already created.

In order to start contributing:

1.  Fork this repository clicking on the "Fork" button on the upper-right area of the page.
2.  Clone your just forked repository:

```bash
git clone https://github.com/your-github-username/iotagent-json.git
```

3.  Add the main iotagent-json repository as a remote to your forked repository (use any name for your remote
    repository, it does not have to be iotagent-json, although we will use it in the next steps):

```bash
git remote add iotagent-json https://github.com/telefonicaid/iotagent-json.git
```

Before starting contributing, remember to synchronize the `master` branch in your forked repository with the `master`
branch in the main iotagent-json repository, by following this steps

1.  Change to your local `master` branch (in case you are not in it already):

```bash
git checkout master
```

2.  Fetch the remote changes:

```bash
git fetch iotagent-json
```

3.  Merge them:

```bash
git rebase iotagent-json/master
```

Contributions following this guidelines will be added to the `master` branch, and released in the next version. The
release process is explaind in the _Releasing_ section below.

## Branching model

There is one special branches in the repository:

-   `master`: contains the last stable development code. New features and bugfixes are always merged to `master`.

In order to start developing a new feature or refactoring, a new branch should be created with name `task/<taskName>`.
This branch must be created from the current version of the `master` branch. Once the new functionality has been
completed, a Pull Request will be created from the feature branch to `master`. Remember to check both the linters and
the tests before creating the Pull Request.

Bugfixes work the same way as other tasks, with the exception of the branch name, that should be called `bug/<bugName>`.

In order to contribute to the repository, these same scheme should be replicated in the forked repositories, so the new
features or fixes should all come from the current version of `master` and end up in `master` again.

All the `task/*` and `bug/*` branches are temporary, and should be removed once they have been merged.

There is another set of branches called `release/<versionNumber>`, one for each version of the product. This branches
point to each of the released versions of the project, they are permanent and they are created with each release.

## Change log

The project contains a version changelog, called CHANGES_NEXT_RELEASE, that can be found in the root of the project.
Whenever a new feature or bug fix is going to be merged with `develop`, a new entry should be added to this changelog.
The new entry should contain the reference number of the issue it is solving (if any).

When a new version is released, the change log is cleared, and remains fixed in the last commit of that version. The
content of the change log is also moved to the release description in the GitHub release.

## Releasing

The process of making a release consists of the following steps:

1.  Create and PR into `master` a new task branch with the following changes:

-   Change the development version number in the package.json (with a sufix `-next`), to the new target version (without
    any sufix)
-   Make sure all the dependencies have fixed versions (usually the IoTAgent library will be on `master`).

2.  Create a tag from the last version of `master` named with the version number and push it to the repository.
3.  Create the release in Github, from the created tag. In the description, add the contents of the change log.
4.  Create a release branch from the last version of `master` named with the version number.
5.  Create a new task for preparing the next release, adding the sufix `-next` to the current version number (to signal
    this as the development version).
