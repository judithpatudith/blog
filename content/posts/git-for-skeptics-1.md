---
title: "Git for Skeptics: Part 1 - Why do I need a million copies of this folder?"
date: 2018-05-08T10:39:17-08:00
draft: false
---
# Why write another intro to Git?

I feel nervous using systems that I don’t understand. When I started work as Mesosphere’s community manager, I needed to learn a basic Git workflow quickly so that I could begin maintaining our open source project’s website right away. But, I had a hard time understanding the workflow because I didn’t quite understand the point of using Git.

The process of forking, cloning, pulling, branching, saving, testing, adding, commenting, committing, pushing, testing again, discussing, and then going six rounds of this process — just to improve website copy — seemed like gross, jargony overkill. It filled me with annoyance, which made the workflow hard to learn.

So, this post and the next one aren’t tutorials or walkthroughs. They’re basic overviews meant to describe a typical Git workflow, and explain the purpose of each step. I hope they can serve as a framework for people who don’t find joy in mechanics but will value them once they understand how those mechanics fit into the bigger picture.

# Why do people use Git?

Git is a version control system: people use it to control who can propose and approve changes to files. To do this Git helps project maintainers keep careful track of who made which changes to a file when, and why.

Anyone can propose changes, but only a few responsible people can accept them. And a single person can work on many changes at a time. To manage these complications, Git (the tool) and GitHub (a collaboration website) can make and save many versions of a file, each with different permissions or for a different purpose. Even when a project only has a single contributor, he or she will frequently use Git, to prepare for the possibility that others will contribute to the project in the future.

The “real” version of a project — the code that builds a public website, for example — is usually stored online in GitHub. When someone wants to make changes to that real version, they need to make a series of personal copies, to protect the “real” version from mistakes, and to make it easy for approvers to understand the changes they want to make.

In this blog, I’ll walk you through the process of copying the official version of a project and explain the purpose of each copy. After we walk through the purpose of these copies, the next post will discuss how to make changes to the files you’re working on, package them up, put that work online, and ask project maintainers to accept your changes.

## Prerequisites:

### Create a GitHub account.

GitHub is a website where project owners keep the official versions of their files, and where other people propose changes to those official versions. For example, the open source product I work on, DC/OS, has all its official files at github.com/dcos. The product’s website, dcos.io, builds from code stored on GitHub at github.com/dcos/dcos-website. Before you can contribute to a project, you’ll need to create a GitHub account for yourself. You can find mine at github.com/judithpatudith.

### Install Git on your computer.

Git is the version control system that helps track changes to files. It runs on your computer and is easiest to interact with through a terminal. If you make a mistake, Git will frequently print a helpful output into your terminal to suggest the correct command.

There are many graphical user interfaces for Git, but adding another layer of abstraction on top of a system that’s already really complicated has always felt (at least to me) more confusing than helpful.

# Copy the project you want to edit.

Once you have a GitHub account and Git installed, you’ll copy the project you want to work on. You will make two copies of the project: one online, and one local. Git will allow you to make many versions of your local copy. Each of those versions will represent a separate piece of work.

The copying process might seem redundant and unnecessary, and it is — if you only plan to contribute to each project once. But, most projects on GitHub will have multiple contributors, and each of those contributors will work on numerous changes at once. Each copy allows contributors to keep multiple, unrelated changes separate, and helps project maintainers to reconcile simultaneous edits from various contributors. Bellow, I’ll explain the goal of each copy and version.

To recap: a typical GitHub workflow uses the following copies/versions:

1. The “real” online copy of the project, which is controlled by someone else.
1. Your online copy on GitHub, which you can add to, and use to request changes.
1. The copy on your computer where you make and test your edits.
1. The many versions on your computer that you use to keep various unrelated pieces of work separate.

You only have to make your online and local copies once.

## Your online copy (fork).

To start contributing code to a project, the first thing you need to do is make an online copy of the official project that you can control. Once you’ve made your changes, you will add them to your online copy. The project maintainers will use GitHub to compare your copy with theirs and decide whether or not to accept your changes into the official version. They don’t want you to change the official version yourself, because if they didn’t like your changes, they would have to back them out. Your online copy allows maintainers to retain complete control of the official version.

