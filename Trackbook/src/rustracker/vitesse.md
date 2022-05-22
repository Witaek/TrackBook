# Vitesse

Les messages portant les informations de vitesses ont un type-code égal à 19.

Les messages de vitesse sont contitués de la manière suivante : 


|                                                     | MSG   | BITS |
|-----------------------------------------------------|-------|------|
| **Type Code**                                       | 1-5   | 5    |
| **Sub-Type**                                        | 6-8   | 3    |
| **Intent change flag**                              | 9     | 1    |
| **IFR capability flag**                             | 10    | 1    |
| **Navigation uncertainty category for velocity**    | 11-13 | 3    |
| **Sub-Type specific fields**                        | 14-35 | 22   |
| **Source bit for vertical rate**                    | 36    | 1    |
| **Sign bit for vertical rate**                      | 37    | 1    |
| **Vertical rate**                                   | 38-46 | 9    |
| **Reserved**                                        | 47-48 | 2    |
| **Sign bit for GNSS and Baro altitudes difference** | 49    | 1    |
| **Difference between GNSS and Baro altitudes**      | 50-56 | 7    |


Dans le cadre de notre travail, tous ces champs ne sont pas utiles. On s'interresse particulièrement aux champs concernant la vitesse, la vitesse verticale ainsi que l'angle de piste des avions.

Les différents sous-types (Sub-type) permettent de distinguer les types de vitesses enregistrés ainsi que les types des avions (subsonniques et supersonniques).

| **Sub-Type** | Type vitesse | Type avion  |
|--------------|--------------|-------------|
| **1**        | GS           | Subsonnic   |
| **2**        | GS           | Supersonnic |
| **3**        | TAS or IAS         | Subsonnic   |
| **4**        | TAS or IAS     | Supersonnic |

On distingue plusieurs types de vitesses : 

<p style="text-align:justify;">

 <ul>
  <li> <p style="text-align:justify;"> <b>Indicated Air Speed (IAS) </b> = vitesse indiquée, c'est la vitesse directement lue dans le cockpit de l'avion, elle est mesurée grâce à des capteurs de pression et varie donc en fonction de l'altitude (baisse lorsque l'altitude augmente); </p></li>
  <li> <p style="text-align:justify;"> <b>True Air Speed (TAS) </b>= c'est la vitesse réelle de l'avion relativement à l'air qui l'entoure;</p> </li>
  <li><p style="text-align:justify;"> <b>Ground Speed (GS) </b> = vitesse au sol, il s'agit de la vitesse réelle corrigée qui tient compte des vents.</p>
</li>
</ul> 

</p>

<p style="text-align:justify;">

Puisque qu'il n'y a actuellement plus d'avions supersonniques en circulation (retrait du concorde en 2003), les sous-types 2 et 4 n'ont pour l'instant pas d'utilité. </p>

## Décodage vitesse

### Sous-type 1


La partie du message de vitesse utile pour le décodage de la vitesse sont les bits 14 à 35 décomposés de la manière suivante : 

|                                      |  | **MSG** | **BITS** |
|------------------------------------------|------|---------|----------|
| **Direction pour la composante de vitesse E-O** | Dew  | 14      | 1        |
| **Composante de vitesse Est-Ouest**         | Vew  | 15-24   | 10       |
| **Direction pour la composante de vitesse N-S** | Dns  | 25      | 1        |
| **Composante de vitesse Nord-Sud**       | Vns  | 26-35   | 10       |

<p style="text-align:justify;">

On calcule la vitesse à partir des composantes Vew et Vns ainsi que des directions Dew et Dns.

On calcule également le track angle (angle de piste) qui permet d'orienter les avions sur la carte à l'aide de ces valeurs.
</p>

### Sous-type 3

<p style="text-align:justify;">

Les messages de sous-type 3 sont émis lorsque la vitesse au sol de l'avion n'est pas connue (par exemple quand le positionnement par satellite n'est pas disponible). Dans ce cas, la vitesse et le track angle sont directement encodés dans le message de la manière suivante : 

</p>

|                                      |  | **MSG** | **BITS** |
|------------------------------------------|------|---------|----------|
| **Bit de status pour le cap magnétique** | SH   | 14      | 1        |
| **Cap magnétique**                       | HDG  | 15-24   | 10       |
| **Type de vitesse (IA or TAS)**          | T    | 25      | 1        |
| **Vitesse**                              | AS   | 26-35   | 10       |
