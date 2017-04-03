---
layout: post
title: React Native
date: '2016-12-11T12:01:39-05:00'
tags:
- react native
- react
---

Since last year, I've been helping a couple of my buddies to kick-start their new metallurgic consultancy company and establish their presence on the Web by various means. One of the idea we got was to develop [a mobile app](http://castingdefect.com/) that would help foundries diagnose and fix casting defects they were having on a day-to-day basis. This is a pretty common issue in this industry and, apart from big ERP solutions, there are no real light-weight alternatives to digitize that data and share knowledge across a foundry on when and how defects occur and how to fix them.

We got this idea pretty much when [React Native](https://facebook.github.io/react-native/) was starting to gain traction in the tech community. Since I was already working full-time and didn't have much time on my hands to develop such an app, React Native felt like a good choice : I'd be saving a loads of time by developing in a language I mastered (JavaScript) and being able to build features for both iOS and Android at the same time. What really hooked me though was the ["learn once, write everywhere" approach](https://facebook.github.io/react/blog/2015/03/26/introducing-react-native.html). I knew from past experiences with [Cordova](https://cordova.apache.org/) that "universal" apps for multiple platforms usually don't offer the best experiences.

With a year behind us and a couple of updates under our belts, I can safely assume this was the right choice. React Native allowed us to iterate quickly on ideas or completely scrap them without ever feeling guilty of losing our "precious" time. It has the flexibility the Web offers while being as powerful as native apps can be. Better, with a single development stack for both iOS and Android, it became easy to share certain modules on both platform while developing custom ones when we felt the need. We basically built a different layout for each environment, but the actual views are the same whether your on your iPhone or Nexus. The killer feature is live reloading as you code. It makes everything so much smoother as faster.

<iframe width="100%" height="315" src="https://www.youtube.com/embed/AF-tDKdK6sI" frameborder="0" allowfullscreen></iframe>

React Native moves *fast* though. Things break all the time and you better read the release notes for each versions if you want to stay on the most up-to-date version of the framework. With that said, various useful tools have recently popped up and made their way to the core program through pull requests. RNPM (now [react-native link](https://github.com/facebook/react-native/pull/7899)) is great for managing dependencies and the newly added [react-native-git-upgrade](https://github.com/facebook/react-native/tree/master/react-native-git-upgrade) is a godsend to keep track of versions changes. The latter really helped out when upgrading from 0.36 to 0.42.

On the user side of things, we've had great feedback for both versions of the app so far. We're slowly building a solid userbase and getting great numbers on repeat usage. We're brainstorming new features and think will have very interesting ideas to try out this next year.