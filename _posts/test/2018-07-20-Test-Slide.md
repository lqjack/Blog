---
layout: slide
title: Jekyll&#58; Make presentation page with reveal.js
description: A presentation slide for how to use reveal.js in Jekyll
theme: black
transition: slide
---


<section data-markdown>
# Create slides using reveal.js and Jekyll

Jan 12, 2016
</section>

<!-- Just to show that markdown and html can be mixed -->
<section>
  <h4>Hi, I am</h4>
  <h3>Manu S Ajith</h3>
  <div style="width:200%;">
    <div style="float:left; width:30%;">
      <img alt="Jeroen De Meerleer" src="http://9piecesof8.com/img/manu.png" style="float: left; width:300px; height:300px;">
    </div>
    <div style="float:right; width:70%;">
      <ul style="float: left; padding-top: 4%;">
          <li>Writes code @RedPanthers</li>
          <li>Am committed to Ruby for some time,</li>
          <li>been dating Go during weekends,</li>
          <li>and recently flirting with Elixir at night</li>
      </ul>
    </div>
  </div>

</section>

<section data-markdown>
### Overview

[reveal.js](https://github.com/hakimel/reveal.js/) lets you to create
beautiful interactive slides using HTML. This presentation will show/demo you
how to use reveal.js and write your presentations in style with [Jekyll](http://jekyllrb.com/)
</section>

<section data-markdown>
### Slide Layout

reveal.js is already included as a `git submodule`, so that we can use it in our layouts.

Also a `slide.html` layout has been added into the `_layouts` folder which would be the base layout for all our slides.
</section>

<section data-markdown>
### Creating Slide

Now, in your page/post YAML front matter, use `slide` for the layout.

You can define *title*, *author*, *description* as well as the slide's *theme* and
*transition*

    --
    layout: slide
    title: Jekyll&#58; Make presentation page with reveal.js
    description: A presentation slide for how to use reveal.js in Jekyll
    theme: black
    transition: slide
    --


</section>

<section data-markdown>
### Slide

Each slide is enclosed in a `&lt;section&gt;` tag.

If you prefer markdown then use

`&lt;section data-markdown&gt;`

</section>

<section data-markdown>
## THE END
</section>