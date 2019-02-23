---
title: "Dhall Survey Review (2018-2019)"
layout: post
tags: dhall survey-review
---

If you had the chance to talk with me lately, it's quite likely that I've mentioned
[Dhall][dhall-lang] in some way or another.

If not, here's a **TL;DR** about Dhall so you can decide if you want to read further:
Dhall is a configuration language, aiming to be a *non-repetitive alternative to YAML*.  
If you wish to read more about it the [website][dhall-lang] is the best place to start 🙂

For the few readers left: if you sometime follow Dhall-news, it could be that you already read 
through [Gabriel][gabriel-twitter]'s post about [what 2018 meant for Dhall][dhall-year-review].
The post awesomely summarizes the last year of development — which brought very many great 
things in Dhall-land — and drafts the roadmap for where Dhall will go in this new year.  
I won't detail about that in here so I encourage you to follow the link above!

What I'll focus on in this post instead is [the yearly Dhall survey][survey] that came
together with the article above.  
I'll review the [survey results][survey-results] and try to draw some insights from all the good
opinions, suggestions and comments from the community ❤️

[Gabriel][gabriel-twitter] already published [his analysis][gabriel-analysis] of the survey
results, and if you read both you'll notice that he does the lovely job of going through
all the feedback, considering it in depth, and then grouping by survey-wide topics; 
I took the slightly different approach of going through the questions and try to highlight the
trends for each of them, only considerig a holistic point of view in the conclusions.

## Overview

