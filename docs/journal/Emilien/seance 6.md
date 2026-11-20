---
layout: default
title: "2026-11-20 : traceur mural avec contrepoids et barillet"
parent: Emilien
grand_parent: Journal de bord
---

# 2026-11-20 : traceur mural avec contrepoids et barillet

**Séance :** planifiée · **Durée :** 3 h

## Ce que l'équipe a fait pendant mon absence

### Séance du 06/11 (planifiée) : changement de machine

- Victor a proposé une nouvelle direction : un **traceur vertical** (« vertical plotter » ou « wall draw ») qui dessine sur un mur, en s'inspirant de la machine **Scribit** et de plusieurs vidéos. Toute l'équipe a validé : **on abandonne le CoreXY**.
- Mathéo et Romain ont étudié l'existant (Scribit, projets « wall draw », traceur polaire) et comparé cette machine au CoreXY par rapport à notre cahier des charges.
- Raisons du choix : aucune machine de ce type n'a été faite au MakerSpace depuis environ 5 ans (d'après Adrien Bracq), elle est plus simple à réaliser et s'adapte facilement au support (mur, tableau blanc).
- Mathéo a étudié la communication entre l'ordinateur, la carte pilote et la tête de dessin : la tête serait pilotée **sans fil** par un **ESP32 en ESP-NOW**, alimenté par une **batterie** qui sert aussi de **contrepoids**.
- Timothé a terminé ses travaux sur le CoreXY : recomptage des poulies (6 poulies folles et 2 poulies moteur) et test du support moteur imprimé (trous du haut mal alignés, modèle corrigé).

### Séance de gestion de projet du 13/11 : découpage fonctionnel

- Cours sur le découpage d'un système : fonction ou solution, « choisir, c'est renoncer », interfaces entre sous-systèmes, diagramme FAST.
- Au tableau, l'équipe a listé les fonctions de la machine et une première solution pour chacune :
  - fixer le stylo : clipsage + alésage, avec un mécanisme à servomoteur ;
  - allumer : bouton ;
  - préparer le dessin : mini logiciel (slicer) sur PC ;
  - communiquer : ESP32 en ESP-NOW ;
  - initialiser le point 0 : à la main par l'utilisateur, guidé par des marquages ;
  - se déplacer : moteurs pas à pas + courroies ;
  - changer de couleur : **barillet ou stylo 4 couleurs ?** (pas encore tranché) ;
  - terminer le dessin : retour sur l'interface et tête rangée pour ne pas gêner la vue du dessin.

![Tableau : fonctions de la machine et solutions envisagées]({{ '/assets/images/timothe-2026-11-13-tableau-decoupage-fonctionnel.jpg' | relative_url }})

## Fait

- Mise à jour avec l'équipe sur le changement de machine.
- Étude du fonctionnement du traceur mural et de la place du changement de couleur (ma partie) sur cette nouvelle machine.

### Principe de la machine

```
      M1 (o)--------------- D ---------------(o) M2
          |  \                             /  |
          |   \  L1                   L2  /   |
         [#]   \                         /   [#]   <- contrepoids
                \                       /
                 \                     /
                  \                   /
                +-----------------------+
                |         TÊTE          |  <- barillet + stylos, servo,
                |          \/           |     ESP32 + batterie
                +-----------------------+
```

- **2 moteurs pas à pas** sont fixés en haut du mur (ou du tableau), écartés d'une distance **D**. Chacun porte une poulie dentée.
- Une **courroie** passe sur chaque poulie. Un bout est accroché à la **tête** (la partie mobile qui porte les stylos), l'autre bout pend avec un **contrepoids**.
- La tête est suspendue entre les deux courroies, qui forment un V. Son poids la tire vers le bas, donc les courroies restent toujours tendues.
- Quand un moteur enroule ou déroule sa courroie, la longueur L1 ou L2 change et la tête se déplace. En jouant sur les deux longueurs, on peut placer la tête n'importe où sur le mur.
- Calcul de position (origine au moteur 1, x vers la droite, y vers le bas) :
  - `L1 = √(x² + y²)`
  - `L2 = √((D − x)² + y²)`
  - Le programme transforme chaque point du dessin (x, y) en deux longueurs, puis en nombre de pas pour chaque moteur. Une ligne droite est découpée en petits segments, car les deux moteurs doivent tourner à des vitesses différentes.

