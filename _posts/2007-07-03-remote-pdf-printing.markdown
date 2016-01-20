---
author: adawes
comments: true
date: 2007-07-03 16:10:37+00:00
layout: post
slug: remote-pdf-printing
title: Remote PDF printing OS X tip
wordpress_id: 19
categories:
- tips and tricks
tags:
- applescript
- linux
- mac
- PDF Services
- printing
- ssh
---

I finally have a solution to the printing situation at work. I typically just hop on the wireless network since it is everywhere in the physics building. The only drawback is not being able to print directly to the department printers (wireless is a campus-wide network so it's not local enough for the printer services).

Fortunately [macosxhints.com](http://www.macosxhints.com/article.php?story=20061203204459481) had a bit about this although with a work-to-home emphasis that also dealt with DNS issues. Using that hint combined with another new favorite [SSHkeychain](http://www.sshkeychain.org/), I have a fully streamlined system that lets me print at work over wireless with only one extra click.

<!-- more -->

Basically I created a workflow in automator (as described [here](http://www.macosxhints.com/article.php?story=20061203204459481)). Then I put it in the PDF Services folder /Library/PDF Services and it just works. For illustration, and cause screenshots are cool:

![remote printing PDF workflow](http://dawes.files.wordpress.com/2007/07/remote-printing-pdf-workflow.png)

And this is how I use it (right there in the regular print dialog)

![PDF services example](http://dawes.files.wordpress.com/2007/07/pdf-services-example.png)



UPDATE (Jan 8, 2007): I have discovered that some PDF files don't adequately embed their fonts, or perhaps they use an encoding that isn't appropriate for the printer. In any case, the PDF shows up with all sorts of letters missing. I'm guessing that this is an issue with the Mac to Linux transition. Even printing to a PDF on the mac, and then scp'ing the file to linux, and printing with "lpr foo.pdf" gives missing characters. My workaround for now is to use the following command as the remote printing command:



`gs -dNOPAUSE -sDEVICE=psrgb -sOutputFile=%pipe%lpr -q -dBATCH foo.pdf`



I'll probably drop this into a shell script somewhere on my linux machine, in order to avoid having the whole thing written in the applescript snippet
