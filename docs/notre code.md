---
layout: default
nav_order: 7
title: Conclusion et notre code 
---

## CONCLUSION
Ce projet nous a permis de mettre en pratique plusieurs compétences techniques dans les domaines de la mécanique, de l’électronique et de la programmation. La réalisation du robot Otto a nécessité la fabrication des pièces par impression 3D, l’assemblage des différents éléments mécaniques, le câblage des composants électroniques ainsi que le développement du programme permettant de contrôler les mouvements et les capteurs du robot.

Les différentes phases de tests ont permis de valider le bon fonctionnement du système et d’apporter les ajustements nécessaires afin d’améliorer la stabilité des déplacements et la fiabilité de la détection d’obstacles. Grâce à ces travaux, le robot est capable d’effectuer les mouvements programmés et d’interagir avec son environnement de manière autonome.

Ce robot a été conçu dans le cadre d’une compétition, ce qui a constitué une motivation supplémentaire tout au long du projet. Cette contrainte a nécessité une attention particulière à la qualité de l’assemblage, à la fiabilité du câblage et à l’optimisation de la programmation afin d’obtenir les meilleures performances possibles. Cette expérience a été enrichissante et formatrice, car elle nous a permis de développer nos compétences techniques tout en travaillant sur un projet concret répondant à un objectif précis.



# voici notre code en libre acces:

Voici un extrait de notre fonction pour faire avancer le robot :

