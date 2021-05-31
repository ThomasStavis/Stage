# Stage : réagencement d'os

Réalisé par Stavis Thomas (L2 Inforatique AMU)

Lien git :

---

# Problème

### Contexte

Après les désastres humanitaires (naturels, industriels, terroristes), de nombreux corps humains sont retrouvés dans des conditions déplorables. Il différentes autorités identifient alors les corps à l'aide des "restes". Pour ce faire, un procédé manuel, long et coûteux est mis en oeuvre dans la recherche et la reconstitution de tissus, organes et os, pour maximiser les chances de réussir une identification.

### Sujet

Seulement les os nous intéressent. La méthode actuelle de reconstitution consiste à rassembler des fragments d'os et à résoudre un puzzle dont on ne connait ni la géométrie 3D, ni le nombre de pièces. Un collage minitieux, long et difficilement réversible des fragments d'os est effectué lorsque ceux-ci s'emboîtent. Lorsque l'os est reconstitué au mieux, son analyse est alors effectuée.

Nous voulons alors informatiser ce processus pour des questions de coût et de temps.

Actuellement, à l'aide de fichier dicom transformés en maillage en format stl, la méthode semi-manuelle suivante est employée :
1. ouvrir ces maillages dans CoudCompare
2. trouver des emboîtements possibles entre 2 fragments
3. transformer leur maillages en nuages de points (10000 points, avec une taille de 5, renommage)
4. calculer la rugosité des points (paramètre de noyau (kernel) à 5)
5. garder uniquement ceux dont la rugosité dépasse 1 (création de nouveaux nuages, renommage)
6. identifier des points d'accroches entre les 2 fragments
7. calculer la position idéale des fragments en fonction de ces points
8.  déplacer les nuages de points initiaux aux bonnes coordonnées
9.  selectionner l'ensemble des points de ces 2 nuages qui forment la fusion
10. calculer une nouvelle fois la position idéale
11. appliquer de nouveau un déplacement aux bonnes coordonnées
12. fusionner les 2 nuages de points 
13. supprimer les points superflus
14. refaire les maillages

Ce processus étant long, il serait possible de fusionner certaines étages en codant un plugin pour CloudCompare. Les seules étapes qu'il resterait seraient : 1, 3-4-5, 2-6, 7-8-9-10-11 et 12-13-14.

### Organisation

Nous allons dans un premier temps nous pencher sur la fusion des étapes 3-4-5 en supposant que nous avons déjà trouver des emboîtement possibles et que nous trouverons facilement les points d'acchoches par la suite.

---

# Gestion du projet