---
layout: post
title: Facebook Conversations
date: '2017-10-28T12:01:39-05:00'
tags:
- facebook
- scraper
---

My buddies and I have a long-standing group conversation on Facebook. It's pretty much the most chaotic discussion ever. In fact, it's not a discussion as much as it is mainly insides jokes and completely random thoughts rarely connected to each other. But since we live spread out across North America, it's pretty much the best spot we have to keep news of each other and remember our good (and no so good) times. For a while now, we've been talking about saving all of these thoughts and jokes somewhere as a backup in case Facebook (or society as a whole) collapses. This conversation will be hitting the five-year mark this winter, so I thought I'd start exploring how we might work this out and possibly produce a super-limited book out of it (because our jokes are *that* good).

## Fetching

First thing is to fetch the actual data. There are two ways to go about this:

- [Download your entire Facebook data](https://www.facebook.com/help/131112897028467);
- Write or use a scraper to fetch the data;

There are up and downsides to both solutions. Facebook's solution is great cause you usually get your data pretty fast by email. But the conversation file you get will contain *all* of your conversations mixed together, so it's a bit of a mess. There are also no emojis (or any Facebook Messenger integrations for that matter) part of the file, so a lot of empty messages will pop up.

A scraper lets you fetch the conversation as it was originally written (with all integrations), but Facebook makes it really hard to scrape. The original scraper I wrote basically scrolled the conversation window up every *x* seconds, fetched the content and saved it to a file. But after scrolling a few hundred pages, the API or the browser would get really slow and eventually timed out or crashed. As far as I know, there's no way to do this programmatically with the API.

After struggling with the scraper, I just moved on and used Facebook's data.

## Organizing

Since Facebook's conversation file is all mixed up, I needed some help to extract our group's conversation. Fortunately, a good samaritan wrote a [Facebook Chat Archive Paster](https://github.com/ownaginatious/fbchat-archive-parser) which basically analyzes and splits your huge conversation file into actual conversation files.

## Presenting

The conversation text file you get is pretty rough. You basically get what everyone said in chronological order with a timestamp and the name of the author. I wanted to make it easier to read so I started parsing and templating the file using good old PHP.

I quickly realized that, while we didn't have any emojis, we still had links to content we shared with each other (GIFs, memes, YouTube videos, you name it). Since most of them were important to the context of the discussion, I decided to include image previews of the links. While looping across all conversation items, I used a simple regex to detect the presence of a URL. I then used the [Embed](https://github.com/oscarotero/Embed) library to fetch the OpenGraph meta image value for that URL and simply replaced the URL with the actual image. Obviously, some links are dead at this point, the parser just ignores those and moves to the next item.

I grouped the discussion by day, then by month, including a page break after each month so it would be easier to scroll once it's in paper format. Sprinkled some CSS and some Google Fonts to make this pretty and voilà! The final HTML file is ready.

## Next steps

Next up will be packaging and printing. I'll have to convert that monstrous HTML file to PDF. I'll probably be using the aptly named [HTML to PDF](https://www.npmjs.com/package/html-pdf) package for this. Printing will be tricky though, I have yet to find a website that does nano-short runs (I'll be needing like 8 of them) at a "reasonable" price.
