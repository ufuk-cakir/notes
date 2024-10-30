---
title: 📝 Obsidian Plugins
---


Here are some of the Obsidian Plugins that I currently use and how I use them.

To install these plugins, you have to find the community plugins section inside the obsidian settings, and then search for the plugin you want to install.

# Dataview
Dataview is a nice tool to querry your obisidan vault and display them as tables, list etc.

For example, I have images of research posters I took at Machine Learning conferences. When I save them inside my obsidian vault, I set the metadata `type` to be `poster`. Because then I can querry all posters inside my obsidian vault with dataview:

![[dataview-example.png]]

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
![[zotero-settings.png]]


## Template
You can find the Zotero obsidian template that I currently use is

```
---
type: literature
title:
  "{ title }": 
authors:
  "{ authors }": 
year:
  "{ date | format(\"YYYY\") }": 
publisher:
  "{ publicationTitle }": 
keywords:
  - "{ allTags }": 
citekey:
  "{ citekey }":
---
> [!meta]- Metadata
> abstract:: {{abstractNote}}
> zotero_link:: {{pdfZoteroLink}}
> Related:: {% for relation in relations -%} {%- if relation.citekey -%} [[{{relation.citekey}}]], {% endif -%} {%- endfor%}
> url:: {{url}}
> doi:: {{doi}}
> bibliography:: {{bibliography}}

---
### Webpage
<iframe src="{{url}}" allow="fullscreen" allowfullscreen="" style="height:100%;width:100%; aspect-ratio: 16 / 10; "></iframe>

---

### Self Notes
{% persist "notes" %}


{% endpersist %}

---

## Reading notes
{% persist "annotations" %}

{%-
    set zoteroColors = {
	    "#2ea8e5": "blue",
        "#5fb236": "green",
        "#a28ae5": "purple",
        "#ff6666": "red",
        "#ffd400": "yellow",
        "#f19837": "orange",
        "#aaaaaa": "grey",
        "#e56eee": "magenta"
    }
-%}

{%-
   set colorHeading = {
		"blue": "ℹ Background information, Prerequisites",
		"green": "❓ Assumptions, Questions, Goals, Problems",
		"purple": "📊 Main findings, Results, Conclusions",
		"red": "🧪Experimental details or Methods",
		"yellow": "⭐ Interesting point, Facts, Examples",
		"orange": "⚠️ Disagree with author",
		"grey": "📅 Vocabulary, Names, Dates, Definitions",
		"magenta": "📄 Important references"
   }
-%}

{%- macro calloutHeader(type) -%}
    {%- switch type -%}
        {%- case "highlight" -%}
        Highlight
        {%- case "image" -%}
        Image
        {%- default -%}
        Note
    {%- endswitch -%}
{%- endmacro %}

{%- set newAnnot = [] -%}
{%- set newAnnotations = [] -%}
{%- set annotations = annotations | filterby("date", "dateafter", lastImportDate) %}

{% if annotations.length > 0 %}
*Imported: {{importDate | format("YYYY-MM-DD HH:mm")}}*

{%- for annot in annotations -%}

    {%- if annot.color in zoteroColors -%}
        {%- set customColor = zoteroColors[annot.color] -%}
    {%- elif annot.colorCategory|lower in colorHeading -%}
    	{%- set customColor = annot.colorCategory|lower -%}
    {%- else -%}
	    {%- set customColor = "other" -%}
    {%- endif -%}

    {%- set newAnnotations = (newAnnotations.push({"annotation": annot, "customColor": customColor}), newAnnotations) -%}

{%- endfor -%}

{#- INSERT ANNOTATIONS -#}
{#- Loops through each of the available colors and only inserts matching annotations -#}
{#- This is a workaround for inserting categories in a predefined order (instead of using groupby & the order in which they appear in the PDF) -#}

{%- for color, heading in colorHeading -%}
{%- for entry in newAnnotations | filterby ("customColor", "startswith", color) -%}
{%- set annot = entry.annotation -%}

{%- if entry and loop.first %}

### {{colorHeading[color]}}
{%- endif %}

> [!quote{{"|" + color if color != "other"}}]+ {{calloutHeader(annot.type)}} ([page. {{annot.pageLabel}}](zotero://open-pdf/library/items/{{annot.attachment.itemKey}}?page={{annot.pageLabel}}&annotation={{annot.id}}))

{%- if annot.annotatedText %}
> {{annot.annotatedText|nl2br}} {% if annot.hashTags %}{{annot.hashTags}}{% endif -%}
{%- endif %}

{%- if annot.imageRelativePath %}
> ![[{{annot.imageRelativePath}}]]
{%- endif %}

{%- if annot.ocrText %}
> {{annot.ocrText}}
{%- endif %}

{%- if annot.comment %}
> - **{{annot.comment|nl2br}}**
{%- endif -%}

{%- endfor -%}
{%- endfor -%}
{% endif %}
{% endpersist %}
```

You can also find it [here](https://github.com/ufuk-cakir/notes/tree/v4/content/assets/zotero-integration-template.md). It is a simplified version of the Tutorials I shared above. You have to copy or download this markdown file, and then you can customize it as you wish!








