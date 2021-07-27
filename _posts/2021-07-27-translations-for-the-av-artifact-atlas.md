---
layout: post
title: "Translations for the A/V Artifact Atlas"
date: 2021-07-27 09:00:00 -0500
tags: [avpres, video, webdev]
---

The [A/V Artifact Atlas](http://avartifactatlas.com/) is a resource for identifying errors and anomalies in analog and digital video. 

For almost a year, I've had the idea to add translations to the A/VAA, to broaden the reach of the resource to communities working with legacy audiovisual materials but speak languages other than English. This got held up for several reasons (other commitments, burnout, lack of funding to pay translators, much less any for myself). 

Anyway, I outlined the structure to allow for those translations to happen and then that pull request sat around for almost a year... until last week!

![AVAA en edition](/images/translate-avaa-en.jpg)

The A/VAA is now available to be translated into French, Japanese, and Spanish. And I can add other languages if I get a group of volunteers.

Someone has volunteered to lead a group to start the translation process into Japanese (Thank you, Hitomi!) -- more details to come. I know a leader for translating into Spanish (Hi, Lorena)! We still need a group to translate into French (or Portuguese, or German, or Mandarin, or anything else).

This quick blog post is about how the A/VAA came to be structured to support multiple languages. Instructions on general contributing can be found [here](http://avartifactatlas.com/contributors_guide.html). And contact me if you are interested in translating -- I can work with you to get translations any way that would be easiest and most comfortable for you (I know lots of people are not comfortable with GitHub, and I'm always happy to teach you how or we can just trade folders full of files to edit).

The A/VAA uses the popular static website generator, [Jekyll](https://jekyllrb.com), to create pages for each Artifact and also page descriptions for Formats. There are also several general-information pages, such as "Contributor's Guide" or "FAQ." Jekyll is based on Markdown, with some YAML at the top of the page to add page metadata. If you don't know what most of these words mean, I'm just saying it's structured data, and that's what we use to structure it.

I'm going to outline how I set up translations. I don't think this is necessarily the best or cleanest way, but it was the fastest way that made the most sense at the time. Refactoring is a good idea, but it's a good idea that takes time on top of time I already don't really have right now. Pull requests are welcome, if you want to clean things up a bit.

![AVAA jp edition](/images/translate-avaa-jp.jpg)

## Config

For adding translations, we start with the `_config.yml` file:

I added this:

```
defaultlang: English
t:
  English:
    title: 'A/V Artifact Atlas'
    description: ''
  Español:
    title: 'A/V Artifact Atlas'
    description: ''
    code: es
  Français:
    title: 'A/V Artifact Atlas'
    description: ''
    code: fr
  日本語:
    title: 'A/V Artifact Atlas'
    description: ''
    code: jp
```

The title and descriptions are blank (and also not translated), but we can add those at a later time. The important thing is that there's a `t` and subsequent languages. The `t` is magic!



![AVAA es edition](/images/translate-avaa-es.jpg)


## Page layouts 

The next big change is in `_layouts/default.html`, which is where the A/VAA's sidebar lives.

Here, we add a little bit of code like this to sort and display a link to each of the languages.

{% raw %}
```
<nav class="sidebar-nav-lang">
    {% assign pages=site.pages | where:"ref", "home" | sort: 'lang' %} 
    {% for page in pages %}
        <a class="sidebar-nav-lang-item" href="{{ site.baseurl }}{{ page.url }}">{{ page.lang }}</a><br/> 
    {% endfor %}
    </ul>
</nav> 
```
{% endraw %}

Right now, this is commented out and not visible on the A/VAA site. I will make it available as the translation work is complete so that it's not misleading to users.

There are top-level posts, and those also have to be shown only if the selected language (or English, if none):

{% raw %}
```
<ul class="posts-list">
  {% assign pages_list = site.pages | where: "menu", true | sort: "order" %} 
  {% for node in pages_list %} 
    {% if node.lang == page.lang %}
      <li>
        <a class="sidebar-nav-item{% if page.url == node.url %} active{% endif %}" href="{{ site.baseurl }}{{ node.url }}">{{ node.title }}</a>
      </li>
    {% endif %} 
  {% endfor %}
</ul>
```
{% endraw %}

The sidebar also a search which needed to work for a regular root URL as well as translated language subfolders. Setting up relational URLs can be tricky to overcome when working with static site generators, if you're not used to it. It's not clean, but for now I just added:

{% raw %}
```
<div class="search">
    <form action="{{ site.baseurl }}{% if site.t[page.lang].code %}/{{ site.t[page.lang].code }}{% endif %}/search.html" method="get">
        <input type="text" id="search_box" class="search-box" name="query">
        <input type="submit" class="search-button" value="search">
    </form>
</div>
```
{% endraw %}

and that works fine.

All of this allows for Jekyll to build pages in the `/es`, `/fr` and `/jp` subpages and allow the sidebar navigation to still work seamlessly. It's kind of magic. You can see where the translations live by going to something like [http://avartifactatlas.com/es/](https://avartifactatlas.com/es/), except you'll notice that right now everything is still in English because we need translators to overwrite the English with the correct language.


![AVAA fr edition](/images/translate-avaa-fr.jpg)



## Content

Now, the content. 

As mentioned, the A/VAA has Artifacts and Formats (another addition made last year) and general top-level pages.

I'm not sold on this structure, but right now I have `es`, `fr`, and `jp` folders in three places:
- At the root level
- Within the `_artifacts` folder (that's Jekyll syntax)
- Within the `_formats` folder

It might work with everything at the top level? But also maybe Jekyll needs them each to be in subfolders with the underscore-preprended folders. I didn't test this out because I was again focusing on getting things working and getting back to chillaxing while watching Olympic skateboarding.

I copied and moved the (default English) artifacts into each of the folders.

At some point, I had already added a `lang` field to the front-loaded YAML metadata, so I didn't have to do this. I think I used `sed` to do this last year. Anyway,since it was already there, I could go in and find-and-replace `English` for the language of the folder for each of the folders (VSCode makes this easy -- ctrl-shift-H and restrict to folders). A real no-code solution!

I did this for the Formats next.

For the top-level pages, I also copied them into folders and did the find-and-replace thing, and manually translated the headers into the language of choice using Google Translate. I think this will help the translators navigate later, and since we'll be having people translate just the pages and not dig into the code itself using a GUI editor layer that lives on top of GitHub, it seemed like the right thing to do. (We have a [Prose.io](https://prose.io) integration on the AVAA, it's pretty cool, check it out)

## Categories

In addition to Artifacts and Formats, another key part of the A/VAA "data model" are the connections between the pages, for browsing. Visual artifacts are inherently difficult to look up, because you only know what the problem looks like and not its technical name. So that's why we have both Categories and Tags to help. Categories are simple: `audio, video, film, digital, analog`. Tags are whatever a new page creator things is helpful. I'm saving Tags as a problem to tackle with a translator-leader later. For categories, I translated (with Lorena's help) each of them and again went in on some find-and-replace action for each of the Artifact pages, per folder. This was kind of annoying and took up some time, but I was also watching Olympic skateboarding (as mentioned), so it was fine and still better than doing it by hand for the NEARLY 100 (92 to be precise) entries. 

Hey I've never counted how many artifacts there are! Now we all know. It's 92! We'll have to have a hackathon that gets us to 100. Although that's something I haven't thought much about -- how to keep all of the translations in sync with each other and the primary English version. Considering there hasn't been a new Artifact added for a long time, I'm not too worried. Plus, it's a good problem to have because it means more people are contributing. 

Tags will probably get translated once by the translator and I'll probably do the slow work of updating them on each of the pages -- I don't think there's an amazing progammatic way to do this that would take less time than just idly copying and pasting, zoning out, while listening to a podcast. (But also if you want to write that script or do that, go for it pleeeeeaz).

## Conclusion 

I'm excited to kick this off, and even more excited once translations start rolling in and getting merged into the codebase, and even even more more excited to add the translation options back to the sidebar for everyone to enjoy.

If you want to organize a working group edit-a-thon day or need help with GitHub Q&A/instruction, I'm happy to help out. 

