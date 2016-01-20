---
author: adawes
comments: true
date: 2015-10-19 15:42:00+00:00
layout: post
slug: inkscape-clipboard-fix-on-mac
title: Inkscape clipboard fix on mac
wordpress_id: 889
categories:
- physics
---

Inkscape is my go-to vector editing program and I've done many publication figures, exam questions, and other general work in inkscape on both mac and linux. I've always just resigned to use clone (ctrl-D) instead of copy/paste since on the mac, the copy/paste cycle results in a pixelated image being pasted into the document. After beating my head against a wall trying to create a pattern-on-path effect, I realized that there must be something wrong with the clipboard implementation on the mac. Sure enough, a quick search took me to the [inkscape FAQ](http://wiki.inkscape.org/wiki/index.php/FAQ#Copying_and_pasting_in_Inkscape_creates_pixellated_images_instead_of_copying_the_vector_objects), and this section in particular:


<blockquote>Starting with XQuartz 2.3.2, X11 has some functionality to exchange the content of the clipboard with OS X. It currently does not know how to deal with vector images, so it just captures the screen, _i.e._, creates a bitmap copy, and then pastes that. You need to deactivate this functionality in X11 preferences > Pasteboard: uncheck "Update Pasteboard when CLIPBOARD changes". However, this will also prevent copying text from any X11 application to Mac OS X ones. It will not prevent copying text from OS X to X11.

When you just want to make a copy of an object within Inkscape, you can also use _duplicate_ (Ctrl-D) rather than _copy/paste_ (Ctrl-C/Ctrl-V) — _Duplicate_ does not interact with the X11/OSX clipboards. For other Inkscape commands involving the system clipboards (_e.g._, _Paste Style_, _Paste Size_ or _Paste Path_ in path effects) there is no alternative workaround other than changing the X11/XQuartz preferences as described above.</blockquote>


On the bright side, I had found the suggested workaround, and was able to effectively duplicate items in my drawings. However, that doesn't work when the effects are expected paths in the clipboard (and they weren't there). Since inkscape is about the only thing I use X11 for on the mac, I went ahead and disabled the X11-mac clipboard sync. I will dive in the the nuanced solutions if I need to. It's been a blessing to have access to many of the path effects and other cool tools in recent inkscape versions.