```arduino
#include <ESP32Servo.h>

//////////////////////////////////////////////
//        RemoteXY include library          //
//////////////////////////////////////////////

#define REMOTEXY_MODE__ESP32CORE_BLE

#include <BLEDevice.h>
#include <BLEServer.h>
#include <BLEUtils.h>
#include <BLE2902.h>

#include <RemoteXY.h>

// RemoteXY BLE configuration
#define REMOTEXY_BLUETOOTH_NAME "BiBot"

// RemoteXY GUI configuration
#pragma pack(push, 1)
uint8_t const PROGMEM RemoteXY_CONF_PROGMEM[] =
  { 255,5,0,0,0,53,0,19,0,0,0,103,97,117,99,104,101,47,100,114,
    111,105,116,101,0,31,1,106,200,1,1,3,0,1,7,15,24,24,0,2,
    31,0,5,59,89,38,38,0,2,26,31,5,4,87,39,39,0,2,26,31 };

struct {
  uint8_t button_01;
  int8_t joystick_01_x;
  int8_t joystick_01_y;
  int8_t joystick_02_x;
  int8_t joystick_02_y;
  uint8_t connect_flag;
} RemoteXY;
#pragma pack(pop)

/////////////////////////////////////////////
//           END RemoteXY include          //
/////////////////////////////////////////////

// Broches
const int BROCHE_HANCHE_GAUCHE = D7;
const int BROCHE_HANCHE_DROITE = D8;
const int BROCHE_PIED_GAUCHE   = D9;
const int BROCHE_PIED_DROIT    = D10;

// Servomoteurs
Servo hancheGauche;
Servo hancheDroite;
Servo piedGauche;
Servo piedDroit;

// Positions courantes : {HancheG, HancheD, PiedG, PiedD}
int posActuelle[4] = {90, 90, 90, 90};

// Deadzone joystick
const int SEUIL = 30;
const int SEUIL_MARCHE  = 40;  // forward / backward
const int SEUIL_VIRAGE  = 25;  // turning — easier to reach
  // Forward/backward take priority only if Y dominates over X

void setup() {
  RemoteXY_Init();
  Serial.begin(115200);

  ESP32PWM::allocateTimer(0);
  ESP32PWM::allocateTimer(1);
  ESP32PWM::allocateTimer(2);
  ESP32PWM::allocateTimer(3);

  hancheGauche.setPeriodHertz(50);
  hancheDroite.setPeriodHertz(50);
  piedGauche.setPeriodHertz(50);
  piedDroit.setPeriodHertz(50);

  hancheGauche.attach(BROCHE_HANCHE_GAUCHE, 500, 2400);
  hancheDroite.attach(BROCHE_HANCHE_DROITE, 500, 2400);
  piedGauche.attach(BROCHE_PIED_GAUCHE, 500, 2400);
  piedDroit.attach(BROCHE_PIED_DROIT, 500, 2400);

  bougerSimultanement(90, 90, 90, 90, 20, 15);
  delay(2000);
}

void loop() {
  RemoteXY_Handler();

  if (RemoteXY.connect_flag == 0) {
    stopperMouvement();
    return;
  }

  int x = RemoteXY.joystick_01_x;
  int y = RemoteXY.joystick_01_y;
  
  if (y > SEUIL_MARCHE && abs(y) > abs(x)) {
    marcherAvant();
  } else if (y < -SEUIL_MARCHE && abs(y) > abs(x)) {
    marcherArriere();
  } else if (x < -SEUIL_VIRAGE) {   // LEFT: x is negative
    tournerGauche();
  } else if (x > SEUIL_VIRAGE) {    // RIGHT: x is positive
    tournerDroite();
  } else {
    stopperMouvement();
  }
}

void bougerSimultanement(int cibleHG, int cibleHD, int ciblePG, int ciblePD, int etapes, int delaiEtape) {
  float depHG = posActuelle[0];
  float depHD = posActuelle[1];
  float depPG = posActuelle[2];
  float depPD = posActuelle[3];

  float pasHG = (cibleHG - depHG) / (float)etapes;
  float pasHD = (cibleHD - depHD) / (float)etapes;
  float pasPG = (ciblePG - depPG) / (float)etapes;
  float pasPD = (ciblePD - depPD) / (float)etapes;

  for (int i = 1; i <= etapes; i++) {
    hancheGauche.write(depHG + (pasHG * i));
    hancheDroite.write(depHD + (pasHD * i));
    piedGauche.write(depPG + (pasPG * i));
    piedDroit.write(depPD + (pasPD * i));
    delay(delaiEtape);
  }

  posActuelle[0] = cibleHG;
  posActuelle[1] = cibleHD;
  posActuelle[2] = ciblePG;
  posActuelle[3] = ciblePD;
}

void marcherAvant() {
  int etapes = 20, delai = 20;
  bougerSimultanement(posActuelle[0], posActuelle[1], 120, 120, etapes, delai);
  bougerSimultanement(60, 60, 120, 120, etapes, delai);
  bougerSimultanement(60, 60, 60, 60, etapes, delai);
  bougerSimultanement(120, 120, 60, 60, etapes, delai);
}

void marcherArriere() {
  int etapes = 20, delai = 20;
  
  // Étape 1 : On incline les pieds à 120 comme à l'avant
  bougerSimultanement(posActuelle[0], posActuelle[1], 120, 120, etapes, delai);
  
  // Étape 2 : INVERSION -> On envoie les hanches à 120 au lieu de 60
  bougerSimultanement(120, 120, 120, 120, etapes, delai);
  
  // Étape 3 : On bascule le poids sur les pieds à 60 comme à l'avant
  bougerSimultanement(120, 120, 60, 60, etapes, delai);
  
  // Étape 4 : INVERSION -> On envoie les hanches à 60 au lieu de 120
  bougerSimultanement(60, 60, 60, 60, etapes, delai);
}

void tournerGauche() {
  int etapes = 15, delai = 15;
  bougerSimultanement(posActuelle[0], posActuelle[1], 105, 105, etapes, delai);
  bougerSimultanement(75, 105, 105, 105, etapes, delai);
  bougerSimultanement(75, 105, 75, 75, etapes, delai);
  bougerSimultanement(105, 75, 75, 75, etapes, delai);
}

void tournerDroite() {
  int etapes = 15, delai = 15;
  bougerSimultanement(posActuelle[0], posActuelle[1], 75, 75, etapes, delai);
  bougerSimultanement(75, 105, 75, 75, etapes, delai);
  bougerSimultanement(75, 105, 105, 105, etapes, delai);
  bougerSimultanement(105, 75, 105, 105, etapes, delai);
}

void stopperMouvement() {
  if (posActuelle[0] != 90 || posActuelle[1] != 90 ||
      posActuelle[2] != 90 || posActuelle[3] != 90) {
    bougerSimultanement(90, 90, 90, 90, 20, 20);
  }
}
```
