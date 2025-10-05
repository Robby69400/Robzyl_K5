># [**Translate 🌐**](https://translate.google.com/translate?sl=auto&tl=en&u=https://github.com/Robby69400/Robzyl_K5/)
# Firmware Quansheng UV-K5 - Robzyl
## Le logiciel est en anglais, les versions disponibles correspondent aux pays cibles pour les bandes: France, Pologne, Roumanie, Turquie, Russie, Tchequie. Ces bandes peuvent se personaliser, voir le manuel.
### Many thanks to Zylka, Yves31 and Francois87.

<h2><a href="https://www.youtube.com/@robby_69400" rel="nofollow">🗲Youtube</a></h2>
<h2><a href="https://t.me/k5robby69">🗲Telegram </a></h2>

# **Manuel Robzyl V5.3 - Firmware Quansheng UV-K5**

## Introduction

Ce firmware, fork de NUNU de NTOIVOLA, est caractérisé par ses multiples fonctions de réception mettant en œuvre l’analyseur de spectre capable de traiter jusqu’à 160 canaux par seconde.

Les liens vers les différentes ressources sont accessibles en fin de document (GitHub, Youtube, Telegram, etc.).

## Avertissements et responsabilités

**Le domaine de la radio est réglementé, chacun est responsable de l’utilisation qu’il fait de sa radio.**

## Nouveautés V5.3
- Bandes : Ajout des versions KO TU et CZ (KO perso, Turquie et la République Tchèque). Le code "origine" la bande apparait à l'écran.
- Spectre : 
    * Simplification du nouveau squelch, on ne règle plus que le trigger up. 
    * Optimisation de l’auto-zoom. 
    * Il est permis de configurer l’affichage au dessus du graphique selon 5 formats 
      * rien
      * 1 ligne grande fréquence 
      * 1 ligne petite fréquence et ctcss ou DCS
      * 2 lignes: ajout mode et canal
      * 3 lignes: ajout dernière fréquence reçue.
    * Améliorations du SpectrumDelay : le timer s'exécute sur l’écran du spectre. Et tous les réglages restent actifs durant ce temps (step, modul., BL, …).
    * L’écran d’historique évolue de manière dynamique, balayable avec les touches ^/v. Touche M pour se positionner en écoute sur une fréquence listée.
    * L’écran de monitoring d’écoute (M) permet de régler plus de registres techniques pour des réglages avancés. Ces valeurs sont mémorisées à l'enregistrement (touche M pour passer en édition, ^/v pour régler).
    * Mode Fréquence : renommé FQ (au lieu de FR)
- Paramètres Spectre : Nouvelle entrée de menu DEFAUT PARAMS (presser 3 pour valider). Réinitialisation des paramètres en mémoire et registres. **A faire à chaque nouvelle version.**
- Mode MR/VFO : 
    * Dans le Menu M, certains pas du menu caché réapparaissent en visible par défaut.
    * Modification de l'accès aux menus cachés : presser uniquement SIDE KEY 1 au démarrage


## Nouveautés V5.2

- Passage en simple VFO (gain de place et simplification interface)
- Spectre : Nouvelle gestion du squelch, ajout nouvel écran sans histogramme, nouveaux menus PTT, FStart/Stop, Step, ListenBw et Modulation).
- Spectre : Historique des fréquences à repenser suite aux travaux sur le squelch.
- Nouveaux Roger Bips 😊

## Démarrage

- **Installation du firmware :**
    * Télécharger la dernière version sur le GitHub (lien en fin de doc).
    * Munissez-vous du câble de programmation USB compatible avec le poste.
    * Brancher le poste à l’ordinateur puis démarrer le K5 tout en appuyant sur le bouton PTT
    * Puis, led allumée fixe, transférer le firmware vers le K5 via le Flasher en ligne ou K5prog-win (lien en fin de doc).
    * Si vous vous apprêtez à remplacer le firmware d’usine, il est recommandé de sauvegarder préalablement vos configuration et calibration à l’aide de K5prog (voir par exemple la vidéo de F5SVP)
    * **A faire en premier à chaque nouvelle version du firmware :** Executer DEFAUT PARAMS dans le menu du spectre.


