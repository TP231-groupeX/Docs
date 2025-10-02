# Nom: Peka Piegang Rayan Chavy
# Matricule: 24G2174

**Thème :** Addition de matrices et Produit Vecteur × Matrice
**Langage :** C

---

## 1. Problème

On souhaite effectuer deux opérations fondamentales de l’algèbre linéaire en langage C :

* L’addition de deux matrices de mêmes dimensions.
* Le produit d’un vecteur par une matrice.

Ces opérations interviennent dans le calcul scientifique, la modélisation et le traitement informatique de données matricielles.

---

## 2. Principe

* **Addition de matrices :** pour chaque paire d’éléments aux mêmes indices, on calcule la somme afin de former une nouvelle matrice.
* **Produit vecteur × matrice :** on multiplie chaque élément du vecteur par les éléments de la colonne correspondante de la matrice, puis on somme les produits pour obtenir un élément du vecteur résultat.

---

## 3. Dictionnaire de données

### Addition de matrices

* `rows` : nombre de lignes des matrices (entier positif).
* `cols` : nombre de colonnes des matrices (entier positif).
* `A[rows][cols]` : première matrice d’entrée.
* `B[rows][cols]` : deuxième matrice d’entrée.
* `C[rows][cols]` : matrice résultat de la somme.

### Produit vecteur × matrice

* `n` : taille du vecteur (et nombre de lignes de la matrice).
* `m` : nombre de colonnes de la matrice.
* `V[n]` : vecteur d’entrée.
* `M[n][m]` : matrice d’entrée.
* `R[m]` : vecteur résultat.

---

## 4. Algorithmes

### 4.1. Addition de matrices

```
DEBUT
  Lire rows, cols
  Pour i ← 0 à rows-1
    Pour j ← 0 à cols-1
      Lire A[i][j]
  Pour i ← 0 à rows-1
    Pour j ← 0 à cols-1
      Lire B[i][j]
  Pour i ← 0 à rows-1
    Pour j ← 0 à cols-1
      C[i][j] ← A[i][j] + B[i][j]
  Afficher C
FIN
```

### 4.2. Produit vecteur × matrice

```
DEBUT
  Lire n, m
  Pour i ← 0 à n-1
    Lire V[i]
  Pour i ← 0 à n-1
    Pour j ← 0 à m-1
      Lire M[i][j]
  Pour j ← 0 à m-1
    R[j] ← 0
    Pour i ← 0 à n-1
      R[j] ← R[j] + V[i] * M[i][j]
  Afficher R
FIN
```

---

## 5. Analyse de complexité

### Addition de matrices

* **Temps :** Chaque élément est traité une fois → O(rows × cols).
* **Mémoire :** Trois matrices de taille `rows × cols` → O(rows × cols).

### Produit vecteur × matrice

* **Temps :** Chaque élément du vecteur résultat demande `n` multiplications et additions pour chaque colonne → O(n × m).
* **Mémoire :** matrice `M[n][m]`, vecteur `V[n]`, résultat `R[m]` → O(n × m).

---

## Conclusion

Ces deux algorithmes démontrent la manipulation des structures de données matricielles en langage C. Leur complexité est proportionnelle à la taille des données, ce qui garantit une efficacité raisonnable. Ils servent de base pour des traitements plus avancés : produit matrice × matrice, inversion ou opérations sur matrices dynamiques.
