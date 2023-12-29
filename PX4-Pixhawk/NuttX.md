### NuttX

|                   | task                                                         | pthread                                              |
| ----------------- | ------------------------------------------------------------ | ---------------------------------------------------- |
| file descriptor   | If `CONFIG_DEV_CONSOLE` is defined, the first three file descriptors (stdin, stdout, stderr) will be duplicated for the new task. <br />File-related operations (open, close, etc.) within a task will have no effect on other tasks. | always share file descriptors with the parent thread |
| control interface | [看下面](Task control interface)                             |                                                      |
|                   |                                                              |                                                      |
|                   |                                                              |                                                      |

### Task control interface

- non-standard

  > - [`task_create()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.task_create)
  > - [`task_delete()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.task_delete)
  > - `task_restart()`
  >
  > 下面支援Posix
  >
  > - [`task_setcancelstate()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.task_setcancelstate)
  > - [`task_setcanceltype()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.task_setcanceltype)
  > - [`task_testcancel()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.task_testcancel)

- standard `posix_spawn`

  > - [`posix_spawn()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.posix_spawn) and [`posix_spawnp()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.posix_spawnp)
  > - [`posix_spawn_file_actions_init()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.posix_spawn_file_actions_init)
  > - [`posix_spawn_file_actions_destroy()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.posix_spawn_file_actions_destroy)
  > - [`posix_spawn_file_actions_addclose()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.posix_spawn_file_actions_addclose)
  > - [`posix_spawn_file_actions_adddup2()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.posix_spawn_file_actions_adddup2)
  > - [`posix_spawn_file_actions_addopen()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.posix_spawn_file_actions_addopen)
  > - [`posix_spawnattr_init()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.posix_spawnattr_init)
  > - [`posix_spawnattr_getflags()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.posix_spawnattr_getflags)
  > - [`posix_spawnattr_getschedparam()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.posix_spawnattr_getschedparam)
  > - [`posix_spawnattr_getschedpolicy()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.posix_spawnattr_getschedpolicy)
  > - [`posix_spawnattr_getsigmask()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.posix_spawnattr_getsigmask)
  > - [`posix_spawnattr_setflags()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.posix_spawnattr_setflags)
  > - [`posix_spawnattr_setschedparam()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.posix_spawnattr_setschedparam)
  > - [`posix_spawnattr_setschedpolicy()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.posix_spawnattr_setschedpolicy)
  > - [`posix_spawnattr_setsigmask()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.posix_spawnattr_setsigmask)

- nonstandard `posix_spawn`

  > - [`task_spawn()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.task_spawn)
  > - [`posix_spawnattr_getstacksize()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.posix_spawnattr_getstacksize)
  > - [`posix_spawnattr_setstacksize()`](https://nuttx.apache.org/docs/latest/reference/user/01_task_control.html#c.posix_spawnattr_setstacksize)

