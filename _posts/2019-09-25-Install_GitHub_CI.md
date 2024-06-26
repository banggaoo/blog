---
title: "Install GitHub CI"
date: 2019-09-25
---

After installed Fastlane, i try to integrate automate build and test with git remote for implement CI. I already use Gitlab CI but i wanna try GitHub CI also.

GitHub CI concept is not different with Gitlab CI. I can add action by adding workflow data in yaml format.

If i want to use Cloud service, there is a virtual environment for MacOS for build iOS app. Fastlane is also installed. So i can test and distribute on virtual machine.

But for distributing apps certificate and provisioning profile are needed. These are sensitive informations so i want to use my own machine.

If i want to trigger CI job on my own machine when GitHub workflow triggered, i have to use javascript action.

Overall there are lots of todo for implement CI on GitHub. GitHub CI is still in the beta so i will look forward to improve.

[About GitHub Actions](https://docs.github.com/en/actions/learn-github-actions?source=post_page-----e34179e23787--------------------------------)
[Creating a JavaScript action](https://docs.github.com/en/actions/creating-actions/creating-a-javascript-action?source=post_page-----e34179e23787--------------------------------)
