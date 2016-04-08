<p align="center">
  <img alt="Lerna" src="https://i.imgur.com/yT7Skxn.png" width="480">
</p>

<p align="center">
  A tool for managing JavaScript projects with multiple packages.
</p>

<p align="center">
  <a href="https://travis-ci.org/kittens/lerna"><img alt="Travis Status" src="https://img.shields.io/travis/kittens/lerna/master.svg?style=flat&label=travis"></a>
</p>

## About

Trying to manage a multi-module project over many separate repositories can be
really difficult. Making changes across repositories is bulky and difficult to
manage. Testing changes across many different packages when they are in separate
locations gets really complicated really fast.

To solve these problems, some projects (Babel, React, Ember, Meteor, and many
others) use **monorepos**. The idea here is to take all the packages within a
project and put them inside a single repo.

Lerna is a tool for managing these types of repos.

## Usage

To start, let's install Lerna from [npm](https://www.npmjs.com/).

```sh
$ npm install --global lerna
```

Now create a new repository:

```sh
$ git init my-cool-project
$ cd my-cool-project
```

And then to turn it into a lerna repo run the following:

```sh
$ lerna init
```

> **Note:** Depending on the project you might want to run this in
> `--independent` mode.







## About

While developing [Babel](https://github.com/babel/babel) I followed a
[monorepo](https://github.com/babel/babel/blob/master/doc/design/monorepo.md) approach
where the entire project was split into individual packages but everything lived in the same
repo. This was great. It allowed super easy modularisation which meant the core was easier
to approach and meant others could use the useful parts of Babel in their own projects.

This tool was abstracted out of that and deals with bootstrapping packages by linking
them together as well as publishing them to npm. You can see the
[Babel repo](https://github.com/babel/babel/tree/master/packages) for an example of a
large Lerna project.

## Usage

```sh
$ npm install -g lerna
$ lerna bootstrap
```

This will create a dummy `VERSION` file as well as a `packages` folder.

### Bootstrap

```sh
$ lerna bootstrap
```

1. Link together all packages that depend on each other.
2. `npm install` all other dependencies of each package.

### Updated

```sh
$ lerna updated
```

1. Check which `packages` have changed since the last release, and log it.

### Publishing

```sh
$ lerna publish
```

1. Publish each module in `packages` that has been updated since the last version to npm with the tag `prerelease`.
2. Once all packages have been published, remove the `prerelease` tags and add the tags `latest` and `stable`.

> If you need to publish prerelease versions, set an env variable. `NPM_DIST_TAG=next lerna publish`.
> This will add the tag you specify instead of `latest` and `stable`.

## How it works

Lerna projects operate on a single version line. The version is kept in the file `VERSION`
at the root of your project. When you run `lerna publish`, if a module has been updated
since the last time a release was made, it will be updated to the new version you're
releasing. This means that you only publish a new version of a package when you need to.
