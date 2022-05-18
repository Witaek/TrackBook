# Introduction

<p style="text-align:justify;">L’ADS-B (Automatic Dependent Surveillance-Broadcast) est un système de contrôle du
trafic aérien. Un avion utilisant l’ADS-B détermine sa position par un système de positionnement satellite et
la renvoit cette dernière (ainsi que d’autres informations sur le vol, altitude, vitesse, modèle de l’avion, etc)
dans toutes les directions aux autres appareils disposant de l’ADS-B. Ces messages sont détectables, puis
démodulables, par toute personne à l’aide d’une clef TNT (tuner RTL2832U, 15€), utilisée en SDR (Soft-
ware Defined Radio), qui permet de définir les paramètres de réception, comme par exemple la fréquence,
depuis l’ordinateur. L’objectif du projet est d’utiliser ces messages envoyés par les avions, et de proposer
une interface graphique à l’utilisateur. Sur cette interface, on souhaite observer en temps réel l’ensemble
des avions à portée de notre antenne ; nous souhaitons également pouvoir observer la trajectoire des avions
ainsi que connaître les informations sur le vol (altitude, vitesse, moteur, ...).</p>

### Description du livrable minimal :  

* Intercepter, démoduler, interpréter des signaux ADS-B envoyés par plusieurs avions
* En extraire des informations sur la position, vitesse, modèle,...
* Utiliser ces données pour générer en temps réel une carte sur laquelle figurent les avions
* Possibilité d’obtenir les informations concernant le vol des avions sélectionnés
  
<br/>
<p style="text-align: center;">
<img  typeof="foaf:Image" src="images/exemple.png"  width="350" height="350" alt="" title="Foto: Edis Škulj/fkmladost.ba">  
</p>

<p style="text-align: center;">
    <b> Exemple de carte recherchée (FlightRadar24) </b>
</p>