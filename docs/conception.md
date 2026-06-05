---
layout: default
nav_order: 5
title: Conception et prototypage
---

## Matériel et composants utilisés

| Composants | Quantité | Fonction |
| :--- | :--- | :--- |
| Carte électronique OTTO-MKS | 1 | Contrôle du robot |
| Servomoteurs 9g | 4 | Mouvements |
| Capteur HC-SR04 | 1 | Détection des obstacles |
| Batterie 9V | 1 | Alimentation |
| Câble USB-C | 1 | Programmation |

Le robot utilise plusieurs composants électroniques et mécaniques nécessaire à son fonctionnement.

### Préparation des matériaux

**La carte électronique Otto-MKS**  
C'est elle qui reçoit le programme écrit et qui commande tous les composants du robot. Elle assure le contrôle du robot. Elle contient un microcontrôleur ESP32-C3 qui exécute, gère l’alimentation, pilote les servomoteurs, traite les informations des capteurs et permet la communication Wi-Fi/Bluetooth.

**Les servomoteurs**  
Les servomoteurs reçoivent des ordres de la carte électronique et se positionnent à l'angle demandé. C'est grâce à eux qu'Otto peut exécuter les mouvements programmés dans son code. Ainsi donc, les servomoteurs sont les actionneurs du robot Otto. Ils convertissent les signaux électriques envoyés par le microcontrôleur en mouvements mécaniques précis des jambes et des pieds, permettant au robot de marcher, tourner et effectuer diverses animations.

**Le capteur HC-SR04**  
Il permet au robot de mesurer la distance entre lui et un objet situé devant lui. En effet, grâce au HC-SR04, le robot peut :
- Détecter un obstacle devant lui. 
- S'arrêter avant de le percuter. 
- Changer de direction pour l'éviter. 
- Réagir à la présence d'objets ou de personnes.   

Le capteur ultrasonique HC-SR04 est un capteur de distance. Il utilise des ultrasons pour détecter les obstacles et mesurer leur éloignement. Les informations recueillies sont transmises au microcontrôleur, qui adapte alors les mouvements du robot Otto.

**La batterie 9v**  
La batterie 9 V sert à alimenter le robot Otto en énergie électrique. Elle est la source d'énergie du robot Otto. Elle fournit la tension nécessaire au fonctionnement de la carte électronique, des servomoteurs et des capteurs, permettant ainsi au robot de fonctionner de manière autonome.

**Le câble USB-C**  
Le câble USB-C relie l'ordinateur à la carte électronique. Grâce à cette connexion, on peut :
- Téléverser le code du robot ; 
- Modifier les programmes ; 
- Tester le fonctionnement des capteurs et des servomoteurs ; 
- Alimenter la carte sans utiliser la batterie.

Il assure le transfert des programmes, la communication des données et l'alimentation temporaire du robot lors des phases de programmation et de test.

## Conception et Assemblage des pièces du robot

### Impression 3D des pièces
La première étape du projet a consisté à fabriquer les différentes pièces constituant la structure du robot Otto grâce à l’impression 3D. Les fichiers de modélisation des composants (tête, corps, jambe et pieds) ont été préparés puis envoyés vers une imprimante 3D. Cette technique de fabrication additive permet de produire des pièces légères, précises et adaptées aux dimensions des composants électroniques. 

Après l’impression, les pièces ont été contrôlées visuellement afin de vérifier l’absence de défauts de fabrication tels que des déformations ou des irrégularités de surface. Certaines pièces ont nécessité ébavurage pour faciliter leur assemblage.

### Assemblage des pièces
Une fois les pièces imprimées, l’assemblage mécanique du robot a été réalisé. Cette étape consiste à fixer les différents éléments de la structure afin de former le châssis complet du robot.

Les servomoteurs ont ensuite été installés dans les emplacements prévus au niveau des hanches et des jambes. Leur positionnement est essentiel car ils assurent les mouvements du robot. Les servomoteurs sont solidement fixés afin d’éviter tout jeu mécanique susceptible d’altérer la précision des déplacements.

Une fois les servomoteurs installés, les jambes et les pieds sont emboîtés sur les axes de sortie des moteurs. Des vérifications ont été effectuées pour garantir la bonne mobilité des articulations et le bon alignement des différents éléments mécaniques.

### Câblage électronique
La troisième étape a consisté à réaliser le câblage électronique du robot. Les différents composants électroniques ont été connectés à la carte électronique Otto-MKS, qui constitue l’unité de commande du système.

Les servomoteurs ont été raccordés aux sorties dédiées de la carte afin de recevoir les signaux de commande nécessaire à leur fonctionnement. Le capteur ultrasonique HC-SR04 a également été connecté pour permettre la détection d’obstacles et la mesure des distances.

L’alimentation électrique du système a été assurée par une batterie 9V, tandis qu’un câble USB-C a été utilisé pour programmer la carte et effectuer les tests de fonctionnement. Une attention particulière a été portée au respect des polarités et à la qualité des connexions afin de garantir la fiabilité du montage et d’éviter tout risque de dysfonctionnement.

Une fois le câblage terminé, plusieurs vérifications ont été réalisées pour contrôler la continuité électrique des connexions et s’assurer du bon fonctionnement de l’ensemble des composants avant la phase de programmation.

## Programmation du robot 

### Programmation avec Arduino IDE
Après l’assemblage mécanique et le câblage électronique, la programmation du robot a été réalisée à l’aide du logiciel Arduino IDE. Cet environnement de développement permet d’écrire, de compiler et de transférer le programme vers la carte Otto-MKS à l’aide d’un câble USB-C.

L’objectif de cette étape était de développer les différentes fonctionnalités nécessaires au déplacement du robot et à son interaction avec l’environnement. Le programme a été écrit en langage C/C++, utilisé par les cartes compatibles Arduino.

Une fois le code terminé, celui-ci a été téléversé sur la carte électronique. Plusieurs phases des tests ont ensuite été réalisées afin de vérifier le bon fonctionnement des servomoteurs et du capteur ultrasonique.

### Fonctions programmées
- **Marche avant :** Une fonction de déplacement vers l'avant a été développée. Cette fonction commande les servomoteurs des jambes et des pieds selon une séquence précise permettant au robot d'avancer tout en conservant son équilibre.
- **Rotation à gauche :** Une fonction de rotation vers la gauche a été programmée afin de permettre au robot de changer de direction. Cette action est réalisée grâce à des mouvements coordonnés des servomoteurs des jambes et des pieds.
- **Rotation à droite :** De la même manière, une fonction de rotation vers la droite a été développée. Cette fonction permet au robot de s'orienter dans l'espace en fonction des besoins du programme ou des informations fournies par les capteurs.
- **Mouvement des hanches :** Les servomoteurs placés au niveau des hanches ont été pilotés afin de générer différents mouvements. Ces mouvements sont indispensables pour assurer les déplacements du robot, améliorer sa stabilité et lui permettre d'effectuer certaines animations.
- **Détection des obstacles :** Le capteur ultrasonique HC-SR04 a été intégré au programme afin de détecter les obstacles présents devant le robot. Lorsque la distance mesurée est inférieure à une valeur prédéfinie, le robot peut s'arrêter ou modifier sa direction afin d'éviter une collision.