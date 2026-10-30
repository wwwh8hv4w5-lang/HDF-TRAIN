# HDF TRAIN 1.4

Jeu 3D dans le navigateur (WebGL 2), construit sur le moteur HDF WALL / FSM3D, de **F.S.M Game House**.

**Jouer en ligne : https://wwwh8hv4w5-lang.github.io/HDF-TRAIN/**

Tout tient dans un seul fichier HTML autonome : `index.html`.

## 1.4 : le portrait de la princesse Ilona

- Un **portrait encadré de la princesse Ilona** est accroché dans la voiture 1, sur la cloison avant de la salle, côté gauche (celui de votre place). Il est au-dessus du dernier banc et sous le bout du porte-bagages, comme les photos des anciens compartiments. On le voit du couloir en allant vers l'avant.
- Le cadre est doré, avec un passe-partout crème, un filet doré et un cartouche « PRINCESSE ILONA ». La photo (540 × 720, JPEG intégré au fichier, environ 89 Ko) garde ses proportions. Elle est affichée avec mipmaps et filtrage anisotrope.
- **Le portrait est fixé à la voiture.** C'est un élément de la voiture 1 : il suit exactement sa position, sa pente et ses virages pendant que le train roule. Comme pour les parois, les secousses n'agissent que sur la caméra : le cadre ne flotte pas et ne glisse pas sur le mur.
- Le cadre est posé à quelques millimètres de la cloison, sans surface confondue avec elle, donc sans scintillement. Il reste dans l'épaisseur déjà bloquante de la cloison : les collisions, les portes, les fenêtres et les actions ne changent pas.
- Le reste ne change pas : l'enquête, le menu principal, les 3 sauvegardes et les voix. Le format des sauvegardes ne change pas (le portrait n'y est pas enregistré) : une sauvegarde de la 1.3 est reconnue par la 1.4.
- **Ce qui a été vérifié** (Chromium sans écran) :
  - le cadre est bien rattaché à la voiture : même matrice que la voiture à chaque image, train arrêté comme lancé ;
  - le portrait se voit depuis le couloir, de près, en biais, pendant une secousse et à un autre moment du trajet ;
  - pas de scintillement ni de déformation ;
  - aucune erreur JavaScript.
- **Ce qui n'a pas été vérifié** : l'iPad/Safari et un vrai GPU.

## 1.3 : menu principal et 3 sauvegardes

- **Menu principal** au lancement : Continuer (la partie la plus récente), Nouvelle partie, Charger une partie, Options (son, voix), Quitter.
- **3 emplacements** sur l'appareil (`localStorage`, clés `hdf-train-partie-1` à `3`). Chacun indique l'affaire (le nom de la victime une fois le corps découvert), l'acte, l'étape, le nombre d'indices, l'heure du train et la date réelle de la sauvegarde. Écraser un emplacement plein demande un deuxième appui.
- **Ce qui est sauvé** : l'état complet, pas une graine. Cela comprend l'affaire (casting, victime, coupable, méthode, témoins, liste), la place et la couleur de chaque voyageur, la position du train, l'heure, les besoins, le sac, le joueur, l'enquête (étapes, indices, chronologie, interrogatoires, fouilles), l'état de chaque voyageur, le contrôleur, les portes et la mémoire des boucles.
- **Sauvegarde automatique** quand on franchit une étape, trouve un indice, change d'endroit (salle, plates-formes, toilettes) ou ouvre le menu, et toutes les 2 minutes. Elle attend toujours un moment sûr. **Sauvegarde manuelle** : menu · Sauvegarder.
- **Pas de sauvegarde** pendant une scène, une conversation, un somme, un événement qui se déclenche, un voyageur qui marche vers une action ou le dénouement (après la déduction). Le jeu le dit, et la sauvegarde automatique réessaie au moment sûr suivant.
- Après un chargement, un écran « Reprendre la partie » attend un toucher, un clic ou une touche, parce que le navigateur exige un geste avant les voix.
- Une nouvelle boucle ou « Recommencer le voyage » reste sur le même emplacement. Une nouvelle partie remet la mémoire des boucles à zéro, sauf la toute première fois : la mémoire d'un joueur de la 1.2 est alors gardée.
- **Ce qui a été vérifié** (tests automatiques, Chromium sans écran, synthèse vocale simulée) :
  - menu principal ;
  - nouvelle partie ;
  - sauvegarde automatique ;
  - sauvegarde depuis le menu avec confirmation d'écrasement ;
  - rechargement, Continuer, reprise par clic ou par touche, avec un état chargé identique à l'état sauvé ;
  - 3 emplacements indépendants ;
  - refus de sauvegarder pendant une scène, avec le motif ;
  - Quitter ;
  - voix après reprise ;
  - aucune erreur JavaScript.
- **Ce qui n'a pas été vérifié** : l'iPad/Safari, une vraie manette (la navigation existe mais n'a pas été essayée), les vraies voix, et une partie jouée de bout en bout puis rechargée à chaque acte.

## 1.2 : voix de synthèse

Les personnages parlent avec les voix françaises de l'appareil (synthèse vocale du navigateur, rien n'est téléchargé, aucune clé).

- Chaque voyageur a sa voix : une voix du bon sexe, une hauteur et un débit (entre 1,0 et 1,1) tirés de son âge et de son identifiant. C'est toujours la même voix pour le même personnage.
- Ce qui est dit : les répliques des voyageurs en dialogue, les réponses des suspects en confrontation, les conversations des voisins et les annonces du contrôleur (sous-titres). Les descriptions, les documents, le sac, les questions du joueur et l'interface ne sont pas dits. Une réplique de plus de 220 caractères est coupée à la fin d'une phrase.
- Les répliques passent une par une, dans une file. Le dialogue avec le joueur passe avant les conversations voisines.
- Le navigateur exige un geste (toucher, clic ou touche) avant de parler. Une réplique refusée faute de geste est gardée, puis dite au geste suivant. Après trois refus, le jeu affiche « Touchez l'écran pour activer les voix ». La manette ne compte pas comme un geste.
- Menu · **Voix : parlées / bruitage / muettes**, mémorisé sur l'appareil. Quand le son est coupé, il n'y a pas de voix. Les voix s'arrêtent si l'onglet est caché ou si le menu est ouvert.
- Ce qui a été vérifié : des tests automatiques avec une synthèse vocale simulée dans Chromium sans écran (choix de la voix selon le sexe, file, refus puis geste, annulation, interruption, plafond, son coupé, onglet caché, bouton, aucune erreur JavaScript).
- Ce qui n'a pas été vérifié : le rendu des vraies voix, l'iPad/Safari et la manette. Le résultat dépend des voix françaises installées sur l'appareil.

Le jeu lui-même (l'enquête, les règles) n'a pas changé par rapport à la 1.1.

© FERAL SYSTEM MEDIA
