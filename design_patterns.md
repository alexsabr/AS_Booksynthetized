#Synthesis of Design Patterns  Elements Of Reusable Object-Oriented Software
see provided License file for Licensing informations.

## Motif de conception 

Les motifs de conceptions (design patterns) sont des agencements d'objets et de leurs relations qui permettent de répondre à des problématiques fréquemment rencontrés lors de la création d'un logiciel dans un langage orienté objet.
En plus de répondre à ces problématiques, ils permettent de le faire "correctement" (cad en respectant les 8 grands principes du génie logiciel : rigueur, décomposition élémentarité,modularité ...). Il s'appuient notamment sur les classes abstraites, les interface et une bonne encapsulation  

 Le livre <u>Design patterns elements of reusable object oriented software</u> du GoF fait référence dans le domaine.

Il existe 3 types de motifs de conceptions orientés objets:

- Les motifs de conception créatifs

  Ils permettent de gérer par qui ,quand et quel objet est créé et quel objet va effectivement être utilisé à un endroit donné. il y a 2 types de motifs de conceptions créatifs; 

  - ceux <u>de classe</u> qui font varier l'objet instancié en usant de l'héritage
  - ceux <u>d'instance</u> qui font varier l'objet instancié en déléguant à une autre instance l'instanciation. 

- Les motifs de conception structuraux

Ils permettent de gérer comment les objets et les classes sont reliés entre elles pour former de plus grosses structures.
Elles mettent l'accent sur la facillité à modifier les composant des structures mises en place,
 en passant par une gestion astucieuse de l'héritage,des classes abstraites, et de la composition. 
  
- Les motifs de conception comportementaux

Preque davantage un problème de programmation fonctionnelle que de programmation orientée objet.
Ces motifs mettent cherchent à faciliter la modification du  travail réalisé par une classe, un objet une fonction  que ce soit à l'exécution ou au développement.
Ils veulent aussi faciliter la coopération entre plusieurs objets pour réaliser une tâche et rendre le fonctionnement du tout lisible.

### motifs de conceptions créatifs

#### Factory

