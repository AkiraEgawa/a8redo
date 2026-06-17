#include "history.h"
#include "msgs.h"
#include <stdlib.h>
#include <string.h>
#include <unistd.h>

int detectCallback(char *readBuff, History *cmdHist) {
  if (readBuff[0] == '!') {
    if (readBuff[1] == '!') {
      if (cmdHist->size == 0) {
        const char *msg = FORMAT_MSG("history", HISTORY_NO_LAST_MSG);
        write(2, msg, strlen(msg));
        return 1;
      }
      strcpy(readBuff, peek(cmdHist, cmdHist->size - 1));
      char msg[4096];
      snprintf(msg, sizeof(msg), "%s\n", readBuff);
      write(1, msg, strlen(msg));
    } else {
      char *endptr;
      char *suffix = readBuff + 1;
      long tmp = strtol(suffix, &endptr, 10);

      if (*endptr != '\0') {
        const char *msg = FORMAT_MSG("history", HISTORY_INVALID_MSG);
        write(2, msg, strlen(msg));
        return 1;
      }
      int n = (int)tmp;
      if (n < cmdHist->total - 9 || n > cmdHist->total || n < 0) {
        const char *msg = FORMAT_MSG("history", HISTORY_INVALID_MSG);
        write(2, msg, strlen(msg));
        return 1;
      } else {
        strcpy(readBuff, peek(cmdHist, n + cmdHist->size - cmdHist->total - 1));
        char msg[4096];
        snprintf(msg, sizeof(msg), "%s\n", readBuff);
        write(1, msg, strlen(msg));
      }
    }
  }
  return 0;
}
