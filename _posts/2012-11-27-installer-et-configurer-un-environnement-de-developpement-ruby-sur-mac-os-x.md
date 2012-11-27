---
layout: post
title: Installer et configurer un environnement de développement Ruby sur Mac OS X
---

## Introduction

Ces derniers temps, j'observe beaucoup de développeurs dans mon entourage voulant s'essayer à Ruby et/ou Rails. Je ne sais pas si c'est grâce à mon lobbying intensif ou si c'est parce que les gens commencent enfin à se rendre compte que **PHP est un langage moisit**, mais on ne va pas se plaindre.

Toujours est-il que quand on a toujours fait du LAMP/MAMP, il peut être un peu difficile de se plonger dans un écosystème totalement différent. Heureusement, le but de cet article est de vous aider dans cette voie !

Aujourd'hui, je vais donc vous expliquer en détail comment reproduire **MON** environnement de développement Ruby (et j'insiste sur le côté totalement subjectif de cet article).

D'ailleurs, certains des outils que je vais vous présenter sont totalement facultatifs (pour ne pas dire tous). Mais dans notre cas, le but est de mettre en place un environnement durable et agréable à utiliser. Bref, un truc qui nous simplifiera la vie au quotidien.

Et c'est exactement ce que vous propose ce tutoriel, à suivre **dans l'ordre**.

**N. B. 1** Cet article n'a pas vocation à vous convaincre que Ruby c'est bien ou que Ruby c'est mieux. Il s'adresse donc surtout à des personnes déjà convaincues qui cherchent à mettre la main à la patte rapidement. **Et qui ont un Mac**. Pour les pauvres, *désolé*.

**N. B. 2** En vrai, seules les parties 1, 2, 4 et 6 sont réellement réservées aux Mac users. Le reste de ce tutoriel est facilement adaptable aux autres systèmes UNIX.

### Sommaire

