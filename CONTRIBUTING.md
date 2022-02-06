# Contributing

When contributing to this repository, please follow the guidelines below.
They are based on [airbnb's javascript style guide](https://github.com/airbnb/javascript#table-of-contents)

<br>

## Table of Contents

- [Contributing](#contributing)
  - [Table of Contents](#table-of-contents)
  - [General](#general)
    - [Naming Conventions](#naming-conventions)
      - [Functions](#functions)
      - [Components](#components)
      - [Enums, Interfaces and Types](#enums,-interfaces-and-types)
    - [Documents](#documents)
    - [Spikes](#spikes)
  - [Version Control](#version-control)
    - [Branch Names](#branch-names)
    - [Branches Lifetime](#branches-lifetime)
    - [Integration](#integration)
    - [Commits](#commits)
    - [Commit Messages](#commit-messages)

<br>
<br>

## General

### Naming Conventions

Folder and file names follow the convention of the main element in them. Thus,
if it is a component, the convention will be the one of a component. If the main
element is a (set of) function(s), files and folders should follow that convention.

#### Functions

As a general rule, [camel case](https://en.wikipedia.org/wiki/Camel_case)
must be used for files and folders.

Incorrect examples:

- "API"
- "this is a function"

Correct examples:

- "api"
- "thisIsAFunction"

#### Components

For React Components, we follow [pascal case](https://techterms.com/definition/pascalcase)

Correct examples of objects:

- "ThisIsAComponent"
- "AnotherComponent"

We mostly avoid adding `index.ts` files for each folder. An `index.ts` is used
only for wrapper folders that contain other components.

<br>

### Enums, Interfaces and Types

Enums, interfaces and types should follow
[pascal case](https://techterms.com/definition/pascalcase) convention with an
uppercase letter related to the element.

Correct examples:

- "EThisIsAnEnum"
- "EAnotherEnum"
- "IThisIsAnInterface"
- "IAnotherInterface"
- "TThisIsAType"
- "TAnotherType"

<br>

### Documents

As a default, documentation should be written on our
[Notion Page](https://www.notion.so/Lemon-Cash-Wiki-6840d45fccda4521a0e363342fba181f).

<br>

### Spikes

_Spikes are initial implementations of features to determine risks and assess
how to the actual implementation will be tackled._

Spikes must be placed inside the `/spikes` folder. Every spike must have its
own folder with a **README.md** file composed of the following sections:

- **Overview:** Purpose of the spike.
- **{Tool/Library/Framework}:** Replace this title by the name of the tool/library/framework being tested and complete with information and links.
- **Running the spike**
  - **Prerequisites:** List of necessary tools to run the spike.
  - **Steps:** Step-by-step guide on how to run the spike.
- **Conclusion:** Conclusion on whether its convenient to implement the tool within the system or not.

<br>
<br>

## Version Control

### Branch Names

The branch name must have the following structure:

`{TYPE}/{feature-description}`

The **TYPE** can be one of:

- **build** "Build system", new build of the system
- **chore** "Chore", update of grunt tasks, etc.; no prod code changes
- **devops** "DevOps", changes to devops related tasks
- **docs** "Documentation", changes to documentation
- **feat** "Features", new features
- **fix** "Bug fixes", new bug fixes
- **perf** "Performance", changes to improve performance
- **refactor** "Refactor", refactor of production code
- **style** "Style", formatting, etc.; no prod code changes
- **spike** "Spike", code for analysis risks or sandbox implementations
- **test** "Testing", add missing tests or refactor; no prod code changes

Examples:

- `docs/parsing-functions`
- `feat/new-amazing-feature`
- `fix/ui-flickering-bug`

<br>

### Branches Lifetime

Every branch that has already been integrated into the source branch, must be
deleted both locally and remotely, to avoid branch cluttering.

<br>

### Integration

When integrating changes from one branch into another, always use **rebase**
instead of **merge**. The purpose is to keep a linear (and clearer) commit
history.

<br>

### Commits

Commits should be small and atomic. For more information about commits best
practices, please head to [this page](https://deepsource.io/blog/git-best-practices/).

<br>

### Commit Messages

Commit messages should comply with the following rules, based on the
[conventional commits](https://www.conventionalcommits.org/en/v1.0.0/) convention:

1. Message length must have no more than 100 characters
2. Commit title must be lowercase
3. Commit title must not end with a period
4. Commit title must have the following structure: **type(optional-scope): description**

**Scope**

The scope identifies the EPIC user story to which the change introduced in
the commit is associated. In short, the overall topic of the feature it is
modifying.

This element is _optional_ in the commit title, but recommended.

**Type**

The type identifies the type of change introduced in the commit, and it can
be [any of the ones specified for branches](#branch-names).

**Examples**

Below you can find some examples of correct commit messages:

```shell
git commit -m "docs: add contributing guidelines document"
```

```shell
git commit -m "fix(endpoints): validation issue on users endpoint"
```

```shell
git commit -m "style(login): update login view to apply styling"
```

<br>