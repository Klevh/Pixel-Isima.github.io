---
layout: page
title: "Tutoriel d'installation de Debian"
date:   2017-01-17 12:00:00 +0200
categories: tutorial
summary: Enfin un tutoriel pour installer linux.
---

# Tutoriel d'installation de Debian

## Introduction

L'installation d'un système Linux peut paraître complexe à première vue. Cependant
Je vais essayer de vous faire passer un bon moment lors de l'installation  de votre
nouveau système.
Dans le cadre de ce tutoriel, je vais vous apprendre comment installer la distribution
Linux Debian en version 8 soit en DualBoot, soit en machine virtuelle.

Avant de commencer, il faut expliquer la différence entre un DualBoot et une
machine virtuelle :
* Une machine virtuelle est un OS qui est exécuté dans un logiciel comme VirtualBox
  ou encore VMWare. C'est-à-dire qu'il vous faut un ordinateur avec un OS déjà
  installé (Windows, Mac OS, une quelconque distribution Linux qui supporte un
  logiciel de virtualisation). Cet OS sera appelé hôte et la machine virtuelle
  qui y sera exécutée est appelée invité.
* Un DualBoot consiste en fait en l'installation d'un second OS directement sur
  une partition de votre ordinateur. Son exécution sera assurée directement par
  le hardware de la même manière que votre OS d'origine.

Chacune de ces solutions a ses avantages et ses inconvénients:
* La machine virtuelle a pour avantage de fournir un OS qui est isolé de votre
  système principal et qui vous permet de bidouiller à souhait sans craindre de
  porter atteinte à vos précieuses données écrites sur le disque dur. Par ailleurs,
  il est très facile de cloner une machine virtuelle (VM) et ainsi de pouvoir
  conserver une copie fonctionnelle à re-cloner dès que votre VM de travail est
  compromise par une manipulation fâcheuse. Néanmoins, son
  exécution sera plus lente. Et oui, vous exécutez dans ce cas un OS qui lui
  même exécute un autre OS ...
* Le DualBoot, quant à lui, fournit un système d'exploitation en accès direct au
  démarrage. Celui-ci sera rapide et performant comme s'il était seul sur
  votre ordinateur. L'inconvénient de cette solution réside dans le fait que
  vous allez travailler directement avec le(s) disque(s) qui contien(nen)t vos
  précieuses données. Vous pouvez donc très facilement supprimer des données de
  manière involontaire ou encore compromettre votre second OS. Il faut toujours
  effectuer les manipulations dangereuses (ex : 'sudo rm') avec précaution.

## Préparation

### Préparation globale

Il y a une seule étape préparatoire commune aux deux installations. Il s'agit de
la récupération d'une image ISO d'installation de Debian. Téléchargez là en
suivant ce lien :

