---
---

# la page de suivi de la Sandbox

## Construction du bac à sable
Construction du bac à sable (75*100 à l’intérieur) et potences pour fixer caméra et projecteur Benq

La hauteur X de la camera est de 40” soit 101,6 cm en prenant comme base le niveau moyen du sable, [source image](http://idav.ucdavis.edu/~okreylos/ResDev/SARndbox/ARSandboxLayout.png) extraite du tuto officiel - soit une altitude de 40” (101,6 cm) pour un bac de 30” (76,2 cm)

**Le bac à sable est construit**, avec une potence qui reçoit la caméra
Le projecteur de focale trop longue est installé sur une table et projette sur le bac au moyen d’un miroir.

- [x] test de sandboxAR
- [x] nouveau test en reprenant le calibrage et calibrage camera et videoprojecteur - voir si le réglage trapèze permettra que la kinect reste hors du champ de projection
- [x] le sable est disponible à la fabrique, à tamiser pour supprimer les débris végétaux.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_5B8C07C20B183E063D3D8662B6D60E82EBB08EB27AA192522639B4089E5C5D95_1537469626199_Golfe.jpg)

## Fabrication maquette qui remplacera le sable

### Les données du Golfe du Morbihan
- [x] Création d’un compte shom pour récupérer les données litho3D du golfe du morbihan
![](https://d2mxuefqeaa7sj.cloudfront.net/s_DA449CE77163142EBDC65072BB3CF6B42770A9D32263ADEAA96AE5F3316FD513_1537430962079_mnt-morbihan.png)

Auray et Vannes ne sont pas inclus dans les données gratuites.

La limite de la rivière d’Auray au nord s’arrête au Boursul au sud des “vides-bouteilles”.

Il faut demander à nos mairies respectives (ou écoles, universités…) de récupérer les dalles manquantes.
- [ ] Auray : 0245_6750, 0250_6750, 0255_6750 et 0245_6755,  0250_6755, 0255_6755,
- [ ] Vannes :

![couverture Lidar du golfe du morbihan](https://d2mxuefqeaa7sj.cloudfront.net/s_D79BECC53225E2841F3159439FDBF3EAEF8D2B1629C67346862060EAB087717F_1539011329501_zone+morbihan+ign+2.png)

- [ ] vérifier si  les 6 carrés dessinés sur la carte suffisent.
- [ ] Reprise du diaporama de jean noel pour faire un version de présentation simplifiée afin de contacter institutionels ou assos ou presse

#### Litto3D
Les relevés Litto3D du Shom https://diffusion.shom.fr existent au pas de 5m et 1m. Ces relevés MNT sont organisés en fichiers couvrant 1 km². C’est-à-dire 200 lignes de 200 colonnes pour le pas de 5m et 1000 lignes de 1000 colonnes pour le pas de 1m. La résolution verticale est le cm. Les données sont en ascii. Une présentation alternative en nuage de points permet de qualifier chaque point suivant le type de relevé qui a permis de le déterminer.
L’accès à ces fichiers est gratuit.

Chaque carré de 1km² est décrit par 3 fichiers. Chaque km² est désigné par ses coordonnées en km qui pourraient être reprises pour définir les zones qui nous intéressent.
sur http://diffusion.shom.fr/loisirs/catalogsearch/result/?q=morbihan on a ça :

----------

Intervention sur le soft pour pouvoir augmenter le niveau par pas de x cm (50, 100 ?)
et mode de gestion de l’interactivité à cogiter (page web ?, sur mini écran, sur pc maitre, potentiomètre,  ? possibilités d’ajouter des paramètres influant sur la hauteur choisie (dépression, vent? et ou déterminant la hauteur prévue (réchauffement en degré)

#### Courbes de niveaux

- [ ] Transformation ou utilisisation des fichiers MNT ou des nuages de points pour générer les courbes de niveaux sous forme d’image utilisable par la découpe laser.
- [ ] Le logiciel ignmap sait lire les données MNT (entre autres) http://ignmap.ign.fr/spip.php?rubrique3 je l’ai installé sur le PC25 sur lequel on a le logiciel sandbox- travaille en relation avec geoportail.

Bon, il faut s’emparer du logiciel pour voir ce qu’on peut en faire…
nb : il y a un outil (assez rustique, disent-ils) qui s’appelle “montées des eaux” et qui ne semble pas très exact pour les rivières.

- [ ] On peut regarder aussi du coté de [QGIS](https://www.qgis.org/fr/site/)
![contours avec méthode Vernant](https://d2mxuefqeaa7sj.cloudfront.net/s_EB4BDC1A5F42E96687F69322712ECB7CBCE7B663CDEFFA31A5E43D419DF58E4F_1541836425749_contour.png)

##### QGIS
**Système d'Information Géographique Libre et Open Source**
https://qgis.org/ubuntu/pool/main/q/qgis/
idem : il faut s’emparer du logiciel pour voir ce qu’on peut en faire…
voir ICI : http://www.pages-perso-philippe-vernant.univ-montp2.fr/Philippe_Vernant/QGIS-MNT.html

Bonne nouvelle :
Qgis permet d’extraire les contours d’altitudes choisies → afin de sortir des images de découpe par couple (par exemple, couche 10 m et couche 11m afin de découper la couche 10 m et d’y graver la couche 11m qu’on pose dessus après (la bonne idée de Ludo)
la méthode →  [voir ici](https://mesange.educagri.fr/htdocs/sigea/supports/QGIS/distance/perfectionnement/M09_Traitement_donnees_raster_gen_web/co/40_N2_Outils_Raster_MNT.html)

Output : fichier Shapefile (. SHP) convertible en SVG ensuite

- [ ] aussi du coté de **SandboxAR**
- [ ] Entrer les relevés MNT dans la sandbox.

À priori à minima port de Vannes et d’Auray ? du moins centré sur ces zones - l’étendue  reste à calculer en fonction de l’épaisseur de la maquette désirée et du type de rendu désiré (avec plus ou moins de marches entre chaque épaisseur de medium. Un des problèmes est que les zones avec rivière ne fonctionnenent pas comme les zones cotières : voir la carte d’auray avec une montée des eaux de 5 mètres ( http://flood.firetree.net/?ll=47.6609,-2.9790&zoom=16&m=1&type=hybrid ou encore sur climate central avec une montée de 3 m : https://ss2.climatecentral.org/#15/47.6643/-2.9778?show=satellite&projections=0-K14_RCP85-SLR&level=3&unit=meters&pois=hide

![](https://d2mxuefqeaa7sj.cloudfront.net/s_DA449CE77163142EBDC65072BB3CF6B42770A9D32263ADEAA96AE5F3316FD513_1537278864933_port-auray5m-flood.firetree.net.png)

![](https://d2mxuefqeaa7sj.cloudfront.net/s_DA449CE77163142EBDC65072BB3CF6B42770A9D32263ADEAA96AE5F3316FD513_1537279174438_part-auray.png)


[ ]
#### Des essais sur la rivière d’Auray donnent :
![](https://d2mxuefqeaa7sj.cloudfront.net/s_32CC047DCDFE631499662F9F9BEC0E3C68AB154930DC38BBC9C619CE5C281725_1540657156259_HAUSSE_NIVEAUX_10m.png)

La rivière est très confinée dans un relief franc : l’effet visuel entre +4m et +10m ne semble pas très spectaculaire. Préférer une zone avec des reliefs peu marqués (marais ?)

### Découpe Prototype maquette MDF

SVG de courbes de niveau pour la zone d’Auray (données SRTM + IGN). Il y a 12 tranches espacées de 5m pour représenter les reliefs de 0 à 55m.
Dimensions prototype :

- X 700mm
- Y 700mm
- Z : 12*epaisseur MDF : donc avec du MDF6mm, 72mm d’épaisseur
![Simulation de l’empilement des 12 tranches horizontales](https://d2mxuefqeaa7sj.cloudfront.net/s_32CC047DCDFE631499662F9F9BEC0E3C68AB154930DC38BBC9C619CE5C281725_1541853328688_file.png)


#### RGE ALTI 1m

Pour Auray, si on souhaite une résolution du mètre, l’IGN propose les relevés RGE ALTI 1m qui sont [gratuits pour les services publics et payant pour les asso](http://www.professionnels.ign.fr/gratuite-des-donnees) à raison de 50€ de mise à disposition + 4€ par km²
Pour le maquettage en médium existe-t-il un programme réalisant l’analyse des iso et leur conversion en fichier CAO.


Si l’on souhaite utiliser la projection de ces zones pour un nivellement du sable à la main tel que montré dans https://youtu.be/nPba_9WzdjI?t=11m37s  un programme est nécessaire pour entrer les relevés MNT dans la sandbox. Le programme conv-asc convertit les données MNT (par ex de l’IGN ou Litto) en données chargeables dans la sandbox. Placer le répertoire de conv-asc dans :
src/SARndbox/etc/SARndbox/conv-asc
Le chargement des données MNT se fait par le menu système vrui qui apparaît lorsqu’une touche du clavier est pressée. Cette touche devient alors un raccourci pour activer/désactiver une fonction. La fonction à sélectionner dans le menu système est “show DEM” .
L’interaction n’est pas intuitive :  

1. placer la souris sur la fenêtre de la sandbox
2. appuyer sur une touche du clavier et la maintenir appuyée
3. placer la souris sur show DEM
4. relacher la touche du clavier
5. un menu de choix de fichier apparaît
6. sélectionner le fichier normalement avec la souris.

Le programme de conversion dans le répertoire conv-asc est le fichier main.cpp. A la ligne 59, on peut modifier le coefficient multiplicateur appliqué aux données. Ne pas oublier de recompiler après modification.
Exemple de tracés obtenus avec le fichier :
 L3D-MAR_FRA_0252_6740_MNT5_20150519_L93_RGF93_IGN69
Pour des altitudes différentes :

![](https://d2mxuefqeaa7sj.cloudfront.net/s_5B8C07C20B183E063D3D8662B6D60E82EBB08EB27AA192522639B4089E5C5D95_1540908280948_geoportail+_0252_6740.png)
![](https://d2mxuefqeaa7sj.cloudfront.net/s_5B8C07C20B183E063D3D8662B6D60E82EBB08EB27AA192522639B4089E5C5D95_1540908280404_L3D_0252_6740_1.png)
![](https://d2mxuefqeaa7sj.cloudfront.net/s_5B8C07C20B183E063D3D8662B6D60E82EBB08EB27AA192522639B4089E5C5D95_1541962029366_L3D_0252_6740_1b.png)

![](https://d2mxuefqeaa7sj.cloudfront.net/s_5B8C07C20B183E063D3D8662B6D60E82EBB08EB27AA192522639B4089E5C5D95_1540908280505_L3D_0252_6740_3.png)
![](https://d2mxuefqeaa7sj.cloudfront.net/s_5B8C07C20B183E063D3D8662B6D60E82EBB08EB27AA192522639B4089E5C5D95_1540908280521_L3D_0252_6740_4.png)
![](https://d2mxuefqeaa7sj.cloudfront.net/s_5B8C07C20B183E063D3D8662B6D60E82EBB08EB27AA192522639B4089E5C5D95_1540908280538_L3D_0252_6740_5.png)

![](https://d2mxuefqeaa7sj.cloudfront.net/s_5B8C07C20B183E063D3D8662B6D60E82EBB08EB27AA192522639B4089E5C5D95_1540908280549_L3D_0252_6740_6.png)
![](https://d2mxuefqeaa7sj.cloudfront.net/s_5B8C07C20B183E063D3D8662B6D60E82EBB08EB27AA192522639B4089E5C5D95_1540908280590_L3D_0252_6740_7.png)


Note : les tracés noirs sont à “oublier” car ils proviennent du bruit de la Kinect sur un fond plat. Les différentes altitudes ont été obtenues en faisant varier le paramètre : demVerticalShift et la zone blanche (zone de transition entre le bleu et le rouge) a été réduite en portant le paramètre demVerticalScale à 100.
Plus d’info dans ce topic : https://arsandbox.ucdavis.edu/forums/topic/dem-help/

Quelques remarques :

1. les fichiers MNT de l’IGN ou L3D du SHOM décrivent des zones carrées. La sandbox adapte les fichiers d’entrée suivant sa résolution qui est rectangulaire. Il convient donc de sélectionner dans le fichier MNT les points à représenter avec le même rapport Lxl.
2. La zone à afficher peut provenir de plusieurs fichiers et il faut juxtaposer les données de ces différents fichiers.
3. Les points non renseignés (nodata_value) des fichiers MNT doivent être modifiés pour les homogénéiser avec les points adjacents.

Ces remarques permettront de spécifier les fonctions que devra réaliser le programme de conversion.

#### MNT Baie de Quiberon

http://diffusion.shom.fr/pro/amenagement/mnt-cotier-morbihan-tandem.html

Ce MNT est disponible avec deux références verticales:
- niveau moyen (NM);
- niveau des plus basses mers astronomiques (PBMA).
Le niveau des plus basses mers astronomiques est le **zéro hydrographique**.

Ce MNT présente des points sur une maille de 20 mètres.

##### Echelle Carte
Taille Sandbox : 988mm x 737mm
Ratio: 1.430

| Echelle Carte | 1 mm (Sandbox) = distance carte (en mètres) | Couverture                                                  | largeur (kms) | hauteur (kms) | Mode     |
| ------------- | ------------------------------------------- | ----------------------------------------------------------- | ------------- | ------------- | -------- |
| 25:000        | 25                                          | Golfe du Morbihan, Auray, Vannes, La Trinité, Port-Crouesty | 24,7          | 18,425        | Paysage  |
| 12:500        | env 12 mètres                               | Vannes et ses abords dans le Golfe (Arradon, Séné)          | 12,35         | 9,21          | Paysage  |
| 1:6250        | env 6 mètres                                | Rivière d’Auray du Bono à Saint-Goustan                     | 6,175         | 4,60          | Portrait |

Le MNT Baie de Quiberon devrait être suffisant pour définir des contours pour la carte du Golfe du Morbihan, qui inclut Auray et Vannes. Ce MNT contient aussi toute la presqu’île de Quiberon, qui peut être un exemple spectaculaire pour la montée des eaux.

Pour une carte au 1:6000, un point de ce MNT tous les 3 mm dans la sandbox.

##### Altitude
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

##### Marée
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

##### Estran
Retrouver la ligne de plus haute mer astronomique (PHMA).
Les deux lignes PBMA et PHMA définissent l’Estran.

##### Isobathes et lignes de côte
Depuis QGIS
Lignes de contour sur le MNT de mètre en mètre.
Considérer une échelle d’altitude variable.
En dessous de 0: ne conserver que deux isobathes, à -2 puis -5 mètres (comme pour les cartes marines)
Au dessus de 0: jusqu’à 15 mètres, on peut travailler sur les lignes de côte de 1 mètre puis passer à des lignes de côtes plus espacées.
