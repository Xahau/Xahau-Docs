---
description: >-
  This document outlines our versioning workflow on GitHub, to streamline the
  development, testing, and deployment of new features and fixes.
---

# Versioning Process

This document outlines the versioning process we use in our GitHub repository. We use a three-branch workflow: `dev`, `candidate`, and `release`. This process ensures that all new features and fixes are thoroughly tested before release.

### Dev Branch

The dev branch is the main branch for ongoing development. All new features, bug fixes, and improvements are merged into this branch. This is the most active branch, and it's where developers should base their work.

To contribute to the dev branch, follow these steps:

1. Fork the repository to your own GitHub account.
2. Clone the forked repository to your local machine.
3. Create a new branch for your feature or bug fix.
4. Make your changes and commit them to your branch.
5. Push your branch to your forked repository on GitHub.
6. Create a pull request from your branch to the dev branch in the main repository.

{% hint style="warning" %}
All merges into the dev branch must be squashed
{% endhint %}

Code maintainers will review your pull request and provide feedback. Once the code is approved, it will be merged into the dev branch.

### Candidate Branch

Once the features in the `dev` branch are ready for testing, they are merged into the `candidate` branch. This branch serves as a staging area for code that is almost ready for release.

The code in the `candidate` branch is thoroughly tested. Any bugs or issues found are fixed in the `dev` branch and then merged back into the `candidate` branch.

The `candidate` branch is typically in this testing phase for about 2 weeks. However, this period can be longer or shorter, depending on the urgency of the fixes or the size of the new features.

1. Create a new PR from the `dev` branch to the `candidate` branch with a name like "Proposed."
2. Update the "High Level Overview of Change" to include the Pull Requests from `dev`. Update the "Context of Change" to include any additional notes about the PR's
3. Merge the pull request into the release branch.

{% hint style="warning" %}
All merges into candidate branch must be done with \`git merge --ff-only dev\`
{% endhint %}

### Release Branch

After the code in the `candidate` branch has been thoroughly tested and all issues have been addressed, it is merged into the `release` branch. This is the final step before the code is released.

The `release` branch contains the code that is currently in production or is about to be released. Only fully tested and stable code should be in this branch.

Once the code is in the `release` branch, it is tagged with a version number. This version number is used to track the release and is also used when creating release notes.

In the `release` branch, a binary is built and published at https://build.xahau.tech/. This binary is the final product that is delivered to the end users.

To release the code, follow these steps:

1. Create a new pull request from the candidate branch to the release branch with a name like "Release".
2. Review the changes and ensure that all tests have passed.
3. Merge the pull request into the release branch.

{% hint style="warning" %}
All merges into the release branch must be done with \`git merge --ff-only dev\`
{% endhint %}

### Summary

This three-branch workflow ensures that all code is thoroughly tested before release. It allows us to catch and fix issues before they reach production, and it provides a clear path for moving code from development to release. The use of a custom LAN for testing and profiling metrics ensures that our code is not only functional but also efficient and performant.