[Télécharger Debian 8 :D](https://www.debian.org/distrib/)

### La préparation pour le DualBoot

En effet, la création d'un DualBoot nécessite une certaine préparation.

#### Une partition

Je vous suggère de créer une partition sur le disque où vous souhaitez installer
votre nouveau système avant de démarrer l'installation. Pour la taille, le choix
est important. Il faut savoir que le fonctionnement de Debian requiert trois
partitions :
* une partition principale où toutes vos données sont installées. Je vous
  conseille d'allouer au moins 20Go à cette partition, mais selon moi, c'est un
  minimum syndical. Le volume à allouer à cette partition dépendra de votre usage. Personnellement,
  je recommande au moins 50Go.
* une partition EFI qui servira au démarrage de votre système (~0.5Go)
* une partition de swap. Le volume de cette partition doit être égal à votre
  quantité de RAM.

La somme des trois partitions va vous donner le volume à allouer à votre
future partition Debian.

#### Préparation BIOS

Il est possible que votre BIOS ait activé certaines options nuisibles à un DualBoot.
Si tel est le cas il faudra les désactiver. Il s'agit, entre autres, de l'option
'Fastboot'.

#### Préparation d'une clé bootable

TODO

### La préparation pour la VM

Dans le cas d'une VM, la préparation est plus simple. Vous n'aurez rien à faire
ni au niveau du disque dur ni au niveau du BIOS. Dans le cadre de ce tutoriel, je
vais vous présenter l'installation d'une VM avec le logiciel VirtualBox.
Vous pouvez le télécharger à partir du lien suivant :

[VirtualBox Download Page](https://www.virtualbox.org/wiki/Downloads)

#### Paramétrage

Lors du lancement de VirtualBox, vous allez vous retrouver face à la page
suivante :

![]({{ site.url }}/assets/tutoDualBoot_ressources/VirtualBox/VBox_init.png)

La première étape est de créer une nouvelle machine virtuelle dans laquelle
installer le nouvel OS. Vous allez donc commencer par cliquer sur "Nouvelle"
(l'icône bleue pour les perchés).

Sur la fenêtre suivante, il vous est demandé de préciser le nom, le type et la
version de l'OS que vous souhaitez installer dans votre VM. Pour le nom, vous
pouvez choisir ce que vous voulez. Je vous conseille néanmoins de choisir un nom
qui a du sens par rapport à ce que vous souhaitez faire de cette VM. En effet,
lorsque vous commencez à avoir 5-6 VM, il est intéressant de savoir rapidement
à quoi chacune d’entre elles sert plutôt que de les démarrer une à une pour savoir laquelle
vous cherchez.
Pour le type, il faudra choisir "Linux" dans le cadre de ce tutoriel :

![]({{ site.url }}/assets/tutoDualBoot_ressources/VirtualBox/Choose_your_dist_1.png)

Ensuite, il vous fait choisir une version d'OS. Nous installons Debian 8, je vous
conseille donc de choisir "Debian (64)".
![]({{ site.url }}/assets/tutoDualBoot_ressources/VirtualBox/Choose_your_dist_2.png)

Une fois ces champs remplis, vous devriez vous retrouver dans la situation suivante :
![]({{ site.url }}/assets/tutoDualBoot_ressources/VirtualBox/Choose_your_dist_3.png)

Cliquez alors sur "Suivant".

À l'étape suivante, on vous demande de choisir le volume de RAM qui sera
accessible par votre VM. Il est important d'allouer suffisamment de RAM à votre
VM pour pouvoir faire ce que vous souhaitez sans pour autant "étouffer" l'hôte.
Pour répondre à ces critères, il est préférable de rester dans la zone verte. Je
vous recommande un minimum de 2Go de RAM pour être tranquille, mais cela va
dépendre de votre matériel disponible.

![]({{ site.url }}/assets/tutoDualBoot_ressources/VirtualBox/Choose_your_ram.png)

Après avoir choisi ce paramétrage, vous pouvez passer à l'étape suivante. On
vous y demande si vous voulez créer un disque dur virtuel. Vous allez donc choisir la
deuxième option : "Créer un disque dur virtuel maintenant" :

![]({{ site.url }}/assets/tutoDualBoot_ressources/VirtualBox/Create_a_VDisk.png)

Puis cliquez sur "Créer".
Pour le type de disque dur virtuel, choisissez VDI:

![]({{ site.url }}/assets/tutoDualBoot_ressources/VirtualBox/Choose_your_VDisk.png)

Puis passez à l'étape suivante.

Ici, on vous demande de choisir le type d'allocation mémoire. Personnellement,
je préfère l'allocation dynamique de mémoire qui évite que la mémoire allouée à
la VM soit directement rendue inaccessible. Néanmoins, c’est à vous de choisir ce que
vous préférez :

![]({{ site.url }}/assets/tutoDualBoot_ressources/VirtualBox/Choose_allocation_type.png)

Ensuite, il vous est demandé de sélectionner le volume de disque à allouer à
votre VM. Dans le cadre d'une allocation de taille fixe, il faudra évidemment que
le volume choisi soit disponible sur le disque dur où sera stocké le disque virtuel. Au niveau de la valeur, le minimum pour travailler sur une VM
Debian est d'environ 8Go, mais je vous recommande de prendre au moins 20Go,
histoire d'être large. Une fois cette valeur choisie, cliquez sur "Créer". Vous
reviendrez à l'écran d'accueil de VirtualBox où vous verrez apparaître le nom de
votre nouvelle VM :

![]({{ site.url }}/assets/tutoDualBoot_ressources/VirtualBox/Configuration_ended.png)


#### Selection de l'ISO

À ce stade, il ne vous reste plus qu'une étape à passer avant de lancer
l'installation de la VM. Sélectionnez votre VM dans la liste et cliquez sur
"Démarrer".
VirtualBox vous demandera alors de choisir une image ISO d'installation.
Choisissez celle que vous avez téléchargée:

![]({{ site.url }}/assets/tutoDualBoot_ressources/VirtualBox/First_VM_Start.png)

L’étape préparatoire est achevée.

## Installation proprement dite

L'installation en elle-même est commune au DualBoot et à la VM. Il y aura juste
une petite différence au moment de choisir le disque d'installation, mais cette
étape va venir plus tard.

Pour l'heure au démarrage on accède à la page suivante :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/start_install_1.png)

Choisissez "Advanced Options". Puis sur la page suivante, choisissez "Graphical
expert install" :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/Start_install_2.png)

C'est ici que commence l'installation. On arrive sur le menu principal de
l'installateur. On va commencer par la sélection du langage :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/001_main_menu.png)

Cliquez sur "Continuer". Sur la fenêtre suivante, choisissez une langue :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/002.png)

Ensuite, choisissez votre position géographique:

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/003_situation_geographique.png)

Puis cliquez sur l'encodage clavier que vous souhaitez ("fr_FR.UTF-8")

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/004.png)