### Le rôle des contrepoids

- Ils gardent la courroie **tendue des deux côtés de la poulie** : les dents ne sautent pas et la courroie ne glisse pas.
- Ils **équilibrent une partie du poids de la tête** : le moteur a moins de couple à fournir, surtout pour la tenir immobile.
- La partie libre de la courroie pend bien droite au lieu de s'emmêler.
- Dans la tête, la **batterie et l'ESP32** servent de **lest** : une tête plus lourde tend mieux les courroies et bouge moins. Il faut garder son centre de gravité **bas et près du mur**, sinon elle bascule et le stylo ne touche plus.
- Il faut éviter de dessiner tout en haut et sur les côtés : les courroies y sont presque horizontales, la tension devient très forte et la précision chute. On dessine dans un rectangle au centre, sous les moteurs.

### Le barillet pour changer de couleur

- Le **barillet** est un cylindre monté sur la tête, qui tient plusieurs stylos rangés autour de son axe, comme le barillet d'un revolver.
- Un **servomoteur** (ou un petit moteur pas à pas pour faire un tour complet) fait tourner le barillet pour amener le stylo de la couleur voulue face au mur.
- Seul le stylo choisi touche le mur.
- Commande : l'ESP32 de la tête reçoit par ESP-NOW les ordres « couleur n° X » et « stylo levé / baissé », et pilote le servomoteur. Les moteurs du mur restent pilotés par la carte principale : **aucun câble ne pend jusqu'à la tête**.

### Discussion du projet avec Adrien Bracq

- On a commencé par se répartir les tâches par interface, à partir de la fonction principale **dessiner** :
  - **A** : déplacer ;
  - **B** : tenir le stylo et changer de couleur.
- Ensuite, deux solutions : soit les **moteurs dans chaque coin** du tableau, soit les **moteurs au milieu**, dans le même bloc que le barillet.
- On a fait un pour et contre de ces solutions :

| Solution | Pour | Contre |
|---|---|---|
| Moteurs dans les coins, filaires | Plus simple | Câblage |
| Moteurs dans les coins, avec des ESP32 qui font communiquer plusieurs modules | Faisable plus tard, stylé, pratique (pas de câblage gênant) | Plus complexe, poids |
| Un seul bloc, moteurs au milieu | Un seul bloc, pas de fils, plus d'équilibre | Poids (les moteurs supportent leur propre poids), place |

- Si le poids est trop important avec la dernière solution, on pourrait **incliner le tableau** pour régler ce problème.

## Pourquoi

- Il fallait comprendre la nouvelle machine avant de reprendre ma partie : le changement de couleur.
- Sur un mur, la tête est suspendue aux courroies. Aller chercher un module stylo dans un parking sur le côté (mon idée de la séance 4) serait difficile : la précision est faible sur les bords et la tête se balance. Avec le barillet, tous les stylos voyagent avec la tête.
- Les stylos tournent tous autour du même axe : après une rotation, la pointe revient presque au même endroit, ce qui facilite l'alignement des couleurs.
- Barillet ou stylo 4 couleurs (« choisir, c'est renoncer ») :
  - le **barillet** permet plus de couleurs et n'importe quel type de stylo ou de feutre, mais c'est un mécanisme de plus à concevoir et du poids en plus sur la tête ;
  - le **stylo 4 couleurs** est plus simple, mais limité à 4 couleurs, et il faut appuyer sur les bons boutons du stylo pour changer de mine.

## Reste à faire

- Calculer combien deux moteurs NEMA 17 peuvent porter en plus de leur propre poids, au point le plus critique.
- Trancher avec Mathéo entre le barillet et le stylo 4 couleurs, puis l'écrire pour ne plus revenir dessus.
- Dessiner le barillet dans Onshape : nombre de stylos, diamètre des stylos ou feutres, fixation du servomoteur.
- Choisir comment lever le stylo.
- Peser la tête complète (batterie, ESP32, servomoteur, barillet, stylos) pour dimensionner les contrepoids et vérifier le couple des moteurs.
- Définir avec Timothé les points d'accroche des courroies sur la tête et la fixation des moteurs sur le mur.
- Délimiter la zone de dessin utile en fonction de l'écart D entre les moteurs.
- Me renseigner sur l'ESP-NOW avec Mathéo.