Fonction : 
Permettre à un client de développer un objet qui sera 
- adapté à son besoin (car il l'a développé) 
- capable de fonctioner dans notre système  (il souhaite l'utiliser mais ne le contrôle pas)
L'ancien code (le notre) pourra appeler/appelera du nouveau code (celui du client),
sans adaptation particulière une fois ce motif mis en place.



Exemple :
On développe un moteur de jeu vidéo et l'on souhaite que certains objets 
/ classes appelés par notre moteur puissent être adaptés par les développeurs à leur besoin. 
On ne peut  pas prévoir  quels seront les besoin des développeur  (plein de types de jeux possibles).
 
On développe une bibliothèque de Lexer-Parser et l'on souhaite que l'utilisateur  nous fournisse les jetons que notre système va utiliser,
adaptés à son besoin.



Comment Faire :

Nous définissons deux classes (Abstraite ou non)
une qui créé des objets usines 
une qui créé des objets cibles (peut aussi être une interface et non une classe)

Les objets cibles servent dans le système,
et le client les développe pour qu'ils soient adaptés à son besoin.

Les objets usines servent à créer des objets cibles.
A chaque fois que notre système à besoin d'instancier un objet cible, il demandera un objet usine de le faire.

Toute la question est ensuite de passer au système le bon objet usine pour qu'il utilise l'objet cible du client.
Pour cela 3 options 
- On passe au système un un objet usine à utiliser 
- le système utilise des paramètres de type pour obtenir la classe
- le système prend en paramètre un nom/identifiant qui lui permet de choisir 
dans une structure de données d'objet usine lequel choisir (dans le livre GOF mais je la trouve monstrueuse) 

utiliser lorsque
- un système doit effectuer une action, mais l'on veut que cette action
soit paramétrable par le client sans que le système ne varie 

conséquences subtiles
- le système ne connait pas et n'a pas a connaitre la classe concrète des composants qu'il utilise
pour fonctionner correctement


#### Abstract Factory


Fonction:

Rendre indépendant l'utilisation d'une famille d'objets travaillant ensemble de la famille choisie parmis une multitude.
Pour se faire, on rend le client indépendant du choix de la famille et de l'instanciation des  objets de ladite famille.

Cela permet lui fournir un même service avec des variation ( en changeant la famille utilisée) 
sans révéler l'implémentation et sans que le client n'ait d'effort d'implémentation supplémentaire à fournir pour s'adapter aux différentes familles.

Exemple : Look & Feel d'une IG, on veut des boutons à composer avec des fenêtres et des barre de défilement.
On veut que le client puisse utiliser ces boutons/fenêtre/barre de défilement indépendamment du LF,
mais  on veut aussi pouvoir lui  garantir qu'elles auront toutes le même L&F
qu'il soit Windows / Apple / Nautilus / ... .  


Cela se fait de la manière suivante :

Tout d'abord cacher la classe concrète (et donc la famille) des objets fournissant un même service 
en les faisant tous hériter d'une même classe abstraite (une par service à fournir).
Ainsi le client ignore la famille utilisée et peu importe, car il aura le service qu'il souhaite grâce à l'interface de la classe abstraite.

Ensuite permettre au client d'instancier ces objets fournissant des service sans connaître leur classe concrète (et donc leur famille).
Pouvoir aussi lui assurer  que les différents objets fournissant différents services n'auront aucun problème à travailler ensemble car seront tous issus de la même famille. 
On créé une classe Abstraite "Usine d'objet à service" qui fournit des méthodes pour générer les objets fournissant les différents service que l'on souhaite.
Enfin, créer pour chaque famille une classe concrète qui hérite de cette classe abstraite et qui peut générer les différents objets de SA famille fournissant les différents services.

Lorsque le client veut créer des objets, on choisit quelle famille d'objet on va lui fournir, on lui fournit alors la classe "Usine d'objet à service" correspondant à la famille souhaité.
Grâce à la classe abstraite de "Usine d'objet à service" le client peut obtenir ses objets à service indépendamment de la famille choisie.

Utiliser lorsque :
- Un système devrait être configuré avec une de plusieurs famille de produits 
- les différents objets fournissant les différents services DOIVENT être de la même famille
- on veut cacher au client l'implémentation

Conséquences subtiles
+ 
-  Rajouter de nouveaux objets à service / de nouvelles familles peut devenir lourd,
si on ajoute une famille il faut que cette famille soit capable de fournir tous les différent objets à service qu'offre notre module/package/bibliothèque
si on ajoute un nouvel objet à service il faut l'implémenter dans toutes les familles 

Astuces d'implémentation
Les "Usines d'objets à service" peuvent être des singletons, pas forcément besoin d'en instancier plusieurs.
L'instanciation des objets fournissant des services est laissé au soin de chaque famille; libre à elle d'utiliser 
quelque méthode d'instanciation que ce soit (par exemple Factory)
En utilisant le motif prototype on peut se simplifier/ s'alléger l'ajout de nouvelle famille en ce qui concerne "l'Usine d'objet à services" concrète.
On a une même "usine d'objet à service" concrète pour toute les familles qui se contente de copier tout ce qu'on lui donne (les objets à service d'une même famille).


#### Builder

fonction
Permet de faire varier indépendamment
- les détails d'implémentation d'un objet
- son processus de fabrication 
(à ne pas confondre avec Bridge qui n'est même pas créationnel, et
 qui permet de faire varier *abstraction* et implémentation !)

cela se fait de la manière suivante

Nous avons 3 type de classe
- Les directeurs auxquels on demande de se débrouiller pour 
	nous obtenir un objet final.
	 Il supervise le Builder **qu'on lui a passé d'une manière ou d'une autre**
	Le directeur est donc paramétrable grâce au Builder qu'on lui fournit.
	Cela peut être au choix le client ou nous qui paramètre le directeur.

- Les Builder qui construisent des objets finaux en de nombreuses étapes,
	à la demande et sous la supervision des directeurs.
	Généralement une classe abstraite / une Interface Builder,
	que le directeur connaît, et différentes implémentation concrète de 
	cette classe abstraite / cette interface

- Les produits finaux qui sont retournés à terme par le Builder puis par le directeur au client

Le client est en maitrîse / sait le type concrect de ce que va lui retourner à la fin le directeur.
Ironiquement seul le directeur ignore le type final de ce qui va lui être retourné.


utiliser lorsque

- Si la méthode de fabrication de différents objet ne varie 
- - que par les détails et pas par l'algorithme de fabrication 
- - que par l'algorithme de fabrication et pas par les détails
- On est entrain d'expérimenter l'explosion combinatoire avec beaucoup
	de surdéfinitions d'un constructeur pour gérer toutes les combinaisons possibles de paramètres

conséquences subtiles

+ Peu importe la variation interne des produits finaux, le directeur ne connaît
	que l'interface de construction la plupart des changements sur les produits ne le 
	concerne donc pas 

+ 

Astuces d'implémentation
Il est envisageable que la classe Builder de base que connaît le directeur soit concrète.
Toutes les étapes de constructions ne feront rien, ce sera lors de l'implémentation de 
class Builder enfant, héritant de ce squelette de classe mère 
que certaines/toutes les méthodes seront redéfinis pour s'adapter à notre besoin.


#### Singleton

Fonction :
Gérer intégralement les accès à une ressource ( éventuellement globale).
Accessoirement, assurer qu'un objet ne sera instancié qu'une seule fois au sein d'un programme.


cela se fait de la manière suivante:
Dans la classe qui  hébergera le singleton, cacher le constructeur, avoir un champ statique qui conservera l'unique instance de la classe,
exposer depuis la classe une méthode qui permettra d'accéder à l'unique instance et l'instanciera si nécessaire.
Attention au Threading lorsqu'on instanciera l'objet au risque d'en instancier plusieurs d'un coup !

utiliser lorsque
On veut qu'une seule instance d'un objet soit utilisé dans un programme,
On veut pouvoir contrôler finement (ou pas) ses accès.

conséquences subtile :

Ironiquement le motif du singleton  n'oblige pas à une seule instance,
on peut tout à fait concevoir une méthode avec plusieurs instance et une distribution 
en fonction d'un quelconque algorithme.

Mal fait / utilisé comme protection de variable globale cela peut compliquer / fausser les test
car on introduit une nouvelle variable avec des états changeant accessible à tous,
qui peut influer sur d'autres composant.

Si les fonctions de l'instance n'ont aucun effet de bord sur elle même / tout court,
on peut voir le Singleton comme une méthode de transformer des méthodes 
de classe en méthode d'objet, transformant quelque part ainsi
les classes en citoyens de premier ordre. On tire alors 
aussi parti de la liaison dynamique.

astuce d'implémentation : 

La création de l'unique instance peut se faire 
- immédiatement au chargement du programme, 
	peut rendre  le lancement du programme plus long 
	mais permet d'éviter des test de sécurité plus tard.

- lorsque l'instance est demandée pour la première fois par quelqu'un
	la demande initiale sera ralentie 



#### Prototype

fonction : Permettre d'user de la liaison dynamique pour 
copier des objets sans connaître leur classe concrète

cela se fait de la manière suivante:

créer une classe abstraite / une interface de clonage 
elle comportera une méthode "clone" à utiliser par le client
dès qu'il voudra dupliquer un objet 
implémenter la copie profonde de la méthode clone
faire utiliser au client cette méthode.

utiliser lorsque
- On veut permettre de dupliquer des objets lourd à configurer
(que ce soit lors de ou post construction)
- On souhaiter éviter d'avoir à utiliser l'héritage juste pour pré-configurer
des classe enfant qui font de toute façon un travail identique 


conséquence subtile
- le client peut dupliquer des objets/ leur configuration
sans connaître leur classe concrète

astuce d'implémentation : 
Avoir un gestionnaire de prototype permet de mettre à
disposition du client plusieurs configuration possible 
et de lui éviter la gestion de ceux-ci 

### motifs de conceptions structuraux

#### Adapteur

Fonction: Permettre la communication entre deux composants / un système et un composant qui seraient autrement incompatibles 
exemple utiliser un analyseur de donnée statistique  qui ne travaille qu'avec des données en XML alors que le système gère les données en JSON
Il emballe le composant / bibliothèque incompatible et s'occupe de faire les conversions entre les deux système.

Ce n'est pas la même chose que Facade : Facade est simplement un accélérateur de configuration,
un "mode facile " pour utiliser des composant.

cela se fait de la manière suivante:

L'adapteur doit tout d'abord exhiber l'interface cible que l'on souhaite avoir.
Ensuite deux façon d'adapter :

par héritage / interfaçage
L'adapteur hérite / implémente l'interface de la classe 
que l'on souhaite adapter.
Permet de surcharger/redéfinir les méthode de cette dernière.
Ne permet pas d'adapter d'autre classe enfants de la classe mère.

par composition
L'adapteur stocke une instance de la classe a adapter 
Permet d'adapter la classe mère mais aussi tous ses descendants
Ne permet pas de surcharger/ redéfinir les methodes d'une instance de la classe adaptée.

utiliser lorsque
- on veut utiliser une classe / interface / bibliothèque 
mais elle ne peut pas être utilisée telle qu'elle dans notre code.


conséquence subtile 

Permet de cacher la bibliothèque/ instance externe;
Ainsi on peut changer le composant tiers utilisé tant qu'on passe par l'adapteur.

astuce d'implémentation : 

Dans un langage avec de l'héritage multiple, l'adaptateur peut hériter 
à la fois de la classe à adapter et de la classe pour laquelle on adapte,
rendant l'adaptateur utilisable dans les deux contexte.

#### Pont / Bridge

Fonction : Permettre à l'implémentation et l'abstraction de varier "librement" l'un de l'autre, 
	tout en restant lié.

cela se fait de la manière suivante:

On a  initialement deux classes avec des interfaces bien définies;

- une classe (abstraite ou non) "AbstractionBase"
- une classe (abstraite ou non) " ImplémentationBase "

AbstractionBase connait par composition ImplémentationBase.
toutes les classes d'Abstraction descendront de la classe AbstractionBase
et définiront le travail qu'elles auront à réaliser au travers de l'interface d'ImplémentationBase
et de l'instance d'Implémentation posséedée.
toutes les classes D'implémentation descendront d'ImplémentationBase 
et ajouteront leur subitilités à l'implémentation en redéfinissant 
les fonction de ImplémentationBase.

utiliser lorsque:
- L'abstraction est fixe mais l'implémentation est choisie / peut varier pendant l'exécution
	exemple : librairie graphique
- des changement dans l'implémentation ne devraient pas forcer le client à recompiler 
le code de l'abstraction (exemple encore interface graphique, pilote etc.)

conséquence subtiles:

astuce d'implémentation : 

Utiliser un motif Abstract Factory permet d'être garanti de l'usage des bons implémenteur/ bonne implémentation
tout particulièrement quand on a plusieurs couple/pont abstract-implémentation à faire travailler ensemble.


#### Composite

fonction : Le client peut traiter de manière identique
 un conteneur d'objet et son contenu.

cela se fait de la manière suivante:

Trois classes (abstraite ou non)
Composant
déclare une interface généraliste que le client va exploiter
pour gérer les composant stockés
pour leur faire faire des actions prévues

Conteneur
Peut stocker des composants
éventuellement peut aussi implémenter les actions prévues

Feuille
Ne peut pas stocker de Composant 
Peut effectuer les actions prévues

utiliser lorsque
Le client doit pouvoir faire effectuer des actions sur un composant donné
sans avoir à savoir s'il fait affaire avec un conteneur ou une feuille.

conséquence subtiles
- L'ajout de nouvelles classes jouant le rôle de feuille est très facile à gérer pour le client,
il n'a pas ou peu besoin de changer son code.
- le client est dans l'impossibilité de savoir s'il travaille avec un conteneur ou une feuille
s'il passe par l'interface du Composant, il peut tenter de faire des choses illogiques 
(comme tenter d'ajouter des enfants à une feuille)
et cela ne sera rattrapé qu'à l'exécution, pas à la compilation

astuce d'implémentation : 
Pour qu'un client sache si un composant est un conteneur,
on peut rajouter une opération dans l'interface de Composant qui permet
d'interroger n'importe quel composant pour savoir s'il s'agit d'un conteneur
Sinon, plus prosaïquement lever une exception si un ajout est tenté sur une classe feuille
(encore une fois vérification dynamique...).

#### Décorateur

Fonction : Ajouter des possibilité à une instance "particulière" d'une classe (pas toutes les instances de la classe).
Et ce de manière transparente pour les utilisateurs.
Evite par ailleurs une explosion combinatoire où chaque composant devrait être doublé, triplé  pour pouvoir permettre toutes les variations possibles.
(exemple rajouter une barre de défilement à une zone de texte, puis une bordure, ou l'inverse, ....)

cela se fait de la manière suivante:
Les classes mère citées peuvent-être abstraites.
Une classe mère composant : elle fait le travail initial qu'on souhaite atteindre.
Une classe mère Décorateur : elle hérite de la classe mère composant. Elle possède aussi par composition 
une une instance de la classe mère composant 
Des classes filles de la classe mère composant : implémentation de différents composant 
Des classes filles de la classe mère décorateur : implémentent de différentes décorations

les classes Décorateur redirigent les appels qu'elles recoivent sur leur interface 

Grâce à cette structure on peut empiler décorateur après décorateur sur un même composant sans que cela ne pose de problème !

utiliser lorsque

conséquence subtiles

plus flexible car des "propriétés/responsabilités" peuvent être entassés,
ajoutés au spprimmées dynamiquement au près d'un objet

allège les classes abstraites hautement placé dans la hiérarchie,
Ajout de "juste ce qu'il faut" en termes de fonctionnalité.

Ajoute un peu de généricité, en effet un décorateur est identique à un composant côté client.
Le code va finir avec pleins de petites classe Décorateurs. 

astuce d'implémentation : 
Garder un composant léger, c'est les décorateurs qui lui apporte des choses,
sinon préférer peut être le pattern stratégie

vie séparée décorateur et son composant?


#### Façade

Fonction: Simplifier la mise en œuvre de plusieurs composants/ d'un agencement complexe de composant pour rendre un service. 

A ne pas confondre avec adapteur :
- Adapteur s'intercale entre deux systèmes incompatibles 
pour les faires fonctionner ensemble, il "modifie" les interface affichées et surtout les fonctionalités.

- Façade masque la complexité d'un système à un autre et par une opération simple permet d'obtenir le service requis en gérant le grand nombre de paramètres de l'autre système.
il faut le voir comme une configuration par défaut.

Ni avec Mediator :
- Mediator promeut  plutôt une architecture monolithique
contrairement à Facade et permet surtout, un peut comme Adapteur,
de fait dialoguer entres-eux des composant incompatibles / sans connaître leur interface respective. 


Exemple la mise en oeuvre d'un compilateur ou de nombreux paramètres sont mis en place par défaut.

cela se fait de la manière suivante:


utiliser lorsque

On veut faciliter la mise en oeuvre d'un système,
et/ou fournir une configuration par défaut à l'utilisateur.

On veut un faible couplage entre les sous-systèmes et le client, 
personne ne sait ce qu'il se passe derrière la facade !

conséquence subtiles:
Il faut s'assurer que la Facade ne devienne pas une excuse pour concevoir un système monolithique qui tourne autour de la Façade,
c'est un ajout pour simplifier l'usage au client, pas un orchéstrateur en arrière boutique.

permet donner à un système la forme de "couches" ooù chaque sous-système sera bien délimité / séparé des autres

astuce d'implémentation : 

Si la facade est une classe abstraite on peut envisager par exemple de mettre le sous-sytème 
derrière une Abstract Factory et gérer silencieusement pour le client, le changement entre différents sous-systèmes ! 
Alternativement même si ça me semble ésotérique mettre une facade à laquelle accède le client et une autre facade entre 
la facade et le sous-système. 

On peut considérer qu' un sous-système a comme une classe une interface publique (à laquelle le client à totalement accès)
et une interface privée uniquement pour le sous-système lui même. La facade fait alors partie (mais peut aussi ne pas être la seule classe)
de cette "interface publique" du sous-système.



#### Flyweight

Fonction : économiser la mémoire consommée en permettant à plusieurs objets de mettre une même ressource en commun.
A utiliser typiquement si nous allons instancier pleins d'objets; fréquemment utilisé avec le motif Factory.

Par exemple : la même texture exploitée plusieurs fois dans un moteur de jeu-vidéo. 

A ne pas confondre avec Singleton qui ont certes des points commmuns:
-ils gèrent/ protègent l'accès à une ressource limitée

Mais aussi de fortes différences hormis le fait que ce soient des motifs structuraux et créatifs:
- l'objet contenu dans un singleton est mutable, celui dans un flyweight est immutable (et oui sinon on ne pourrait pas le partager !)

cela se fait de la manière suivante:
Le client s'adresse à une interface pour récupérer
sa ressource statique en fonction d'une clé qu'il possède.
A notre implémentation de faire le lien entre la clé et 
la ressource souhaité et de la lui retourner.
L'interface peut éventuellement aussi permettre au client d'ajouter
de nouvelles ressources à stocker en fonction d'une clé. 

utiliser lorsque
un même état statique risque d'être 
instancié à de nombreuses reprises (i.e pour rien)
quand il pourrait être réutilisé, faisant alors des économies de place


conséquence subtiles
Ne servira à rien si il y a beaucoup d'état statiques très peu partagés entre objets
Il faut bien gérer la libération de mémoire de cette ressource statique
une fois qu'elle n'est plus utilisée

astuce d'implémentation : 
Une variation du flyweight pourrait permettre de muter les instances qu'il conserve
et renverrait alors l'utilisateur vers 
à joindre alors avec un composite/stratégie pour permettre cette action.

Les motifs stratégie  et état peuvent être implémentés
en utilisant le motif flyweight. 



#### Proxy

fonction : Se faire passer pour une ressource pour gérer son accès à l'exécution.
pour retarder sa fabrication effective jusqu'au dernier moment,
celui de son utilisation effective.

cela se fait de la manière suivante:
soit la classe (abstraite ou non) Ressource qui représente la ressource que l'on souhaite utiliser.
La classe Proxy hérite de cette classe Ressource.
La classe proxy agrège et/ou gère  une classe fille Ressourcefille qui hérite 
de la classe mère Ressource. 
Cette classe Ressourcefille peut être abstraite, derrière une Abstract Factory, etc.


utiliser lorsque:
On veut réguler l'accès à une ressource, mais discrètement à l'exécution
(pas comme singleton qui de toute façon se limite à un seul objet).

astuce d'implémentation : 
Dans les langages qui le permettent, on peut surcharger les opérateurs d'accès
à la ressource pour permettre au proxy d'intercepter l'appel.

Le motif du proxy peut être vu comme un décorateur particulier qui ne lui diffère que par son intention
Le motif du décorateur ajoute des responsabilité à la volée à un objet,
le proxy permet de gérer à l'exécution l'accès à un objet, sans que le client ne le sache.

Il peut aussi être vu comme un motif adapteur à l'exécution; 
présentant la même interface que la Ressource adaptée, 
mais modifiant/limitant les actions à l'exécution.

### motifs de conceptions comportementaux

#### Chaîne de responsabilité 

Fonction:
Permettre d'assurer que le traitement d'un message sera traité par le bon objet dans une chaîne d'objet.
Pour chaque objet maillon dans la chaîne, il traite le message s'il peut le traiter,
sinon il passe le message à l'objet maillon suivant de la chaîne
(exemple les exceptions, la réaction aux évènements des interfaces graphiques)   


Cela se fait de la manière suivante:

Une classe/interface Gestionnaire (abstraite ou non) peut traiter une requête 
selon un format standard. On peut lui ajouter un successeur auquel faire passer
la requête s'il se trouve dans l'incapacité de traiter la requête.
Des classes héritent / implémentent l'interface Gestionnaire.

conséquence subtile :
Le traitement de la requête n'est pas garanti;
que se passe-t-il si aucun des gestionnaires n'est en mesure de traiter la requête fournie ?

Utiliser lorsque:
Plusieurs objets peuvent traiter une requête et on ne sait pas qui a priori.
On veut envoyer une requête a une grappe d'objet sans avoir à spécifier le destinataire explicitement.
Le jeu d'objets qui peut gérer une requête devrait être spécifié dynamiquement.

Astuce d'implémentation :
On programme à l'interface/ à la classe abstraite;
ainsi on peut profiter des gestionnaires d'évènements  successifs avec des classes conrètes différentes
qui sont tout à fait compatibles les un avec les autre car ils ont la même interface.




#### Memento

Fonction : Sauvegarder l'état d'un objet dans le temps sans briser l'encapsulation.
(exemple historique des activités dans un logiciel de dessin / d'édition de texte ... / l'envoyer sur le réseau ?)

cela se fait de la manière suivante:
Soit la classe Origine, qui possède l'état qu'on souhaite stocker/ restaurer.
Grâce à une interface elle est capable de stocker / restaurer des informations sur son état 
à un objet d'un autre classe Memento. Cette classe Menmento stocke les informations qui lui sont fournis
Nous avons une classe Memento, elle stocke des informations qui lui sont fournis.
Enfin le client, gère les Memento comme bon lui semble, sans tenter d'accéder à leur contenu

utiliser lorsque:

conséquence subtile :
Ce motif s'utilise très bien avec le motif "Commande" pour conserver l'historique des commandes !

astuce d'implémentation : 
La classe Memento peut être interne à la classe Origine, mais alors le Memento n'est pas générique,
ou alors il doit ensuite être envoyer dans un Gestionnaire de Memento qui lui peut gérer toute sorte de Memento.

En utilisant finement les accès  aux interfaces, on peut faire de sorte que le Memento expose,
une grande interface de sauvegarde/chargement aux objets de la classe origine; 
et une toute petite interface "d'administration" au client.


#### Observateur

fonction : Motif des interfaces graphiques par excellence,
il permet  à l'exécution a différents Objets de s'identifier comme étant intéressés 
par des variation d'état de quelque chose (par exemple un autre objet ou une ressource).

A ne pas confondre avec Chain of Reponsibility,
où des "résolveur d'évènement" se font suivre un message les un après les autres s'ils ne savent pas le résoudre.

cela se fait de la manière suivante:
Nous avons une classe (abstraite ou non) émetteur;
qui expose  une  interface permettant :
- de se signaler comme étant intéressés par les variations  proposés; 
- de se désinscrire.
- de récupérer des informations sur l'état actuel 

Nous avons une classe (abstraite ou non ) récepteur
qui permet de s'identifier auprès d'un observateur pour
- suivre des variations
- se désinscrire.
Ils exhibent une méthode qui leur permet d'être notifié lors d'une variation.


utiliser lorsque
- on veut signaler des changements à des objets sans souffrir d'un fort couplage
- on veut que deux arbres d'abstraction communiquent ensemble tout en restant indépendant.


conséquence subtile :
- Attention si les observateurs sont lourds / nombreux, un petit changement du sujet peut 
avoir des conséquences lourdes en performances car il déclenche de nombreux calculs
dans tous les observateurs.

astuce d'implémentation : 
La variation d'état peut être très précise et décrire à l'observateur ce qu'il s'est passé
ou au contraire très vague, le contraignant à demander à l'objet émetteur ce qu'il s'est passé.
Un objet peut tout à fait ignorer des messages.

Le motif Observateur peut être utilisé par le motif Médiateur.

#### Stratégie

fonction :
  Rendre une partie bien délimitée du code utilisé dans une fonctionnalité interchangeable
cela se fait de la manière suivante:
Une classe mère (Abstraite ou non) Stratégie
de laquelle hérite différentes implémentation d'algorithme, chacune dans leur classe propre
le client intéragit avec elles
- soit uniquement via l'interface exhibée par la classe mère Abstraite stratégie  
- soit pas du tout car le client intéragit avec une classe tierce qui elle choisira la bonne stratégie à utiliser
  pour répondre à la demande du client.
utiliser lorsque:
- plusieures classes varient entre-elles uniquement par leur comportement, pas par leur interface & membres
- différents algorithmes faisant la même chose doivent être choisis en fonction de leur utilité.
- un des algorithmes utilise une structure de données qui lui est propre, le client ne devrait pas avoir à y être exposé.

conséquences subtiles :
- la disparition de switch / de suites de branchement conditionels. 
  (la stratégie est décidée une fois auparavant pour tout le monde et ensuite on ne fait
  qu'appliquer la stratégie choisie sans soucier de ce qu'elle est;
  les décideurs décident, les exécutant exécutent)
- l'inutilité de faire des sous classe 
  plutôt que de faire des classes enfant juste pour changer le comportement, autant utiliser une seule classe
  qui ne fait que changer de comportement ! Les changements globaux n'en seront que facilités
- nécessité de se contorsionner face à des changements locaux 
- ajout potentiel d'un entête pour la communication. 

astuce d'implémentation : 
- Une usine abstraite (abstract factory) peut permettre d'établir des familles d'algorithmes,
par exemple de synchroniser algorithmes et structures de stockage 
- le motif du singleton ou du flyweight peut permettre d'éviter d'avoir beaucoup d'objets stratégie.


#### Template 

fonction :décomposer un long algorithme systématique comprenant 
  des briques primitives qui peuvent varier indépendamment les unes des autres,
  et qui comportent tous des parties identiques que l'on veut regrouper.

A ne pas confondre avec le motif stratégie 
- fourni une famille d'algorithmes faisant tous la même chose, différemment.

Dans Template c'est un même algorithme que l'on décompose et auquel laisse soin à autrui de paramétrer;
Le paramétrage est plutôt statique, via héritage, que dynamique, via composition comme dans stratégie.
Et le résultat final varie contrairement à stratégie où il s'agit de la méthode d'atteindre un même résultat qui varie.

Reste quand même que ce motif a un côté "c'est juste l'utilisation standard de la liaison dynamique"

cela se fait de la manière suivante:
Une classe AlgoComplet (abstraite ou non )
présente une interface comportant 
- une méthode (si possible finale) executerAlgo qui va exécuter dans un  ordre défini et connu les différentes étapes
- des méthodes EtapeAlgo(qui seront redéfinies) qui vont être exécutés dans un certain ordre par executerAlgo.


utiliser lorsque:
- des mécanismes communs à différentes sous classes devraient être localisés
    à un même endroit pour respecter le principe DRY (ne pas se répéter); seul le code
    qui varie sera localisé autre part.

- pour limiter l'extensibilité à des endroits bien particuliers;
 en définissant la méthode mère comme finale on l'empêche d'être modifiée
 en crééant des crochets particulier sur lesquels  le client peut s'accrocher pour modifier la méthode
 mère à certains endroits.
 

conséquences subtiles:
- permet à de l'ancien code (Executeralgo) d'appeler du nouveau code contenu dans Etapealgo


astuce d'implémentation : 
- minimiser le nombre minimum d'opération qu'un lient *DOIT* redéfinir pour pouvoir utiliser 
  executer algo
Les méthodes d'usine peuvent se révéler très utiles.

#### Etat 

fonction : 
lorsque un objet a plusieurs / de nombreux états 
bien déterminés et ségrégés, il exhibe la même interface
mais son comportement varie en fonction de l'état.
Il "a l'air "de changer de type concret.

A ne pas confondre avec 

- stratégie: propose différentes
implémentations qui font la même chose 
et avec la même interface 

Quand état propose différentes implémentations avec 
la même interface qui font **d'autres choses**

- template: Etat agrège des objets pour proposer différents comportements
template agrège des fonctions pour proposer différents comportements

utiliser lorsque : 

chaque / beaucoup des opérations de l'objet comportent
une pile de branchement conditionels en fonction de son état

cela se fait de la manière suivante :
Une interface/classe abstraite état delaquelle héritent
les différentes implémentations des états.
Une classe contexte qui agrège les différents états
et exhibe l'interface de l'état en temps voulu.

conséquence subtile :
- très OOP, les états sont bien ségrégés
- les transistions d'état sont explicites et faciles à tester.
- permet d'éviter les grosses fonctions avec de multiples 
branchement conditionels qui testent à chaque fois la même chose


astuce d'implémentation : 
une machine à état finis pourrait servir ici.
on pourrait envisager de rajouter dynamiquement des états possibles et des conditions 


#### Commande

fonction : 
Encapsuler une action dans un objet,
ce qui permet de les stocker, les ordonner et de gérer
des actions impossibles subtilement.

utiliser lorsque : 
on veut stocker,  ordonner, rejouer et annuler 
des actions. 
Une action peut souvent être vue comme un appel de méthodes.

cela se fait de la manière suivante :

Une classe (abstraite )/interface Commande
défini les différentes opération possibles d'une commande.

Une classe Receveur,
telle que les commandes puissent agir sur ses objets. 
Généralement ceux qui contiennent la logique métier.

Une classe commandeconcrète implémente différentes commandes.
Généralement elles ne contiennent pas la logique 
du travail mais sait simplement qui appeler et avec quoi 
pour que le travail soit fait.

Une classe ou autre Invoqueur
capable de générer/ de demander à générer des commandes
pour effectuer des actions. Peut ne jamais connaître
ni l'implémentation (voire l'abstraction) de commande;
ni de celui qui va recevoir la commande.

conséquence subtile :
- découple l'objet/classe émettrice de la commande du destinataire.
- transforme potentiellement des fonctions 
(des citoyens de seconde zone en langages OO) en objets,
les rendant des citoyens de première zone.
- facilité à ajouter de nouvelles commandes

astuce d'implémentation : 
Possibilité Utiliser le motif usine abstraite pour 
relier différentes commandes à différents groupes d'objets;
où au contraire avoir des commandes universelles servant comme 
source de loi dans le projet.



Motifs reliés : 
Memento pour stocker un historique de commande
Décorateur pour ajouter dynamiquement des responsabilités aux commandes 

#### Interpréteur

fonction : littéralement un automate /
une grammaire abstraite, en accéléré,
pour résoudre des problèmes métiers présentant un langage simple.

utiliser lorsque : 
- un besoin métier possède des règles complexe et précises 
qui s'articulent d'une certaine façon 
- pour analyser des entrées d'utilisateurs 
(toute sorte d'entrées textuelles, intéractions avec UI, etc)

cela se fait de la manière suivante :

Une classe NoeudAbstrait regroupe 
toutes les opérations qu'il est possible de faire sur les différents noeuds.
De cette classe découlent deux classes filles.

NoeudTerminal
chaque symbole de la langue est terminal

NoeudNonTerminal
Agrège des NoeudsAbstrait qu'ils soient ou non terminaux.
Permet de diriger la structure des phrases du langage
(comment peuvent ou non se suivre les symboles) 

conséquences subtiles :
- Il est facile de créer initialement, d'étendre, d'utiliser et de modifier la grammaire.
- Ironiquement une grammaire complexe est difficile à maintenir
et nécessiterait sûrement un lexer-parser
astuce d'implémentation : 

motifs exploitables avec :
Composite, pour faire les différents noeuds 
Décorateur, pour ajouter des responsabilités à certains noeuds

#### Itérateur *

fonction : permettre d'accéder séquentiellement 
aux données d'un agrégat sans se soucier de la classe concrète de l'agrégat

Cela se fait de la manière suivante :
Une classe abstraite agrégat exhibe une méthode pour créer un itérateur
Une classe abstraite itérateur qui exhibe tout ou partie des méthodes 
d'agrégats suivantes : Premier élément,  élément suivant , élement courant, estàlafin
une implémentation concrète de la classe itérateur est lié fonctionnellement à l'agrégat de données sur lequel elle itère 

Utiliser lorsque :
cf. fonction

Conséquence subtile :
couplé au motif stratégie, 
on peut varier la méthode d'itération sans problème 
et sans changement côté client.

Itération interne et externe 

Un itérateur externe renvoit chaque élément itéré à l'utilisateur
qui peut directement effectuer des actions dessus, il est plus flexible à utiliser
pour le client.
Il est peut être plus dangereux car il exhibe directement les éléments de l'agrégat.

Un itérateur interne est équivalent à la fonction map, il applique à chaque élément
la fonction/ la suite d'instruction qui lui a été fourni en argument.
Il est plus facile à implémenter et potentiellement plus sûr car on peut limiter
les actions que le client effectue sur les éléments de l'agrégat.
 

Astuce d'Implémentation : 

Attention lors du parcours de l'agrégat à bien 
gérer la modification du contenu de l'agrégat 
notamment les accès concurrentiel. 

L'itérateur pourrait être un objet instancié 
plutôt qu'une interface rattachée à l'agrégat.

Peut être un lien avec composite,
qui permet la traversée
Peut être un lien avec stratégie / état
qui permettent de changer la méthode de parcours
/ le comportement de l'itérateur.

#### Médiateur 
Fonction : Réduire le couplage inter-objets en les faisant
tous se référer vers un responsable, le "médiateur" pour 
aiguiller leurs requêtes.

Cela se fait de la manière suivante:

Le médiateur exhibe une manière 
pour les "composants inférieurs"
de communiquer avec lui. 
Les "composant inférieurs" communiquent avec le médiateur,
et non pas entres eux.

A ne pas confondre avec Facade,
Facade ne fait que transmettre les messages
du client vers les bons composant et fait de la pré-configuration
Mediateur **est** la configuration.

à utiliser lorsque :

un jeu de composants communiquent 
entres eux de manière **définie** mais complexe
avec un résultat destructuré difficile à comprendre.

Lorsque la situation précédente amène à de nombreuses inter-dépendances,
qui rendent difficile la réutilisation d'un seul composant.
Une fois appliqué, ce motif permet de paramétrer 
la communication entre ces composant sans avoir à user de beaucoup d'héritage.

conséquence subtile :
le contrôle est centralisé,
c'est une qualité car le péramétrage est facilité
c'est un défaut car le système risque de devenir monolithique

Le couplage entre les composants est très réduit,
ils deviennent tous interchangeables

Les échanges entre les composants sont abstraits,
cela aide à séparer le comportement des objets,
de leur communication avec les autres.

astuce d'implémentation : 

utiliser le motif de l'Observateur pour faire communiquer 
entres eux les différents les composants inférieurs et le médiateur



#### Visiteur *

fonction : permettre à un jeu d'opérations de s'exécuter sur une architecture d'objets
aux classes concrètes (variées), sans avoir à polluer les dites classes avec ces méthodes.
l'ajout d'une opération au jeu d'opération est grandement facilité 

cela se fait de la manière suivante:

Une classe abstraite/interface visiteur qui offre des méthodes de visite, **une** par classe concrète. 

Des classes implementationVisiteurs qui découlent de visiteur et qui implémentent toutes les méthodes
de la classe abstraite/interface.

Dans chaque classe qui doit pouvoir se faire vistier une méthode "AccepterVisiteur" qui prend en paramètre un visiteur
étant donné que la classe connait sa classe concrète, elle sait quelle méthode de Visiteur appeler pour être bien visité. 

utiliser lorsque: 
- une opération doit être effectuée sur tous les éléments d'une structure d'objet
(par exemple toString en Java ou bien des logs à émettre)

- ne garder que l'aspect métier dans les structures 
et séparer l'administratif autre part

conséquence subtile :

Augmente "fortement" le couplage, 
visiteur doit potentiellement connaître chaque classe concrète ... que de travail !
Encore plus si l'implémentation varie souvent (même si on peut mitiger cela avec d'autre classes abstraites côté implémentation).

astuce d'implémentation : 