//number 1

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <signal.h>
#include <sys/wait.h>

int main() {
  int filed[2];
  char message[100];

  pipe(filed);

  for (int i = 0; i < 3; i++) {
    processid_t processid = fork();
    if (pid == 0) {

      close(filed[0]);

      snprintf(message, sizeof(message), "Child %d: Hello, parent", i + 1);
      write(filed[1], message, strlen(message));

      sleep(rand() % 5);

      kill(getpprocessid(), SIGINT);

      exit(0);
    }
  }

  close(filed[1]);

  for (int i = 0; i < 3; i++) {
    int bytes_read = read(filed[0], message, sizeof(message));
    if (bytes_read > 0) {
      printf("Parent: Received message from child %d: %s\n", i + 1, message);
    }
  }

  for (int i = 0; i < 3; i++) {
    wait(NULL);
  }

  return 0;
}
