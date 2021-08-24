# Introduction

Twitter [Bluesky](https://blueskyweb.org/) is [@jack](https://twitter.com/jack/status/1204766078468911106)'s ask to solve:

1. Is it safe to trust governments or companies to label misinformation?
2. Why can't users install their own newsfeed or recommendation algorithms?
3. How can healthy content not lose out to reactionary or emotional posts?

It was an honor to have [Mark](https://twitter.com/marknadal)'s work included in the official [ecosystem](https://blueskycommunity.net/) [document](https://twitter.com/bluesky/status/1352302818418446337). ERA bluesky **is not** Twitter's official system, but a *Work-in-Progress* of one of the [proposals](https://gitlab.com/arnoldjun/bluesky/-/blob/master/design/proposals/Mark-Nadal-Bluesky-Proposal.md) considered by [the team](https://blueskyweb.org/). It was allowed to be published publicly and is a good starting point for context to the project:

 - [Twitter Bluesky: A Decentralized Protocol Proposal](https://hackernoon.com/twitter-bluesky-a-decentralized-protocol-proposal-hi193337)

# ERA bluesky

We're going to live build the proposal using protocols that already exist. So ERA bluesky will serve as both a documentation reference, explanation, sample specification, and a usable app, all in one. First, let's cover some prerequisite capabilities:

## Identity

Before we can do anything online, we need a way to represent ourselves. This is what we call an "identity".

### History

1. In the 1990s people could make different guest accounts on a home computer. This was their original profile. However, if the hardware broke or if you installed a different operating system on it, your identity would be lost.
2. Early email ([SMTP](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol)), [IRC](https://en.wikipedia.org/wiki/Wikipedia:IRC/Tutorial#Nickname_registration), and instant messengers let you use your same identity even if you bought a new computer, or across many mobile devices.

Let's pause and realize how profound that is. Your identity could survive across the death of many machines. That is useful.

But there is a catch, your identity was now owned by a company. This set the standard for the next 25 years, for better and for worse.

3. As the web ([HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)) grew, people suddenly had the problem of needing an "identity" for each service. Having to "*Forgot Your Password?"* makes the pain point clear.

We should note how strange this is though, if my identity can survive across hardware, why is it so hard for it to work across services?

4. [Cryptography](https://gun.eco/docs/Cartoon-Cryptography) solves that. Even if you used many services, you could "[sign](https://gun.eco/docs/Cartoon-Cryptography#signatures)" off and encrypt ([make private](https://gun.eco/docs/Cartoon-Cryptography#encryption)) your data with the same [verifiable](https://gun.eco/docs/Cartoon-Cryptography#cryptography) identity, in a way that [nobody but you owns](https://gun.eco/docs/Cartoon-Cryptography#security). Historically, the user experience (UX) has been terrible, but modern tools like [Party](http://party.lol/) and [Mask](https://mask.io/) help fix that.

This finally leads us to today. To decentralize Twitter, user accounts must be cryptographically secure so that they are not owned by any company. However, since most people do not know how to use cryptography, it is important that normal web like logins work. We have this built, already today:

 - [3FA: Cryptographically Secure Account Recovery without Servers](https://twitter.com/marknadal/status/1427715775838572545)

### Features

Ownership becomes a very important feature. If we do not want to depend on a company, we must *at least* have a copy of our data backed up on our computer. However, we also do not want our identity to be dependent on the hardware either, like in (1) above. So let's define a **user story**:

 1. Any device I use should be able to use my same identity.
 2. I want to know what devices are/were used, to protect my identity, and see their health, to protect what I own.
 3. I want to add or remove the devices.

Because the web is the most popular application delivery method, our reference implementation should exist as a simple [HTML](https://en.wikipedia.org/wiki/HTML) page specification:

...
