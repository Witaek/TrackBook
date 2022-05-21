# Contexte

<p style="text-align:justify;">
Le résultat finale présente sous forme de carte interactive des avions, toutefois, l’information a suivit un long processus avant de pouvoir être présentée sous une forme compréhensible pour l’utilisateur.

Nous allons donc nous intéresser au voyage d’un message ADS-B.

Comme nous l’avons spécifié en introduction, l’*Automatic Dependent Surveillance-Broadcast* (ADS-B) est un mode de communication qui sert au contrôle aérien.

Les deux premières lettres de l’acronyme permettent de comprendre les enjeux du formatage et du mode de transmission des messages.

*« Automatic »* signifie que les messages sont envoyés automatiquement, il n’est pas nécessaire de solliciter le transpondeur de l’avion pour obtenir une réponse (ce qui se fait dans d’autre méthode de contrôle aérien). Cela impose donc aussi d’avoir un programme suffisamment performant pour soutenir les flows de messages.

*« Dependent »* caractérise la provenance de ces informations. Tout est transmis par l’avion lui-même. Par exemple pour sa position, il la défini à partir de son système GPS embarqué avant de la transmettre. L’implication directe concerne le formatage des messages : il faut, dans un nombre de bits limités, transmettre suffisamment d’informations pour lier le message à l’avion et donner des informations suffisamment précises, et diverses (positions, vitesse, numéro de vol, …)

# Format

Ainsi, le format d’un message ADS-B se présente sous la forme suivante :

Il comporte 112 bits, divisés en parties distinctes, chacune portant des informations spécifiques :

* **[0 ; 4] : Downlink format :** C’est le format de transmission, on ne s’intéresse ici qu’au 17, qui est le plus largement utilisé dans l’aviation civile.

* **[5 ; 7] : Capabilty :** C’est un champ à utilisation technique que l’on traite techniquement du programme mais dont l’utilité pour un utilisateur lambda est faible, le résultat n’est dans pas présenté dans l’interface graphique (il permet d’obtenir notamment l’importance des tourbillons marginaux créés par l’avion, et qui sont un phénomène dangereux pour un autre avion situé derrière, et est donc utilisé par les contrôleurs pour assurer une bonne séparation.

* **[8 ; 31] : adresse ICAO :** C’est l’élément le plus important du message, il s’agit d’un code hexadécimal et unique à l’avion tout au long de sa « vie ». Ce code étant unique et se trouvant dans tous les messages, c’est lui qui va permettre de lier des messages reçus indépendamment et à l’avion émetteur.

* **[32 ; 87] : data :** Ces 56 bits sont le cœur du message, c’est eux qui transportent l’information spécifique au vol à l’instant t. Les 5 premiers correspondent au « Type Code », qui nous indique le type de data reçu. Il peut s’agit de la vitesse, de la position, ou du numéro de vols, dont leurs formatages peuvent varier (nous le détaillerons plus tard).

* **[88 ; 111] : CRC :** Ces derniers bits correspondent au contrôle de redondance cyclique (CRC). Ils sont calculés à l’émission de façon à ce qu’une opération logique sur l’ensemble des 112bits donne un résultat spécifique, permettant ainsi de valider l’intégrité du message reçu. En effet, on reçoit de nombreux messages mais entre l’avion et notre antenne de réceptions, ils ont pu est dégradés d’une telle façon que l’information transportée est erronée. Maintenant que l’on connait ce qu’est un message ADS-B, nous allons pouvoir étudier tout son cheminement. Nous utiliserons par la suite le terme anglais de Squitter pour désigner un tel message.</p>