1. [Command Line Tools for Xcode](#s1)
2. [iTerm 2](#s2)
3. [zsh & oh-my-zsh](#s3)
4. [Homebrew](#s4)
5. [rbenv & Ruby](#s5)
6. [Pow](#s6)
7. [Pry](#s7)

## 1) <a id="s1"></a> Command Line Tools for Xcode

L'étape indispensable (et susceptible de prendre un peu de temps) est l'installation des Command Line Tools for Xcode. C'est un gros package contenant l'ensemble des outils qui vont nous être utiles pour la suite.

> This package enables UNIX-style development via Terminal by installing command line developer tools, as well as Mac OS X SDK frameworks and headers. Many useful tools are included, such as the Apple LLVM compiler, linker, and Make. If you use Xcode, these tools are also embedded within the Xcode IDE,
and can be installed on your system using the Downloads preferences pane within Xcode 4.5.

À noter que pour peu que vous ayez déjà développé sur Mac, il y a de grandes chances pour que vous ayez déjà installé la suite.

D'ailleurs, si vous avez Xcode (et que votre version est à jour, c'est important) vous pouvez directement vous rendre dans les préférences à l'onglet téléchargement, puis vous n'aurez plus qu'à cliquer sur un bouton.

![Xcode](http://dl.dropbox.com/u/894783/pym.github.com/images/3/xcode.png)

Pour les autres, il vous faudra un compte développeur Apple (gratuit), puis vous rendre sur [la page des téléchargements](https://developer.apple.com/downloads/). Une fois là bas, sélectionnez la version des Command Line Tools correspondant à votre OS (Lion ou Mountain Lion).

## 2) <a id="s2"></a> iTerm 2

[iTerm 2](http://www.iterm2.com/) est un remplaçant du Terminal fournit par défaut avec Mac OS X qui apporte tout un tas de fonctionnalités supplémentaires totalement indispensables : un vrai split pane (avec différentes sessions), la recherche, l'instant replay ou encore la possibilité de docker la fenêtre en haut ou en bas de l'écran et de lui assigner une hotkey (à la [TotalTerminal](http://totalterminal.binaryage.com/)). Plutôt qu'un long discours, je vous invite à consulter [la liste des features](http://www.iterm2.com/#/section/features).

Je vous conseille de chopper [la version beta](http://code.google.com/p/iterm2/downloads/list) qui est bien assez stable (et qui en plus est Retina ready).

Adoptez-le et on passe à la suite !

## 3) <a id="s3"></a> zsh & oh-my-zsh

[zsh](http://www.zsh.org/) est un shell Unix avec [plein de features chouettes](http://en.wikipedia.org/wiki/Z_shell#Features) : la complétion et la correction des commandes, un historique partagé entre les sessions, etc.

Mais sa véritable puissance se révèle avec [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) et ses plugins :

> A community-driven framework for managing your zsh configuration. Includes 40+ optional plugins (rails, git, OSX, hub, capistrano, brew, ant, macports, etc), over 80 terminal themes to spice up your morning, and an auto-update tool so that makes it easy to keep up with the latest updates from the community.

### Installation

Normalement, zsh est déjà présent sur votre machine.

Et oh-my-zsh s'installe en une ligne de commande :

    $ curl -L https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh | sh

En plus, le script se chargera même de remplacer votre shell par défaut !

### Configuration

Une fois oh-my-zsh installé, vous trouverez un fichier `.zshrc` dans votre home. Il s'agit du fichier de configuration de zsh (l'équivalent de `.bashrc` pour Bash).

On éditera ce fichier au fur et à mesure de l'avancement, donc soyez attentifs. En attendant, jetez un oeil au fichier et regardez comme il est joliment commenté !

### Bonus : Powerline

Si vous cherchez un thème sexy pour oh-my-zsh, essayez [Powerline](https://github.com/jeremyFreeAgent/oh-my-zsh-powerline-theme).

## 4) <a id="s4"></a> Homebrew

> The missing package manager for OS X

[Homebrew](http://mxcl.github.com/homebrew/) est **LE** gestionnaire de paquets pour OS X. Le seul. Si vous en utilisiez un autre jusque-là, voici les liens des procédures de désinstallation pour [MacPorts](http://guide.macports.org/chunked/installing.macports.uninstalling.html) et [Fink](http://www.finkproject.org/faq/usage-fink.php).

### Installation

La façon la plus simple pour installer Homebrew est d'ouvrir un terminal et de lancer la commande suivante :

    $ ruby -e "$(curl -fsSkL raw.github.com/mxcl/homebrew/go)"

Toutefois, je ne saurais trop vous conseiller de parcourir leur wiki, qui vous en apprendra un peu plus sur le fonctionnement et l'utilisation de Homebrew. Notamment [la page décrivant la procédure d'installation](https://github.com/mxcl/homebrew/wiki/Installation) .

Une fois Homebrew installé, pensez bien à lancer un `brew doctor` histoire d'être sûr que tout tourne sans problèmes. Si vous en avez, suivez les instructions et corrigez-les avant de passer à la suite.

### Configuration zsh

Ouvrez votre `.zshrc` et rendez-vous à la dernière ligne qui vous permet de personnaliser votre `$PATH` (juste après `# Customize to your needs…`).

Dans la liste des répertoires, ajoutez `/usr/local/bin` en premier, afin que les formules que vous installerez soient prédominantes en cas de conflit avec des binaires systèmes.

Vous devriez donc avoir quelque chose dans ce genre là :

    export PATH=/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin

### Bonus : ack, git, macvim

Maintenant que vous disposez d'une base clean, on peut installer quelques formules utiles !

#### ack

> ack is a tool like grep, optimized for programmers

    $ brew install ack

Super rapide et conçu pour la recherche de code, [ack](http://betterthangrep.com/) est devenu un de mes outils préférés. Par exemple par défaut, il recherche dans les sous-répertoires et ignore les dossiers de votre VCS. De la bombe !

#### git

    $ brew install git

La version de Git livrée avec les Command Line Tools n'est pas à jour et… j'aime bien avoir un Git à jour !

#### macvim

    $ brew install macvim --override-system-vim

[MacVim](http://code.google.com/p/macvim/) offre l'avantage de fonctionner exactement comme Vim, mais en utilisant les raccourcis Mac, en plus d'être à jour par rapport à la version système. En bonus, il vient avec une GUI (que je n'ai jamais ouverte).

## 5) <a id="s5"></a> rbenv & Ruby

Ruby est déjà installé sur Mac OS X, mais la version `1.8.7` se fait vieillote et puis on ne veut pas utiliser la version système de toute façon.

Pour installer une version plus récente de Ruby, nous allons utiliser rbenv & ruby-build.

> rbenv lets you easily switch between multiple versions of Ruby. It's simple, unobtrusive, and follows the UNIX tradition of single-purpose tools that do one thing well.

[rbenv](https://github.com/sstephenson/rbenv) vous permet de gérer différentes versions de Ruby depuis votre compte utilisateur (il n'altère en rien votre système).

### Fonctionnement

Parce que je suis un mec sympa, je vous colle le [How It Works](https://github.com/sstephenson/rbenv#section_1) de leur page GitHub :

> rbenv operates on the per-user directory `~/.rbenv`. Version names in rbenv correspond to subdirectories of `~/.rbenv/versions`. For example, you might have `~/.rbenv/versions/1.8.7-p354` and `~/.rbenv/versions/1.9.3-rc1`.

> Each version is a working tree with its own binaries, like `~/.rbenv/versions/1.8.7-p354/bin/ruby` and `~/.rbenv/versions/1.9.3-rc1/bin/irb`. rbenv makes shim binaries for every such binary across all installed versions of Ruby.

> These shims are simple wrapper scripts that live in `~/.rbenv/shims` and detect which Ruby version you want to use. They insert the directory for the selected version at the beginning of your `$PATH` and then execute the corresponding binary.

> Because of the simplicity of the shim approach, all you need to use rbenv is `~/.rbenv/shims` in your `$PATH`.

### Installation de rbenv & ruby-build

On ouvre son terminal et on installe les 2 formules suivantes :

    $ brew install rbenv
    $ brew install ruby-build

#### Configuration zsh

Au choix, à faire dans votre `.zshrc` :

- Activez le [plugin rbenv](https://github.com/robbyrussell/oh-my-zsh/blob/master/plugins/rbenv/rbenv.plugin.zsh) (qui ajoute aussi d'autres choses)

**OU**

- Rendez-vous à la fin du fichier et ajoutez sur une nouvelle ligne :

      if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi

### Installation de Ruby

On commence par lister les versions disponibles avec rbenv :

    $ rbenv install -l
    Available versions:
      …
      1.9.3-p125
      1.9.3-p194
      1.9.3-p286
      1.9.3-p327
      1.9.3-preview1
      1.9.3-rc1
      2.0.0-dev
      2.0.0-preview1
      …

Puis on installe la dernière version stable, ici la `1.9.3-p327` :

    $ rbenv install 1.9.3-p327

Enfin on définit la version globale de Ruby à utiliser par défaut :

    $ rbenv global 1.9.3-p327

Et on vérifie que tout s'est bien passé :

    $ ruby -v
    ruby 1.9.3p327 (2012-11-10 revision 37606) [x86_64-darwin12.2.0]

### Nota bene

Après l'installation d'une nouvelle version de Ruby, la commande `rbenv rehash` est lancée automatiquement. Cette commande (qui sert à installer les `shims`) est à lancer à chaque fois que vous installerez une gem qui contiendra des binaires.

## 6) <a id="s6"></a> Pow

![Pow](http://dl.dropbox.com/u/894783/pym.github.com/images/3/pow.png)

[Pow](http://pow.cx/) est un [serveur Rack](http://en.wikipedia.org/wiki/Rack_(web_server_interface)) pour Mac OS X développé par les petits mecs de [37signals](http://37signals.com/).

> Pow is a zero-configuration Rack server for Mac OS X. It makes developing Rails and Rack applications as frictionless as possible. You can install it in ten seconds and have your first app up and running in under a minute. No mucking around with `/etc/hosts`, no compiling Apache modules, no editing configuration files or installing preference panes. And running multiple apps with multiple versions of Ruby is trivial.

Ça à l'air sexy hein ? Et ça l'est !

### Installation

Comme pour la plupart des autres outils que l'on a utilisé jusque-là, une ligne suffit :

    $ curl get.pow.cx | sh

Maintenant, en supposant que vous ayez une application Ruby `myapp` dans votre dossier `~/Projects`, il ne vous reste plus qu'à créer un lien symbolique depuis le répertoire de Pow qui pointera vers le dossier de votre application :

    $ cd ~/.pow
    $ ln -s ~/Projects/myapp

Et vous pourrez voir directement votre application tourner sur `myapp.dev`. Même plus besoin de lancer `rails s` !

### Configuration

On peut configurer [pas mal de choses](http://pow.cx/manual.html#section_3) dans Pow en créant un fichier `.powconfig` dans notre répertoire utilisateur.

Dans notre cas, il y en a surtout une qui nous intéresse. En effet, on utilise rbenv. Mais le truc, c'est que Pow n'en a aucune idée… Au point où il utilisera la version système de Ruby si on ne lui dit rien !

La solution est très simple, on créé donc un ficher `.powconfig` dans notre répertoire utilisateur dans lequel on ajoute :

    export PATH=$(rbenv root)/shims:$(rbenv root)/bin:$PATH

Suite à quoi il faudra redémarrer Pow :

    $ touch ~/.pow/restart.txt

Ainsi, Pow utilisera la version de Ruby définie par rbenv et les [gems](http://en.wikipedia.org/wiki/RubyGems) associées ! Elle est pas belle la vie ?

### Powder

Comme faire des `ln` et des `touch` était encore trop lourd pour gérer Pow, des mecs se sont amusés à nous pondre des [gems](http://en.wikipedia.org/wiki/RubyGems) pour nous simplifier la vie.

Et [Powder](https://github.com/rodreegez/powder) est ma préférée !

On l'installe donc via un simple :

    $ gem install powder

Maintenant, pour lier une application au domaine local `.dev` correspondant, on se place dans le répertoire de l'app et on fait un :

    $ powder link

*And it's done.*

Powder rend l'utilisation de Pow vraiment **magique**. Pensez à faire un `powder -h` pour voir tout ce qu'il apporte.

### Bonus : Anvil

[Anvil](http://anvilformac.com/) est un utilitaire qui vous permet de gérer vos sites configurés avec Pow via une interface graphique. Mais bon, ça serait trop facile.

## 7) <a id="s7"></a> Pry

![Pry](http://dl.dropbox.com/u/894783/pym.github.com/images/3/pry.png)

> [Pry](http://pryrepl.org/) is a powerful alternative to the standard IRB shell for Ruby. It features syntax highlighting, a flexible plugin architecture, runtime invocation and source and documentation browsing.

Et croyez-moi, rien que pour le dernier point, ce shell Ruby est génial !

Si vous avez 17 minutes et 42 secondes devant vous, je vous conseille d'aller directement mater le [screencast d'introduction de Josh Cheek](http://pryrepl.org/screencasts.html). Vous aurez droit à un tour des fonctionnalités, puis Josh vous apprendra comment utiliser Pry en tant que debugger pour vos projets.

### Installation

On suit les conseils de Josh et on installe Pry (avec pry-doc) de la façon suivante :

    $ gem install pry pry-doc --no-rdoc --no-ri

### Exemple d'utilisation

On exécute Pry :

    $ pry

On crée une string `s` en tapant au hasard sur le clavier :

    [1] pry(main)> s = "! tsacneercs el retam rella'd tid suov no'uqsiup siaM"
    => "! tsacneercs el retam rella'd tid suov no'uqsiup siaM"

On cherche une méthode qui pourrait nous être utile avec `find-method` (au hasard, `reverse`) :

    [2] pry(main)> find-method reverse s
    String
    String#reverse
    String#reverse!

On se rencarde sur la méthode trouvée avec `show-doc` :

    [3] pry(main)> show-doc s.reverse

    From: string.c (C Method):
    Number of lines: 3
    Owner: String
    Visibility: public
    Signature: reverse()

    Returns a new string with the characters from str in reverse order.

       "stressed".reverse   #=> "desserts"

Et on fait ce que nous dit le monsieur :

    [4] pry(main)> puts s.reverse
    Mais puisqu'on vous dit d'aller mater le screencast !
    => nil

## Conclusion

Si vous avez tenu jusqu'à la fin et suivi de manière attentionnée ce tutoriel, vous disposez dès à présent de l'environnement clean et fonctionnel du parfait hipster Rubyiste. Bravo !

Des remarques ? Des questions ? Ou mieux : des outils à partager ? Les commentaires sont là pour ça ! :)
