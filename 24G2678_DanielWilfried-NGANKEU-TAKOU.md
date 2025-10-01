Practical Work INF231 – 9 Exercises

**Student:** **Ngankeu Takou Daniel Wilfried**

**Matricule:** **24G2678**

**Course:** **INF231**

**Assignment:** Exercices 4 et 5 
**Date:** 24/09/2025 

# Documentation Exercices 4 et 5

## Exercice 4: Multiplication par Addition

### Énoncé du problème
Écrire un programme qui multiplie deux entiers positifs a et b en utilisant seulement l'opération d'addition (+1). Créer deux fonctions : une pour l'addition et une pour la multiplication.

### Mon algorithme

**Fonction addition :**
1. Initialiser sum = x
2. Répéter y fois : sum = sum + 1
3. Retourner sum

**Fonction multiplication :**
1. Initialiser result = 0
2. Répéter b fois : result = add(result, a)
3. Retourner result

### Mon code
 </pre>```c
#include <stdio.h>

int add(int x, int y) {
    int sum = x;
    for (int i = 0; i < y; i++) {
        sum = sum + 1;  // J'ajoute 1 exactement y fois
    }
    return sum;
}

int multiply(int a, int b) {
    int result = 0;
    for (int i = 0; i < b; i++) {
        result = add(result, a);  // J'ajoute 'a' exactement b fois
    }
    return result;
}

int main() {
    int a, b;
    printf("Enter a and b: ");
    scanf("%d %d", &a, &b);

    printf("%d * %d = %d\n", a, b, multiply(a, b));
    return 0;
}
```

### Exemple d'exécution
```
Entrée:
Enter a and b: 4 3

Sortie:
4 * 3 = 12
```

**Trace d'exécution pour multiply(4, 3) :**
- i=0: result = add(0, 4) = 4
- i=1: result = add(4, 4) = 8  
- i=2: result = add(8, 4) = 12
- Retour: 12

### Ma complexité
- **Temps :** O(a × b) 
  - add(x, y) fait y itérations donc O(y)
  - multiply(a, b) appelle add() b fois avec des valeurs qui prennent O(a) temps
  - Total : b × a = O(a × b)
- **Espace :** O(1) - seulement quelques variables entières
- **Invariant multiply :** Après k itérations, result = k × a
- **Invariant add :** Après j itérations, sum = x + j

---

## Exercice 5: Test de Tri

### Énoncé du problème
Écrire un programme qui vérifie si un tableau d'entiers est trié en ordre croissant. Le programme doit lire un tableau et afficher s'il est trié ou non.

### Mon algorithme
1. Lire la taille du tableau
2. Lire les éléments du tableau
3. Pour i de 0 à taille-2 :
   - Si tableau[i] > tableau[i+1] :
     - Afficher "Array not sorted"
     - Terminer
4. Si on arrive ici : Afficher "The Array is sorted"

### Mon code
```c
#include <stdio.h>
#include <stdlib.h>

void sortTest(int arr[], int size) {
    for(int i = 0; i < size-1; i++) {
        if(arr[i] > arr[i+1]) {
            printf("Array not sorted\n");
            return;  // Arrêt précoce : pas besoin de continuer
        }
    }
    printf("The Array is sorted\n");
}
      
int main() {
    int size;
    printf("Enter the size of your array: ");
    scanf("%d", &size);
    
    int arr[size];
    for(int i = 0; i < size; i++) {
        printf("Enter element %d:\n", i+1);
        scanf("%d", &arr[i]);
    }
    
    sortTest(arr, size);
    
    return 0;
}
```

### Exemples d'exécution

**Cas 1 : Tableau trié**
```
Entrée:
Enter the size of your array: 4
Enter element 1: 2
Enter element 2: 5
Enter element 3: 8
Enter element 4: 10

Sortie:
The Array is sorted
```

