Practical Work INF231 – 9 Exercises

**Student:** Ngankeu Takou Daniel Wilfried 
**Matricule:** 24G2678
**Course:** INF231
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