- **Prise en main rapide :**
    * Les menus cachés : les menus peu utilisés ont été cachés dans une optique de simplification. Pour afficher le menu complet, il suffit de démarrer le poste en pressant SIDE KEY 1
    * La programmation avec Chirp : le driver à utiliser pour dialoguer avec le poste sous Robzyl est à télécharger (lien en fin de doc). Attention de ne pas être en mode spectre pour pouvoir communiquer avec le PC.
    * Restauration du dernier état : suite à l’arrêt du K5, son redémarrage reprend dans le mode actif à son extinction en tenant compte de vos derniers paramètres de spectre sauvegardés.
    * Les principales fonctionnalités propres au firmware Robzyl sont décrites dans la suite de ce document. Pour les fonctions de base du K5, veuillez vous reporter à sa documentation.

## Les modes VFO et Mémoire

Ces modes sont accessibles alternativement par un appui long sur la touche 3. En haut de l'écran, 3 niveaux sont reportés : GL Glitch, RS RSSI et NO Noise. Puis en partie latérale drite, le niveau de l'audio.

### Mode VFO

<img width="512" height="320" alt="screenshot_2025-10-04_21-30-50-553Z" src="https://github.com/user-attachments/assets/0834c2ce-2328-4c7b-851f-890313e5dcc2" />

Le mode simple VFO permet de saisir librement une fréquence. Le menu touche M donne accès à tous les paramètres de step, modulation, etc.

### Mode Mémoire

<img width="512" height="320" alt="screenshot_2025-10-04_21-32-11-731Z" src="https://github.com/user-attachments/assets/deaa65fd-f563-43cc-8d43-6f67e6e871ff" />

Cet autre mode permet de naviguer dans la banque des 200 mémoires nommées du K5. Cette banque est à préparer et à injecter dans le K5 depuis Chirp.

## Le mode spectre

### Fonctionnalités communes du mode spectre

Ecran principal :

<img width="512" height="320" alt="screenshot_2025-10-05_14-28-17-315Z" src="https://github.com/user-attachments/assets/6cce5d99-b7c2-4144-aecf-852e9f1d6629" />

- Ligne 1 :
    * Type de spectre : SL (Scan Listes), FQ (Plage de fréquences), BD (Bandes => le code bande apparait en 1er)
    * Valeur trigger UP Uxxx du squelch (valeur de déclenchement sur signal montant)
    * Délai de capture du RSSI d’un signal de 0 à 12 ms. Permet d’accélérer la vitesse de scan, mais cela réduit le rapport signal sur bruit.
    * Modulation courant FM/AM/USB
    * Niveau de la batterie
- Ligne 2/3/4 : Fréquence en cours et CTCSS/DCS. Affichage pouvant varier selon le type de spectre et l'option d'affichage retenue (1/2/3 lignes).
- Corps : Représentation graphique et dynamique des canaux analysés avec leur niveau de signal.
- Ligne 5 : Etendue en cours et infos complémentaires : BL (une blacklist de fréquences est en cours).

### Affectation des touches

- Touche 1 : Passer une fréquence à l’écouter (« skip »)
- Touche 2 : Accès à l’écran simplifié de type scanner simple
- Touche 3 : Sélection de la largeur de bande d’écoute
- Touche 4 : Menu de choix mono ou multiple SL/BD
- Touche 5 : Accès aux Paramètres, puis ^/v pour naviguer, 1/3 pour changer des valeurs, 1/M pour saisir Fstart/Fstop.
- Touche 6 : Navigation dans les modes SL/BD/RG/FQ
- Touche 7 : Sauvegarde des principaux paramètres
- Touche 8 : Options d'affichage N lignes 
      * rien
      * 1 ligne grande fréquence 
      * 1 ligne petite fréquence et ctcss ou DCS
      * 2 lignes: ajout mode et canal
      * 3 lignes: ajout dernière fréquence reçue.