Puis cliquez directement sur "Continuer" à la fenêtre suivante, car le choix
présélectionné correspond à ce que l'on souhaite.

Ensuite, on revient au menu principal sur lequel on passe directement à la
configuration du clavier (je suppose que vous ne nécessitez pas de synthèse
vocale).

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/005.png)

Choisissez la langue associée à la disposition du clavier que vous avez :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/006.png)

Ensuite nous allons passer au montage de la partition d'installation :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/007.png)

Passez directement à l'étape suivante :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/008.png)

Puis continuez jusqu'à revenir au menu principal. Nous allons passer au
chargement des composants d'installation :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/009.png)

Sur cette nouvelle fenêtre, il va falloir choisir les composants suivants :
* cfdisk-udeb
* choose-mirror
* crypto-dm-modules-3.16.0-4-amd64-di
* driver-injection-disk-detect
* fuse-modules-3.16.0-4-amd64-di
* loa-media
* lowmem
* mbr-udeb
* multipath-modules-3.16.0-4-amd64-di
* nbd-modules-3.16.0-4-amd64-di
* ntfs-modules-3.16.0-4-amd64-di
* parted-udeb
* rescue-mode
* squashfs-modules-3.16.0-4-amd64-di
* udf-modules-3.16.0-4-amd64-di
* virtio-modules-3.16.0-4-amd64-di

et passer à l'étape suivante :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/010.png)

Passons au chargement des pilotes :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/011.png)

Sur la page suivante, choisissez "Oui" :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/012.png)

Puis continuez, quel que soit le résultat.

Nous allons passer à la détection du matériel réseau :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/013.png)

Puis nous allons paramétrer la connexion réseau :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/014.png)

Choisissez la configuration automatique du réseau (choisissez oui). Puis
continuez jusqu'à atteindre la fenêtre suivante :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/015.png)

Nommez le système à votre guise. Puis continuez jusqu'à revenir au menu
principal. Nous allons ensuite choisir le miroir de l'archive Debian :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/016.png)

