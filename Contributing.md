---
path: "/docs/support/contributing"
title: "Contributing to Galasa"
---


# Contributing to Galasa

Anyone can contribute to the Galasa project and we welcome your contributions!

There are multiple ways to contribute: report bugs, fix bugs, contribute code, improve upon documentation,etc.  You must follow these guidelines:
* [Raising issues](https://github.com/galasa-dev/projectmanagement/CONTRIBUTING.md#raising-issues)
* [Coding Standards](https://github.com/galasa-dev/projectmanagement//CONTRIBUTING.md#coding-standards)
* [Raising documentation issues](https://github.com/galasa-dev/projectmanagement/CONTRIBUTING.md#raising-doc-issues)

## Raising issues
Please raise any bug reports on the [Galasa project repository's GitHub issue tracker](https://github.com/galasa-dev/projectmanagement/issues). Be sure to search the list to see if your issue has already been raised.

A good bug report is one that make it easy for everyone to understand what you were trying to do and what went wrong. Provide as much context as possible so we can try to recreate the issue.

We ask you follow these steps through the submission process.
1. Open PR's against the "projectmanagement" branch, as we ensure changes pass our series of verification buckets before pushing to master.
2. A team of "reviewers" will be notified, will perform a review, and if approved will invoke a full integration build.
3. Based on the results of the build, and if further review is needed, more discussion will occur.
4. If the reviewer is satisfied with the results, and agrees to the change, the PR will be merged, otherwise the PR will be closed with an explaination and suggestion for followup.


## Coding Standards
Please ensure you follow the coding standards used throughout the existing code base. Some basic rules include:
* all files must have a Copyright including EPL license in the header.
* all PRs must have a passing build.

## Raising documentation issues

If you find something incorrect or incomplete in our docs, let us know. For new topics, large updates to existing docs, or general suggestions and ideas, create an issue in the *galasa.dev* repository.
All changes should be contributed as pull requests:

   1. Make a fork of this repository (top-right).
   2. Make your changes in a branch of your fork.
   3. Create a pull request for your changed branch.

Please format your code using Prettier:

```npm run format```
