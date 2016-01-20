---
author: adawes
comments: true
date: 2010-10-05 13:32:24+00:00
layout: post
slug: davmail-for-exchange-email-and-contacts
title: DavMail for exchange email and contacts
wordpress_id: 364
categories:
- computing
- open source software
- tips and tricks
tags:
- email
- exchange
- ical
- ldap
- thunderbird
---

I finally have a reasonable solution for working with email, contacts, and calendar information on the campus exchange server. I've written about this before and never been totally satisfied with my previous solutions. Now I am happy to say that using [DavMail](http://davmail.sourceforge.net/) has been great.
<!-- more -->
The basic idea is that DavMail sets itself up as a middle-man. It can access the exchange features from the Outlook Web Access (OWA) pages and it presents those to your mail and calendar clients as if they are legitimate servers running standard services (POP, IMAP, SMTP, LDAP etc). So you point your client at a local server and DavMail relays the local requests to the OWA page and gives you access. In other words, DavMail takes the outlook web access webpage and lets Thunderbird, or iCal access the information directly. It is easy to install and setup and even gives very detailed logs which can be helpful for finding out how things are configured and if they are working correctly.
