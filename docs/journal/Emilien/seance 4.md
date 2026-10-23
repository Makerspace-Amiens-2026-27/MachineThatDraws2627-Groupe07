---
layout: default
title: "2026-10-23 : porte-stylo et changement de couleur"
parent: Emilien
grand_parent: Journal de bord
---

# 2026-10-23 : porte-stylo et changement de couleur

**Séance :** planifiée · **Durée :** 3 h

## Fait

- Discussion avec Mathéo sur le mécanisme qui tient le stylo et sur le changement de couleur automatique.
- Étude d'une vidéo de référence : un traceur qui change de stylo tout seul.
  - Chaque stylo est monté dans son propre support, rangé dans un emplacement sur le côté de la machine.
  - La tête vient chercher un support, l'accroche, dessine, puis le repose et prend le suivant.
  - Un détecteur de pointe mesure la position X et Y de la pointe de chaque stylo, puis la machine trace une mire d'alignement pour vérifier que les couleurs se superposent bien.
- Brainstorming au tableau sur l'architecture du changeur de stylo et de la machine :

![Schémas du changeur de stylo et de la machine au tableau]({{ '/assets/images/emilien-2026-10-23-tableau.jpg' | relative_url }})

- Le changeur de stylo est découpé en **4 blocs** :
  1. **Parking** : il range les modules stylo sur le côté de la machine, avec des rainures en haut et en bas et une butée pour poser et reprendre un module.
  2. **Module stylo** (un par couleur) : il tient le stylo, serré par une vis. Il porte 4 aimants à l'arrière et une encoche pour le verrou (« lock »).
  3. **Module verrou** : il est placé derrière le module stylo, avec 4 aimants pour l'aligner et un **servomoteur qui sert de verrou**.
  4. **Module guidage** : il est fixé sur le chariot, derrière le module verrou. Des **rails** permettent au module verrou de monter et descendre. Un **ressort imprimé en 3D en zigzag** le pousse vers le bas, et un **2e servomoteur** le remonte pour ne pas dessiner tout le temps.
- Autres schémas au tableau : 2 variantes de ressort (en spirale autour d'un axe, ou guidé dans un rail), la came du servomoteur qui soulève, le déplacement XY en **CoreXY** (2 moteurs fixes en haut du cadre, 2 courroies 1 et 2 qui se croisent) et le mouvement haut/bas du stylo sur le chariot.
- Recherche CAO : j'ai trouvé sur internet un fichier d'un changeur de stylo complet, que j'ai importé dans **Onshape**. Nous n'allons garder que le système de **« suspension »** (rails + ressort zigzag) et de **surélévation avec les servomoteurs**.

## Pourquoi

- Ce système simplifie beaucoup le changement d'outil : une seule accroche sur la tête et un module par couleur.
- Les aimants servent à aligner le module stylo. C'est le servomoteur « lock » qui le tient vraiment, pour qu'il ne se décroche pas pendant le dessin.
- Avec le ressort, le stylo appuie toujours avec la même force sur le papier. Le servomoteur n'a qu'à soulever l'ensemble pour lever le stylo, et il n'a pas besoin de forcer pour dessiner.
- Partir d'un fichier existant fait gagner du temps sur la partie suspension / surélévation. Le reste (module stylo, parking, verrou) sera adapté à notre machine.
- Chaque stylo a sa pointe à une position légèrement différente : sans mesure de la pointe, les couleurs ne tomberaient pas au même endroit.

## Reste à faire

- Adapter dans Onshape le système de suspension et de surélévation aux dimensions de notre chariot.
- Dessiner notre module stylo et le verrou (encoche, aimants, servomoteur).
- Imprimer un ressort zigzag et tester sa raideur.
- Réfléchir au détecteur de pointe et aux capteurs de remise à zéro.
