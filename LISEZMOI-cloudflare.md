# Agenda Escrime — Mettre en ligne la version PARTAGÉE (Cloudflare)

Avec cette version, tout le monde voit les mêmes données : si ta mère
ajoute un événement sur son téléphone, ton père le verra en actualisant
la page sur le sien. C'est gratuit avec un compte Cloudflare.

## Ce dont tu as besoin
- Un compte Cloudflare (gratuit) : https://dash.cloudflare.com
- Le fichier `worker-agenda-escrime.js` (il contient TOUT : la page + le code serveur)

## Étape 1 — Créer le Worker
1. Connecte-toi sur https://dash.cloudflare.com
2. Dans le menu de gauche : **Workers & Pages** (ou « Compute »)
3. Clique **Create** → **Create Worker** (pas « Pages » cette fois !)
4. Donne-lui un nom, par exemple `agenda-escrime`, puis **Deploy**
5. Clique **Edit code** : un éditeur s'ouvre
6. Supprime tout le code d'exemple, puis colle **tout le contenu** du
   fichier `worker-agenda-escrime.js` (ouvre-le avec le Bloc-notes,
   Ctrl+A puis Ctrl+C, et Ctrl+V dans l'éditeur Cloudflare)
7. Clique **Deploy** (en haut à droite)

## Étape 2 — Créer la petite base de données (KV)
1. Menu de gauche : **Storage & Databases** → **KV**
2. Clique **Create a namespace**, appelle-le `agenda-escrime-donnees`, valide

## Étape 3 — Relier la base au Worker (le "binding")
1. Retourne dans **Workers & Pages** → clique sur ton worker `agenda-escrime`
2. Onglet **Settings** → section **Bindings** → **Add binding**
3. Choisis **KV namespace**
4. Dans « Variable name », écris exactement :  `AGENDA`
   (en majuscules, c'est important !)
5. Dans « KV namespace », choisis `agenda-escrime-donnees`
6. Enregistre (**Save / Deploy**)

## Étape 4 — C'est en ligne !
Ton agenda est accessible à l'adresse du worker, du genre :

    https://agenda-escrime.TONCOMPTE.workers.dev

(l'adresse exacte est affichée sur la page du worker). Envoie ce lien
à ta famille : tout le monde verra et modifiera le MÊME agenda.

## Bon à savoir
- Toute personne ayant le lien peut modifier l'agenda (statuts,
  événements…). Pour un usage familial c'est parfait ; ne publie pas
  le lien publiquement si tu ne veux pas que n'importe qui le change.
- Si deux personnes modifient exactement en même temps, c'est la
  dernière sauvegarde qui gagne (cas très rare en pratique).
- Le fichier `agenda-escrime-2026-2027.html` reste utilisable tout
  seul (sans Cloudflare) : dans ce cas il sauvegarde dans le
  navigateur de chaque appareil, séparément, comme avant.
- Pour modifier les compétitions de base plus tard, redemande-moi
  une mise à jour du fichier, recolle le nouveau code dans le worker,
  et re-déploie : les données sauvegardées ne seront pas perdues
  (elles sont dans le KV, pas dans le code).
