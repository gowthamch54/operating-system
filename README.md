#for problem - 3 
#include <stdio.h>

int main() {
    int A[100][4];  // Process array: A[i][0] = Process ID, A[i][1] = Burst Time, A[i][2] = Waiting Time, A[i][3] = Turnaround Time
    int i, j, n, total = 0, index, temp;
    float avg_wt, avg_tat;

    // Input number of processes
    printf("Enter number of processes: ");
    scanf("%d", &n);

    // Input burst times
    printf("Enter Burst Time:\n");
    for (i = 0; i < n; i++) {
        printf("P%d: ", i + 1);
        scanf("%d", &A[i][1]);
        A[i][0] = i + 1;  // Assign process ID
    }

    // Sorting processes by burst time
    for (i = 0; i < n; i++) {
        index = i;
        for (j = i + 1; j < n; j++) {
            if (A[j][1] < A[index][1])
                index = j;
        }
        temp = A[i][1];
        A[i][1] = A[index][1];
        A[index][1] = temp;

        temp = A[i][0];
        A[i][0] = A[index][0];
        A[index][0] = temp;
    }

    // Waiting time for first process is 0
    A[0][2] = 0;
    for (i = 1; i < n; i++) {
        A[i][2] = 0;
        for (j = 0; j < i; j++)
            A[i][2] += A[j][1];
        total += A[i][2];
    }

    // Average waiting time
    avg_wt = (float)total / n;
    total = 0;

    // Turnaround time
    printf("P\tBT\tWT\tTAT\n");
    for (i = 0; i < n; i++) {
        A[i][3] = A[i][1] + A[i][2];
        total += A[i][3];
        printf("P%d\t%d\t%d\t%d\n", A[i][0], A[i][1], A[i][2], A[i][3]);
    }

    // Average turnaround time
    avg_tat = (float)total / n;
    printf("Average Waiting Time= %f\n", avg_wt);
    printf("Average Turnaround Time= %f\n", avg_tat);

    return 0;
}
