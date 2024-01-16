prosty programik reagujący na sygnały:

```c
#include <stdio.h>
#include <signal.h>
#include <unistd.h>
#include <sys/types.h>

void handleSignal(int signum) {
    if (signum == SIGINT) {
        printf("Jestem nieśmiertelny. Mój PID: %d\n", getpid());
    } else if (signum == SIGHUP) {
        printf("Przestaję reagować na SIGINT.\n");
        signal(SIGINT, SIG_IGN);  // Ignore SIGINT
    }
}

int main() {
    signal(SIGINT, handleSignal);
    signal(SIGHUP, handleSignal);

    while (1) {
        sleep(1);  // Sleep to keep the program running
    }

    return 0;
}
```

----------------------

czekanie aż child skończy pracę:

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <stdlib.h>
#include <time.h>

void childProcess() {
    // Display child process details
    printf("Proces potomny: PID=%d, PPID=%d\n", getpid(), getppid());

    // Seed the random number generator with the current time
    srand(time(NULL));

    // Generate a random number between 1 and 50
    while (1) {
      int randomNumber = (rand() % 50) + 1;
      printf("Wylosowana liczba: %d\n", randomNumber);

      // Check if the random number is divisible by 5
      if (randomNumber % 5 == 0) {
          printf("Proces potomny kończy działanie.\n");
          exit(0);
      }
    }

}

int main() {
    // Fork a child process
    pid_t childPID = fork();

    if (childPID == -1) {
        perror("Błąd przy fork()");
        exit(EXIT_FAILURE);
    }

    if (childPID == 0) {
        // Code executed by the child process
        childProcess();
    } else {
        // Code executed by the parent process
        // Wait for the child process to finish
        wait(childPID);

        // Display parent process details
        printf("Proces nadrzędny: PID=%d\n", getpid());
    }

    return 0;
}
```

----------------

zrobienie paru forków naraz, while keeping track of which is which:

```c
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <stdlib.h>
#include <time.h>
#include <stdbool.h>

void something(int n) {
    while (1) {
        printf("jestem child%d\n", n);
        sleep(1);
    }
}

int main() {

    //parent PID
    pid_t parentPID = getpid();

    // Fork a child process
    pid_t child1PID = fork();
    pid_t child2PID = -1;

    if (parentPID==getpid()) {
        child2PID = fork();
    }

    sleep(1);

    if (child1PID==0) {
        // printf("CHILD1: parentid=%d, child1PID=%d, child2PID=%d, getpid()=%d\n", parentPID, child1PID, child2PID, getpid());
        something(1);
    } else if (child2PID==0) {
        // printf("CHILD2: parentid=%d, child1PID=%d, child2PID=%d, getpid()=%d\n", parentPID, child1PID, child2PID, getpid());
        something(2);
    } else if (getpid() == parentPID) {
        bool didWeKillChild1 = false;
        bool didWeKillChild2 = false;
        srand(time(NULL));

        while (didWeKillChild1==false || didWeKillChild2==false) {
            sleep(1);
            int randomNumber = (rand() % 50) + 1;
            printf("parent generated random number %d\n", randomNumber);
            if (randomNumber<10 && didWeKillChild1==false) {
                kill(child1PID, SIGKILL);
                didWeKillChild1 = true;
            }
            if (randomNumber>40 && didWeKillChild2==false) {
                kill(child2PID, SIGKILL);
                didWeKillChild2 = true;
            }
        }
    }

    return 0;
}
```