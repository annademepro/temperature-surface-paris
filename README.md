# Température de surface et densité du logement : Paris et petite couronne

Projet universitaire réalisé en binôme (Université Paris Cité, L3, 2023) par **Anna Deme** et **Xiabing Chen**.

Ce projet croise des **températures de surface calculées à partir d'images satellites Landsat 8** et des **données socio-économiques** (population, logements, taux de pauvreté, végétation) à l'échelle de **Paris et de la petite couronne** (départements 75, 92, 93 et 94).

## Objectif

Observer comment la température de surface évolue entre 2013 et 2021 et la mettre en regard de la densité de population et de logements dans les quatre départements.

## Données

| Donnée | Source |
|---|---|
| Images Landsat 8 (bande 10 thermique, bandes 4 et 5) | USGS EarthExplorer |
| Population et logements, recensements (1968 à 2017) | INSEE, traitements Apur |
| Chiffres clés socio-économiques par département | Apur (opendata.apur.org) |
| Fonds de carte des départements | [à compléter : source du fichier .shp] |

Dates des images : 19 juillet 2013 et 22 juillet 2021.

## Méthode

**Dans QGIS** : calcul de la température de surface (LST) en six étapes, puis découpage des rasters selon les départements.

1. Luminance spectrale TOA : `L = ML × Qcal + AL` (bande 10)
2. Température de luminosité : `BT = K2 / ln(K1 / L + 1) − 273,15`
3. NDVI : `(Bande 5 − Bande 4) / (Bande 5 + Bande 4)`
4. Proportion de végétation : `Pv = ((NDVI − NDVImin) / (NDVImax − NDVImin))²`
5. Émissivité : `ε = 0,004 × Pv + 0,986`
6. Température de surface : `LST = BT / (1 + (0,00115 × BT / 1,4388) × ln(ε))`

Les formules suivent le tutoriel cité en bibliographie.

**Dans Excel** : téléchargement des données de recensement, filtrage des départements 75, 92, 93 et 94, courbes d'évolution et graphiques.

**Dans Magrit** : cartes de stocks et de ratios (densité du logement, bâti consacré aux activités).

**Dans QGIS** : jointure entre les tableaux Excel et les fichiers .shp, cartes thématiques du nombre de logements par département.

## Résultats

- Cartes de la température de surface en juillet 2013 et en juillet 2021.
- Courbes de l'évolution de la population et des logements par département depuis 1968.
- Cartes du nombre de logements par îlot et par département (2017).
- Tableau comparatif des chiffres clés des quatre départements.

## Limites

- Les températures ne sont pas disponibles sous forme de tableau Excel : l'analyse reste une **mise en regard** et non une corrélation statistique.
- Les images Landsat 8 disponibles datent de 2013 : impossible de remonter avant cette date.
- Les valeurs minimales de la carte de 2021 (autour de -9 °C) paraissent aberrantes en juillet. Elles proviennent probablement de nuages, de zones d'eau ou de valeurs manquantes et devraient être masquées.

## Outils

QGIS · Magrit · Excel · données Landsat 8

## Contenu du dépôt

```
data.gouv.fr
presentation/   présentation du projet (PDF)
cartes/         cartes exportées (PNG)
donnees/        tableaux de données (Excel ou CSV)
```

## Références

- USGS EarthExplorer : earthexplorer.usgs.gov
- Apur, données ouvertes : opendata.apur.org
- Tutoriel de calcul de la LST avec Landsat 8 : giscrack.com
- Z. Coraline et P. Olivier, *Îlot de chaleur urbain : conséquences sur les bâtiments*, ECIC, 2014
