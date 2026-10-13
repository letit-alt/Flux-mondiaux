# Flux Mondiaux — mise à jour du dossier

Site : https://letit-alt.github.io/Flux-mondiaux/

## Structure

| Fichier | Rôle | À modifier pour une mise à jour ? |
|---|---|---|
| `index.html` | Interface, carte Leaflet (intégrée), logique de l'application | Non, sauf nouvelle fonctionnalité |
| `data.js` | Toutes les données (`window.FLUX_DATA = {...}`) | **Oui, c'est le seul fichier à changer** |
| `README_MAJ.md` | Ce guide | — |

Les deux fichiers `index.html` et `data.js` doivent rester dans le même dossier. Le site marche aussi en ouvrant `index.html` en local, sans serveur.

## Sections de `data.js`

| Section | Contenu | Fréquence conseillée |
|---|---|---|
| `markets` | Bandeau de prix : `value`, `unit`, `date`, et soit `ref_pct` (variation en %), soit `ref_value` (valeur de référence) avec `ref_label` | Chaque semaine |
| `weekly` | Synthèses hebdomadaires (la plus récente en premier) : `week`, `date`, `points[]`, `takeaway` | Chaque semaine |
| `news` | `last_updated` + `items[]` : `date`, `market`, `countries[]` (ids), `resources[]`, `headline`, `summary`, `source`, `url` | Chaque semaine |
| `tension` | Indice de tension : `months[]` et, par chokepoint, `history[]` (un score par mois), `current` (`trafic`/40, `attaques`/35, `cout`/25), `trend`, `note` | Chaque mois : ajouter le mois dans `months` et un score dans chaque `history` |
| `timeline` | Événements de la frise : `date`, `title`, `text`, `chokepoints[]`, `resources[]`, `level` (`crise`, `tension`, `détente`, `adaptation`) | Quand un événement majeur survient |
| `chokepoints` | Fiches des points de passage, routes et alternatives ; mettre à jour `generated` | Quand la situation change |
| `countries`, `commodities`, `historical` | Fiches pays, producteurs et importateurs, cas historiques | Rarement |
| `impact` | Scénarios « Impact marchés » par chokepoint | Rarement |

Ids des ressources : `oil`, `gas_lng`, `wheat`, `copper`, `nickel`, `lithium`, `semiconductors`, `fertilizers`, `container`.
Ids des chokepoints : `hormuz`, `malacca`, `suez`, `panama`, `bosphorus`, `bab_el_mandeb`.

## Procédure

1. Demander à Claude « actualise le dossier Flux Mondiaux » : il recherche les actualités, met à jour `data.js` et les dates `news.last_updated`, `markets.as_of` et `chokepoints.generated`.
2. Publier sur GitHub : **Add file → Upload files**, déposer `data.js`, puis **Commit changes**.
3. GitHub Pages se met à jour en une à deux minutes. Si l'ancienne version s'affiche encore, recharger la page sans le cache (Ctrl+Maj+R, ou Cmd+Maj+R sur Mac).

## Fond de carte

Tuiles Esri World Dark Gray (sans clé API), avec un repli automatique sur OpenStreetMap. CARTO (`basemaps.cartocdn.com`) n'est plus utilisé, car il exige désormais une clé.
