# Projet ELEC - PCB

## Architecture

Cette section présente l'architecture d'un thermomètre autonome fonctionnant à
l'aide d'un panneau solaire. L'objectif est de mesurer la température d'un lieu
et d'afficher sur des afficheurs 7 segments tout en assurant une alimentation
énergétique durable à l'aide d'une batterie rechargeable.

### Composants principaux

Les composants que nous utiliserons sont les suivants :

| Référence | Composant | Quantité | Remarques |
| --------- | -------------- | -------------- | ---- |
| ATTINY85 | Microcontrôleur | 1 | Gestion des capteurs et de l'affichage |
| MCP9700AT-E/LT | Capteur de température | 1 | Mesure de la température |
| 157119S12801 | Afficheur 7 segments | 3 | Affiche numérique de la température |
| PET Solar panel | Mini panneau solaire | 1 | Recharge la batterie |
| CD4511 | Décodeur BCD vers 7 segments | 3 | Simplifie le pilottage de l'afficheur |
| | Batterie rechargeable | 1 | Alimentation autonome |
| 74HC595 | Registre à décalage | 2 | Sérialisation des données |

### Schéma fonctionnel

1. Le panneau solaire charge la batterie via un circuit de gestion de charge.
2. La batterie alimente le microcontrôleur et les afficheurs 7 segments.
3. Le microcontrôleur lit la température via le capteur et affiche les valeurs
sur les afficheurs 7 segments.

Le schéma fonctionnel est présent dans le document `documents/schema.pdf`.

Ce projet permettra de développer une solution autonome et durable pour la
mesure de la température. La conception d'une carte PCB optimisera l'intégration
des composants et la gestion énergétique.

## Fonction de transfert du capteur de température

La fonction de transfert du capteur de température est explicitée dans la partie
4 (*Applications information*) de la fiche de donnée du capteur de température
(`documents/thermal_sensor_datasheet.pdf`).

Cette dernière nous informe que

$$
V_{OUT} = T_C \times T_A + V_{0°C}
$$

avec $V_{OUT}$ la tension de sortie du capteur, $T_C$ le coefficient de
température, $T_A$ la température ambiante et $V_{0°C}$ la tension de sortie du
capteur à 0°C.

On a alors,

$$
\begin{align*}
    V_{OUT} &= T_C \times T_A + V_{0°C} \\
    V_{OUT} - V_{0°C} &= T_C \times T_A \\
    T_A &= \frac{V_OUT - V_{0°C}}{T_C}
\end{align*}
$$

avec $V_{0°C} = 500 V$ et $T_C = 10.0 V$.
