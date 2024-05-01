---
title: 💡 Introduction
---

This page will give a short introduction into academic note-taking with [Obsidian](https://obsidian.md/).
Obsidian is a powerful knowledge base that works on top of a local folder of plain [Markdown](https://en.wikipedia.org/wiki/Markdown)files, which makes it extremely portable and flexible.

# Why Obsidian?
- Flexibility: Everything is ordered in Markdown files. This allows you to organize and link your notes in a non-linear fashion. 
- Extensibility: There are a lot of open source plugins available to extend the base functionality. Or: you can just code up one yourself!
- Local Storage: All your data is stored locally, which means: your notes, your data. Additionally, you are not forced into a ecosystem. If you want to switch to a different note taking app, you have all your notes in a simple file format
- Graph View: Visualize and navigate relationships between notes, which makes it easier to see how ideas connect.

If you want to read a more extensive overview, check out [this great article!](https://notes.nicolevanderhoeven.com/obsidian-playbook/Using+Obsidian/01+First+steps+with+Obsidian/An+overview+of+Obsidian). You will also find installation instructions there. It covers all the basic setup, which I do not need to repeat here. Check it out! 

In the following I want to talk about how I use obsidian :) 



# What works for me

> [!warning] Disclaimer
>  Note-taking and organizational methods are deeply personal. What works effectively for one person may not suit another. It's important to explore and adapt strategies to fit your own needs. Always remember, there are no one-size-fits-all rules in personal productivity! :)


The reason I like obsidian is because it shifts my thinking from "Which folder should I put this note?" to "How does this concept relate to others?". It helps me break down notes into the most fundamental parts, which forces me to understand them on the most basic level.

Think about this situation: 

>[!quote] Gedankenexperiment
>You are studying for a Reinforcement Learning course and decide to use a note-taking app to organize your thoughts. Typically, you might create a folder labeled "Reinforcement Learning Course" and fill it with notes on various algorithms like PPO and Q-Learning. As you learn more about optimization methods, you realize they intersect with other topics. In a conventional setup, you might add a marginal note like "This is also used in XY" and move on.

And then?

This note will probably get lost in a sea of text. It is just another piece of isolated information. But this exact connection is crucial for a broader understanding, because it links two different concepts.

This is where Obsidian shines!

Obsidian helps you to link those two concepts in an explicitly and visual way. Instead of losing crucial connections, you enhance your understanding by visually mapping how different ideas relate to each other. The foundation of this method is called the [[Zettelkasten Method]].
![[obsidian-vault-example.png]]

This helps me because I can see instantly, which concepts are related in the graph view.


# Use Cases

## References
I use my obsidian vault as a reference of things I learned, but also things I need regularly, but cant remember.
For example, I have a note containing the terminal command to create a conda environment from a yaml file

```python
conda env create -f environment.yml
```

because I always forget it..





## Literature
Maybe the best and most useful use case of this obsidian workflow is how it applies to literature review.

Lets again think of the following scenario:

>[!quote] Gedankenexperiment
>You are writing a literature review paper where you have to read through a lot of academic
>papers. There a lot of ways how to approach this: simply downloading all pdfs and taking notes somewhere, and then in the end bring it together. This can get messy very fast, since you may miss some connections between papers, say *Balkiz et. al* improves a methodology from *Paşa et al.*. It would be so cool if there was a way to make these connections more explicity and visually appealing...


Well, there is!

You can use a combination of a reference manager like Zotero and Obsidian, and then could do something like this:

1. Find all important papers and load them in Zotero
2. Read through the paper and make notes inside Zotero (highlight, add comments etc)
3. Use a community plugin to load in your literature notes from Zotero into Obsidian. This is the crucial part, because now this exact paper is a note inside your obsidian vault. This means you can link different notes to the paper note and vice versa
4. Link related papers in your obsidian vault to the one that you important

with this workflow you can connect concept notes in your vault to literature. For example if you come back months later, you could see in the graph view that *Balkiz et al.* used Genetic Algorithms in their methodology, without having to read thorugh the paper. Cool right?

Check [[zotero-obsidian-setup]] for more information on how to setup this workflow.


