<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="logo/logo-planete-hymnes-blanc.png">
    <img src="logo/logo-planete-hymnes.png" alt="Planète Hymnes" width="560">
  </picture>
</p>

<p align="center"><b>Les hymnes nationaux de 249 pays et territoires, sur une carte du monde.</b></p>

---

Planète Hymnes est un site d'une seule page pour explorer les hymnes nationaux du monde : on part d'une carte, on clique sur un pays et on découvre son hymne, ses auteurs, ses dates et ses paroles avec une traduction française. Les données vivent dans un Google Sheet : une correction dans le tableur apparaît sur le site au chargement suivant, sans toucher au code.

## Fonctionnalités

- **Carte du monde interactive** : zoom à la molette ou au pincement, boutons par continent, points cliquables pour les îles et micro-États, liste complète des pays sous la carte.
- **Fiche pays** :
  - carte régionale avec les voisins cliquables ;
  - nom officiel, capitale, superficie, langues officielles, monnaie, gentilé, pays frontaliers ;
  - hymne : titre original et français, parolier, compositeur, dates des paroles, de la musique et d'adoption ;
  - paroles originales, translittération et traduction française, côte à côte (en onglets sur mobile) ;
  - lien d'écoute vers Wikimedia Commons, ou lecteur intégré si un fichier audio est renseigné.
- **Recherche** :
  - suggestions de pays pendant la frappe dans la barre du haut ;
  - recherche dans les traductions, les paroles originales, les translittérations, les titres et les auteurs, sans tenir compte des accents ;
  - plusieurs mots : tous doivent apparaître ; entre guillemets : expression exacte (`"terre de nos pères"`) ;
  - filtres par champ et par continent, tri par nombre d'occurrences ;
  - mots surlignés dans la fiche ouverte depuis un résultat ;
  - dernières recherches et mots les plus fréquents des traductions.
- **Quiz** : 10 questions à partir du drapeau, d'un extrait de paroles ou du titre de l'hymne, avec choix de la zone.
- **Au hasard** : ouvre la fiche d'un hymne tiré au sort.
- Mode sombre automatique, affichage adapté au mobile.

## Contenu du dossier

```
planete-hymnes/
├── index.html                         le site (une seule page, tout compris)
├── README.md                          ce fichier
├── donnees/
│   └── Hymnes_nationaux_du_monde.xlsx classeur à importer dans Google Sheets
└── logo/
    ├── logo-planete-hymnes.svg / .png         logo pour fond clair
    ├── logo-planete-hymnes-blanc.svg / .png   logo pour fond sombre
    ├── icone-planete-hymnes.svg / .png        icône seule (globe et onde)
    └── icone-planete-hymnes-app.svg / .png    icône sur fond, format carré (réseaux, favicon)
```

`index.html` contient le code, la mise en page, le fond de carte et une copie de secours des données : il fonctionne seul. Le dossier `logo/` sert au README et à vos supports ; le site n'en a pas besoin.

## Mettre le site en ligne sur GitHub Pages

1. Créez un dépôt sur GitHub, par exemple `planete-hymnes`.
2. Déposez-y `index.html`, `README.md` et le dossier `logo/` (bouton **Add file → Upload files**).
3. Allez dans **Settings → Pages**. Sous **Build and deployment**, choisissez **Deploy from a branch**, la branche `main` et le dossier `/ (root)`, puis **Save**.
4. Après une à deux minutes, le site est en ligne à l'adresse `https://<votre-identifiant>.github.io/planete-hymnes/`.

Le dossier `donnees/` n'a pas besoin d'être publié : il sert à créer ou recréer le Google Sheet.

## Les données : le Google Sheet

Le site lit l'onglet **Hymnes** du Google Sheet à chaque chargement. Le pied de page indique la source utilisée :

- point vert, « Données en direct du Google Sheet » : la lecture a réussi ;
- point gris, « Copie embarquée » : le Sheet n'a pas pu être lu, le site affiche la copie incluse dans `index.html`.

### Créer ou remplacer le Google Sheet

