prosty programik który odpala thread i czeka aż zakończy dzialać:

```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <unistd.h>
#include <time.h>

void *myThread(void *arg) {
  
  while (1) {

    int randomNumber = (rand()%50) + 1;
    printf("generated slop: %d\n", randomNumber);

    if (randomNumber<10) {
      break;
    }

    sleep(0.5);

  }

  return NULL;

}

int main(){
  
  srand(time(NULL));
  
  pthread_t threadId;
  pthread_create(&threadId, NULL, myThread, NULL);
  pthread_join(threadId, NULL);

  return 0;
}
```

---------------------------------

programik który odpala `x` threadów, i przekazuje im parametry (also semaphores):

```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <unistd.h>
#include <semaphore.h>

// Define the maximum number of employees
#define MAX_EMPLOYEES 100

sem_t printerSemaphore;

// Function to simulate an employee using the printer
void *Employee(void *arg) {
    int *id = (int *)arg;

    while (1) {
        // Simulate employee's work
        printf("Employee %d is working\n", *id);
        usleep(rand() % 2000000 + 1000000);  // Sleep for a random time between 1 and 3 seconds

        // Decide whether the employee wants to use the printer (random decision)
        if (rand() % 2 == 0) {
            sem_wait(&printerSemaphore);  // Wait for the printer to be available

            // Simulate using the printer
            printf("Employee %d is using the printer\n", *id);
            usleep(rand() % 2000000 + 1000000);  // Simulate printing time

            sem_post(&printerSemaphore);  // Release the printer
        }
    }

    return NULL;
}

int main() {
    int numEmployees;

    // Read the number of employees from a file (assuming "employees.txt" for simplicity)
    FILE *file = fopen("employees.txt", "r");
    if (file == NULL) {
        perror("Error opening file");
        exit(EXIT_FAILURE);
    }

    fscanf(file, "%d", &numEmployees);
    fclose(file);

    // Check if the number of employees is within the allowed range
    if (numEmployees <= 0 || numEmployees > MAX_EMPLOYEES) {
        fprintf(stderr, "Invalid number of employees\n");
        exit(EXIT_FAILURE);
    }

    // Initialize the printer semaphore
    sem_init(&printerSemaphore, 0, 1);

    // Create an array to store thread IDs
    pthread_t employeeThreads[numEmployees];

    // Create threads for each employee
    for (int i = 0; i < numEmployees; i++) {
        int *employeeId = malloc(sizeof(int));
        *employeeId = i + 1;
        pthread_create(&employeeThreads[i], NULL, Employee, (void *)employeeId);
    }

    // Wait for all employee threads to finish (although they run indefinitely)
    for (int i = 0; i < numEmployees; i++) {
        pthread_join(employeeThreads[i], NULL);
    }

    // Destroy the printer semaphore
    sem_destroy(&printerSemaphore);

    return 0;
}
```