Choisissez le protocole HTTP, puis le pays (choisissez de préférence le pays
dans lequel vous êtes pour avoir une connexion plus rapide !) et enfin le
miroir (le premier est souvent le meilleur, mais libre à vous d'en choisir un
autre). Ensuite, sauf si votre connexion à internet se fait via un proxy, vous
pouvez cliquer directement sur "Continuer" pour revenir sur le menu principal.

Nous allons poursuivre avec la création du premier utilisateur :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/017.png)

À cet instant il faut vous poser une question : voulez-vous utiliser la
connexion de l'utilisateur root ? Si vous ne savez pas ce qu'est l'utilisateur
root alors je vous conseille de choisir "Non". Je vous conseille également d'activer
les mots de passe cachés :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/018.png)

Il va falloir ensuite donner votre nom complet :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/019.png)

puis choisir un login utilisateur :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/020.png)

et enfin il va falloir entrer un mot de passe :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/021.png)

Lancez la libération de mémoire, puis passez à la configuration de l'horloge :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/022.png)

Confirmez l'utilisation de NTP pour régler l'horloge. Et continuez jusqu'au
menu principal.

Nous allons passer à la détection des disques durs :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/023.png)

Une fois cette étape achevée, passons au partitionnement des disques :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/024.png)

Nous allons avoir une différence entre VM et DualBoot pour cette étape :

##### VM

Pour une VM c'est assez simple. En effet dans la mesure où la VM est installée
sur un disque dur virtuel, vous n'aurez pas besoin de faire vous même le
partitionnement et vous contenter d'utiliser le partitionnement assisté sur
disque entier:

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/025.png)

puis continuer jusqu'à cette fenêtre où vous choisirez "Tout dans une seule
partition" :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/026.png)

Vous pourrez ensuite terminer le partitionnement :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/027.png)

C'est tout ce qu'il y a à faire.

##### DualBoot

Pour un DualBoot c'est un peu plus compliqué. On va commencer par choisir un
partitionnement manuel :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/028.png)

Ensuite, il va falloir choisir la partition que vous avez créée lors de la phase
de préparation :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/029.png)

puis continuer en choisissant "Créer une nouvelle partition" :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/030.png)

Nous avons trois partitions à créer si vous vous souvenez bien, une partition de
boot, une partition de swap et une partition de données.

###### EFI boot

pour la partition de boot vous allez lui allouer 0.5 Gb :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/031.png)

Placez-la au début :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/032.png)

Cliquer sur "Utiliser comme" puis sur "Continuer" pour choisir le type de
partition :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/033.png)

Il va falloir choisir "Zone réservée pour le secteur d'amorçage BIOS" :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/034.png)

Puis terminez le paramétrage de cette partition :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/035.png)

###### Swap

Cliquez ensuite sur le plus gros "Espace libre" de la partition que vous avez
réservé pour cette installation. Nous allons y créer la partition de Swap :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/036.png)

Choisissez à nouveau "Créer une nouvelle partition", puis allouez-lui autant de
mémoire que vous avez de RAM:

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/037.png)

Placez-la, elle aussi, au début, et sélectionner encore une fois "Utiliser comme",
pour choisir le type de partition "espace d'échange ("swap")" :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/038.png)

Puis terminez le paramétrage de cette partition.

###### Partition de données

Sélectionnez à nouveau le plus gros espace disponible de votre partition
réservée :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/039.png)

Puis créez une nouvelle partition et allouez-lui le reste de mémoire
disponible :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/040.png)

Laissez les paramètres tels qu'ils sont et terminez le paramétrage de cette
partition :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/041.png)

Terminer le partitionnement :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/042.png)

et validez l'application des changements.

Une fois de retour au menu principal, nous allons passer à l'installation du
système de base :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/043.png)

Cette étape peut prendre quelques minutes.

Il va vous être demandé de choisir le noyau Linux à installer. Choisissez
"linux-image-amd64" (cette valeur pointera toujours sur la dernière version du
noyau disponible).

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/044.png)

Pour l'image système, vous avez le choix entre image générique et image ciblée. Je
vous laisse faire votre choix.

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/045.png)

#### APT

Nous allons maintenant configurer le gestionnaire de paquet :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/046.png)

