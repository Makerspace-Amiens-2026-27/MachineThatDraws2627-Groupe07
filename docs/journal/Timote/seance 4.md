---
layout: default
title: "2026-10-23 : support moteur et dimensions"
parent: Timote
grand_parent: Journal de bord
---

# 2026-10-23 : support moteur et dimensions

**Séance :** planifiée · **Durée :** 3 h

## Fait

- Point sur les prochaines étapes de la mécanique : finir l'assemblage Onshape, vérifier les courroies, faire l'inventaire des pièces, puis fabriquer et monter.
- Mesure de l'**entraxe des trous du plateau** dans Onshape (paramètre de la répétition linéaire) : **20 mm** dans les deux directions, avec 21 × 21 trous, soit une grille de **400 × 400 mm**.
- Recherches sur le moteur **17HE12-1204S** (standard NEMA 17) :
  - corps de 42 × 42 × 30 mm, arbre Ø 5 mm avec méplat (en D) ;
  - 4 trous de fixation M3 à **31 mm d'entraxe**, épaulement de centrage Ø 22 mm ;
  - cotes à vérifier au pied à coulisse sur le vrai moteur.
- Recherches sur les **vis CHC M3** : tête Ø 5,5 × 3 mm, donc un lamage d'environ Ø 6 à 6,5 mm sur 3,2 à 3,5 mm de profondeur.
- **Support moteur, premier jet** : modélisé en 3D (disponible sur Onshape) et imprimé, surtout pour vérifier que les vis rentrent bien.
- Suite du support : ajout des **trous pour visser le moteur** lui-même.
- Suite à un manque de communication dans l'équipe, j'ai dû **refaire le modèle 3D du support**. La nouvelle pièce est imprimée : le premier jet est **nickel, sans défaut**.
- Demande pour obtenir des **poulies de distribution** : c'est possible, il faut juste donner le nombre exact. J'en ai compté 8, mais Adrien Bracq m'a conseillé de revérifier, il y en a peut-être trop.

## Pourquoi

- Connaître l'entraxe du plateau permet de placer le cadre, les supports moteur et les poulies sur ses trous.
- Le plateau est carré (400 mm) alors qu'une feuille A4 fait 297 × 210 mm : la course du chariot doit couvrir la zone A4 (plus une marge), pas tout le plateau.
- Imprimer un premier jet permet de valider les tolérances avant d'imprimer la pièce finale. Côté support, on vise des trous de Ø 3,2 à 3,4 mm pour les vis, un trou central d'au moins Ø 22,5 mm pour l'épaulement du moteur, et environ 0,2 mm de jeu en impression 3D.
- Un CoreXY classique utilise en général 2 poulies dentées (sur les moteurs) et 6 à 8 poulies folles selon la conception : d'où l'intérêt de recompter sur notre assemblage.

## Reste à faire

- Recompter les poulies nécessaires sur l'assemblage Onshape avant de faire la demande.
- Monter le moteur sur le support imprimé pour valider la fixation.
- Finir l'assemblage Onshape et vérifier que le chariot couvre bien tout l'A4 sans collision.
- Tracer le chemin des courroies en esquisse pour confirmer la longueur (~1,40 à 1,50 m chacune).
- Définir avec Mathéo la fixation du stylo sur le chariot.
