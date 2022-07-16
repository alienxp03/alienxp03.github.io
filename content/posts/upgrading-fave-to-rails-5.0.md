---
title: "Upgrading Fave to Rails 5.0"
date: 2022-06-06T11:30:03+00:00
# weight: 1
tags: ["rails", "fave"]
author: "Me"
showToc: true
TocOpen: false
draft: true
hidemeta: false
comments: false
description: "Upgrading Fave to Rails 5.0"
# canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---

In [Fave](https://myfave.com), we are still largely powered by our majestic monolith Ruby on Rails app. On 3rd November 2021, we finally reached
a big milestone and upgraded our app from 4.2 to 5.0!

![Image](/rails-5.0-alienxp03.jpg)

Initially, we wanted to upgrade earlier. However priority changed. Truth is, it took us around 3 years and 3 months before we finally finished the upgrade. I'm hoping to share on our Rails upgrade journey and why it took us so long to reach here.

## 1. Dual boot

When we first started the project, our naive solution was to create a pull request and slowly update the codebase to make it compatible with both version of Rails. However, it started to get bigger and getting harder to do code review.

Reading on how [Github does it](https://github.blog/2018-09-28-upgrading-github-from-rails-3-2-to-5-2/) definitely helps us a lot in this case. Moving forward, we decided that dual boot is how we can incrementally update our codebase. Using [next_rails](https://github.com/fastruby/next_rails) is not necessary but it does make it easier for us.

```ruby
if Fave.next?
  # code for Rails 5.0
else
  # code for Rails 4.2
end
```

## 2. Gems

Gems are definitely one of my favourite thing about Rails. There's a gem for almost everything. However, left unchecked, it can cause different issues.

In our case, having too many gems make it hard for us to upgrade our Rails app. Some gems are no longer maintained, some have too many dependencies.

In our journey to upgrade our app, we decided that sometimes it's easier to remove a gem than upgrading it. Less is more. When we absolutely need to upgrade a particular gem, do it one gem at a time so it's easier to keep track of the changes.


## 3. Forks

Sometimes, there are cases where we decided to fork certain gems and customize it to our own workflow. Most of the time we realized that we didn't keep our fork up to date with the upstream. Outdated forks are risky and it's hard for us to move upgrade our codebase.

The solutions here are not easy. If we do need to fork a repo, our best option here is to always keep it up to date with the upstream. Monkey patch might not be a popular option, but if we can manage it right, it's a lot easier than maintaing a fork. Each solution has it's own pros and cons.


## 4. Negotiating priorities

Engineers love to talk about the technicalities. In fact, we love it too much that sometimes we forgot not everyone understand the technical jargon that we are using.

When we couldn't explain in simple words on why we need to upgrade Ruby on Rails, our team leads might not understand
the importance of it. Instead of saying `we need to upgrade Rails because we can use ActionCable`, we can try to reword it to `Rails 5 allows us to use real-time update feature`.

When we can't explain it in simple terms, it's hard for others to truly understand what's our goal and objectives. And it's hard to prioritize something that not everyone understand.

The truth is, we're not working alone. If we can't explain it in simple terms, there are others in our team that could help. In the end, it's a team effort. Communication is the key here.

## 5. Help others to help you

For our Rails upgrade, we created a Slack channel to have a discussion and gather people for the project. I remember being so enthusiastic
about the project and I was so sure that people would like to be involved in it. Few weeks after we started the project, we barely getting any help. Took me a while, but I decided to try with a different approach and posted this on the Slack channel.

![Image](/rails-upgrade/slack-rails-upgrade.jpg)

What I did was create a specific instruction on what kind of help that we need, and how exactly can others help. In less than few weeks, we managed to fix all of our test and run both Rails 4 and 5 on our CI. Turns out, people were excited with the project. They're just not sure on how can they contribute.


## 6. Have a plan

When we first started, we have a rough idea on what we're trying to do. However it wasn't final. Now that we've done it, all that's left is just to document our steps and keep improving it. This is how it looks like for us.


```r
1. Setup dual boot for current and next Rails.
2. Run both Rails version in CI
  i. Current Rails version must always be green.
  ii. Next Rails version is allowed to fail until we fix all the errors.
3. All test in CI must pass
4. Run full regression test with our QA team.
  i. Combination of both automated and manual testing.
5. Switch all staging servers to use new Rails version.
6. Canary release on production.
7. Once everything is stable, remove old Rails version from the codebase.
```

---

In the end, we are happy with the upgrade. Just like any other project, not everything is about coding and we certainly learned our lesson here. It was a long journey for us but it was worth it.


---

### Resources

- https://github.blog/2018-09-28-upgrading-github-from-rails-3-2-to-5-2/
- https://github.com/fastruby/next_rails
- https://www.fastruby.io/blog/rails/upgrades/upgrade-rails-from-4-2-to-5-0.html