Choisissez non pour la fenêtre suivante :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/047.png)

Activez l'utilisation d'un miroir réseau :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/048.png)

Choisissez "HTTP", puis le pays dans lequel vous êtes la majorité du temps (pour
avoir une connexion plus rapide vers le miroir lors du téléchargement ou de la
mise à jour d'un paquet), et enfin choisissez le miroir (le premier est souvent
le meilleur). Et passez l'étape suivante si vous n'avez pas de proxy.

On va par la suite vous demander si vous souhaitez autoriser l'installation de
logiciels non libres. Ce choix dépend de vous. Personnellement je choisis
toujours oui :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/049.png)

Les services à utiliser sont les suivants :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/050.png)

L'étape suivante est le choix des logiciels à installer, parmi lesquelles,
l'interface graphique que vous utiliserez.

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/051.png)

Cette étape est assez longue en général, suivant la qualité de votre connexion
internet. L'installateur vous demandera si vous souhaitez envoyer des
informations sur vos statistiques d'utilisation des paquets. À vous de voir ce que vous
voulez partager ou non.

Ensuite va venir un point important, le choix d'une interface graphique.
Certains utilisateurs n'en voudront pas, auquel cas, il suffira de ne pas en
choisir. Pour les autres voici les choix disponibles :
* GNOME : ma préférée
* XFCE :  une interface plutôt moche, mais légère (recommandée pour les VM ayant
  besoin de limiter la consommation de RAM).
* KDE
* Cinnamon : une interface ressemblant (de loin) à celle de Windows XP.
* MATE
* LXDE


Ensuite, il y a d'autres éléments à choisir. Il vous est offert d'installer un
serveur web, un serveur d'impression, un serveur SSH, les utilitaires usuels
du système. Si vous ne savez pas ce que sont ces autres éléments, je vous
recommande d'installer le serveur d'impression, le serveur SSH et les
utilitaires, l'interface graphique étant laissée à votre appréciation :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/052.png)

La suite peut être plus ou moins longue suivant les éléments que vous avez
choisi et encore une fois votre connexion internet (ne soyez pas surpris si cette étape
prend plus de 30min).

Une fois cette étape achevée, on revient au menu principal d'où l'on va lancer
l'écriture du programme de démarrage (GRUB) sur le disque dur ou le disque
virtuel :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/053.png)

Le programme va vous demander si vous souhaitez installer GRUB sur le secteur
d'amorçage, c'est-à-dire le point du disque dur qui est lu en premier au
démarrage de l'ordinateur. Choisissez "oui" :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/054.png)

Pour ceux qui procèdent à l'installation d'un DualBoot ne vous inquiétez pas,
GRUB vous proposera, à chaque démarrage de l'ordinateur, sur quel OS vous
souhaitez démarrer avec Debian en temps que valeur par défaut.

Choisissez d'installer GRUB sur le disque dur où votre OS est installé :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/055.png)

Puis forcez l'installation sur le chemin des supports amovibles EFI :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/056.png)

Vous pouvez maintenant terminer l'installation :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/057.png)

Validez l'utilisation de l'horloge UTC :

![]({{ site.url }}/assets/tutoDualBoot_ressources/InstallateurDebian/058.png)

Après ce point, votre ordinateur ou votre VM va redémarrer.

## Post installation
Cette étape ne concerne que les VM, les DualBoot devraient être opérationnelles.
En effet au redémarrage de votre VM, il est possible que vous vous retrouviez
avec une mauvaise résolution, c'est-à-dire une résolution de VM très inférieure
à celle de votre écran. Pour régler cela, il suffit de lancer un terminal et d'y
taper la commande suivante pour installer les additions clients de VirtualBox :

```bash
sudo apt-get install virtualbox-guest-*
```

![]({{ site.url }}/assets/tutoDualBoot_ressources/TheVM/001.png)

Pour terminer cette étape, il vous suffira de redémarrer et votre VM sera
pleinement opérationnelle.