A copy of a Git project folder is called a “repository” or “repo” for short. Repos contain extra git versioning information that helps Git keep track of changed files. The name “repo” distinguishes folders that can interact with Git from those that can’t.

To make an online copy of a repo, you’ll click the “fork” button at the top right of the screen. This will give you a new copy of the repo in your GitHub account. For example, when I forked the DC/OS website repo, I got a copy of it in my GitHub account at github.com/judithpatudith/dcos-website/.

GitHub provides an online GUI for editing files stored there, but using it isn’t good practice because:

- You can’t test any files you’re editing while they’re online, which makes it hard to know whether you’re fixing things or introducing new mistakes.
- Saving modifications online using GitHub creates an official record of each save. If you’re working on a file and need to save it multiple times, all these extra records could confuse the person who ultimately has to approve your work.

## Your local copy (clone).

To properly make and test your edits, you’ll need a local copy of the repo on your personal computer. Making changes locally separates your work-in-progress and testing from the approval process.

For example, the website repo I work on contains tools that can build a copy of the website on my computer. I can open that website in my browser, and it will update in real time as I save changes. Testing like this is helpful for me because I know right away when I make a mistake. I couldn’t do live testing if I just edited my online copy of the repo directly.

The testing necessary for each project is different, and some projects won’t have any test tooling. But, you will still want to make all your edits on your local copy instead of online. Having a local copy lets you save your work in progress without creating public records of each save (a must for newbs like me who make a lot of changes and mistakes), and lets you use your favorite text editor (experienced developers care about this a lot).

Downloading a copy of a repo is called “cloning.” Cloning a repo isn’t the same as downloading a folder because, in addition to the project files themselves, cloning also gets you all the version information for the repo. You can clone a repo using the `git clone` command, followed by the pastable information that pops up when you click the green “clone or download” button on your fork of that repo.

The copy of the repo you download will serve as your sandbox. It’s where you mess things up, try things out, and ultimately make the changes you want. Git doesn’t automatically create any records for the changes you save in this repo. You will tell it which files you want to be included in a given record later on.

## Your separate pieces work (branch).

Often one contributor will be working on multiple different changes to the same repo. To account for this, Git lets you create many different versions of the same repo, called “branches.” Ultimately when you ask someone to review changes, you will ask them to accept or reject all the edits on a single branch.

For example, I might be simultaneously working on unrelated changes to dcos.io/releases and dcos.io/community. My boss might need to accept my edits to the community page, and another manager might need to accept my edits to the releases page. Git version control lets me keep these two sets of changes on separate branches (even though I’m working on both at the same time) so that I can ultimately submit them to two different approvers.

Even if the same person will review all your changes, it’s still kind to keep unrelated pieces of work separate. It makes it much easier for your reviewer to understand the goal of your changes and accept them later.

### The relationship between branches and the repo’s directory.

You might be tempted to think of each branch as a different copy of your project files, but technically branches aren’t copies. You’ll interact with all the branches of your repo in the same directory on your computer. When you’re in that directory, you will always be looking at one version of that directory (one branch).

When you switch to a different branch of the repo, most of the files in your directory will change to look like the version you’ve just selected. But, if you’ve saved changes to any files, those will stay the same as they were when you last saved them, regardless of what branch you check out. Git knows that you’ve intentionally changed those files, and is waiting for you to tell it which version of the project to add the changes to (or for you to tell it that you don’t want to keep the changes).

Maintainers can only review changes that have been added to a branch. Branches tell them which version of your repo to compare to which version of theirs.

# For Mechanics see Part 2.

In this post, we’ve gone over all the copies of a project that you need to make in order to propose edits: your online copy which you have permissions for, your offline copy for testing, and the many versions of your offline copy, where you store separate pieces of work. In the next post, we’ll discuss how to make changes, select which ones to include in your change requests, and how to put them on the online where project maintainers can review them.
