 
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
### Variance
#### $$
V(X) = \frac{\sum^{n}_{i=1} (x_{i}-\bar{x})^2}{n}
$$
simplifie
#### $$
V(X) = \frac{\sum^{n}_{i=1} x_{i}^2}{n}-\bar{x}^2
$$
### Ecart type
$$
\sigma = \sqrt{ V(X) } 
$$

### Intervalle inter-quartile
$$
I = Q_{3} - Q_{1}
$$
### Intervalle inter-decile
il existe 4 intervalles:
$D_{9}-D_{1};D_{8}-D_{2};D_{7}-D_{3};D_{6}-D_{4}$


# Statistique descriptive bivariee
### frequence partielle
#### $$
f_{ij} = \frac{n_{ij}}{n}
$$
## Distribution marginales
est l'etude de distribution de X sans tenir compte de Y ou l'inverse.
### Effectif marginal
#### $$
n_{i.} = \sum^{p}_{i=1} n_{ij}
$$
#### $$
n_{.j} = \sum^{q}_{j=1} n_{ij}
$$
### Effectif marginal
#### $$
f_{i.} = \sum^{p}_{i=1} f_{ij}
$$
#### $$
f_{.j} = \sum^{q}_{j=1} f_{ij}
$$
![[Pasted image 20250118143733.png]]
![[Pasted image 20250118144100.png]]
### Moyennes marginales
#### $$

\bar{x} = \frac{1}{n}  \sum^{p}_{i=1} n_{i.}x_{i} = \frac{1}{n}  \sum^{p}_{i=1} \sum^{q}_{j=1}n_{ij}x_{i}
$$