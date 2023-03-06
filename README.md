# MyShell
Author: Ze Sheng (Owen Sanazas)


## Source Files
* myshell.c
* shell-behaviour.c
* shell-behaviour.h
* job.c
* job.h
* utils.c
* utils.h

## Progress
* ✓ - Finished
* O - In progess
* ? - Have problem
* blank - Not started

Section | State
:----: |:----:
ctrl + c  | ✓
ctrl + z  | ✓
Non-interactive mode | ✓
Command parser | ✓
File redirection | ✓
multi-lvl pipeline | ✓
job struct | ✓
jobList Linkedlist| ✓
All job helper funcs | ✓
Bultin cmd: jobs | ✓
Bultin cmd: fg | ✓
Bultin cmd: bg |   ✓
Memory leaks check | ✓
Invalid R/W check | ✓
Zombie processes check | ✓
Foreground check |  ✓
Background check |     ✓



## Overview of work accomplished
* This shell can be run in the non-interactive mode successfully.
* All commands that are not job control builtins commands are handled by pipe. The standard input/output will be redirected and combining redirection is also supported.
* We manage each job in a JobNode struct and use a linked list struct JobList to store all background jobs. 
    ````
    // Job Node
    typedef struct JobNode {
        int pgid;                           // process group id of the current running job
        enum JobStatus status;              // Job status
        struct parsed_command *command;     // job's command
        struct JobNode *prev;               // Prev job pointer
        struct JobNode *next;               // Next job pointer
        int jobId;                          // Job priority
    }JobNode;


    // Linked-list structure to manage jobs
    typedef struct JobList {
        JobNode *head;
        JobNode *tail;
        int jobCount;
    }JobList;
    ````
* Background processes (if existed) will be polled at the beginning of each loop of the shell.
* The jobs can be managed through job control builtins (fg, bg, jobs).
* The status of the jobs can be reported correctly.
* Ctrl-C, Ctrl-D, Ctrl-Z, and other signal are handled correctly.