1. Importez `donnees/Hymnes_nationaux_du_monde.xlsx` dans Google Drive et ouvrez-le.
2. **Fichier → Enregistrer au format Google Sheets** : le site ne peut pas lire un fichier Excel stocké dans Drive, seulement un vrai Google Sheet.
3. **Partager → Accès général : « Tous les utilisateurs disposant du lien » → Lecteur**.
4. Copiez l'identifiant du Sheet, la partie de l'adresse entre `/d/` et `/edit` :
   `https://docs.google.com/spreadsheets/d/`**`1X5fjdG6RI3TUXjmJb3v6Wc5Mnm7AVmIjOOCmQP8bNys`**`/edit`
5. Dans `index.html`, cherchez la ligne `const SHEET_ID =` (vers la ligne 362) et remplacez l'identifiant entre apostrophes.

Le site est déjà relié au Sheet ci-dessus ; ces étapes ne servent que si vous en créez un nouveau.

### Modifier les données

Chaque ligne de l'onglet **Hymnes** est un pays ou un territoire. Vous pouvez corriger librement le texte des cellules. Quelques règles pour que le site s'y retrouve :

| Colonne | À savoir |
|---|---|
| **Code ISO** | Code à deux lettres (FR, DE…) qui place la ligne sur la carte. Ne pas modifier. |
| **Pays / territoire** | Nom affiché sur le site. Sert de secours si le code ISO manque. |
| **Continent** | Une de ces valeurs : Afrique, Amérique du Nord, Amérique du Sud, Asie, Europe, Océanie. |
| **Statut** | Les lignes qui commencent par « État » sont traitées comme des États (quiz « États souverains seulement »). |
| **Paroles reproduites** | `Oui` : les paroles s'affichent et sont cherchables. `Non` : la fiche renvoie vers la source. `Sans objet` : hymne sans paroles. |
| **Paroles translittérées** | Laisser `— (écriture latine)` pour les langues en alphabet latin : la colonne est alors masquée. |
| **Remarques** | La mention « utilise l'hymne de » indique un territoire qui partage l'hymne d'un autre pays ; le site les regroupe. |
| **Fichier audio direct** | Collez l'adresse d'un fichier `.mp3` ou `.ogg` (par exemple un lien `upload.wikimedia.org`) : un lecteur apparaît dans la fiche. |

Ne renommez pas l'onglet **Hymnes** ni les en-têtes de colonnes : le site les reconnaît par leur nom. L'ordre des colonnes, lui, peut changer.

> Si des dates disparaissent sur le site, sélectionnez les colonnes de dates et appliquez **Format → Nombre → Texte brut**. Google Sheets devine parfois mal le type d'une colonne qui mélange années et texte (« vers 1880 »).

## Les paroles et leurs droits

Les paroles ne sont reproduites que lorsqu'elles datent d'avant 1929 et relèvent du domaine public. Pour les autres hymnes, la fiche renvoie vers Wikipédia. Les traductions françaises sont des traductions de travail à relire avant toute publication officielle ; quand une version française officielle existe (Belgique, Suisse, Canada, Haïti), c'est elle qui figure.

## Limites connues

- Le site a besoin d'internet : pour lire le Google Sheet, charger les bibliothèques de carte (D3, TopoJSON), les polices et les images de drapeaux. Sans images, les drapeaux s'affichent en emoji.
- Les infos pays (capitale, langues, monnaie…) proviennent d'un référentiel ouvert intégré au fichier ; elles ne viennent pas du Sheet. La population n'y figure pas.
- Les mentions « à vérifier » dans la colonne Remarques signalent les informations les moins sûres.
- L'Antarctique n'apparaît pas : il ne relève d'aucune souveraineté. Les îles subantarctiques sont rattachées à un continent selon la classification M49 de l'ONU.

## Sources et crédits

- **Fond de carte** : [Natural Earth](https://www.naturalearthdata.com/) (domaine public), via [world-atlas](https://github.com/topojson/world-atlas) (licence ISC).
- **Référentiel pays** (noms, codes, capitales, langues, monnaies, frontières) : [mledoze/countries](https://github.com/mledoze/countries), sous licence [ODbL 1.0](https://opendatacommons.org/licenses/odbl/1-0/).
- **Drapeaux** : [flagcdn.com](https://flagcdn.com/).
- **Enregistrements** : [Wikimedia Commons](https://commons.wikimedia.org/).
- **Bibliothèques** : [D3.js](https://d3js.org/) 7.8.5 et [TopoJSON](https://github.com/topojson/topojson) 3.0.2 (licence ISC).
- **Polices** : Figtree, Josefin Sans et Literata, via Google Fonts (licence SIL Open Font).
