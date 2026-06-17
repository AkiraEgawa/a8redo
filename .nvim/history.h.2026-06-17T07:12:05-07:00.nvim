#pragma once
#ifndef STACK_H
#define STACK_H

#include <stdio.h>
#include <string.h>

typedef struct circularArray {
  char *history[10];
  int head;
  int size;
  int total;
} History;

void initHistory(History *h);
void push(History *h, char *command);
char *peek(History *h, int index);
void displayHist(History *h);
void dealloStack(History *h);

#endif
