# Xamarin-GitHubActions-DevOps
 This repo contains the result of my work combining GitHub Actions with Xamarin to Automatically Build iOS & Android apps

You can take a look at the article [here](https://levelup.gitconnected.com/using-github-actions-with-ios-and-android-xamarin-apps-693a93b48a61?source=friends_link&sk=cd81773f2e5a5931ae49c9362b4db795) that has more details. It will also give you a better understanding of what you see in the Actions folder.

Also, here's a short snippet of what to do [for GitLab](https://stackoverflow.com/questions/42757115/has-anyone-successfully-built-xamarin-forms-with-gitlab-ci/63233029#63233029)

The master branch has a working CI/CD pipeline, the other branches are all experimental branches. To test the CI/CD functionality, clone this repo, create a branch with a text change in a new branch based on master, and then create a PR. That will launch a GitHub workflow Action
