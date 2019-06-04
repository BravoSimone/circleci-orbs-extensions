# DO NOT USE ME YET

I'm an experiment and master branch will be force pushed!

<hr>

This repo is an experiment to see if we can use CircleCI Orbs to automate
builds configuration on all our extensions.

### The problem

Everytime a new Solidus version is released or goes EOL we need to refresh
the CI configuration adding or removing a version.


### Orbs Solution

Using Orbs we can define a shared configuration that every extensions will
use at its latest version.

#### Steps taken

This is just my personal notes, I think we'll remove them later if this works.

#### Created a namespace

This is needed only for the first time, new orbs will not need this

```
> circleci namespace create solidusio github solidusio
```

#### Created this orb

```
> circleci orb create solidusio/extensions
```

#### Validate the orb

```
> circleci orb validate orb.yml
```

#### Publish the orb

The [orb-tools Orb](https://github.com/CircleCI-Public/orb-tools-orb) is used
for publishing development and production versions of this Orb.

PRs will create a development release of the orb, while merging in master will
release a new version of the orb, using semver and following these rule:

> Modifications to jobs or commands trigger a potential major release;
> modifications to executors, examples, or @orb.yml trigger a minor release;
> modifications to the orb’s config.yml file trigger a patch release;

Or you can release manually:

```
> circleci orb publish orb.yml solidusio/extension@dev:first
> circleci orb publish orb.yml solidusio/extension@dev:first patch
> circleci orb publish orb.yml solidusio/extension@dev:first minor
> circleci orb publish orb.yml solidusio/extension@dev:first major
```