- Touche 9 : Choix de la modulation
- Touche 0 : Accès à l’écran d'historique
- Touche M : Passage en Monitoring sur une fréquence
- SIDE KEY 1 : Passer du mode Normal à FL (verrouillage de fréquence puis Monitor)
- SIDE KEY 2 : Blacklister une fréquence à l’écouter
- Touche \*/F : Réglage squelch paramètre Uxxx
- Touche ^/v : Naviguer dans les SL ou les bandes.  

### Menu des paramètres

<img width="512" height="320" alt="screenshot_2025-10-05_14-32-13-994Z" src="https://github.com/user-attachments/assets/9078e00c-1f75-4392-a601-f3609348f452" />

- RSSI Delay : temps de capture du RSSI en ms. Une valeur trop faible peut faire rater des signaux.
- SpectrumDelay : Permet de définir le temps d’attente sur un signal à l’écoute et retombé sous le squelch. Si la valeur est à l’infini : pressez la touche Exit pour quitter l’écran d’écoute.
- PTT (Option de passage en émission) : LAST RECEIVED = dernière fréquence entendue, LAST VFO FREQ = fréquence en VFO, NINJA MODE : Mode de communication expérimental par saut de fréquence à chaque PTT entre 2 K5 utilisant le spectre en mode Ninja sur une Scanlist commune. Voir vidéo sur YouTube.
- Fstart/Fstop : paramétrage des fréquence ^/v en mode FR.
- Step : paramétrage de la canalisation des fréquences en mode FR.
- ListenBW : paramétrage de la largeur de la bande d’écoute.
- Modulation : FM/AM/USB
- DEFAUT PARAMS et touche 3 pour réinitialiser les paramètres du spectre ainsi que les registres.

### Spectre en vue simplifiée

<img width="512" height="320" alt="screenshot_2025-10-05_14-34-58-915Z" src="https://github.com/user-attachments/assets/e8695e3a-1f62-4036-8a89-6981e7c63f9c" />

Cet écran offre une vue plus synthétique du scan en cours tout en permettant le réglage aisé des paramètres de squelch.

### Monitoring de fréquence

<img width="512" height="320" alt="screenshot_2025-10-05_14-36-09-820Z" src="https://github.com/user-attachments/assets/857d8dd4-fa79-4507-ab95-2946183717ec" />

Le monitor se lance avec la touche M sur une fréquence en écoute.

### Historique des fréquences

<img width="512" height="320" alt="screenshot_2025-10-05_14-38-50-421Z" src="https://github.com/user-attachments/assets/5627c391-008e-4442-af0d-c41065b5d612" />

L'historique évolue dynamiquement au gré des fréquences reçues. Il est possible de naviguer dans la liste, touche M pour passer en monitoring sur la fréquence. Et touche PTT pour copier la fréquence vers le mode VFO.

### Conseils

- La valeurs de réglage du squelch dépend de votre environnement, de votre antenne et de votre choix de délai RSSI.
- RSSI Delay : commencer par exemple à 5 ms et ajuster jusqu'à obtenir un bon compromis entre vitesse et réception.
- Trigger Up Uxxx : commencer par exemple à 5 et ajuster jusqu’à ne plus recevoir de bruits


## Spectre sur les ScanLists (mode SL)
 
- Fonction : Permet de charger dans le spectre les mémoires affectées à des scanlists.
- Lancement : Depuis le mode VFO/MR, touche F+4
- Utilisation et Conseils :
  - Préalablement les fréquences en mémoires doivent avoir été affectées à une scanlist (ex. SL1 = PMR, SL2 = Répéteurs, SL3=Aéro, etc.)
  - A la première utilisation, passer dans chaque SL (^/v) pour ajuster les paramètres de squelch U puis mémoriser vos valeurs avec la touche 7. 
  - Enfin charger vos SL dans le spectre via le menu de sélection en touche 4.

