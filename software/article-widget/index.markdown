---
author: adawes
comments: true
date: 2010-12-23 18:12:47+00:00
layout: page
slug: article-widget
title: Article Widget
wordpress_id: 389
---




## About the Article dashboard widget


<span class="caption">](http://dawes.files.wordpress.com/2010/12/science.png)</span>

This is a supplemental site for the support of Article, a dashboard widget I wrote for quickly accessing articles by volume and page number. I personally use it for following citations when I'm reading an article. An example workflow would be to use this widget to locate the journal webpage for the article and then from there import the citation to [Connotea](http://www.connotea.org/), [CiteULike](http://www.citeulike.org/) or [BibDesk](http://bibdesk.sourceforge.net/), whichever you prefer. You can find a mirror of this information at the [original article widget site](http://newton.ns.pacificu.edu/~dawes/code.html).


## Download


[Article_1.2.wdgt.zip [80.6 kB] version 1.2](article/Article_1.2.wdgt.zip)


## Installation


Mac OS X 10.4 or higher is required. Leopard works fine. If you’re using Safari, click the [download link](Article_1.2.wdgt.zip). When the widget download is complete, show Dashboard (press F12 by default), click the Plus sign to display the Widget Bar and click the widget’s icon in the Widget Bar to open it. If you’re using a browser other than Safari, click the download link. When the widget download is complete, unarchive it and place it in /Library/Widgets/ in your home folder. Show Dashboard, click the Plus sign to display the Widget Bar and click the widget’s icon in the Widget Bar to open it.


## Usage





	
  * Choose your field in the first pulldown menu

	
  * Select the journal you are looking for in the second pulldown menu

	
  * Type in the volume number in the first text field

	
  * Type the starting page number in the second text field

	
  * Hit enter/return and you should find yourself at the abstract page for that article.*


*Note: this may require having journal access through a university library or other arrangement.

The only strangeness is that for accessing the ArXiv you will have to either:

	
  * enter the subfield specifier—such as "quant-ph"—in the first field and the article number in the second field (old citation style like "nlin/0506006")

	
  * enter the month-year code in the first field, and the id number in the second field (new citation style like "0705.4238")




## Supported Journals (so far):





	
  * Phys. Rev. Lett.

	
  * Phys. Rev. A-E

	
  * Science

	
  * Nature

	
  * Optics Express

	
  * Optics Letters

	
  * ArXiv.org (old and new style)

	
  * Rev. Sci. Inst.

	
  * all ACS journals (Chemistry)

	
  * Others being added daily


We are trying to add the journals that you request. To make it faster and easier for us you may include the following information: a valid journal citation in the requested journal: i.e. "Science, 308, 672" and the URL of the abstract for that article (copy and paste from your web browser is fine).


## Adding your own journals:


This is only for those interested in editing html and javascript files. If you break the widget by tinkering then just download a fresh copy and try it again.

To edit the widget innards right- (or control-) click on the widget icon which can be found in ~/Library/Widgets. Choose "Show Package Contents." This will open a new finder window with all the widget guts. You will be editing article.html and article.js


### article.html


Scroll to lines 71-76 and add an element to the array journals[i] where i corresponds to the index of your scientific field. Right now 1 is physics, 2 is General Science etc. This could change though so just check what other journals are already listed to be sure you're in the right place. Create an entry that looks like "Journal Title Abbreviated|jta" where you replace the part before the pipe "|" with your abbreviated journal title and the part after the pipe with a unique word or acronym that will identify your journal. Typically we use the first letters of the journal title words but check what is listed so it doesn't repeat one that's been used. Remember what you've written as the journal identifier. Save the file and close it.


### article.js


This file is the widget brain, all you are doing is adding a snippet of code to form the URL for your journal based on a volume and page number query. Copy the code blocks that starts with "if (journal == "pra")", be sure to get both closing curly braces.

Replace the "(journal == "pra")" with "(journal == "newjournalid")" where you insert the journal identifier you have chosen. Only one step left, the URL. Go to the web page for an abstract in your journal or better yet search for one that you know exists. Copy the URL for the abstract page to article.js near your new copy of the line that looks like:

    
    widget.openURL("http://link.aip.org/link?"+"pra"+"/"+volume+"/"+page);


Notice that this URL is broken up into bits that correspond to the volume and page numbers. This is how the article widget works. It has a lookup table for journals and it creates the proper URL based on what you enter. To make a lookup table entry for your journal just do the same as above for your new journal URL. Find the volume and page numbers in the URL and replace them with the volume and page variables in article.js. Save both article.js and article.html. Give your new and improved widget a try and see if it works.

Hopefully these instructions are clear, if you notice anything missing or have suggestions on how to clarify the process, feel free to let me know. Also if you get your favorite journal to work, send me your article.html and article.js files and I'll include your contribution and list you in the credits below. This is open source for a reason, lets all make it better.


## Credits:


Major thanks go to Scott Sayres from Penn State who has added support for Phys. Rev. B-E, Rev. Sci. Inst., and the complete collection of ACS titles. He also gave the widget it's flipping skills. We've started a collaboration on this widget so expect to see other features as we both find time to add them.

Also thanks to Michel Cote for fixing the APS journals that were broken when AIP stopped linking to APS. Phys. Rev. should work as intended in version 1.2 and later.


## Terms of Service


This software is copyrighted © Andrew Dawes and Scott Sayres, some rights reserved. You may freely download this software, distribute it, and make full use of it for whatever purpose you like. There is no warranty express or implied. Hack it if you want, all dashboard widgets come with their own source code! I've provided it under the terms of the [Creative Commons GPL](http://creativecommons.org/licenses/GPL/2.0/) so do the right thing.

Please feel free to contact me with any questions about the widget, if you would like to add another journal to the list of supported journals, or if you find any bugs.


