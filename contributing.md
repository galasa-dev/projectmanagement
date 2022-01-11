# Contributing to Galasa

Anyone can contribute to the Galasa project and we welcome your contributions!

There are multiple ways to contribute: report bugs, fix bugs, contribute code, improve upon documentation,etc.  You must follow these guidelines:
* [Raising issues](https://github.com/galasa-dev/projectmanagement/blob/main/contributing.md#raising-issues)
* [Coding Standards](https://github.com/galasa-dev/projectmanagement/blob/main/contributing.md#coding-standards)
* [Raising documentation issues](https://github.com/galasa-dev/projectmanagement/blob/main/contributing.md#raising-documentation-issues)

## Raising issues
Please raise any bug reports on the [Galasa project repository's GitHub issue tracker](https://github.com/galasa-dev/projectmanagement/issues). Be sure to search the list to see if your issue has already been raised. If your issue is already raised, feel free to leave a comment to let us know you have found the same issue or to add useful information. See something that you might be able to help with? Show us your best solution!

You can raise a new issue by clicking the "New issue" button on the [Issues tab](https://github.com/galasa-dev/projectmanagement/issues) of the project management repository. Add a title and description for your issue. If you can, label your issue to help describe what area(s) the issue falls under. You can select more than one label if applicable. When you're finished, click "Submit new issue".

A good bug report is one that make it easy for everyone to understand what you were trying to do and what went wrong. Provide as much context as possible so we can try to recreate the issue.


## Coding Standards

If you would like to contribute code, please ensure you follow the coding standards used throughout the existing code base. Some basic rules include:

* all files must have a Copyright including [EPL license](https://github.com/galasa-dev/managers/blob/main/LICENSE) in the header.
* all submissions must have a signed [Developer Certificate of Origin](https://github.com/galasa-dev/managers/blob/main/CONTRIBUTIONS.md)
* all pull requests (PRs) must have a passing build.


All changes should be contributed as pull requests:

   1. Make a fork of the relevant repository (top-right).
   2. Make your changes in a branch of your fork.
   3. Create a pull request for your changed branch. 
   
We ensure changes pass our series of verification buckets before pushing to main.

- A team of "reviewers" will be notified of the pull request, will perform a review, and if approved will invoke a full integration build.
- Based on the results of the build, and if further review is needed, we might need to ask you for a bit more information.
- If the reviewers are happy with the results, and agree to the change, the PR will be merged, otherwise the PR will be closed with an explaination and suggestion for followup.

## Raising documentation issues

If you find something incorrect or incomplete in our docs, let us know. For new topics, large updates to existing docs, or general suggestions and ideas, create an issue in the [galasa.dev repository](https://github.com/galasa-dev/galasa.dev/issues).

All changes should be contributed as pull requests:

   1. Make a fork of the [galasa.dev repository](https://github.com/galasa-dev/galasa.dev).
   2. Make your changes in a branch of your fork.
   3. Create a pull request for your changed branch.

Please format your code using Prettier:

```npm run format```
