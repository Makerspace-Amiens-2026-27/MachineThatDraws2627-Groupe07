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
- Idées retenues pour notre machine :
  - un support de stylo avec des **rainures en haut et en bas** et une **butée** pour prendre, poser, accrocher et décrocher le stylo ;
  - des **aimants plus gros** pour que le support tienne mieux sur la tête ;
  - des **capteurs de remise à zéro** (fins de course), bien visibles sur la vidéo.

## Pourquoi

- Ce système simplifie beaucoup le changement d'outil : une seule accroche sur la tête et un support par couleur.
- Sur la vidéo, la machine est verticale et la gravité aide à poser les stylos. La nôtre est à plat, mais le guidage par rainures et la butée rendent la prise et la dépose plus stables et plus fiables.
- Chaque stylo a sa pointe à une position légèrement différente : sans mesure de la pointe, les couleurs ne tomberaient pas au même endroit.

## Reste à faire

- Dessiner en CAO un premier support de stylo (rainures, butée, logement des aimants).
- Choisir la taille des aimants.
- Réfléchir au détecteur de pointe et aux capteurs de remise à zéro.
