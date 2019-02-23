---
title: "Git for Skeptics: Part 2 - Why is saving changes so freaking complicated?"
featured_image: '/images/luke-van-zyl-562366-unsplash.jpg'
date: 2018-11-08T11:22:03-08:00
draft: false
---
In my last post I explained why you need to copy a repo so many times to edit it with Git. Don’t know what a “repo” is? See Part 1.

In this post, I’ll explain why saving a change with Git is so complicated. Each step accomplishes a separate goal and serves as a checkpoint where you can backtrack or edit. The whole process includes making testable modifications, grouping those changes by goal or step, explaining your groups of changes and assigning them to a branch, putting the changed branch online, and asking your reviewer to have a look.

# What’s the point of Git history?

When I first started using Git, I thought I was creating a record of my edits so that maintainers could back out my changes if I made a mistake. I was confused about why Git included so many tools for editing change records if the whole point was to keep track of the work I had done.

![Photo by Giammarco Boscaro on Unsplash](/images/giammarco-boscaro-380907-unsplash.jpg)
[_Photo by Giammarco Boscaro on Unsplash_](https://unsplash.com/photos/zeH-ljawHtg/)

What I’ve learned is that Git history isn’t intended to tell the story of my editing process. Instead, it’s supposed to explain what changes I want to make to a file and why. It should help my reviewers evaluate:

1. whether or not they agree with my stated goals.
1. whether the changes I’ve proposed accomplish what I said they would.

With that big picture in mind, let’s talk about the purpose of each step to make and propose changes.

# Lets make history!

So, now that we know what we're trying to accomplish, lets walk through each step required to make changes with git, and explain to repo maintainers why they should accept your changes.

Those steps are:

1. Make sure you know which branch you're editing.
1. Create a new branch for your changes.
1. Make, save, and test your changes.
1. Group changes based on their goals.
1. Explain those groups of changes.
1. Put the changes and explanations online.
1. Ask for a review.

## Base changes on the branch you’re trying to edit.

As we discussed in the previous post, whenever you look at a Git repo, you are always looking at one specific version called a branch. When you switch versions, all the files you are looking at refresh to match the version you selected. It doesn’t matter whether you’re looking at the repo’s directory in your terminal or using your computer’s GUI; if the directory you’re looking at has Git versioning information in it, you are always looking at a specific version.

When you clone a repo (download it from GitHub), it already has one or more branches in it. You must base your edits on the branch that you ultimately want to change. That way the only differences between the original branch and your new one should be the changes you propose.

![Photo by Luke van Zyl on Unsplash](/images/luke-van-zyl-562366-unsplash.jpg)
[_Photo by Luke van Zyl on Unsplash_](https://unsplash.com/photos/zrT3d_PI8YA/)

Creating a new branch for your changes protects your copy of the original branch from mistakes. If you mess up while editing and accidentally commit unwanted changes, you can always create another new branch from the original version and start over. If you edit the original directly, it’s more complicated to start over when things get too weird to fix.

Making a new copy of the branch also helps keep your local repo synchronized with the online copy. Git can easily update local branches from the corresponding branch online — if you haven’t changed the local branch since you last synced it with the online one. So, if you plan to propose changes to the same branch frequently, you only want to change the local branch by pulling in approved changes from the online copy. If you don’t own the repository you are contributing to you can set up your local copy to update from the official online copy instead of your online copy, by adding it as a “remote.” Your local branch then updates with all the newest changes, not just the ones you made yourself.

When you want to start editing, first switch to (or “checkout”) the branch you want to edit with the command `git checkout` followed by the branch name. Always make sure it is up to date with the official online copy before you create a new branch to edit. You can do this by downloading (or “pulling”) recent fixes from the online copy with the command `git pull`. Then you’ll be ready to create and switch to your new branch by using the checkout command again with the option `-b` (which creates a new branch) followed by the new branch name.

Branch names should only be a word or two, but try to be descriptive. For example, if I were going to create a branch to add this post to a blog, I might name it `jm/git-blog_2` (my initials and a description of my goal). Your reviewers see your branch’s name and interact with it since they check your changes by downloading your branch, and ultimately accept or reject all the changes on the branch at once.

## Make, test, and save a change.

Now that you’ve created a branch for your edits, it’s time to start changing things.

Some Git repos contain tools that watch your local directory (or a part of it) for saved changes and check to make sure that the code still works. If your repo has tooling like that, you should start it before you start editing, so that you’ll immediately know if you make a breaking mistake.

For example, the repos for many websites contain code that builds the website on a developer’s computer, makes it available through their browser, and updates when they save their files so they can see their changes live.

GitHub can’t provide an environment to run tests in the same way that your computer can, and for complicated changes, it’s powerful to get immediate feedback as you work, especially if you’re new to coding. Testing is one of the main reasons to make a local copy of your repo, and you should definitely test if you can. I like to start my tests before I even begin editing, so I know I’m not starting with broken code.

![Photo by rawpixel on Unsplash](/images/rawpixel-602156-unsplash.jpg)
[_Photo by rawpixel on Unsplash_](https://unsplash.com/photos/cFHTKGEiMbY)

Git isn’t keeping a record of saved changes in your directory yet or adding them to any particular branch. It’s annoying that saving changes isn’t enough to edit a file with Git, but there’s a reason: it gives you the ability to experiment without creating Git history and avoids confusing your reviewers with your trial and error. Requiring that you explicitly add changes to the Git record is the control part of version control. Once you’re happy with a change, you can add it to your branch. Before you’re happy, the changes don’t belong to any particular version at all and are “invisible” to your reviewers.

## Bundle changes that share a goal.

Next, it’s time to decide how to best explain your changes to your reviewers, by grouping them. For example, I might want to change the title of a blog post, add a filter to all the pictures, and swap the first two sentences because of feedback from my boss. All of those changes would happen on the same branch, but they’re all independent of each other and would have different explanations.

Grouping your changes by their goals helps reviewers to evaluate whether or not your edits do what they were intended to. For example, when I add a filter to all the pictures in a blog post, I change multiple flies to address the same feedback. If I accidentally replace one of the pictures instead of adding a filter and explain all the changes with a note saying “Add a filter to pictures.” my reviewer can easily see that not all the changes I made do what I described.

![Photo by Anurag Arora on Unsplash](/images/anurag-arora-193335-unsplash.jpg)
[_Photo by Anurag Arora on Unsplash_](https://unsplash.com/photos/4_TruUQJWnY)

You can check which files you’ve saved changes to by using the command `git status`. Files with saved changes appear in red. You can collect (or “add”) the files you want to explain together by using the `git add` command followed by the file path. If you recheck the status, you will see that your added file displays in green.

It’s possible to add all the files you’ve changed at once, but I’d recommend adding them individually. It’s easy to lose track of the project you’re working on or accidentally save changes to files that aren’t part of your current work. You can exclude those changes by not adding them, which means that they won’t be included in Git history and won’t be sent to your reviewer to check or approve. Grouping files manually, one by one prevents any unintended changes from sneaking onto your branch.

Adding your files doesn’t commit them to any branch. Using Git, the process of selecting files and committing them to a particular branch are separated, to protect your branch from changes that aren’t related to the piece of work represented by your particular branch. If you accidentally add a file that is unrelated to your current work, you can remove it from the group before you commit it, preventing it from confusing reviewers and keeping your Git history clean.

## Make a record of your changes.

Once you’re happy with the files you’ve grouped, it’s time to save them to the branch you’re on and create a record in Git to explain the changes you’re requesting. This process is called “committing” the changes. You commit changes to your branch and add a message by typing `git commit -m` followed by your message in quotes. This command commits your changes to the branch you have currently checked out.

As we discussed earlier, your message should tell your reviewer what the changes in the current files are supposed to do. It might seem unnecessary for a blog post or simple change, but for code changes, it isn’t always immediately apparent what each edit does. Breaking these changes down into pieces can help your reviewer evaluate your design and each change. Try to make sure your commit message is short and specific.

![Photo by João Silas on Unsplash](/images/joao-silas-74207-unsplash.jpg)
[_Photo by João Silas on Unsplash_](https://unsplash.com/photos/I_LgQ8JZFGE)

Commits are the indivisible, atomic units of Git history. Making one change per commit is called “commit atomicity” and is a requirement for contribution to many open source projects. Think of each commit as a sentence in an essay. The commit messages you record cumulatively make up your first draft.

Git has advanced tools to edit your commit messages, which can improve how the “essay” reads to your reviewers. But, for beginning contributors, a reasonable effort to make one commit explaining each building block of a project is usually enough. Your mentors or reviewers might like to use these tools to help improve your work. Because commits are the atomic units of Git history, frequently committing small changes helps your collaborators make smaller and more specific tweaks.

## Put your changes online.

Once you’ve committed your changes, its time to put them online. If you’re still working on your edits, you’ll want to do this to back up your work, and if you’re finished, you’ll need to do it so that your reviewers can evaluate the changes you’re proposing. When you upload changes, you upload everything that has been committed to your branch at once and nothing that you haven’t committed. Make sure you’ve committed your work before trying to upload it.

You can only upload your changes to a GitHub repository that you have permission to control. If you’re contributing to a project that you don’t own, this online repository is your fork of the original project. You upload the branch you made your changes on using the `git push` command followed by the online repo you want to upload to and the branch name.

![Photo by Daria Nepriakhina on Unsplash](/images/daria-nepriakhina-608450-unsplash.jpg)
[_Photo by Daria Nepriakhina on Unsplash_](https://unsplash.com/photos/guiQYiRxkZY)

If you need to keep working on your branch later, you can make more changes locally, add them, commit them and push the new commits to the same branch.

## Request a review.

Now that your changes are online as part of a new branch, you can ask reviewers to take a look at them by opening a pull request (PR for short). A pull request is a GitHub-specific concept that makes it easy for reviewers to see the difference between your branch and the original one, and see which changes are part of which commit. Your PR is also where you get feedback from your reviewers. They can comment on your changes line by line and ask for improvements.

![Photo by Trey Gibson on Unsplash](/images/trey-gibson-730708-unsplash.jpg)
[_Photo by Trey Gibson on Unsplash_](https://unsplash.com/photos/LxphooAHzvc/)

To make those improvements, all you need to do is go back to your local copy, make the requested changes, commit them, and push them to the same branch. Anything you push to your branch automatically shows up on the open PR.

PRs can either be merged or closed. There isn’t a way within the pull request process for your reviewer to accept some commits and not others. Once your reviewer is happy with all the changes on your branch, they will merge it into the original branch you wanted to change. Congratulations, your changes are now done!

# Geez, that was a lot of work!

Even though there are many steps required to make changes in Git, they all make sense once you know why they are necessary. Changing files locally on your computer lets you experiment and test your changes without confusing your reviewers. Adding files lets you group them into easily explainable atomic changes. Committing them lets you explain each group and creates your Git history. Pushing them puts them online where reviewers can see them. Opening a PR opens up a conversation about them with your reviewers. Finally, the merge gives your reviewers ultimate control over what changes get made to their projects, so they can make sure that nothing breaks.

The long process of making and saving changes is designed to facilitate a conversation between you and the maintainers of your target project, and protect that project from breaking changes. I hope my explanation gives you a better understanding of the jargon and process necessary for contributing to open source software with Git! I hope it gives you the patience to slog through the Git documentation — patience that I didn’t have when I was first starting. Happy Hacking!
