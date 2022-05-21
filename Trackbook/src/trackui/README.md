# Trackui

<p style="text-align:justify;">L’interface graphique est codée en JavaScript. On utilise Leaflet qui est un package permettant de générer une carte. Cette carte affiche en temps réel les avions dont la position est partagée.

Cependant comme ce n’est pas toujours le cas (selon le type de transpondeur de l’avion), et afin de présenter les informations supplémentaires tel que le numéro de vol, l’altitude et la vitesse, on a fait le choix d’ajouter un tableau contenant la liste des avions.

De plus, ce tableau dispose de code OACI « cliquable » pour les avions dont la position est visible sur la carte. Lorsque l’on clique sur un bouton, la carte se recentre alors sur l’avion sélectionné et affiche son icone et sa trajectoire dans une couleur différente afin de le mettre en valeur.

Enfin, la collecte des informations se fait en récupérant les informations du geojson généré par Rustracker toutes les 1,5 secondes. Le geojson est une FeatureCollection qui regroupe plusieurs Features qui sont nos avions. Ces Features ont pour ID le code OACI, et sont des LineString, c’est-à-dire que le champs geometry contient l’ensemble des points qui composent la trajectoire, puis dispose en attribut du reste des informations de l’avion.

En itérant sur toutes les Feature, on ajoute pour chacune un calque à la carte qui affiche la trajectoire, et l’icone que l’on oriente grâce au « track angle » (la route suivie par l’avion). Chacun de ses calques sont dans un même groupe de calque.

A chaque nouvelle réception des données du geojson, on vide alors ce groupe de calque afin de le reremplir avec les informations actualisées</p>