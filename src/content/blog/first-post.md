---
title: 'Another Blog, Another First post'
description: 'Starting blogs can be fun'
pubDate: '2024-05-27'
heroImage: '/blog-placeholder-3.jpg'
---

Hello! I was going to write about my excitement to play with some new tech and get some writing goals set up to succeed - but I must begin instead documenting a bug report.

In Astro.New's 'Blog' example in StackBlitz https://astro.new/blog?on=stackblitz (which seems to work, doubtful StackBlitz is Free and Open, haven't checked yet - there were two other options to investigate also)
When making edits to first-post.md, in the front-matter:

pubDate: '2024-05-27' and pubDate: '2024 05 27' emit, respectively:
May 26, 2024   and    May 27, 2024 

in the rendered blog. In Astro astro.build, the static-site-generator software I chose to explore as a blog platform today.
Of course, the very first thing I try uncovers a bug. This is my gift and my curse, and has been a vital asset in my career as a technologist.

It's likely a JavaScript problem. I can likely hunt it down and correct it.
But... Should I invest my energy in this? The VERY FIRST THING is broken. 

I understand TIME is DIFFICULT but.......

I want to focus on writing, not fixing a writing platform.
At the same time, I also want automated software forges to continuously static-host to my vanity URLs.
And I want a live-reloading web frontend authoring experience. (Looking mostly good so far)
One has to accept a certain amount of yak-shaving in such an adventure.

And this time, I'm going to work with an editor too. A human in-person editor. (Editor, add your intorduction note here when you exist)

Sigh. In order to actually contribute code to the astro project, I'm going to need to engage with the great beast Microsoft's tentacle, GitHub. Feels bad.

Instead of writing about my awesome stuff, I'm instead immediately confronted by adversarial jank. I didn't even want this to start as a technical blog! 

I opened this adventure today to document my work in SCULPTURE, and instead I'm wrestling with global-scale hateware mongers capturing and gatekeeping my communties. They enslave the unicorn with a crown for a collar, they cage the pheonix - they undermine the beauty of the Freedom and human purity of our best and brightest. And now they stand between me and contributing to this Astro project and having a nice time writing. And sharing warmth with my friends.

Every day, the world seems to ask me to compromise. My ideals, my sense of honour, justice, virtue, peace. I'm out of place, out of touch, committed to a spiritual truth that most would never recognize. Is it time to compromise for this? Another compromise.

Honestly it really rather stings. "Feed the beast, everyone else is doing it. What's wrong with you?"
How many hills can I die on?

I reluctantly make the choice to live as others do and I make a github account and I use it to sign in to stackblitz

Somehow, after signing in to save, I have been given some other web editor that is noticably more sluggish and it just feels bad oh my god why why why why

Why does it have to be shit? It was really good literally a minute ago before it helpfully loaded the github-specific integrations that janked it up. COME ON!

We are in it I guess. I enable GitHub Pages and Actions for Astro.

lol, of course, a git error.

We git pull, and try again to push.

Okay, Pages published SOMETHING, but the links are all broken because of baked in wrong assumptions. On the prime example with the default plugins.

https://ryanmakes.github.io/ryanmakes-website-stackblitz/blog/first-post/ At least it seems to be exist-y.

Asset paths are broken too. This wants to be deployed under more specific circumstances... I think I need to rename it to give it some special extra github juicing? I have a memory of something like that.

Yeah, gotta rename it ryanmakes.github.io (the repo name)


Okay, upon reloading everything, https://ryanmakes.github.io/blog/first-post/ is working right enough, and I guess I can use these credentials to make my bug report. God help me. 

Actually, it seems like it's time for my weekly meetup. We'll see if I come back to this jank later.

---

We return from dinner, with a request that we supply an RSS feed 'with full content'. Let's see what we can do. 

We see from https://docs.astro.build/en/guides/rss/ this guide that RSS is available but not installed and turned on by default.

Uhhh wait, it's already here? https://ryanmakes.github.io/rss.xml ? Maybe it's included because I started from the 'blog' example.

Digging further is even more confusing. There's a lot of fancy modern and contemporary magic stuffed into Astro that's likely going to become a series of distractions from writing.

Hopefully, I can keep the content itself portable and relatively publishing-tech-agnostic.

The date problem seems to be z.coerce.date() which seems to be zod.js

The in-browser environment has become painfully slow. I'm going to commit and restart the browser I guess?

I found the source of the problem with the date strings.
Using https://npm.runkit.com/zod and this minimal reproduction code:

```
var zod = require("zod")

var schema = zod.coerce.date();

console.log( schema.parse("2024 05 27") )
console.log( schema.parse("2024-05-27") )
```

The output is 
```
Mon May 27 2024 00:00:00 GMT-0400 (Eastern Daylight Time)
Sun May 26 2024 20:00:00 GMT-0400 (Eastern Daylight Time)
```

I'm reporting to Astro and Zod Discord communities and seeing what happens.

---

A very frustrating experience that was, dear lord. I will spare you the details.
The end is that YYYY-MM-DD with dashes is 'the standard' and (although it is not explicitly set) UTC is the default time for this github action setup.
We have changed the frontmatter for this post to include dashes, and we're going to hit commit to publish and find out what happens.

Godspeed to us all.

Oh no wait fuck becuase it still displays fucking wrong in StackBlitz where I'm trying to do my fucking live authoring. How do I set the timezone here to UTC? 

This adventure has wearied me deeply. Trying to get a fucking answer from the guys trying to help me on Discord is maddening. "The date being wrong isn't a bug - your perception of the nature of time is wrong." is surely a way to respond to a bug report I had not considered before. 

Not like they didn't... shed some light... but holy fuck and jesus christ there is no way!

Configuring the TimeZone in StackBlitz, and first understanding What Is StackBlitz, and then setting it to UTC, to match GitHub Actions (where it is an unconfigured default) will end this arc for me and release my soul from this pain.

Investigating this caused me to open another tab for the original example linked from astro.new
and!
Still snappy as ever! The extra github jank REALLY weighs this thing down.

StackBlitz is COMPLICATED and there is a lot going on. Getting the dates to render here correctly may matter a little less than it is worth to fix, knowing that it static renders correctly coming out of github pages actions, but

its not right

and accepting this bullshit

just primes accepting more and more and more fucking stupid broken goddamned bullshit.


It looks like some uncommitted changes unsaved are still persisted beyond the tab being closed and opened again - localstorage, or cloud trickery?

XXXXX

The StackBlitz setup got jankier, then simply stopped working - on commit it would say git failed. I'm typing this in github's web editor.

It looks like maybe if I can use the non-cursed version of stackblitz, maybe with sourcehut, that could be okay. Something to try out later.


It's well past two in the morning so I think that's enough of this little AstroJank blogging adventure for today.

