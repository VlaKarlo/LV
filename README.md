# LV

// Worst-fit

#include <stdio.h>
#include <stdlib.h>
int main() {

    //unos
    int n,m,i,j;
    printf("Unesite broj procesa\n");
    scanf("%d", &n);
    printf("Unesite broj memorijskih blokova\n");
    scanf("%d", &m);
    int *processSize = (int*) calloc(n, sizeof(int));
    int *blockSize = (int*) calloc(m, sizeof(int));
    int *allocation = (int*) calloc(n, sizeof(int));
    for(i=0; i<n; i++){
        allocation[i] = -1;
    }
    printf("Unesite velicinu procesa\n");
    for (i=0; i<n; i++)
        scanf("%d", &processSize[i]);
    printf("Unesite velicinu memorijskih blokova\n");
    for (i=0; i<m; i++)
        scanf("%d", &blockSize[i]);

    //logika

    for(i=0;i<n;i++){
        int biggestIndex = 0;
        for(j=0;j<m;j++){
            if(blockSize[j]>=processSize[i]&&blockSize[j]>=blockSize[biggestIndex]){
                biggestIndex = j;
            }
        }
        allocation[i] = biggestIndex;
        blockSize[biggestIndex] -= processSize[i];
    }


    //ispis
    printf("\nProcess PID \t Process size \t Block number\n");
    for (i=0; i<n; i++){
        printf(" %d \t\t\t %d \t\t\t", i+1, processSize[i]);
        if (allocation[i] != -1)
            printf("%d\n", allocation[i] +1);
        else
            printf("Not allocated\n");
    }
}

// First-Fit

#include <stdio.h>
#include <stdlib.h>
int main() {

    //unos
    int n,m,i,j;
    printf("Unesite broj procesa\n");
    scanf("%d", &n);
    printf("Unesite broj memorijskih blokova\n");
    scanf("%d", &m);
    int *processSize = (int*) calloc(n, sizeof(int));
    int *blockSize = (int*) calloc(m, sizeof(int));
    int *allocation = (int*) calloc(n, sizeof(int));
    for(i=0; i<n; i++){
        allocation[i] = -1;
    }
    printf("Unesite velicinu procesa\n");
    for (i=0; i<n; i++)
        scanf("%d", &processSize[i]);
    printf("Unesite velicinu memorijskih blokova\n");
    for (i=0; i<m; i++)
        scanf("%d", &blockSize[i]);

    //logika
    for(i=0;i<n;i++){
        for(j=0;j<m;j++){
            if(blockSize[j]>=processSize[i]){
                allocation[i] = j;
                blockSize[j] -=processSize[i];
                break;
            }
        }
    }


    //ispis
    printf("\nProcess PID \t Process size \t Block number\n");
    for (i=0; i<n; i++){
        printf(" %d \t\t\t %d \t\t\t", i+1, processSize[i]);
        if (allocation[i] != -1)
            printf("%d\n", allocation[i] +1);
        else
            printf("Not allocated\n");
    }
}

