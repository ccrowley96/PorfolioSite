---
title: Portfolio Site
subtitle: Personal blog & portfolio site.
date: 2020-06-20
github: https://github.com/ccrowley96/PorfolioSite
tags: 
    - 11ty
    - javascript
    - scss
    - nunjucks
---
![_site folder](/img/porftoliosite/portfoliosite2.png)
I've gone through many iterations of my personal website.  The main problem with all previous versions was the difficulty in adding new content. Whenever I worked on a new project, I wanted an easy way to push up project info, without duplicating a page of HTML each time.  I would always get bored of the static design I had made and re-write another version the next year.

What I needed was a templating engine.  A framework to generate static content based on simple inputs like markdown files.

I'd used <a href="https://gohugo.io/" target="_blank">Hugo</a> before to set up a blog, but I wanted to work with something new & something in JavaScript.  I stumbled across <a href="https://www.patrickweaver.net/" target="_blank">Patrick Weaver's Site</a> and thought his tag system, blog, and portfolio were awesome.  I wanted to build something similar.

I messaged him on LinkedIn and he pointed me to <a href="https://www.11ty.dev/" target="_blank">11ty</a>, a Node.js based static site generator.  So I set off trying to build a full portfolio / blog theme from scratch.  After a day of frustration, I had simple portfolio and blog items working, but I had never used templating languages such as *liquid, nunjucks, handlebars, or mustache* before, so progress was slow.

I ended up getting caught up on the tagging system. So, after some research, I found a <a href="https://github.com/11ty/eleventy-base-blog" target="_blank">base blog template</a> that provides easy github-pages deployment, a tagging system, and a blog boilerplate.  I'd recommend that others start with a base template as well to get familiar with the 11ty file structure, _includes system, and to learn how tagging / pagination works.

After setting up the base template, I extended it, adding a 'portfolio' section with its own tagging system.  I added SCSS support (which took wayyy to long).  I added some design flair and found a really nice <a href="https://supersimpleslider.com/" target="_blank">image carousel package</a> and <a href="https://mattboldt.com/demos/typed-js/" target="_blank">typing animator</a>.  In the coming months, I plan to make the design more 'my own' and build several other features, but I really like how the site turned out.  I'm hoping this site will last me for the coming years, even as I dive into the rabbit hole that is JavaScript.  At least I'll be able to document my progress.

*One of the great things about modern web development is the ability to create complex systems in days rather than months or years. Building on top of the frameworks and libraries created by others allows for this type of rapid learning and development.*

Here's an example of how this process works.  To create a project post, I created a `microsoftgarage.md` file with the markdown shown below.

### `microsoftgarage.md`
```yaml
---
title: Microsoft Garage
subtitle: A Holographic Cancer Cell Visualizer
date: 2018-08-20
externalLink: https://mcec.microsoft.ca/blog/vancouver-interns-brings-holograms-to-bc-cancer/
videoLink: https://www.youtube.com/embed/4OouJKwl5bM
images:
    - /img/microsoftgarage/hololens.jpg
    - /img/microsoftgarage/bc_cancer_fund.jpg
    - /img/microsoftgarage/badge.jpg
    - /img/microsoftgarage/sleep.jpg
tags: 
    - microsoft
    - unity
    - hololens
---
## Project 
Developed a mixed-reality cancer tumor data visualizer and companion web app for Microsoft HoloLens...
```

My templates will handle structuring the HTML, filling in the dynamic content such as the title, GitHub link, etc., and 11ty will handle building the files into static content to be served online (through GitHub pages in my case).

All of the markdown files found in the **projects** folder are set to use the `project.njk` layout (template / layout are used somewhat arbitrarily here). The `project.njk` layout pulls the front-matter data for each project (title, subtitle, date, etc..) and renders it into HTML.  This removes the need for rewriting bulky HTML files for each post.

### Project Post Layout File `project.njk`
{% highlight liquid%}
<h1>{{ title }}</h1>
<h3>{{subtitle}}</h3>
{% if externalLink %}
    <div class="externalLink"><a href="{{ externalLink | url }}" target="_blank">Live project link!</a></div>
{% endif %}
{% if github %}
    <div class="github-link"><a href="{{ github | url }}" target="_blank">View code on Github</a></div>
{% endif %}

{{ content | safe }}

{% if videoLink %}
<h3>Video Link</h3>
<div class="video-container">
    <iframe width="100%" height="100%" src="{{videoLink}}" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
{% endif%}

{% if images %}
<div class="{% if images.length > 1 %} slider{% endif %} projectImageContainer">
    {%for img in images%}
        <img class ="projectImage" src="{{img}}" />
    {% endfor %}
</div>
{% endif %}
{% endhighlight %}

The `project.njk` layout is *chained* into another layout named `base.njk` which adds all of the HTML Head data, css stylesheets, scripts, and the navigation bar.

When I'm ready to push up a new blog post, project, or site update, I use the `eleventy` command to build the `_site/` folder.  This builds all of the static files, for all of the tags, projects, posts, and pages.  The `_site/` folder contents are shown below.
### `_site/` Build Folder
![_site folder](/img/porftoliosite/portfoliosite1.png)

I have a `.travis.yml` file in my project folder which configures **TravisCI** to build and deploy the `_site/` folder to a `gh_pages` branch each time I push to the master branch of the associated GitHub repo.

I'm still new to 11ty & learning, but I see the benefits of static site generation for making sites such as this.  Don't hesitate to reach out if you have questions about how I built this site, or if you'd like clarification on this post!