**Cas 2 : Tableau non trié**
```
Entrée:
Enter the size of your array: 4
Enter element 1: 5
Enter element 2: 2
Enter element 3: 8
Enter element 4: 1

Sortie:
Array not sorted
```

**Trace pour [5, 2, 8, 1] :**
- i=0: arr[0]=5 > arr[1]=2 → Condition vraie → "Array not sorted" → return

### Ma complexité
- **Temps :**
  - **Meilleur cas :** O(1) - première paire mal ordonnée
  - **Pire cas :** O(n-1) = O(n) - tableau complètement trié
  - **Cas moyen :** O(n/2) - erreur vers le milieu
- **Espace :** O(1) - pas de mémoire supplémentaire
- **Invariant :** Si j'arrive à l'indice k, alors ∀i < k, arr[i] ≤ arr[i+1]

### Justification de ma méthode

**Pourquoi l'arrêt précoce ?**
Dès que je trouve deux éléments consécutifs dans le mauvais ordre, je sais que le tableau n'est pas trié. Continuer serait inutile.

**Pourquoi size-1 dans la boucle ?**
Je compare arr[i] avec arr[i+1], donc i doit aller jusqu'à size-2 maximum pour éviter un débordement.

### Optimisation possible
Ma solution est déjà optimale en temps pour le pire cas O(n), car il faut au minimum vérifier tous les éléments adjacents dans le cas d'un tableau trié.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


**TP No.2 du 25/09/2025**
**Theme:** **Ecrire des fonctions qui permettront d'effctuer des operations sur les listes chaines simples, doubles et circulaires**
# Exercices INF 231 - Listes Chaînées en C

## Documentation-Complete

##  Usage

### Compilation

Pour compiler le programme, utilisez GCC :

```c
gcc -o tp2.c 
```


### Exécution

Pour exécuter le programme :

```c
./tp2
```

### Utilisation interactive

Le programme affiche un menu avec 6 options :

```
=== MENU PRINCIPAL ===
1. Supprimer toutes les occurrences d'un élément
2. Insérer dans une liste simple triée
3. Insérer dans une liste double triée
4. Insérer en tête/queue (liste simple circulaire)
5. Insérer en tête/queue (liste double circulaire)
0. Quitter
```

Pour chaque option, suivez les instructions affichées à l'écran.

---

##  Présentation du Code

### Structure du projet

Le programme est organisé en plusieurs sections :

#### 1. **Structures de données**
```c
typedef struct NodeSimple {
    int data;
    struct NodeSimple* next;
} NodeSimple;

typedef struct NodeDouble {
    int data;
    struct NodeDouble* next;
    struct NodeDouble* prev;
} NodeDouble;
```

#### 2. **Fonctions principales**
- `supprimerOccurrences()` - Suppression d'éléments
- `insererTrieSimple()` - Insertion triée (liste simple)
- `insererTrieDouble()` - Insertion triée (liste double)
- `insererTeteCirculaireSimple()` / `insererQueueCirculaireSimple()` - Insertion circulaire simple
- `insererTeteCirculaireDouble()` / `insererQueueCirculaireDouble()` - Insertion circulaire double

#### 3. **Fonctions utilitaires**
- `estTrieSimple()` / `estTrieDouble()` - Vérification du tri
- `trierListeSimple()` / `trierListeDouble()` - Tri automatique
- `saisirListeSimple()` / `saisirListeDouble()` - Saisie interactive
- `afficherListeSimple()` / `afficherListeDouble()` - Affichage

#### 4. **Programme principal**
Menu interactif permettant de tester toutes les fonctionnalités.

---

## Documentation Algorithmique

---

## Exercice 1 : Suppression d'occurrences

### Le Problème

**Énoncé :** Lire un élément et supprimer toutes ses occurrences dans une liste simplement chaînée.

**Entrée :** 
- Une liste chaînée simple `L`
- Un élément `x` à supprimer

**Sortie :**
- La liste `L` sans aucune occurrence de `x`

