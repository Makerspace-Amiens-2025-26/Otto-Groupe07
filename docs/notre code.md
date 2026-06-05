---
layout: default
nav_order: 5
title: Conclusion et notre code 
---

## CONCLUSION
Ce projet nous a permis de mettre en pratique plusieurs compétences techniques dans les domaines de la mécanique, de l’électronique et de la programmation. La réalisation du robot Otto a nécessité la fabrication des pièces par impression 3D, l’assemblage des différents éléments mécaniques, le câblage des composants électroniques ainsi que le développement du programme permettant de contrôler les mouvements et les capteurs du robot.

Les différentes phases de tests ont permis de valider le bon fonctionnement du système et d’apporter les ajustements nécessaires afin d’améliorer la stabilité des déplacements et la fiabilité de la détection d’obstacles. Grâce à ces travaux, le robot est capable d’effectuer les mouvements programmés et d’interagir avec son environnement de manière autonome.

Ce robot a été conçu dans le cadre d’une compétition, ce qui a constitué une motivation supplémentaire tout au long du projet. Cette contrainte a nécessité une attention particulière à la qualité de l’assemblage, à la fiabilité du câblage et à l’optimisation de la programmation afin d’obtenir les meilleures performances possibles. Cette expérience a été enrichissante et formatrice, car elle nous a permis de développer nos compétences techniques tout en travaillant sur un projet concret répondant à un objectif précis.



# voici notre code en libre acces:

Voici un extrait de notre fonction pour faire avancer le robot :

```arduino
// Fonction pour la marche avant du robot Otto-MKS
void marcheAvant() {
  // Avancer la jambe gauche
  servoJambeGauche.write(120);
  delay(200);
  
  // Avancer la jambe droite
  servoJambeDroite.write(60);
  delay(200);
  
  // Remettre au centre
  servoJambeGauche.write(90);
  servoJambeDroite.write(90);
}
```