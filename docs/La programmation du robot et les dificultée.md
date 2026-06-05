---
layout: default
nav_order: 4
title: La programmation du robot et les dificultée
---

## La programmation du robot et les dificultée

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

## Résultats et difficultés rencontrées

### Résultats
À l'issue de la conception et de la programmation du robot, plusieurs objectifs ont été atteints :
- **Déplacement du robot :** le robot est capable d'effectuer des mouvements de marche en avant grâce à la coordination des servomoteurs qui actionnent ses membres. 
- **Rotation et changement de direction :** le programme permet au robot de tourner à droite ou à gauche afin de modifier sa trajectoire selon les besoins. 
- **Détection d'obstacles :** grâce à l'intégration d'un capteur de distance, le robot peut détecter la présence d'un obstacle devant lui et adapter son comportement pour éviter une collision. 
- **Fonctionnement autonome :** l'ensemble des composants électroniques et du programme permettent au robot d'exécuter automatiquement les tâches prévues sans intervention permanente de l'utilisateur. 

Ces résultats montrent que les principales fonctionnalités définies au début du projet ont été réalisées avec succès.

### Difficultés rencontrées
L'une des principales difficultés a concerné le réglage des servomoteurs. Chaque moteur devait être correctement calibré afin d'obtenir des mouvements précis et synchronisés. Un mauvais réglage provoquait des mouvements irréguliers ou empêchait certaines articulations de fonctionner correctement.

**Équilibre du robot**  
Le maintien de l'équilibre du robot a également été complexe. Lors des premiers essais, le robot avait tendance à basculer ou à perdre sa stabilité pendant la marche. Cette difficulté était liée à la répartition du poids, à la position des composants et à la synchronisation des mouvements.

**Difficultés de programmation**  
La programmation a demandé plusieurs phases de tests. Certaines erreurs dans le code empêchaient le bon fonctionnement des capteurs ou des moteurs. Il a fallu corriger les algorithmes de déplacement, ajuster les temps d'exécution et vérifier les connexions entre le matériel et le logiciel.

### Solutions apportées
Pour résoudre ces difficultés, plusieurs actions ont été mises en œuvre :
- Réalisation de nombreux essais afin de calibrer correctement les servomoteurs et obtenir des mouvements plus fluides. 
- Modification de la structure et de la répartition des composants pour améliorer la stabilité et l'équilibre du robot. 
- Ajustement progressif des angles de déplacement et des vitesses de rotation des moteurs. 
- Débogage du programme en identifiant les erreurs puis en corrigeant les parties du code responsables des dysfonctionnements. 
- Mise en place de tests successifs après chaque modification afin de vérifier l'efficacité des corrections apportées. 

Grâce à ces ajustements, les performances du robot se sont progressivement améliorées, permettant d'obtenir un fonctionnement plus fiable, plus stable et conforme aux objectifs du projet.