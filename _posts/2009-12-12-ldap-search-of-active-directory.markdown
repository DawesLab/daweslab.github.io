---
author: adawes
comments: true
date: 2009-12-12 04:05:38+00:00
layout: post
slug: ldap-search-of-active-directory
title: LDAP search of Active Directory
wordpress_id: 256
categories:
- physics
---

Our campus operates an MS Exchange server so there is a university-wide address book hosted for all to use. As a mac/linux/unix user, this is sub-optimal for me, but I know I have the tools to work around it. The challenge is matching command-line options with the server's expectations. This probably won't work for you verbatim, but if you find yourself in a similar situation, it may get you closer to something that works. I'm happy to try to help if you post a comment or question.

<!-- more -->

The first challenge for me is that there are certificate issues with the LDAP server. I was able to find out the name of the server from tech services, that is an important part of the solution. The server offers a certificate that is self-signed and has expired (don't get me started). I found this out by using openssl command-line tools to log in and establish an SSL session:

    
    openssl s_client -connect bailey.ad.pacificu.edu:636
    


This returned three errors about the certificate, all of which made it clear that there was badness that I couldn't fix alone, so I had to ignore it. Fortunately there is a workaround for ldap. In the ldap.conf file (which is located in /private/etc/openldap/ldap.conf on mac) you need to have the line:

    
    TLS_REQCERT     never
    


This will keep certificate issues from sinking you; so do this first, it will at least eliminate one major potential problem. Note, there are other options for TLS_REQCERT (see man ldap.conf for details) if you want to try to make certificates work the right way.

Next, you get to tweak the command line as needed. For reference, I'm running Mac OSX 10.4 on PPC hardware. The ldapsearch tool is installed by default so for me the appropriate command is (the \\ mean the line continues, you don't have type them):

    
    ldapsearch -x -D "PACIFIC\netID" -W \\
    -H ldaps://bailey.ad.pacificu.edu:636 \\
    -b "DC=ad,DC=pacificu,DC=edu" \\
    -LLL -v "(sn=smith)" cn sn
    


Replace `netID` with your own username. This will search for someone with a surname that matches "smith" (sn=smith) and return the common name (cn) and the surname (sn). The -x forces simple authentication, the -D specifies the bind name and it is my username (with domain first: domain\username), -W makes it ask for my password, and -H specifies the URL for the server. Note that the URI has "ldaps" for the protocol. This is how our server is set up, to use SSL on port 636, even though the certificate is expired and self-signed (go figure). The -b specifies the search base. For most cases, this will probably be everything after the first dot in the host name (i.e., "DC=bar,DC=bang,DC=com" for a host that is foo.bar.bang.com). The -LLL specifies the output format, if you want other things returned, run man ldapsearch to get details. The -v is for "verbose".

Another option is to let the server return all of the information for any entries that match. To do this, simply leave out -LLL and drop the cn and sn from the end. This will let you find out all sorts of information about yourself (or about others) all of which is stored in the LDAP directory. This can be very helpful for getting apps like Thunderbird up and running. More on that later when I post part two to[ Exchange LDAP in Thunderbird](http://dawes.wordpress.com/2009/12/05/exchange-ldap-in-thunderbird/).

Update: See my post on [DavMail](http://dawes.wordpress.com/2010/10/05/davmail-for-exchange-email-and-contacts/). It makes all these issues go away and works very well in my situation. In short, DavMail creates an interface between an Exchange server and your standards-compliant internet applications (IMAP mail client, LDAP addressbook etc).
