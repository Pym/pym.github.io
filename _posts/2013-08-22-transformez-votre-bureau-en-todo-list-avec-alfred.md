---
layout: post
title: "Transformez votre bureau en todo list avec Alfred"
author: pym
image: images/5/remove-thumb.png
---

[Zach Holman](http://zachholman.com/), un mec de chez GitHub qui aime bien donner des conférences, a récemment partagé sur son repository dotfiles [un script simpliste](https://github.com/holman/dotfiles/commit/d774e970a88a04aca8024178849301af6d6ac5c3) lui permettant de gérer ses todos… à l'aide de son bureau !

### /bin/todo

> Creates something for me to do.
>
> I've used literally every todo list, app, program, script, everything. Even
> the ones you are building and haven't released yet.
>
> I've found that they're all nice in their nice ways, but I still don't use
> them, thus defeating the purpose of a todo list.
>
> All `todo` does is put a file on my Desktop with the filename given. That's
> it. I aggressively prune my desktop of old tasks and keep one or two on there
> at a time. Once I've finished a todo, I just delete the file. That's it.
>
> Millions of dollars later and `touch` wins.
>
> <small>Zach Holman</small>

Et voilà à quoi ressemble le "code" :

{% highlight console %}
$ touch ~/Desktop/"$*"
{% endhighlight %}

*SO HARDCORE*

Étant dans une situation similaire à Zach – à savoir : j'ai essayé des dizaines d'applications différentes pour gérer mes todos mais au final je n'arrive pas à en utiliser une plus de 2 jours d'affilé – je me suis décidé à tester cette solution.

Je lui trouvais plusieurs avantages :

- Rien à installer.
- J'aime avoir un bureau clean. Y avoir mes tâches m'encouragerait donc à m'en débarrasser plus vite pour retrouver un bureau propre.
- Aucune application à lancer et pas besoin d'aller sur un site pour consulter ma todo list. Elle est là et je suis forcé de la voir plusieurs fois par jour.

Cependant, un point m'embêtait tout de même. J'ai beau avoir [iTerm2]({% post_url 2012-11-27-installer-et-configurer-un-environnement-de-developpement-ruby-sur-mac-os-x %}/#s2) ouvert en permanence, il y a un outil que je trouve encore plus adapté pour faire le job et que j'utilise tout autant : [Alfred](http://www.alfredapp.com/).

## Introducing Desktop Todo

> [Desktop Todo](https://github.com/Pym/alfred-workflow-desktop-todo) allows you to create/delete empty items on your desktop from Alfred. That's it.

Je me suis donc inspiré du concept de Zach (en l'améliorant un peu) pour créer un workflow Alfred. Et je tenais à partager ça avec vous, les gens cool de l'Internet.

Le lien est en fin d'article, mais avant de télécharger le workflow je vais quand même vous expliquer rapidement comment il fonctionne.

### Créer une tâche

Ouvrez Alfred et tapez `t` suivi du nom de votre truc à faire.

![Pow](/images/5/add.png)

Ce qui aura pour effet de créer un fichier vide `sauver le monde` sur votre Bureau (`~/Desktop`).

Et entre nous celle là, c'est pas une des plus faciles.

### Créer une tâche colorée

En ajoutant `-c` suivi d'un numéro de couleur (liste ci-dessous) en paramètre de la commande précendente, cela renseignera l'étiquette du fichier (de la même façon que vous pourriez le faire avec un clic droit).

    t -c2 truc super important

Créera un fichier vide `truc super important`, "étiquetté" en rouge (je reprends le terme bizarre de Mac OS X).

Couleurs disponibles :

1.  Orange
2.  Rouge
3.  Jaune
4.  Bleu
5.  Violet
6.  Vert
7.  Gris

### Lister et supprimer des tâches

Ouvrez Alfred et tapez `d` suivi d'un espace et vous devriez avoir quelque chose dans ce genre là :

[![Pow](/images/5/remove-thumb.png)*Mon bureau à la date de rédaction de cet article*](/images/5/remove.png){: .thumbnail }

Une pression sur la touche `Entrée` et boum : la tâche disparait de votre bureau comme par magie.

## TL;DR

[Télécharger DesktopTodo.alfredworkflow](https://github.com/Pym/alfred-workflow-desktop-todo/releases) (GitHub)
