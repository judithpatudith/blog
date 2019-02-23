---
title: "GitHub: 10 tips for good pull requests"
featured_image: '/images/vidar-nordli-mathisen-593129-unsplash.jpg'
date: 2019-02-17T09:11:40-08:00
draft: false
---

A pull request is a GitHub-specific concept that allows reviewers to compare changes you request with the current versions of the files you're changing. For background on the process of changing files with Git see the introductions.

# What's the point of a Pull Request?

A Pull Request (PR) is a collection of commits that you ask to copy from one branch of a project to another, plus metadata that GitHub provides to help you and your reviewer talk about the changes in those commits. When you open a PR, you are asking a repo's maintainers evaluate and hopefully accept all of the changes on a particular branch that you created. Your PR should explain two things to your reviewers, what you want to change, and why you want to change it.

# What makes a PR good?

Good PRs are easy to understand and evaluate. It can help to think of your PR like a persuasive essay. A  good one should be self-explanatory and should consider your reader's point of view. It should be easy to merge, and hopefully the process of merging it will build the relationship between you and your reviewer.

## PR's should be self-explanatory.

Open source projects can have many places where members discuss potential changes. You might use chat or a forum for discussions, design docs for architecting new features, or tracking software for reporting bugs and improvements. You might have discussed the change you're requesting at length in one (or more) of these systems, but you should still briefly summarize the conclusions from that discussion in your PR.

Many projects ask you to include an issue number in your PR, and if they ask for it, you should include it for reference. However, an additional brief description of the issue in the PR can do two things for your reviewers:

1. Gives them the immediate context in case they are already familiar with the issue.
1. Helps them search for your PR when they have many to review.

![Photo by kevin laminto on Unsplash](/images/kevin-laminto-634747-unsplash.jpg)
_[Photo by kevin laminto on Unsplash](https://unsplash.com/photos/nYqNbJR-c6o)_

The summary is especially helpful if you've discussed the issue in more than one place. No one wants to dig through a bug tracker, their chat history, and three design docs to find out how a change should look. Give your reviewer the TL;DR (Too Long; Didn't Read) summary, and add the links to sources for their reference, just like you would if you were writing an essay.

## Consider your reviewer's point of view.

When you are deciding what information to include in your PR, consider the reviewer's point of view. Most projects value contributions and want to take them when possible. It's possible to accept changes that benefit the project and don't introduce errors or other problems. Those two criteria are what your reviewer is trying to check. Help them by being clear about what your changes should accomplish and what you changed.

