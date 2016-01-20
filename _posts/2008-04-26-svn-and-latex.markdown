---
author: adawes
comments: true
date: 2008-04-26 17:14:42+00:00
layout: post
slug: svn-and-latex
title: SVN and LaTeX
wordpress_id: 137
categories:
- computing
- open source software
- physics
- tips and tricks
- try this at home
tags:
- google code
- latex
- subversion
- svn
- thesis
---

[![200th revision](http://dawes.files.wordpress.com/2008/04/svn_revisions.png?w=265)](http://dawes.files.wordpress.com/2008/04/svn_revisions.png)

For anyone curious about the process of managing a LaTeX document with the Subversion (SVN) version control system, I have to highly recommend it. Now that my dissertation is officially finished, I have a bit of time to explain the process I used to back-up, archive, and otherwise manage the beast.

<!-- more -->

The three major components of the computing end of my dissertation were [Textmate](http://macromates.com) (and the LaTeX and SVN bundles), [Google Code](http://code.google.com), and of course [LaTeX](http://www.latex-project.org).

I set up a project at Google Code (free hosting for < 100 MB) which includes SVN access, a project wiki, and a nice web interface. Almost all of my LaTeX was written in the Textmate editor simply because it has a lot of useful macros and plugins including a feature that lets you drag and drop images to make figures (it automatically inserts the \begin{...} \end{...} code and has lots of other type-savers.

Another advantage of Textmate is built-in SVN support. The above screen capture shows the result of an SVN "commit" which happened to be my 200th revision. In the end, I had 202 revisions, but the last two were trivial (adding an updated figure file, and a little typo).

There is a fair bit of documentation out there about how to do each of these things individually, so I won't reiterate any of the instructions here. I mainly want to suggest this approach to anyone who is managing a large document, or especially sharing the responsibility with multiple authors.

I don't know if this was an intended use for Google Code, but it certainly serves the computing community well. If you are interested, the repository for my thesis (i.e. the source code) is available at [http://code.google.com/p/dawes-phd-thesis/](http://code.google.com/p/dawes-phd-thesis/)