First things first: what an amazing response! This year's responses have been **61**,
more than *three* times as much as [last year's survey][last-year-survey].  
At this rate, in ~15 years the whole Earth will be using Dhall.  
Pretty good eh?

More seriously, a quick comparison between this and last year's results shows that
the composition of the survey respondents - that is, the classification of users according 
to their kind of usage - is wildly different. (graphs below)

Most notably it looks like a whole lot more people is using Dhall for work and personal projects:
- "using Dhall at work" doubled from 16.7% to 31.6% (now 18 respondents)
- "using Dhall for personal projects" quadrupled from 5.6% to 19.3% (now 11 respondents)

![2017-2018 responses composition](/images/dhall-results-2017.png)

![2018-2019 responses composition](/images/dhall-results-2018.png)

### "Would anything encourage you to use Dhall more often?"

So which are the wishes of this mostly-industrial-users population?

The set of these answers is really interesting but varied, so I'll list all the things that
were mentioned more than once. I also tried to consolidate similar things under the same
umbrella if they were close enough:

- More examples of patterns beyond "syntax tutorials": from project structure, design patterns
  and evolving schemas to newtypes and homogeneous records (~6 answers)
- More implementations (Python, C#, Go, Java, Scala) (~5 answers)
- Optionally present keys in a dictionary (~4 answers)
- Somehow better imports: smarter import resolution and caching, and importing from JSON (~4 answers)
- More real-world examples and use-cases: CLI configuration, client-server comms, orchestration (~3 answers)
- More Nix integration (~3 answers)
- Better performance (~3 answers)
- Unicode is kinda scary (~2 answers)

These are all actually valid concerns, and most of them have been already considered or
there's the intention to address them. Some are a bit surprising, like the point about Unicode.
(more on this one later)

I'll just briefly leave a note here about the "optionally present keys in a dictionary"
problem: I don't know if the comments about this are from users of [dhall-kubernetes][dhall-kubernetes],
but the combination of Optionals and Records is sometimes hairy to deal with in there (we have an
[issue open about it][optional-keys-record-1], and there's one in the [Dhall repo too][optional-keys-record-2]).  
I've been considering if [row types](https://www.reddit.com/r/haskell/comments/4f7fyn/what_are_row_types_exactly/)
would make this nicer to deal with, but they'd probably complect the standard too much, at least
at this stage.

### "What do you use Dhall for?"

Now, for everyone who whished to have examples of usecases, here's what people are using Dhall for:
- Configuring one or more DevOps tools (~13 answers)  
  The list is long here: Kubernetes (5), Terraform (3), Concourse (2), Prometheus, Kops, GoCD,
  docker-compose, Ansible, Packer
- Configuring an application (~10 answers)
- Configuring a CLI tool (~6 answers)
- As a templating language (~6 answers)
- As a configuration DSL (~4 answers)  
  (note: the answers don't detail more, but I suppose this application is a "more involved"
  extension of the previous case)
- As a data-storage format (~4 answers)

Wow, it looks like the list of usecases is expanding 👏

Given this fact, I'll broadcast a message here to all Dhall users:
- If you're using Dhall for anything it would be suuper lovely if your could put together
  an example of how you're using it! It would help very much everyone else looking for
  how to do things, or figuring out if Dhall fits their usecase.  
  It doesn't need to be fancy, e.g. a GitHub gist would be totally great 🙂  
  And we'd be extra thankful if you could send it over, e.g. to [Dhall's Twitter account][dhall-twitter],
  or just [in an issue][issues]
- If you're using Dhall at your company, please consider [opening an issue][issues]
  about adding a mention to the [list of production users][production-use]! 


### "Why do you use Dhall?"

So Dhall is employed for doing all of these cool things, but why so?

Reading through it looks like there is pretty much agreement on why one should reach for Dhall:
1. **Type safety** (~15 answers)
2. **Functions/abstraction** (~8 answers)
3. **More coherent than JSON/YAML/HCL/Nix/etc** (~11 answers)  
   In particular, many of them pointed out how much less repetitive than YAML this is.

A pretty big pain point in the DevOps world is the single-source-of-truth
problem, because with all the different formats it's very often necessary to duplicate information.  
With Dhall, that problem is no more. I particularly liked how this response sums this up:

> Derive config files for each system from one common Dhall configuration type

### "What should Dhall development focus on?"

This is kinda close to [the second question](#would-anything-encourage-you-to-use-dhall-more-often),
but less of a "whishlist" and more of a practical question, of "what should we do next?"

In fact, the opinions converge on the two most popular answers to the second question,
which are the clear winners here:
- We need real-world examples, starter apps, tutorials, patterns  
  (mentioned ~12 times)
- We need more language bindings (e.g. Go, Python)  
  (mentioned ~13 times)

This answer pretty much sums up the need for examples and guides:

> Widely used, typical use cases. Most people configure something "simple", show me how Dhall
can improve my workflow (validation against a "schema", deduplication, sharing of common config between applications)

Other things mentioned more than once were:
- Editor support (~3 times)
- Performance could be improved (~3 times)

### "Would you fund open source work on Dhall?"

This one is interesting. Most of the respondents, 52% (~23 answers), would happily buy
Dhall books and merchandise. I guess it's time to make tees and stickers 😄

Other popular options were:
- Patreon, 38% (17 answers)
- Donation button and project bounties, 32% (14 answers)

Financing open source is hard, and one of the reasons is that there will be different incentives
depending on the source of the funds, which is a thing that might get in the way of success.
You can read something about it [here][opensource-financing], and Gabriel touched on this point
briefly in his analysis.  
And as he noted, it's quite likely that the majority of answers that went to the "books and 
merch" answer are directed towards the book, given the many answers asking for more documentation.

## Conclusions

I personally have a few takeaways from this analysis:
- The language is pretty stable at this point, and can address pretty well several
  ["production use-cases"][production-use] 🎉
- The needs of the community are quite clear! This is great news.  
  The less-good news is that the wishes of the community are labor-intensive (i.e. not much
  low-hanging-fruit), so it will take some effort (and probably funding) to get there 😊
- Some number of answers worried about Unicode-by-default.  
  This is probably due to the feeling one might get when reading code samples that contain
  characters not on the keyboard, something like "and now how do I type this?"  
  This is a UX perspective I missed before, and I'll definitely switch
  at least the documentation and examples in [spago][spago] and [dhall-kubernetes][dhall-kubernetes]
  to use ASCII everywhere if that helps approachability.
- [dhall-kubernetes][dhall-kubernetes] needs some refactoring. The reasons why it's not in the
  best possible shape right now are several:
  - The domain is hard. Kubernetes is quite complex and its objects are huge.
    Moreover, there are some impedance-mismatch issues between how Kubernetes handles things
    (i.e. almost everything is basically optional) and Dhall works (e.g. a common problem is with 
    recursive record merging not crossing the "Optional" type boundary), and we're still figuring out
    how to go forward with that to provide the nicest experience possible.
  - It was started when we didn't have "best practices" and "patterns" for Dhall yet.
    Now [we have some][nethack], so it will get better.
- The focus of the community as a whole should go into writing down more docs, FAQs, examples,
  patterns, tutorials, and production-reports (I'll follow up with some posts myself on this)  
  The great news about this is that every user can contribute to this 😍
- The focus of the contributors (and future contributors!) should go into spawning more language
  integrations, so that:
  - the language would become accessible by a wider audience
  - the usecase of using Dhall as an agnostic and efficient wire format would become more viable  
  
  If you're interested in developing a new language integration, watch this space: I kept a diary from
  building the [Clojure integration][dhall-clj], and I'll publish the post as
  soon as it'll be fully standard-compliant. (but anyways feel free to
  [send your questions over - I have open DMs][my-twitter] - or [open an issue][issues])
- A corollary of this last point is that the evolution of the standard should now slow down
  in order to get other implementations off the ground.  


And now for some answers to questions that popped up in various responses:
- Someone called for more integration with DevOps tools.  
  If you wish to integrate with Kubernetes, there's already a project with complete bindings
  for the Kubernetes objects: [dhall-kubernetes][dhall-kubernetes]  
  And it would be indeed nice if there were any examples of how to use Dhall with Kubernetes,
  and how to mix it with other DevOps tools, e.g. Terraform. I'll be writing another post soon
  about how we integrate the two at work 🙂
- Some answers were wondering if there is a Java language binding yet.  
  And there is! You should take a look at the [dhall-eta project][dhall-eta], it wraps the
  reference implementation in an idiomatic Java binding 😎
- Some people asked about an "informal place to ask quick questions": it's definitely welcome
  to [open an issue][issues] to ask a random question 😊
  Though if you wish for more chat-like setting, you can find me and some other users and
  contributors in the `#dhall` channel of the [Functional Programming Slack][fp-slack]
- Some answers were wondering about examples of using Dhall as configuration for CLI programs.
  I think a good example of that is [spago][spago], which is a PureScript package manager that uses
  Dhall for its configuration.  
  It makes use of several Dhall features in interesting ways - e.g. record merging, http imports,
  caching of hashed imports, etc - you can get an idea already by just skimming the README.
- For everyone whishing to see some "project organization patterns", I'd recommend taking a
  look at the [dhall-nethack][nethack] project, as it very nicely explains some common
  patterns for managing Dhall projects, e.g.:
  - [keeping the Prelude configurable][nethack-prelude]
  - conventions for grouping things, like [`types.dhall`][nethack-types] and [`defaults.dhall`][nethack-defaults]
  - the [render pattern][nethack-render]


### Thanks!

Last but not least, the "open question" responses were really thankful and supportive 😊

So I hope this post gives a good overview of the feelings of the community!  

I'd like to say thanks to Gabriel and all the contributors for all the work so far,
to the users for the support, to everyone who took the time to fill the survey,
and to the dear reader who read this far 🙂


[dhall-twitter]: https://twitter.com/dhall_lang
[gabriel-twitter]: https://twitter.com/GabrielG439
[my-twitter]: https://twitter.com/fabferrai
[dhall-year-review]: http://www.haskellforall.com/2019/01/dhall-year-in-review-2018-2019.html
[dhall-lang]: https://dhall-lang.org/
[dhall-clj]: https://github.com/f-f/dhall-clj
[fp-slack]: https://fpchat-invite.herokuapp.com/
[production-use]: https://github.com/dhall-lang/dhall-lang/wiki/Dhall-in-production
[nethack]: https://github.com/dhall-lang/dhall-nethack
[nethack-prelude]: https://github.com/dhall-lang/dhall-nethack/blob/master/Prelude.dhall
[nethack-types]: https://github.com/dhall-lang/dhall-nethack/blob/master/types.dhall
[nethack-defaults]: https://github.com/dhall-lang/dhall-nethack/blob/master/defaults.dhall
[nethack-render]: https://github.com/dhall-lang/dhall-nethack/blob/master/render/Config.dhall
[spago]: https://github.com/spacchetti/spago
[issues]: https://github.com/dhall-lang/dhall-lang/issues
[survey]: https://docs.google.com/forms/d/e/1FAIpQLSfQApsRF-lv6UXE1IHCLiABHrN9VN4NO6Tz4h61mKSiw76pBQ/viewform?hl=en
[survey-results]: https://docs.google.com/forms/d/e/1FAIpQLSfQApsRF-lv6UXE1IHCLiABHrN9VN4NO6Tz4h61mKSiw76pBQ/viewanalytics?hl=en
[last-year-survey]: https://docs.google.com/forms/d/e/1FAIpQLSed1N8eDTGsTpcff516MRRJdjM6wDNfYOxs1u8TufS7ecOKTw/viewanalytics
[dhall-kubernetes]: https://github.com/dhall-lang/dhall-kubernetes
[dhall-eta]: https://github.com/eta-lang/dhall-eta
[optional-keys-record-1]: https://github.com/dhall-lang/dhall-kubernetes/issues/46
[optional-keys-record-2]: https://github.com/dhall-lang/dhall-lang/issues/340
[opensource-financing]: https://github.com/nayafia/lemonade-stand
[gabriel-analysis]: http://www.haskellforall.com/2019/02/dhall-survey-results-2019-2019.html