![Photo by Gaetano Cessati on Unsplash](/images/gaetano-cessati-128379-unsplash.jpg)
_[Photo by Gaetano Cessati on Unsplash](https://unsplash.com/photos/IIMPbLjtKL8)_

Leave out information about your working process, or the story of how you made your changes. As a beginner, I was very inclined to give these details to show my reviewer that I had done my work correctly, but I quickly found that they were at best unnecessary and at worst confusing.

If there are problems with your process that show up in your PR, your reviewer can ask about them. If this happens, it is totally ok, and an excellent opportunity to learn. Following the persuasive essay analogy, you wouldn't include details about your writing process in your essay itself, but your editor might give you notes on it. The same is true for PRs.

# Making PRs easy to merge.

There are a few things you can do while making changes that make it significantly easier for reviewers to accept your PR. Best practices make it easy for your reviewers to understand the changes you made, and easy for them to incorporate those changes into the current state of the repo.

## Maintain commit atomicity.

Atomicity is the idea that each commit in your history should contain the smallest unit of explainable change. Your commit messages are like the sentences in an essay, and commit atomicity helps your reviewers check that your changes line up with your intentions.

When your reviewer evaluates your PR, they can walk through it commit by commit, and check that each commit accomplishes the right thing. Viewing individual commits is a massive help for reviewers evaluating big PRs, so they don't have to think about every file at once.  

## Keep PRs small if possible.

Big PRs that touch many files or drastically change things are hard to accept, for three reasons.

1. *They're hard to understand.* It might be tough for reviewers to understand the approach you used to make a significant change, or how each commit relates to that approach.
1. *They're hard to evaluate.* It might be hard for reviewers to check whether or not your changes all do what you say they do, or if they might have unintended consequences.
1. *They're hard to merge.*  When your PR changes lots of files, chances are higher that someone else could change one of the same files you did during the time that it takes to make and review your PR. If their changes overlap with yours, it causes a conflict. Git won't know which version to accept. Conflicts make it more complicated to accept your changes and require additional steps to resolve.

![Photo by Vidar Nordli-Mathisen on Unsplash](/images/vidar-nordli-mathisen-593129-unsplash.jpg)
_[Photo by Vidar Nordli-Mathisen on Unsplash](https://unsplash.com/photos/cSsvUtTVr0Q)_

Sometimes it's necessary to make big PRs. If you know you have to make significant changes, consider whether you can break your project up into incremental improvements that each add functionality that stands on its own. It usually isn't a good idea to open a PR that relies on other PRs to function, so if you think your PR might be too big to review, strategize with your reviewer about your plan before you start changing things.

## Consider how long your project takes.

Significant changes take longer to make and review than small ones. The longer your change takes to get accepted, the higher the risk that you'll run into issues with Git's concept of "time."

There are many resources on Git's concept of time, and most of them are very confusing because Git's "timeline" has literally nothing to do with time, and it turns out that time is a pretty crappy analogy for it. Git's "timeline" is the sequence of the commits on a particular branch (which has nothing to do with the time at which you made those changes, and which you can manipulate in almost every conceivable way, entirely unlike time).

![Photo by Nathan Dumlao on Unsplash](/images/nathan-dumlao-553945-unsplash.jpg)
_[Photo by Nathan Dumlao on Unsplash](https://unsplash.com/photos/LPRrEJU2GbQ)_

I'll add more details on this in another post. For now, the important thing to know is that if you spend a lot of time making changes, the chances are high that someone else will have changed the official version of the project while you were working. In this case, Git has a few options about where in the branch's commit sequence to put your changes. If your changes and someone else's conflict, things get even more complicated.

# Project specific considerations.

The above set of best practices apply to many of the PRs that you make, especially as a new contributor. Many repos have additional rules about making and submitting changes, which can vary a lot from repo to repo. Before you open your PR (and ideally before you start making your contribution) look in the repo for a file called CONTRIBUTING.md or something similar. If present, it contains useful information about how to make changes, format commits messages, or submit your PR. Of course, if anything in the contributing file disagrees with the guidelines I laid out here, follow the maintainers' instructions rather than mine.

## Use the template.

Some repos have formatting inside of the GitHub Graphical User Interface (GUI) window where you fill in the description of your work. If the repo you're contributing to has this templating, conform to it as closely as possible. The repo maintainers customized the template to tell contributors what information they should include in their PRs.

## Commit message formatting.

Some repos have guidance on how to format your commit messages. Depending on the way that repo maintainers merge your PR, these rules may apply to every commit message or only the last one, which GitHub generates from the subject and description you add in the GUI. If you aren't sure how to format your commit messages for a project, ask a maintainer.

# Notes on etiquette

A pull request, at its heart, is a way for humans to communicate. Although you’re communicating about technology, there’s a human on the other end of the line. You and your reviewer will each bring your own attitudes, expectations, and previous experience to the review process. There also can be language barriers and other communication challenges. A PR usually involves giving and receiving feedback, which in itself can be a delicate process, and to complicate matters, this feedback is mostly in writing, online, and public.

If you work in technology, employers can look at your GitHub profile as a type of portfolio, to see what work you do and how you go about it. It’s a good idea to communicate well when opening and corresponding on PRs, to build strong relationships and demonstrate your working style.

![Mind Feast](/images/113879892_da760475e7_o.jpg)
_Photo by Judith Malnick_

## Be patient

Standards for time to first response and time to review differ from project to project and depend on whether or not you are an employee of the company that controls your target project. Give the project maintainers some time to get back to you about your PR. I would not expect a 24-hour response. A week is getting a bit long, even if you are an outside contributor, and I’ll usually comment on my PR after about five business days to bump it back up to the top of a maintainer’s inbox.

## Always try communicating on the PR first

A PR is a tool for communicating about changes, and it only works if you use it. If your reviewer has given you notes you don’t understand, ask for clarification by replying to their comments on the PR. If you haven’t heard back from your reviewer in a while (or haven’t made the first contact with a reviewer after five days) always ping them on the PR before sending them a message on another channel (e-mail, slack, whatever).

When you’ve pinged them a couple of times on the PR, have been waiting for a response for over a week, and have a pressing reason that you need a prompt review, it might make sense to ask them about it another way. If you do this, always include a link to your PR in your note to them, so they don’t need to hunt around for it.

## Be kind

A pull request is just that, a request. If you are contributing to an open source project that you aren’t employed to work on you are doing that project a valuable favor, but you also get something out of your contribution: perhaps experience, the functionality you need, or entertainment.

Whatever your reason is for contributing, make it a mutually beneficial and enjoyable process by being nice. Being kind to your reviewers can also get you faster and more detailed reviews. Your reviewers, like all humans, want to spend more time working with people who are nice to them.

![Photo by rawpixel on Unsplash](/images/rawpixel-1135715-unsplash.jpg)
_[Photo by rawpixel on Unsplash](https://unsplash.com/photos/E9ErAZVSGJg)_

Because of the history of technology, some projects you interact with could have an established harsh culture. Your reviewer might not be kind to you. Rude correspondence sucks, and if it happens the best things to do (if possible) are maintain your composure, describe what about the interaction put you off,  and choose whether or not you want to engage with that particular project.

I hope that projects with crappy cultures will either change or fade away as open source contributors become more diverse and professional. Being assertive but not reactionary, and choosing what’s best for you puts you on the right side of history. If you care about the projects that you contribute to, sometimes the kindest thing to do for them is to tell them what makes their culture off-putting to newcomers. If they are worth your contributions, they should make an effort to change. If not, it's ok to walk away.

# Don’t be shy!

Maintainers open source their projects because they want contributors like you to improve them! If you’re making contributions in good faith and doing your best to follow project guidelines, most maintainers are grateful for your PRs, whether they are perfect or not.

I still make plenty of mistakes with the mechanics of contributing and project maintainers have kindly helped me to learn how to do things better. Most of the tips in this blog come from trial and error, and from fantastic project maintainers who took the time to help.

![Photo by Limor Zellermayer on Unsplash](/images/limor-zellermayer-1163067-unsplash.jpg)
_[Photo by Limor Zellermayer on Unsplash](https://unsplash.com/photos/j5MCxwaP0R0)_

If you want to contribute to a project but are worried about “doing it wrong” you aren’t alone. Some of the best engineers I know still get nervous about submitting PRs. Don’t let that stop you from doing excellent work on cool projects! Good maintainers always appreciate a well-intentioned PR. Happy Hacking!
