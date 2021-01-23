---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---
# Strikeback Bot

## Introduction

Like a lot of kids one of my boys wanted a PS5 for xmas.  I missed the pre-orders and failed miserably to secure one for my son in that first round.  Once it became apparent that most of the pre-orders had gone to bots and scalpers I decided that I needed to gain an advantage if I was to make that xmas dream come true and thus what I initially termed "snipernet" was born.

Being a software engineer with more than a few years experience I quickly cobbled together a working solution in a few hours.  I got the site scrapers working and integrated instant notifications via Slack so if I'd lined everything up properly I'd know about new stock within about 15s of it going live.


## How does it work?

There is a little app that pretends to be a web browser that periodically goes to each site in turn, performs a search for "PS5 console" and scrapes the results out of the page.  Sometimes the results include the PS5 but it's out of stock, other times sites don't list the PS5 because it's out of stock.  The data scraped out of the page is converted into a common format.  We get things like the name of the retailer, title of the item, its price and if it's in stock.  This is all dumped into a database for tracking.

We apply a filter to each item we find.

In the case of the PS5 we know the RRP so we can pretty much ignore anything below £359.99 but unfortunately some websites don't provide us with prices of things that are out of stock so we still have to include anything we don't have a price for.

We continue to apply some filters to the item to determine if it is really a PS5 or just some other bundle of things that just so happens to match our criteria.  If the item passes all these filters then we hopefully have a PS5 that we can monitor.

At this point if we think the item is in stock we generate a notification and immediately push a tweet out to twitter.  
Now twitter doesn't like us spamming it so to keep the number of tweets down we continue to tweet every ten minutes after that first tweet until the item goes out of stock.

## What's it running on?

It's running from my home network on an Intel NUC.  That's a quite powerful but very small computer.  The NUC has Ubuntu installed on it along with a thing called Docker.  The app is containerised and deployed using Portainer which is a admin suite for Docker.

Even though everything is running locally in my house everything is conneted to a UPS so should we have a powercut things should still carry on running.