**Exemple :**
```
Entrée : L = [1, 2, 3, 2, 4, 2, 5], x = 2
Sortie : L = [1, 3, 4, 5]
```

### Le Principe

L'algorithme fonctionne en deux phases :

1. **Phase 1 - Suppression en tête :**
   - Tant que la tête contient l'élément à supprimer, on avance la tête et on libère la mémoire

2. **Phase 2 - Suppression dans le reste :**
   - On parcourt la liste avec deux pointeurs : `current` et `prev`
   - Si `current` contient l'élément, on le supprime en reliant `prev` au suivant
   - Sinon, on avance les deux pointeurs

**Pourquoi deux phases ?**
- La tête n'a pas de prédécesseur, elle nécessite un traitement spécial

### Dictionnaire des Données

| Variable | Type | Rôle |
|----------|------|------|
| `head` | `NodeSimple*` | Pointeur vers la tête de la liste |
| `current` | `NodeSimple*` | Pointeur pour parcourir la liste |
| `prev` | `NodeSimple*` | Pointeur vers le nœud précédent |
| `element` | `int` | Élément à supprimer |

### Algorithme

```
ALGORITHME supprimerOccurrences(head, element)
DÉBUT
    current ← head
    prev ← NULL
    
    // Phase 1 : Supprimer en tête
    TANT QUE (current ≠ NULL ET current.data = element) FAIRE
        head ← current.next
        LIBÉRER(current)
        current ← head
    FIN TANT QUE
    
    // Phase 2 : Supprimer dans le reste
    TANT QUE (current ≠ NULL) FAIRE
        SI (current.data = element) ALORS
            prev.next ← current.next
            LIBÉRER(current)
            current ← prev.next
        SINON
            prev ← current
            current ← current.next
        FIN SI
    FIN TANT QUE
    
    RETOURNER head
FIN
```

### Analyse de Complexité

**Complexité temporelle :**
- **Meilleur cas :** O(1) - L'élément n'existe pas ou liste vide
- **Cas moyen :** O(n) - On parcourt toute la liste
- **Pire cas :** O(n) - On parcourt tous les n éléments

**Complexité spatiale :** O(1)
- Utilisation de pointeurs uniquement (mémoire constante)
- Pas de structure auxiliaire

