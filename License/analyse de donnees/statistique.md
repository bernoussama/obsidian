 
## Frequence
 
 $$
 f_{i}=\frac{n_{i}}{N}
 $$
![[Pasted image 20241019150524.png]]
![[Pasted image 20241019150809.png]]

## Cas de variable qualitative
### diagramme en barres
![[Pasted image 20250111133838.png]]
### diagramme circulaire
![[Pasted image 20241019154258.png]]
### Angle de modalite
### $$
\alpha = f_{i} \times 360 = \frac{n_{i}}{N} \times 660
$$

![[Pasted image 20250111144708.png]]
## Moyenne arithmétique
### $$
\overline{X} = \frac{1}{N} \sum_{i=1}^{k} n_i c_i = \sum_{i=1}^{k} \frac{n_i}{N} c_i = \sum_{i=1}^{k} f_i c_i

$$
$n_{i}$ :
$c_{i}$ : centre 
## Centre
$$
c_{i} = \frac{\text{borne inferieur} +\text{borne superieur}}{2}
$$
ou:
$$
c_i = \frac{l_i + u_i}{2}
$$
- $l_{i}​$ est la **borne inférieure** de la $i$-ème classe.
- $u_i$​ est la **borne supérieure** de la $i$-ème classe.

## Quartiles

#### Serie continue:
 classe contenant premiere valeur $> \alpha \times N$  contient le quartile.
## Mediane
### Serie non continue:
#### serie paire

### 1er quartile
### $$
Q_1 = a_{i-1} + (a_i - a_{i-1}) \times \frac{0.25N - N_{q-1}}{N_q - N_{q-1}}
$$
- `aᵢ₋₁` : La borne inférieure de la classe contenant le premier quartile.
- `aᵢ` : La borne supérieure de la classe contenant le premier quartile.
- `(aᵢ - aᵢ₋₁)` : L'amplitude (ou la largeur) de la classe contenant le premier quartile.
- `0.25N` : La position théorique du premier quartile (25% de l'effectif total).
- `Nq₋₁` : L'effectif cumulé _avant_ la classe contenant le premier quartile.
- `Nq` : L'effectif cumulé _jusqu'à_ la classe contenant le premier quartile (incluse).
- `(0.25N - Nq₋₁)` : Le nombre d'observations à "parcourir" à l'intérieur de la classe pour atteindre Q1.
- `(Nq - Nq₋₁)` : L'effectif de la classe contenant le premier quartile.
### 3eme quartile
### $$
Q_3 = b_{i-1} + (b_i - b_{i-1}) \times \frac{0.75N - N_{l-1}}{N_l - N_{l-1}}
$$
