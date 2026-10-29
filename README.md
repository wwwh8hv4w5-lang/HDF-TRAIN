# HDF TRAIN 1.2

Jeu 3D dans le navigateur (WebGL 2), construit sur le moteur HDF WALL / FSM3D, de **F.S.M Game House**.

**Jouer en ligne : https://wwwh8hv4w5-lang.github.io/HDF-TRAIN/**

Tout tient dans un seul fichier HTML autonome : `index.html`.

## 1.2 : voix de synthèse

Les personnages parlent avec les voix françaises de l'appareil (synthèse vocale du navigateur, rien n'est téléchargé, aucune clé).

- Chaque voyageur a sa voix : une voix du bon sexe, une hauteur et un débit (entre 1,0 et 1,1) tirés de son âge et de son identifiant. C'est toujours la même voix pour le même personnage.
- Ce qui est dit : les répliques des voyageurs en dialogue, les réponses des suspects en confrontation, les conversations des voisins et les annonces du contrôleur (sous-titres). Les descriptions, les documents, le sac, les questions du joueur et l'interface ne sont pas dits. Une réplique de plus de 220 caractères est coupée à la fin d'une phrase.
- Les répliques passent une par une, dans une file. Le dialogue avec le joueur passe avant les conversations voisines.
- Le navigateur exige un geste (toucher, clic ou touche) avant de parler. Une réplique refusée faute de geste est gardée, puis dite au geste suivant. Après trois refus, le jeu affiche « Touchez l'écran pour activer les voix ». La manette ne compte pas comme un geste.
- Menu · **Voix : parlées / bruitage / muettes**, mémorisé sur l'appareil. Quand le son est coupé, il n'y a pas de voix. Les voix s'arrêtent si l'onglet est caché ou si le menu est ouvert.
- Ce qui a été vérifié : des tests automatiques avec une synthèse vocale simulée dans Chromium sans écran (choix de la voix selon le sexe, file, refus puis geste, annulation, interruption, plafond, son coupé, onglet caché, bouton, aucune erreur JavaScript).
- Ce qui n'a pas été vérifié : le rendu des vraies voix, l'iPad/Safari et la manette. Le résultat dépend des voix françaises installées sur l'appareil.

Le jeu lui-même n'a pas changé par rapport à la 1.1.

© FERAL SYSTEM MEDIA
