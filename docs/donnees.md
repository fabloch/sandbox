


## MNT Baie de Quiberon

http://diffusion.shom.fr/pro/amenagement/mnt-cotier-morbihan-tandem.html

Ce MNT est disponible avec deux références verticales:
- niveau moyen (NM);
- niveau des plus basses mers astronomiques (PBMA).
Le niveau des plus basses mers astronomiques est le **zéro hydrographique**.

Ce MNT présente des points sur une maille de 20 mètres.

### Echelle Carte
Taille Sandbox : 988mm x 737mm
Ratio: 1.430

| Echelle Carte | 1 mm (Sandbox) = distance carte (en mètres) | Couverture                                                  | largeur (kms) | hauteur (kms) | Mode     |
| ------------- | ------------------------------------------- | ----------------------------------------------------------- | ------------- | ------------- | -------- |
| 25:000        | 25                                          | Golfe du Morbihan, Auray, Vannes, La Trinité, Port-Crouesty | 24,7          | 18,425        | Paysage  |
| 12:500        | env 12 mètres                               | Vannes et ses abords dans le Golfe (Arradon, Séné)          | 12,35         | 9,21          | Paysage  |
| 1:6250        | env 6 mètres                                | Rivière d’Auray du Bono à Saint-Goustan                     | 6,175         | 4,60          | Portrait |

Le MNT Baie de Quiberon devrait être suffisant pour définir des contours pour la carte du Golfe du Morbihan, qui inclut Auray et Vannes. Ce MNT contient aussi toute la presqu’île de Quiberon, qui peut être un exemple spectaculaire pour la montée des eaux.

Pour une carte au 1:6000, un point de ce MNT tous les 3 mm dans la sandbox.

### Altitude
Sur le MNT Baie de Quiberon

NODATA: 1387509
MINVALUE: -79,09
NEGATIVE: 7365004
MAXVALUE: 93,52
POSITIVE: 3935248
ZERO: 1489

( Etonnant, distribution relativement uniforme des points sur une échelle de 1 mètre pour les couches de 0 à 15m
0m 154154  1m 140489 2m 124185 3m 122682 4m 115302 5m 176387 6m 140593 7m 110181
8m 107326 9m 106435 10m 105670 11m 101992 12m 102564 13m 100164 14m 104140 15m 102593 )

### Marée
Au zéro hydro des fichiers il convient d’ajouter les hauteurs de marée.
Les hauteurs de marée peuvent être très variables dans le golfe entre les différents points de référence.
Ainsi Port-Navalo et Auray peuvent voir des Pleine Mer à plus de 5 mètres quand les plus grandes marées pour Vannes et Arradon sont de 3 mètres avec des horaires différents de 2 heures.

|     | Vannes | Arradon | Port-Navalo | Auray  |
| --- | ------ | ------- | ----------- | ------ |
| 115 |        |         |             |        |
| BM  | 0.15 m | 0.15 m  | 0.13 m      | 0.27 m |
| PM  | 3.30 m | 3.00 m  | 5.53 m      | 5.12 m |
| 30  |        |         |             |        |
| BM  | 1.10 m | 0.88 m  | 2.03 m      | 1.95 m |
| PM  | 2.18 m | 1.99 m  | 3.80 m      | 3.31 m |

### Estran
Retrouver la ligne de plus haute mer astronomique (PHMA).
Les deux lignes PBMA et PHMA définissent l’Estran.

### Isobathes et lignes de côte
Depuis QGIS
Lignes de contour sur le MNT de mètre en mètre.
Considérer une échelle d’altitude variable.
En dessous de 0: ne conserver que deux isobathes, à -2 puis -5 mètres (comme pour les cartes marines)
Au dessus de 0: jusqu’à 15 mètres, on peut travailler sur les lignes de côte de 1 mètre puis passer à des lignes de côtes plus espacées.
