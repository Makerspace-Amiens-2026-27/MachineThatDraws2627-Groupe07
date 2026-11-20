---
layout: default
title: "2026-11-20 : séance 6"
parent: Victor
grand_parent: Journal de bord
---

# 2026-10-23 : Travail de reflexion en groupe dans l'optique d'identifier une piste à suivre afin de commencer le prototypage



**Séance :** planifiée · **Durée :** 3 h

## Fait

Nous avons pu discuter en début de séance avec Adrien Bracq de façon à pouvoir lui expliquer nos idées et choix techniques face à la question du prototype pour notre machine.
L'échange avec Adrien Bracq était riche, ce dernier nous a mené à une remise en question de nos choix, cela nous a remis sur la bonne direction en ce qui concerne notre angle d'attaque vis à vis de la problématique de créer une machine capable de dessiner sur un tableau blanc.

Après l'intervention de Monsieur Bracq, nous avons pesé le pour et le contre de différentes solutions techniques qui nous étaient venues à l'esprit.

Voici nos trois idées principales (concernant le déplacement et la constitution interne de notre robot).

- Idée 1 : Les moteurs  sont placés sur les côtés du bord supérieur du tableau. Les câbles partent des boitiers-moteurs. Le "Robot" ne possède donc aucun moteur à l'intérieur, seul le barillet de changement de feutre compose le robot.
 
- Idée 2 : Les moteurs sont aussi placés dans des boitiers sur le bord supérieur du tableau, cependant, aucun fil n'est présent, les câbles sont mis en mouvement à disance par communication de plusieurs ESP32, (Un par boitier moteur et un dans le robot).

- Idée 3: Les moteurs sont directement inclus dans le robot. Les câbles restent tendus depuis le haut du tableau, toute la partie moteur se fait depuis le robot.


Nous n'avons pas encore opté pour un choix final, étant dans la contrainte de soummettre un prototype fonctionnel, nous sommes donc parti (provisoirement) sur la troisième idée, la plus simple selon nous.

