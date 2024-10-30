---
title: 📝 Obsidian Plugins
---


Here are some of the Obsidian Plugins that I currently use and how I use them.

To install these plugins, you have to find the community plugins section inside the obsidian settings, and then search for the plugin you want to install.

# Dataview
Dataview is a nice tool to querry your obisidan vault and display them as tables, list etc.

For example, I have images of research posters I took at Machine Learning conferences. When I save them inside my obsidian vault, I set the metadata `type` to be `poster`. Because then I can querry all posters inside my obsidian vault with dataview:

```dataview
table 
where type="poster"
```

You can go crazy and think of any kind of scenario where you might want to querry your vault for specific variables.


# Omnivore

This is a nice tool if you want to import content from the web inside your obsidian vault. This service is completely free and has a nice browser addon, where you can bookmark and highlight webpage inside the [ Omnivore ](https://omnivore.app/website) , and the obsidian plugin will automatically sync these.

This is the template I use inside the omnivore obsidian settings under `Article Template`

```
# {{{title}}}

## Links
[Read on Omnivore]({{{omnivoreUrl}}})
[Read Original]({{{originalUrl}}})

{{#highlights.length}}
## Highlights

{{#highlights}}
> {{{text}}} [⤴️]({{{highlightUrl}}}) {{#labels}} #{{name}} {{/labels}} ^{{{highlightID}}}
{{#note}}

{{{note}}}
{{/note}}

{{/highlights}}
{{/highlights.length}}

## Content
{{{ content }}}
```


This will get the entire content of the webpage, with all your Highlights and labels.


# Zotero Integration
I use the Zotero Integration plugin to load in my paper data from Zotero inside Obsidian.

Here are some nice references that should help you setup Zotero with Obsidian:
- https://www.youtube.com/watch?v=CGGeMrtyjBI&ab_channel=DannyTalksTech
- https://www.youtube.com/watch?v=m-J-v0JdL3w&ab_channel=BryanJenks (more comprehensive)

The settings I currently use are
![[Pasted image 20241030152349.png]]


## Template
You can find the Zotero obsidian template that I currently use [here](https://github.com/ufuk-cakir/notes/tree/v4/content/assets/zotero-integration-template.md). It is a simplified version of the Tutorials I shared above. You have to copy or download this markdown file, and then you can customize it as you wish!








