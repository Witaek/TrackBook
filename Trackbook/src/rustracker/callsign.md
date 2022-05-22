# Callsign

<p style="text-align:justify;">Le callsign permet d'identifier un avion en vol. A la différence de l'icao, le callsign n'est pas unique, plusieurs avions effectuant le même trajet à des moments différents auront le même callsign. La donnée du callsign est contenue dans les messages dont le type-code est compris entre 1 et 4. Un tel message est structuré de la manière suivante : </p>

| **Data** | **TC** | **CA** | **C1** | **C2** | **C3** | **C4** | **C5** | **C6** | **C7** | **C8** |
|----------|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------|
| **BITS** | 5      | 3      | 6      | 6      | 6      | 6      | 6      | 6      | 6      | 6      |

On retrouve le type code (TC) contenu dans les 5 premiers bits suivi de la catégorie de l'engin (CA). Ensuite, chaque bloc de 6 bits permet de déterminer un caractère du callsign.

Pour trouver le callsign il suffit de convertir chaque bloc de 6 bits en décimal, les 8 nombres obtenus sont alors les indices des caractères du callsign dans l'alphabet suivant : 

>#ABCDEFGHIJKLMNOPQRSTUVWXYZ#####################0123456789######

Par exemple, le callsign associé au message suivant est **KLM1023** : 

| **MSG**  | **00100** | **000** | **001011** | **001100** | **001101** | **110001** | **110000** | **110010** | **110011** | **100000** |
|----------|-----------|---------|------------|------------|------------|------------|------------|------------|------------|------------|
| **DATA** | TC        | CA      | 11         | 12         | 13         | 49         | 48         | 50         | 51         | 32         |
| **DATA** | 4         | 0       | K          | L          | M          | 1          | 0          | 2          | 3          | -          |
