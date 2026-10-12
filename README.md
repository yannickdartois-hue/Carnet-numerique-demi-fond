# Carnet numérique de demi-fond · Seconde et Terminale

Application hors ligne (PWA) du lycée Georges Pompidou, Castelnau-le-Lez. Version **v11 · 12/10/2026** (affichée en bas de l'accueil).
Une tablette par binôme : les élèves remplissent leur carnet de course à chaque séance, puis montrent un QR code que le professeur scanne.

## Contenu du dépôt
| Fichier | Rôle |
|---|---|
| `index.html` | toute l'application (élève + mode prof), bibliothèques QR incluses |
| `sw.js` | fonctionnement hors ligne (cache) |
| `manifest.webmanifest`, `icon-192.png`, `icon-512.png` | installation sur l'écran d'accueil |
| `.github/workflows/tests.yml` | tests automatiques lancés par GitHub à chaque dépôt (onglet *Actions*) |
| `src/` | sources : `head.html` (style), `core.js` (séances, barèmes, calculs), `app.js` (interface), `lib/` (QR), `build.sh` (assemble `index.html`), `tests/` (tests Playwright) |

## Installation
1. GitHub Pages : *Settings → Pages → Deploy from a branch → main / (root)*.
2. Sur chaque tablette (Wi-Fi) : ouvrir l'adresse, puis **Ajouter à l'écran d'accueil**.
3. Sur l'iPad du professeur : idem (indispensable, sinon Safari efface les données au bout de 7 jours sans ouverture).

## Utilisation élève
- **Choisir son niveau** à l'accueil : deux couloirs de piste distincts, **Seconde** (S1-S8, vert) et **Terminale** (T1-T9, indigo). Les contenus sont différents ; chaque niveau n'affiche que ses binômes. La tablette retient le dernier niveau choisi (*⇄ Changer de niveau* pour basculer).
- **Créer le binôme** à la 1re séance, dans le bon niveau : classe, prénoms, noms, F/G.
- **Saisie sans clavier** : boutons − / + (tours, plots, distances, FC, VMA) et −5 −1 +1 +5 pour les temps. La case reste modifiable au clavier (on peut taper 1'52, 1:52 ou 112). Une alerte ⚠ apparaît si une valeur est invraisemblable (plus de 9 tours en 3', FC hors 80-230, 500 m hors 1'15-4'30, temps à plus de 20 % du prévu…).
- **Compter en direct** ⏱ (coach) : sur le 3' et le 1'30 mesuré, bouton Départ au sifflet, gros bouton TOUR, bip et grille des plots à mi-course puis au sifflet final ; sur le 500 m, passage au 250 m et arrivée. Tout est rempli automatiquement, avec le graphique des temps au tour.
- **Objectifs du jour** : VMA mesurée (S1 puis S6 ; T2 puis re-test T6) et objectifs calculés. En S2, S3, T3 et T4, l'élève les calcule d'abord, puis *Vérifier mes calculs*. VMA modifiée = case orange, signalée au prof.
- **Calculatrice** 🧮, **consignes** ⓘ repliables, **idées de conseils** 💡 pour le coach (tirées des résultats : régularité du 3', T/L du 36", écart du 1'30, séries, moitiés du 500 m), à toucher pour les ajouter.
- **Ma progression** : courbes du 3' (ou du 500 m), du 1'30 projet / réalisé et des projets tenus par séance (repère ¾).
- **QR à montrer** : la page du binôme signale les séances remplies mais pas encore scannées, ou modifiées depuis l'envoi.
- **Séance en étapes** : une barre numérotée en haut (piste) montre les étapes remplies. Sur téléphone, **une étape à la fois** (boutons ou glisser le doigt) ; *Tout afficher* pour revenir à la page complète.
- **Lisibilité au soleil** : thème clair imposé (mode sombre en option dans *Données*) ; pictogrammes au trait à la place des émojis.
- **Présence** repliée en une ligne (« Léa et Hugo présents ») : *Absent ou blessé ?* pour la modifier. **Coach remplaçant** (bouton rouge) et **corriger les noms** : inchangés.

## Nouveautés pédagogiques (v11)
- **Projets ambitieux** : un projet ne compte comme tenu que s'il vaut au moins 95 % de la dernière distance réalisée (1'30) ou de la VMA (3', 500 m). Sinon l'élève voit « Projet prudent » et la distance minimale à viser. On évite qu'un élève prudent obtienne le degré 4 sans progresser.
- **Écart au projet** : courbe dans *Ma progression* et colonne « Écart 1'30 début → fin » côté prof. C'est l'indicateur principal de « gérer son allure » : il doit baisser.
- **Effort ressenti (RPE 0 à 10)** à la place des trois sensations ; **charge = RPE × durée** (UA). La FC devient facultative.
- **Coach évaluable (AFL3)** : avant la course principale, le coach écrit son **pronostic** ; après, le coureur dit si le conseil l'a aidé. Côté prof, colonne « Comme coach » : aide x/y et précision moyenne du pronostic.
- **Échauffement à cocher** (3 parties, compteur des 4 exercices de la partie 2) au lieu du texte libre.
- **Pratique adaptée** (avis médical, asthme, reprise) : bouton dans la présence ; tolérances élargies (3' à 20 m, 1'30 en zone 2, temps à 4 s) ; signalé au prof.

## Utilisation professeur (bouton *Prof*, code **1275**)
- *Scanner* (caméra, photo ou texte collé) → *Classe* : tableau S1-S8 ou T1-T9, projets tenus, degré AFL2, épreuve blanche, AFL1, répartition AFL2/AFL3 choisie en Terminale, total /20.
- **Points d'attention** en haut du tableau : QR manquants à la dernière séance, aucun projet tenu sur 3 séances, VMA modifiée, 2 absences ou plus, coach qui n'écrit jamais « Ta réussite ».
- **↺ QR de restauration** (à côté du nom, ou dans le détail) : QR animé qui recrée le binôme sur une tablette effacée ou neuve (accueil → *Restaurer un binôme*). Les séances déjà présentes ne sont pas écrasées.
- **Quel est cet appareil ?** À la 1re ouverture du mode prof, déclarer *appareil du prof* (le seul qui stocke la classe) ou *tablette d'élève* (réglages et chrono seulement : le scan y est refusé). Modifiable dans *Données*.
- **Rattrapage** : sur la page du binôme, *QR de rattrapage* regroupe toutes les séances non envoyées (QR animé si besoin) ; *Envoyer en fichier* passe par AirDrop ou le partage ; côté prof, *Scanner → Fichier reçu*.
- **Chrono de classe** (onglet *Chrono*, sur ton téléphone branché à une enceinte) : 36"/36", test 36"/24", 1'12/1'12, 3' et 1'30 avec mi-course, 2 × 6', ou réglage libre ; bips, 3-2-1, voix française (« Partez », « Stop », « Mi-course »), écran maintenu allumé.
- *Étoiles* : ★ AFL2 / ★ AFL3 par séance. *Données* : export CSV, sauvegarde JSON, code prof.
- **Réglages de la tablette** (onglet *Données*, à faire sur chaque tablette élève) : option *nom de famille en initiale seulement* (le prof garde le nom complet déjà reçu) et **fin de cycle : effacer une classe** de la tablette, avec le nombre de séances jamais scannées.

## Données personnelles
Aucune donnée n'est envoyée sur Internet : tout reste dans le navigateur des tablettes et de l'appareil du professeur. Le dépôt ne contient que le code.
Faire une **sauvegarde JSON** après chaque séance. En fin de cycle, effacer la classe des tablettes.

## Mise à jour
Remplacer les fichiers dans le dépôt et **changer le numéro de version** dans `sw.js` (actuellement `carnet-df-v11` → `v12`…). À la prochaine ouverture en Wi-Fi, un bandeau « Nouvelle version installée → Recharger » apparaît ; les données ne sont pas touchées.
Pour modifier l'application : éditer `src/core.js` ou `src/app.js`, lancer `sh build.sh` dans `src/`, copier le nouvel `index.html` à la racine.
Les données enregistrées portent un **numéro de version** (`schema`) : une version future saura relire et convertir celles de cette année.
**Tests automatiques** : après chaque dépôt, onglet *Actions* du dépôt GitHub → coche verte = tout fonctionne ; croix rouge = ne pas installer cette version sur les tablettes. Si le dossier `.github` n'est pas accepté par le glisser-déposer, créer le fichier via *Add file → Create new file* en tapant le chemin `.github/workflows/tests.yml` et en collant son contenu.

Le code prof n'est pas une sécurité (il est lisible dans le code source) : il évite seulement qu'un élève ouvre le mode prof par erreur.
