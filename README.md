# Choisto DL

Plugin Jellyfin de téléchargement : liens directs, 1fichier, Torbox, magnets et .torrent, importés directement dans vos bibliothèques.

**[Télécharger la dernière version](https://github.com/Choisto/Choisto-DL-Releases/releases/latest)** · Jellyfin 12.1 ou plus récent

<!-- Shown under the changelog on every release page. Keep each paragraph on one line: GitHub turns every line break in release notes into a visible one. -->

## Choisto DL, c'est quoi ?

Un gestionnaire de téléchargements intégré à Jellyfin. Vous collez un lien, vous choisissez une bibliothèque, et le serveur télécharge le fichier, le renomme comme Jellyfin l'attend et le range dans la bibliothèque.

## Fonctionnalités

**Page Downloads dans le menu principal** (administrateurs uniquement)
- Collez jusqu'à 200 liens d'un coup : un par ligne, ou un bloc de texte copié d'une page. Les liens sont extraits du texte, les doublons ignorés, et ceux qui sont refusés restent affichés avec la raison.
- Suivez la file en direct : progression, vitesse, pause, reprise, annulation.
- La file survit aux redémarrages et aux mises à jour ; un téléchargement interrompu reprend là où il s'était arrêté.

**Sources prises en charge**
- **Liens HTTP / HTTPS directs**, avec reprise des transferts interrompus.
- **1fichier** : via une clé API Premium (pleine vitesse, plusieurs à la fois, reprise possible ; *non testé en conditions réelles*), ou en gratuit, en invité ou connecté à un compte, avec gestion automatique des files d'attente et des délais.
- **Torbox** (service debrid) : liens des hébergeurs pris en charge par Torbox, **liens magnet** et **fichiers .torrent**. Un torrent donne un téléchargement par vidéo (les samples, sous-titres et images sont écartés) ; une fois le torrent importé, le plugin le retire du compte Torbox, mais seulement s'il l'y a lui-même ajouté.

**Séries intelligentes (avec Torbox)**

Un torrent envoyé vers une bibliothèque de séries n'est pas téléchargé en entier : il reste sur Torbox et chaque épisode apparaît tout de suite dans Jellyfin, lu en streaming. Seuls l'épisode en cours et les suivants (3 par défaut) sont gardés sur le disque, pour chaque spectateur ; les épisodes vus sont libérés au bout de 7 jours.

**Import dans les bibliothèques**
- Renommage automatique selon les conventions de Jellyfin, par exemple :
  - `The.Matrix.1999.1080p.BluRay.x264-GRP.mkv` → `The Matrix (1999)/The Matrix (1999).mkv`
  - `Breaking.Bad.S01E02.720p.HDTV.mkv` → `Breaking Bad/Season 01/Breaking Bad S01E02.mkv`
- **Extraction des archives** `.rar` (multi-volumes compris), `.zip` et `.7z`, sans outil à installer.
- Scan de la bibliothèque après import, regroupé quand plusieurs téléchargements finissent ensemble.
- Aucun fichier existant n'est jamais écrasé.

**Fiabilité**
- Nouvelle tentative automatique en cas d'erreur réseau (coupure, délai dépassé, erreur 5xx…), avec un délai qui s'allonge à chaque tentative.
- Les fichiers trop petits pour être des vidéos (20 Mo par défaut), comme une page d'erreur enregistrée sous le nom d'un film, sont refusés.

## Installation

Nécessite **Jellyfin 12.1** ou plus récent.

1. Dans Jellyfin, ouvrez **Tableau de bord → Extensions → Dépôts** et ajoutez :
   ```
   https://github.com/Choisto/Choisto-DL-Releases/releases/latest/download/manifest.json
   ```
2. Installez **Choisto DL** depuis le catalogue, puis redémarrez le serveur.
3. Réglez le plugin dans **Tableau de bord → Extensions → Choisto DL** (clés 1fichier et Torbox, dossier de travail, nombre de téléchargements simultanés…), puis ouvrez **Downloads** dans le menu principal.

Les mises à jour apparaissent ensuite directement dans le catalogue de Jellyfin.
