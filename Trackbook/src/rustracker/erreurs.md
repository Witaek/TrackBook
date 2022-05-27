# Gestion des erreurs de positions :

<p style="text-align:justify;">L’algorithme de CPR présente un avantage certain. Toutefois, il peut comporter des erreurs. Ces erreurs sont principalement dû au décodage des indexes des zones de latitude et longitude, et à d’autres calculs sensibles. Principalement lors de la transition de l’avion entre deux zones distinctes.</p>

<p style="text-align:justify;">Comme présenté par la NASA [biblio], ces erreurs sont dû à l’utilisations de nombre flottant. Leur code fournit des preuves en temps réel de leurs résultats grâce à l’ACSL.</p>

<p style="text-align:justify;">Cependant, nous devons trouver un moyen de traiter ces erreurs lorsqu’elles surviennent. </p>

<p style="text-align:justify;">Plusieurs solutions sont suggérées dans l’ouvrage de Junzi Sun, dont la cohérence de la position de l’avion en fonction de la portée de l’antenne. Cette solution n’est pas envisageable pour nous car les récepteurs communiquent de façon anonyme avec le serveur.</p>

<p style="text-align:justify;">En observant les positions aberrantes que nous obtenions, on a remarqué une oscillation de la trajectoire. Nous avons donc imaginé une autre solution, qui est un test de cohérence. </p>

<p style="text-align: center;">
<img  typeof="foaf:Image" src="../images/erreur.png"  alt="" title="erreur">  
</p>

<p style="text-align:justify;">Comme présenté postérieurement, les messages de vitesses donnent une information : le « Track angle », qui est le cap suivi par l’avion (entre 0° et 360°). Or ce cap peut aussi être obtenu par une déduction à partir des deux dernières positions connues qui créent un vecteur dont la direction est égale au cap (bien que plus imprécis).</p>

<p style="text-align:justify;">En comparant les deux résultats obtenue sur les toutes premières positions décodées de l’avion, nous pouvons détecter ces oscillations qui sont impossible avec un cap constant et donc éliminer ces trajectoires problématiques. </p>

# Mise en pratique :

<p style="text-align:justify;">Cette comparaison de cap était initialement effectuée sur tous les points de la trajectoire, cependant le calcul est lourd et a entraîné un retard du serveur sur les messages reçus. Nous avons donc fait le choix de tester seulement les premières positions de l'avion.</p>