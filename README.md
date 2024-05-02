# Template repo for PHP SDK

This template helps developers get started with publishing the PHP SDK to Packagist package repository.

## Contents

This repository contains the following:

- A `README` that contains the instructions

## Instructions

1. Create a new target PHP SDK Repo by clicking the **Use this template** button at the top of this repository.

1. If you already have a Control Repo:

    1. Update your `LIBLAB_GITHUB_TOKEN` actions secret to a new token that has access to all your existing SDK repos, as well as this new one.

    1. Update the [`githubRepoName` field in the `php` section](https://developers.liblab.com/cli/config-file-overview-language/#githubreponame) of your liblab config file to the name of your new repo.

1. Run the GitHub Action `Generate SDKs using liblab` in the Control Repo that builds the SDK, and raises a PR against this target SDK Repo. This will be triggered automatically when you commit and push the update to the liblab config file.

1. Review and merge the PR.