<img width="512" height="320" alt="screenshot_2025-10-05_14-38-50-421Z" src="https://github.com/user-attachments/assets/eea95ec1-ad3f-4342-a4b2-7ecbe41d024a" />

On navigue dans ce menu avec les touches ^/v
  - Touche 5 : choisir une SL en excluant les autres
  - Touche 4 : choisir/invalider une ou plusieurs SL
  - Touche \* : affichages des mémoires affectées à la SL sélectionnée

Les SL choisies apparaissent avec un symbole \*. Puis faire Exit pour lancer le spectre. Touche 7 pour enregistrer sa configuration.

# Spectre sur plage de Fréquences (mode FQ) :

- Fonction : Permet d’analyser une gamme de fréquence à partir d’une fréquence centrale ou bien à partir d’une étendue définie
- Lancement : Depuis le mode VFO/MR, touche F+5
- Utilisation et Conseils :
  - La fréquence issue du VOF/MR est portée au spectre en tant que fréquence centrale. Ensuite, vos pouvez agir sur le paramétrage de votre spectre selon vos besoins en step, modulation, etc. Réglages touche 5.
  - L’entendue des fréquences basse/haute peut être ajustée dans le menu via les paramètres FStart/FStop. Sur ces paramètres faire 1 pour accéder à la saisie et M pour valider (touche \* pour la virgule).
  - Ajuster votre squelch.

## Spectre sur les Bandes Prédéfinis (mode BD)

- Fonction : Permet d’analyser en spectre des bandes prédéfinies (ex. PMR, CB, AERO, HAM, etc.).
- Lancement : Depuis le mode VFO/MR, touche F+6
- Utilisation et Conseils :
  - Les bandes sont stockées dans un fichier bands.h personnalisable avec recompilation du firmware (procédure en lien en fin de doc).
  - Il est possible de paramétrer 32 bandes.

### Exemple de fichier de configuration
Les fréquences sont définies en 10 Hz 144MHz s'écrit 14400000.
Il y a 32 bandes max et le nom fait maximum 12 caractères
Les steps sont à choisir parmis:
  S_STEP_0_01kHz,
  S_STEP_0_1kHz,
  S_STEP_0_5kHz,
  S_STEP_1_0kHz,
  S_STEP_2_5kHz,
  S_STEP_5_0kHz,
  S_STEP_6_25kHz,
  S_STEP_8_33kHz,
  S_STEP_10_0kHz,
  S_STEP_12_5kHz,
  S_STEP_25_0kHz,
  S_STEP_100kHz,
  S_STEP_500kHz,

Les modulations parmis:
	MODULATION_FM,
	MODULATION_AM,
	MODULATION_SSB,

<img width="741" height="130" alt="bands h" src="https://github.com/user-attachments/assets/dc352144-cb45-4a49-b9cb-8a8375f98935" />

De la même manière qu’en mode SL, il est demandé à la 1ère utilisation de paramétrer et sauvegarder la valeurs du squelch sur les bandes qui vous intéressent. Touches ^/v pour naviguer dans les bandes.

Ensuite le menu touche 4 permet de choisir les bandes à analyser de la même manière que le menu en mode SL :

<img width="512" height="320" alt="screenshot_2025-10-05_14-44-35-765Z" src="https://github.com/user-attachments/assets/938d3712-3cd3-4588-8c66-cb17d3016c6f" />

## FAQ

- Est-il possible de verrouiller son K5 en bande PMR uniquement ? :
Oui : Affichage menus cachés, menu No 48, valeur PMR446 ONLY.

- Le firmware est-il compatible avec les mod SI4732 ? :
Non, mais ce sera peut-être envisageable.

- Le firmware est-il compatible avec les mod EEPROM ? :
Non, mais c’est une évolution possible.