**Nombre d'opérations :**
- Comparaisons : n (une par élément)
- Suppressions : k (où k = nombre d'occurrences)
- Affectations : 2n (current et prev)

---

## Exercice 2 : Insertion triée (liste simple)

### Le Problème

**Énoncé :** Insérer un élément dans une liste simplement chaînée triée en maintenant l'ordre croissant.

**Entrée :**
- Une liste triée `L` (ordre croissant)
- Un élément `x` à insérer

**Sortie :**
- La liste `L` contenant `x`, toujours triée

**Exemple :**
```
Entrée : L = [1, 3, 5, 7, 9], x = 4
Sortie : L = [1, 3, 4, 5, 7, 9]
```

### Le Principe

L'algorithme recherche la position correcte pour insérer l'élément :

1. **Cas spéciaux :**
   - Liste vide : le nouvel élément devient la tête
   - Insertion en tête : si l'élément est plus petit que la tête

2. **Cas général :**
   - Parcourir jusqu'à trouver un nœud dont le suivant est plus grand que l'élément
   - Insérer après ce nœud

**Invariant :** La propriété de tri est maintenue après insertion.

### Dictionnaire des Données

| Variable | Type | Rôle |
|----------|------|------|
| `head` | `NodeSimple*` | Pointeur vers la tête de la liste |
| `nouveau` | `NodeSimple*` | Nouveau nœud à insérer |
| `current` | `NodeSimple*` | Pointeur pour trouver la position |
| `element` | `int` | Valeur à insérer |

### Algorithme

```
ALGORITHME insererTrieSimple(head, element)
DÉBUT
    nouveau ← ALLOUER(NodeSimple)
    nouveau.data ← element
    nouveau.next ← NULL
    
    // Cas : liste vide ou insertion en tête
    SI (head = NULL OU head.data ≥ element) ALORS
        nouveau.next ← head
        RETOURNER nouveau
    FIN SI
    
    // Trouver la position d'insertion
    current ← head
    TANT QUE (current.next ≠ NULL ET current.next.data < element) FAIRE
        current ← current.next
    FIN TANT QUE
    
    // Insérer après current
    nouveau.next ← current.next
    current.next ← nouveau
    
    RETOURNER head
FIN
```

### Analyse de Complexité

**Complexité temporelle :**
- **Meilleur cas :** O(1) - Insertion en tête
- **Cas moyen :** O(n/2) = O(n) - Insertion au milieu
- **Pire cas :** O(n) - Insertion en queue

**Complexité spatiale :** O(1)
- Un seul nœud alloué

**Nombre d'opérations :**
- Comparaisons : k (où k = position d'insertion, 0 ≤ k ≤ n)
- Affectations : 3 (création + insertion)
- Allocation : 1

---

## Exercice 3 : Insertion triée (liste double)

### Le Problème

**Énoncé :** Insérer un élément dans une liste doublement chaînée triée.

**Entrée :**
- Une liste doublement chaînée triée `L`
- Un élément `x` à insérer

**Sortie :**
- La liste `L` avec `x` inséré, maintenant l'ordre

**Exemple :**
```
Entrée : L = [1] ⇄ [3] ⇄ [5], x = 2
Sortie : L = [1] ⇄ [2] ⇄ [3] ⇄ [5]
```

###  Le Principe

Similaire à l'exercice 2, mais on gère **deux pointeurs** (next et prev) :

1. Trouver la position d'insertion (comme liste simple)
2. **Mise à jour des 4 liens :**
   - `nouveau.next` → nœud suivant
   - `nouveau.prev` → nœud courant
   - `suivant.prev` → nouveau (si existe)
   - `courant.next` → nouveau

**Avantage :** Parcours bidirectionnel possible.

### Dictionnaire des Données

| Variable | Type | Rôle |
|----------|------|------|
| `head` | `NodeDouble*` | Tête de la liste |
| `nouveau` | `NodeDouble*` | Nouveau nœud |
| `current` | `NodeDouble*` | Position d'insertion |
| `element` | `int` | Valeur à insérer |

### Algorithme

```
ALGORITHME insererTrieDouble(head, element)
DÉBUT
    nouveau ← ALLOUER(NodeDouble)
    nouveau.data ← element
    nouveau.next ← NULL
    nouveau.prev ← NULL
    
    // Liste vide
    SI (head = NULL) ALORS
        RETOURNER nouveau
    FIN SI
    
    // Insertion en tête
    SI (head.data ≥ element) ALORS
        nouveau.next ← head
        head.prev ← nouveau
        RETOURNER nouveau
    FIN SI
    
    // Trouver la position
    current ← head
    TANT QUE (current.next ≠ NULL ET current.next.data < element) FAIRE
        current ← current.next
    FIN TANT QUE
    
    // Insérer après current (4 liens)
    nouveau.next ← current.next
    nouveau.prev ← current
    
    SI (current.next ≠ NULL) ALORS
        current.next.prev ← nouveau
    FIN SI
    
    current.next ← nouveau
    
    RETOURNER head
FIN
```

### Analyse de Complexité

**Complexité temporelle :**
- **Meilleur cas :** O(1) - Insertion en tête
- **Cas moyen :** O(n/2) = O(n)
- **Pire cas :** O(n) - Insertion en queue

**Complexité spatiale :** O(1)

**Différence avec liste simple :**
- Même complexité temporelle
- Plus d'affectations (4 liens au lieu de 2)
- Avantage : parcours bidirectionnel

---

## Exercice 4 : Insertion tête/queue (liste circulaire simple)

### Le Problème

**Énoncé :** Implémenter l'insertion en tête et en queue dans une liste simplement chaînée circulaire.

**Particularité :** Le dernier nœud pointe vers la tête (pas NULL).

**Entrée :**
- Liste circulaire `L`
- Élément `x`
- Position : tête ou queue

**Sortie :**
- Liste `L` avec `x` inséré

**Exemple :**
```
L = [1] → [2] → [3] → (retour à 1)
Insertion tête(4) : [4] → [1] → [2] → [3] → (retour à 4)
Insertion queue(5) : [1] → [2] → [3] → [5] → (retour à 1)
```

### Le Principe

**Liste circulaire :** `dernier.next = head` (toujours)

**Insertion en tête :**
1. Trouver le dernier nœud
2. Nouveau pointe vers head
3. Dernier pointe vers nouveau
4. Nouveau devient la nouvelle tête

**Insertion en queue :**
1. Trouver le dernier nœud
2. Nouveau pointe vers head
3. Dernier pointe vers nouveau
4. Head reste inchangée

### Dictionnaire des Données

| Variable | Type | Rôle |
|----------|------|------|
| `head` | `NodeSimple*` | Tête de la liste circulaire |
| `nouveau` | `NodeSimple*` | Nœud à insérer |
| `dernier` | `NodeSimple*` | Dernier nœud de la liste |
| `element` | `int` | Valeur à insérer |

###  Algorithmes

#### Insertion en tête

```
ALGORITHME insererTeteCirculaireSimple(head, element)
DÉBUT
    nouveau ← ALLOUER(NodeSimple)
    nouveau.data ← element
    
    // Liste vide
    SI (head = NULL) ALORS
        nouveau.next ← nouveau  // Pointe sur lui-même
        RETOURNER nouveau
    FIN SI
    
    // Trouver le dernier nœud
    dernier ← head
    TANT QUE (dernier.next ≠ head) FAIRE
        dernier ← dernier.next
    FIN TANT QUE
    
    nouveau.next ← head
    dernier.next ← nouveau
    
    RETOURNER nouveau  // Nouvelle tête
FIN
```

#### Insertion en queue

```
ALGORITHME insererQueueCirculaireSimple(head, element)
DÉBUT
    nouveau ← ALLOUER(NodeSimple)
    nouveau.data ← element
    
    SI (head = NULL) ALORS
        nouveau.next ← nouveau
        RETOURNER nouveau
    FIN SI
    
    dernier ← head
    TANT QUE (dernier.next ≠ head) FAIRE
        dernier ← dernier.next
    FIN TANT QUE
    
    nouveau.next ← head
    dernier.next ← nouveau
    
    RETOURNER head  // Tête inchangée
FIN
```

### Analyse de Complexité

**Complexité temporelle :**
- **Insertion tête :** O(n) - Doit trouver le dernier
- **Insertion queue :** O(n) - Doit trouver le dernier

**Complexité spatiale :** O(1)

**Optimisation possible :**
- Garder un pointeur vers le dernier → O(1) pour les deux opérations

---

## Exercice 5 : Insertion tête/queue (liste circulaire double)

### Le Problème

**Énoncé :** Implémenter l'insertion en tête et en queue dans une liste doublement chaînée circulaire.

**Particularités :**
- `dernier.next = head`
- `head.prev = dernier`

**Exemple :**
```
L = [1] ⇄ [2] ⇄ [3]
     ↑____________|

Insertion tête(4) : [4] ⇄ [1] ⇄ [2] ⇄ [3]
                     ↑_________________|
```

### Le Principe

**Avantage majeur :** `head.prev` donne directement le dernier nœud !

**Insertion en tête :**
1. `dernier ← head.prev` (O(1) !)
2. Mettre à jour 4 liens
3. Nouveau devient head

**Insertion en queue :**
1. `dernier ← head.prev` (O(1) !)
2. Mettre à jour 4 liens
3. Head reste inchangée

### Dictionnaire des Données

| Variable | Type | Rôle |
|----------|------|------|
| `head` | `NodeDouble*` | Tête de la liste |
| `nouveau` | `NodeDouble*` | Nœud à insérer |
| `dernier` | `NodeDouble*` | Dernier nœud (= head.prev) |
| `element` | `int` | Valeur à insérer |

### Algorithmes

#### Insertion en tête

```
ALGORITHME insererTeteCirculaireDouble(head, element)
DÉBUT
    nouveau ← ALLOUER(NodeDouble)
    nouveau.data ← element
    
    // Liste vide
    SI (head = NULL) ALORS
        nouveau.next ← nouveau
        nouveau.prev ← nouveau
        RETOURNER nouveau
    FIN SI
    
    dernier ← head.prev  // Accès direct !
    
    // Mise à jour des 4 liens
    nouveau.next ← head
    nouveau.prev ← dernier
    head.prev ← nouveau
    dernier.next ← nouveau
    
    RETOURNER nouveau  // Nouvelle tête
FIN
```

#### Insertion en queue

```
ALGORITHME insererQueueCirculaireDouble(head, element)
DÉBUT
    nouveau ← ALLOUER(NodeDouble)
    nouveau.data ← element
    
    SI (head = NULL) ALORS
        nouveau.next ← nouveau
        nouveau.prev ← nouveau
        RETOURNER nouveau
    FIN SI
    
    dernier ← head.prev
    
    nouveau.next ← head
    nouveau.prev ← dernier
    head.prev ← nouveau
    dernier.next ← nouveau
    
    RETOURNER head  // Tête inchangée
FIN
```

### Analyse de Complexité

**Complexité temporelle :**
- **Insertion tête :** O(1) - Accès direct au dernier
- **Insertion queue :** O(1) - Accès direct au dernier

**Complexité spatiale :** O(1)

**Comparaison avec liste circulaire simple :**
| Opération | Simple | Double |
|-----------|--------|--------|
| Insertion tête | O(n) | O(1)  |
| Insertion queue | O(n) | O(1)  |
| Parcours avant | O(n) | O(n) |
| Parcours arrière |  | O(n)  |

---

## Tableau Récapitulatif des Complexités

| Exercice | Opération | Temporelle (pire cas) | Spatiale |
|----------|-----------|----------------------|----------|
| 1 | Suppression occurrences | O(n) | O(1) |
| 2 | Insertion triée simple | O(n) | O(1) |
| 3 | Insertion triée double | O(n) | O(1) |
| 4 | Insertion circulaire simple | O(n) | O(1) |
| 5 | Insertion circulaire double | O(1)  | O(1) |

---

## 🔧 Fonctionnalités Supplémentaires

### Vérification et Tri Automatique

Le programme vérifie automatiquement si une liste est triée avant l'insertion :

```c
if (!estTrieSimple(liste)) {
    printf("La liste n'est PAS triée ! Tri en cours...\n");
    liste = trierListeSimple(liste);
}
```

**Complexité du tri :** O(n²) - Tri par insertion

---

## Concepts Clés

### Pointeurs en C
- `next` : pointeur vers le nœud suivant
- `prev` : pointeur vers le nœud précédent
- `head` : pointeur vers la tête de la liste

### Gestion mémoire
- `malloc()` : allocation dynamique
- `free()` : libération de mémoire
- Toujours libérer la mémoire allouée !

### Types de listes
1. **Simple** : Un seul sens de parcours
2. **Double** : Parcours bidirectionnel
3. **Circulaire** : Le dernier pointe vers le premier
4. **Circulaire double** : Les deux extrémités se rejoignent

---

## Notes

- Tous les algorithmes utilisent une allocation dynamique
- La gestion des cas limites est essentielle (liste vide, un élément)
- Les listes circulaires doubles sont les plus efficaces pour l'insertion aux extrémités

---
