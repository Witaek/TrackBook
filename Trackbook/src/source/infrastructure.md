# Infrastructure

<p style="text-align:justify;">
Comme présenté précédemment, l'architecture mise en place implique que le code de *SOURCE* soit installé sur une station, en l'occurence un raspberry, qui soit lui même connecté à une anntenne.</p>

<p style="text-align:justify;">
Nous l'avons mis en pratique, en installant une antenne spécialisé pour l'ADS-B sur le toit d'une maison située près de Castres dans le Tarn. Les conditions d'installation font qu'elle possède une meilleure réception vers l'Ouest (en théorie).</p>

<p style="text-align: center;">
<img  typeof="foaf:Image" src="../images/antenne_irl.jpg"  alt="" title="antenne">  
</p>

<p style="text-align:justify;">
Cette antenne est alors connectée à un filtre 1090MHz (1), puis au dongle RTL-SDR (2) qui s'assure de l'échantillonage. La connexion éthernet permet de transmettre au serveur situé à Evry les messages binaires reçus.</p>

<p style="text-align: center;">
<img  typeof="foaf:Image" src="../images/source.png"  alt="" title="raspberry">  
</p>

# Performance de l'antenne
<p style="text-align:justify;">
On observe une très bonne performance de l'antenne. Assurant une bonne réception dans les 300km au sud, voir 500km</p>

<p style="text-align: center;">
<img  typeof="foaf:Image" src="../images/diagramme.png"  alt="" title="reception">  
</p>