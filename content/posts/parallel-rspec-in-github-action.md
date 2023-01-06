---
title: "Running RSpec in parallel on GitHub Action"
date: 2022-12-22
tags: ["rails", "github action", "rspec"]
author: "Me"
draft: true
---

There are a lot of CI providers our there and GitHub Actions is one of it. One good thing about GitHub Actions is that
if you are already hosting your code on GitHub, it's quite easy to get started with GitHub Actions too.

### Typical CI setup

When it comes to CI, things are quite straight-forward when our project is small. Things start to be more complicated as our project grows.
Our test suite might only need few seconds to be completed when we started the project. As we grow our team, having high CI coverage gives
us some confident about our project as whole.

Unfortunately by now, it might took us 30 minutes, or few hours to complete one whole test suite. This is not uncommon. We could optimize our
test suite better and make it run faster, but that's an entirely different topic.

In this example, I'm going to walk through on how to setup GitHub Actions to run RSpec in parallel for a Rails project.


