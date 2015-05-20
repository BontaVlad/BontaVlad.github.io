---
layout: post
tags: markdown
title: "Which Markdown?"
date: 2013-07-29 14:00
---

Which [markup processor][allprocessors] should I use? My needs for one happen to be simple: 
it should be under active development, should make embedding $$\LaTeX$$ dead simple, and should
be deployable with Markdown on Github Pages, since I plan to compose posts in
[prose.io](http://prose.io). On offer, we have [Redcarpet][redcarpet], [RedCloth][redcloth],
[Rdiscount][rdiscount], [kramdown][kramdown] and [Maruku][maruku].

   * Maruku: The last commit was 4 years ago, I'll give this a pass.
   * Redcarpet: Word is that it's wicked fast since it's in C.
   * RedCloth: This is at Textile processor.
   * Rdiscount: Also written in C, supports a [superset][rdextra] of Markdown.
   * kramdown: Also supports a [superset][krextra] of Markdown, and plays well with embedded $$\LaTeX$$ math!

I'm split between kramdown and Rdiscount. They're both actively maintained and well
documented, Let's look at the interesting features they each provide:

   * kramdown:
      1. Supports tables.
      2. Supports custom attributes for block and span elements *(very useful)*. 
      3. Supports footnotes.
      4. Supports ID's for headers, useful for TOC's linking to subheadings.
      5. Automatic TOC generation.
      6. Support block and span level embedded $$\LaTeX$$, rendered via MathJax.
   * Rdiscount:
      1. Supports paragraph centering.
      2. Supports image sizes.
      3. Supports custom attributes for block and span elements.
      4. Supports tables.

I'm giving kramdown a try, and am really liking its sensible syntax errors, native support
for embedded math and custom attributes. I think I'll stick with this for a while.

[allprocessors]: https://www.ruby-toolbox.com/categories/markup_processors
[redcarpet]: https://github.com/vmg/redcarpet
[redcloth]: https://github.com/jgarber/redcloth
[rdiscount]: https://github.com/davidfstr/rdiscount
[rdextra]: http://www.pell.portland.or.us/~orc/Code/discount/#Language.extensions
[kramdown]: https://github.com/gettalong/kramdown
[krextra]: http://kramdown.rubyforge.org/syntax.html
[maruku]: https://github.com/remi/maruku
