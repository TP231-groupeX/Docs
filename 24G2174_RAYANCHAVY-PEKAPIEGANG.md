Programmes en C : Addition de Matrices et Produit Vecteur × Matrice
Introduction
Ce document présente deux programmes écrits en langage C :
•	Addition de deux matrices de mêmes dimensions
•	Produit d’un vecteur et d’une matrice
Ces programmes sont largement utilisés dans les calculs numériques, l’algèbre linéaire et les applications informatiques nécessitant la manipulation de données sous forme matricielle. Chaque programme est accompagné de commentaires détaillés pour en faciliter la compréhension et l’apprentissage.
________________________________________
1. Programme : Addition de deux matrices
Description :
Ce programme demande à l'utilisateur les dimensions de deux matrices, lit les éléments de chacune d'elles, effectue leur addition élément par élément et affiche la matrice résultante.
Code source :
#include <stdio.h>

int main() {
    int i, j;
    int rows, cols;

    printf("=== Addition de deux matrices ===\n");

    // Étape 1 : Demander les dimensions des matrices
    printf("Entrez le nombre de lignes : ");
    scanf("%d", &rows);
    printf("Entrez le nombre de colonnes : ");
    scanf("%d", &cols);

    // Déclaration des matrices en fonction des dimensions
    int A[rows][cols], B[rows][cols], C[rows][cols];

    // Étape 2 : Lecture des éléments de la première matrice A
    printf("\n--- Saisie de la matrice A ---\n");
    for (i = 0; i < rows; i++) {
        for (j = 0; j < cols; j++) {
            printf("A[%d][%d] = ", i, j);
            scanf("%d", &A[i][j]);
        }
    }

    // Étape 3 : Lecture des éléments de la deuxième matrice B
    printf("\n--- Saisie de la matrice B ---\n");
    for (i = 0; i < rows; i++) {
        for (j = 0; j < cols; j++) {
            printf("B[%d][%d] = ", i, j);
            scanf("%d", &B[i][j]);
        }
    }

    // Étape 4 : Calcul de la somme élément par élément
    for (i = 0; i < rows; i++) {
        for (j = 0; j < cols; j++) {
            C[i][j] = A[i][j] + B[i][j];
        }
    }

    // Étape 5 : Affichage du résultat
    printf("\n=== Résultat : A + B ===\n");
    for (i = 0; i < rows; i++) {
        for (j = 0; j < cols; j++) {
            printf("%d\t", C[i][j]);
        }
        printf("\n");
    }

    return 0;
}
2. Programme : Produit Vecteur × Matrice
Description :
Ce programme calcule le produit d'un vecteur et d'une matrice.
Le résultat est un nouveau vecteur. Cette opération est très utilisée en algèbre linéaire, dans les systèmes d’équations et dans plusieurs applications scientifiques.
Code source :
#include <stdio.h>

int main() {
    int i, j, n, m;

    printf("=== Produit Vecteur * Matrice ===\n");

    // Étape 1 : Demander les dimensions
    // n = nombre d'éléments du vecteur (et nombre de lignes de la matrice)
    // m = nombre de colonnes de la matrice
    printf("Entrez la taille du vecteur (nombre de lignes de la matrice) : ");
    scanf("%d", &n);
    printf("Entrez le nombre de colonnes de la matrice : ");
    scanf("%d", &m);

    int V[n], M[n][m], R[m];

    // Étape 2 : Saisie du vecteur
    printf("\n--- Saisie du vecteur ---\n");
    for (i = 0; i < n; i++) {
        printf("V[%d] = ", i);
        scanf("%d", &V[i]);
    }

    // Étape 3 : Saisie de la matrice
    printf("\n--- Saisie de la matrice ---\n");
    for (i = 0; i < n; i++) {
        for (j = 0; j < m; j++) {
            printf("M[%d][%d] = ", i, j);
            scanf("%d", &M[i][j]);
        }
    }

    // Étape 4 : Calcul du produit
    // Pour chaque colonne j de la matrice, on fait la somme des produits
    for (j = 0; j < m; j++) {
        R[j] = 0; // Initialiser l'élément j du résultat
        for (i = 0; i < n; i++) {
            R[j] += V[i] * M[i][j];
        }
    }

    // Étape 5 : Affichage du résultat
    printf("\n=== Résultat : V * M ===\n");
    printf("[ ");
    for (j = 0; j < m; j++) {
        printf("%d ", R[j]);
    }
    printf("]\n");

    return 0;
}
Conclusion
Ces deux programmes illustrent des opérations fondamentales en algèbre linéaire :
•	L’addition de matrices, utilisée pour combiner des données.
•	Le produit vecteur × matrice, utilisé pour transformer un vecteur par une matrice.
Ils constituent une base solide pour comprendre la manipulation de structures de données en langage C et peuvent être étendus pour traiter des cas plus complexes (produit matrice × matrice, allocation dynamique, etc.).

