#include "history.h"
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>

void initHistory(History *h) {
  h->head = 0;
  h->size = 0;
  h->total = -1;
}

char *strdup(const char *s) {
  size_t len = strlen(s) + 1;
  char *copy = malloc(len);
  if (!copy)
    return NULL;
  memcpy(copy, s, len);
  return copy;
}

void push(History *h, char *command) {
  h->total++;
  if (h->size != 10) {
    h->history[h->size] = strdup(command);
    h->size++;
  } else {
    free(h->history[h->head]);
    h->history[h->head] = strdup(command);
    h->head = (h->head == 9) ? 0 : h->head + 1;
  }
}

char *peek(History *h, int index) {
  if (index >= h->size) {
    printf("Impossible");
    return 0;
  }
  int trueIndex = (index > h->head) ? index : (h->head + index) % h->size;
  return (h->history[trueIndex]);
}

void dealloStack(History *h) {
  for (int i = 0; i < h->size; i++) {
    free(h->history[i]);
  }
}

void displayHist(History *h) {
  char msg[4096];
  int tail = (h->head == 0) ? h->size - 1 : h->head - 1;
  for (int i = 0; i < h->size; i++) {
    int len = snprintf(msg, sizeof(msg), "%d\t%s\n", h->total - i,
                       h->history[(tail - i + h->size) % h->size]);
    if (len == 0)
      printf("displayHist: error has occurred\n");
    write(1, msg, len);
  }
}
