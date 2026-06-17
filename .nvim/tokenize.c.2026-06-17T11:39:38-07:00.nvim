#define _POSIX_C_SOURCE 200809L
#include "tokenize.h"
#include <stdlib.h>
#include <string.h>
#include <unistd.h>

int split(char *input, char *words[], int max_words) {
  char *saveptr;
  int count = 0;

  char *token = strtok_r(input, " \t\n", &saveptr);
  while (token != NULL && count < max_words) {
    words[count++] = token;
    token = strtok_r(NULL, " \t\n", &saveptr);
  }
  return count;
}
