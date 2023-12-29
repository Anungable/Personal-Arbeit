Linux分成**User space**和**Kernel space**，兩者之間透過Interface溝通。

<img src="https://embetronicx.com/wp-content/uploads/2017/08/kernel-space-vs-user-space.png" alt="Linux Device Driver Part 1 - Introduction" style="zoom:67%;" />

### Linux Kernel Module

若要加上自己寫的code到Linux kernel內，可以透過1.持接寫入kernel原始碼（base kernel, under /boot/）然後編譯，或是2.在run time的時候加入 （又稱loadable kernel modules, **LKM**）

LKM例子：device driver, system calls, filesystem driver

Device driver：硬體抽象化

Filesystem driver：disk上文件和路徑的interpretation

System calls：userspace get services from kernel, 通常會值些寫入base kernel而非LKM

---

運行在kernel的叫module，優先權高於application，非sequential

運行在userspace的叫application

這兩個的memory space是分開的，以免互相影響。

---

### Linux device driver

- character device：R/W char by char, e.g. printer, keyboard
- block device：R/W bulk of data, e.g. USB, HDD, CD-ROM
- network device：R/W packet of data, e.g. ethernet card

---

### Module Parameters Macros

- `module_param`：initialize argument

  ```shell
  module_param(value, int, S_IWUSR|S_IRUSR)
  ```

  `S_I`: common header

- `module_param_array`：pass array as an argument

  ```shell
  module_param_array(name, type, num, perm)
  ```

  `perm`: permission

- `module_param_cb`：register the callback

