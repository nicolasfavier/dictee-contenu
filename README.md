# Dictée : contenu téléchargeable

Dictées téléchargeables par l'app Dictée, en plus de celles embarquées dans l'APK.
Servi par [jsDelivr](https://www.jsdelivr.com/), avec `raw.githubusercontent.com` en secours.

Ce repo est une **sortie de publication** : on ne l'édite pas à la main. Les
dictées sont préparées dans le repo de l'app (sources, audio, image, tests), puis
publiées ici par `scripts/contenu/publier.py` du repo de l'app.

## Contenu

```
catalogue.json      liste des dictées téléchargeables
images/ID.svg       illustration, affichée avant tout téléchargement
dictees/ID.zip      paquet de la dictée : ID_full.mp3, ID_N.mp3, ID_N_slow.mp3
```

## URLs

- Catalogue, lu sur la branche (cache vidé à chaque push par
  `.github/workflows/purge.yml`) :
  `https://cdn.jsdelivr.net/gh/nicolasfavier/dictee-contenu@main/catalogue.json`
- Paquets et images, lus sur un tag immuable `vN` :
  `https://cdn.jsdelivr.net/gh/nicolasfavier/dictee-contenu@vN/dictees/ID.zip`
- Secours, si jsDelivr ne répond pas :
  `https://raw.githubusercontent.com/nicolasfavier/dictee-contenu/<ref>/<chemin>`
  (GitHub Pages ne sert pas les tags). L'app vérifie le sha256 de chaque paquet.

## Format du catalogue

```json
{
  "format": 1,
  "dictees": [
    {
      "id": 1001,
      "titre": "…",
      "auteur": "…",
      "niveau": 2,
      "index": 12,
      "minutes": 4,
      "nbSegments": 18,
      "texte": "… mot|29| …",
      "acces": "gratuit",
      "versionAppMin": 36,
      "version": "v1",
      "image": "images/1001.svg",
      "imageSha256": "…",
      "paquet": { "url": "dictees/1001.zip", "taille": 612345, "sha256": "…" }
    }
  ]
}
```

- `format` : version du format, l'app ignore un catalogue d'un format inconnu.
- `id` : 1000 et plus. Les ids inférieurs sont réservés aux dictées de l'APK.
- `acces` : `gratuit` ou `pass`.
- `versionAppMin` : `versionCode` minimal de l'app pour afficher la dictée.
- `version` : tag où lire `image` et `paquet`. Un fichier publié sous un tag ne
  change plus : pour corriger une dictée, on republie sous un nouveau tag.
- `texte` : même syntaxe que `assets/data/dictee.csv` (annotations `|n|`).

## Conditions d'utilisation

Public ne veut pas dire libre de droits : voir [CGU.md](CGU.md). Le contenu est
réservé à l'application Dictée, toute réutilisation est interdite sans
autorisation.

## Limites

jsDelivr refuse une version de repo de plus de 50 Mo. Au-delà d'une centaine de
dictées, demander un relèvement par une issue sur `jsdelivr/jsdelivr` (projet
éducatif), sans découper en plusieurs repos.
