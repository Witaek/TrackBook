# Rustracker

<p style="text-align:justify;">Le serveur est chargé du traitement des messages binaires qui sont reçus par une ou plusieurs sources.

Lorsque l’on reçoit un squitter, on commence par le découper dans le stocker sous forme de struct squitter, qui dispose de méthode permettant d’en récupérer les différentes sections.

A partir de son code OACI, on va associer le squitter à un nouvel objet avion (la struct plane), qui a pour attribut l’ensemble des informations utiles associées à un avion. Chaque avion sera ensuite stocké dans une hashmap ayant pour clef son code OACI. Associé un nouveau squitter reçu à un avion déjà existant dans notre structure de donnée sera alors plus efficace.

Une fois le squitter lié à l’avion, on en extrait les informations. En l’occurrence nous traitons 3 types de données : altitude, vitesse, et numéro de vol. Nous allons détailler séparément leurs analyses dans la section suivante.

# Opérationabilité

Maintenant que nous avons une structure de donnée avec toutes les informations exploitables, il faut pouvoir la rendre opérationnelle, c’est-à-dire que l’on soit en mesure de créer une carte interactive des avions. Nous avons fait le choix que le programme génère un geojson qui pourra être lu de manière passive par notre interface graphique.

Pour ce faire, on fait face à plusieurs enjeux :

- Pouvoir générer ce geojson à intervalle régulier, sans interrompre le processus de réception
des squitter.

- Être capable de retirer les avions qui sortis de notre champ de réception depuis un certains
temps.

Pour ces deux problèmes, nous avons décider d’utiliser de la programmation asynchrone. Deux threads vont être capables de communiquer avec le thread principal de réception des messages à travers des channels.

Le premier thread est chargé de gérer la durée de vie des avions. Il envoie un signal à notre thread principal toute les 30 secondes, dès que le thread principal reçoit ce signal, il va parcourir la hashmap contenant chaque avion, et mesurer depuis combien de temps il n’a pas reçu de nouveaux messages depuis plus de 30 secondes, alors on considère que l’avion est sorti de notre champ de réception, et est donc retiré de notre mémoire.

Le second thread lui génère le geojson. Un package de Rust spécialement créer pour les geojson propose une struct dans laquelle on stocke nos avions (avec moins d’information que notre struct plane détaillé plutôt, on ne mettra dans le geojson seulement celle utiles à l’interface graphique) et qui grâce à une méthode de conversion en string de cette struct, nous permet d’éditer le contenu de notre plane.geojson.</p>