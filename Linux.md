`rc` : The rc at the end of a file is related to the phrase "**run commands**"; its use derives from the /etc/rc. * files used to start most Unix  systems. The rc command **performs normal startup initialization for the system**.



## Mutex

`mutex`：mutual exclusion, a synchronization mechanism used to control access to shared resources in a multithreaded environment and ensure only one thread can access to the critical code and resource at a given time.



Implemented using `pthread_mutex_t`



### Initialization

```c
#include <pthread.h>

pthread_mutex_t my_mutex = PTHREAD_MUTEX_INITIALIZER;  //statically initialization
pthread_mutex_t my_mutex = pthread_mutex_init();	   //dynamically initialization
```

### Lock and Unlock

To protect the critical section of code

```c
#include <pthread.h>

pthread_mutex_lock(&my_mutex); 		//acquire mutex

pthread_mutex_unlock(&my_mutex);	//release mutex
```

```c
#include <pthread.h>
#include <stdio.h>

// Shared resource
int shared_variable = 0;

// Mutex
pthread_mutex_t my_mutex = PTHREAD_MUTEX_INITIALIZER;

void *thread_function(void *arg) {
    for (int i = 0; i < 100000; ++i) {
        // Lock the mutex before accessing the shared resource
        pthread_mutex_lock(&my_mutex);

        // Critical section (shared resource access)
        shared_variable++;

        // Unlock the mutex when done with the critical section
        pthread_mutex_unlock(&my_mutex);
    }

    return NULL;
}

int main() {
    pthread_t thread1, thread2;

    // Create two threads
    pthread_create(&thread1, NULL, thread_function, NULL);
    pthread_create(&thread2, NULL, thread_function, NULL);

    // Wait for threads to finish
    pthread_join(thread1, NULL);
    pthread_join(thread2, NULL);

    // Print the final value of the shared variable
    printf("Shared variable: %d\n", shared_variable);

    return 0;
}
```

## Process Creation and Execution

### spawn

creation of a new process, a process can be spawned using various commands, such as `fork()` or `exec()` or `clone()`

##### Fundamental

```c
#include <unistd.h> //C 和C++ 程式設計語言中提供對POSIX 作業系統API 的訪問功能的標頭檔的名稱
#include <stdio.h>

int main() {
    pid_t child_pid = fork(); //fork():在當前的process分支建立一個一模一樣的子process
    //pid：process ID

    switch(child_pid){
        // PID == -1 代表 fork 出錯
        case -1:
            perror("fork()");
            exit(-1);
        
        // PID == 0 代表是子程序
        case 0:
            printf("I'm Child process\n");
            printf("Child's PID is %d\n", getpid());
            break;
        
        // PID > 0 代表是父程序
        default:
            printf("I'm Parent process\n");
            printf("Parent's PID is %d\n", getpid());
    }

    return 0;
}
```

##### 殭屍程序

不做任何事但佔用系統資源的程序，當父程序結束但子程序還在運行的話就會發生。

解決方式：`signal()` 或 `wait()`

```c++
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>

int main(){
    int exit_status;
    pid_t PID = fork();

    switch(PID){
        case -1:
            perror("fork()");
            exit(-1);
        case 0:
            printf("[Child] I'm Child process\n");
            printf("[Child] Child's PID is %d\n", getpid());
            printf("[Child] Enter my exit status: ");
            scanf("%d", &exit_status);
            sleep(3);
            break;
        default:
            printf("[Parent] I'm Parent process\n");
            printf("[Parent] Parent's PID is %d\n", getpid());
            wait(&exit_status);
            // WEXITSTATUS is an macro
            printf("[Parent] Child's exit status is [%d]\n", WEXITSTATUS(exit_status));
    }

    return 0;
}
```

### trampoline

A **trampoline** typically refers to a small piece of code used to redirect execution flow.



Can be used to perform tasks like jumping to a different section of code, setting up a specific environment, or achieving  position-independent code execution.

Handle the software vulnerabilities, such as buffer overflows or code injection attacks.



可以在不同的CPU之間傳遞control flow，當一个任務需要在不同的CPU之間切換時，他會通過trampoline將自己的狀態保存到一个共享的數據結構中，並將control flow傳遞给另一個CPU的trampoline。接收到控制流的trampoline會根據共享數據結構中的訊息恢復任務的狀態，並繼續執行任務。
