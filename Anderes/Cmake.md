| CMake 指令列表                                        | 說明                                                         |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| cmake_minimum_required                                | cmake 的最小的版本                                           |
| set(variable value… [PARENT_SCOPE])                   | 設置變量variable的值value, [PARENT_SCOPE] 可選擇表示變量的作用域 |
| list(APPEND list element…)                            | 把 element 附加到 list 中                                    |
| list(GET list index variable)                         | 从 list 中獲取给定index的值放到變量中                        |
| include(file/module)                                  | 導入file或 module 並執行                                     |
| file(GLOB_RECURSE variable RELATIVE path expression)  | 生成匹配expression的相對于 path 的文件列表                   |
| message(STATUS string)                                | 向終端輸出string                                             |
| set_property(GLOBAL PROPERTY name value)              | 設置全局屬性 name 的值為 value                               |
| option(variable help_string [value])                  | 設置variable 的值                                            |
| add_subdirectory(directory)                           | 添加一个需要 build的子文件夹                                 |
| include_directories(directory)                        | 把目錄directory添加到可以被cmake include 的文件的搜索路徑中  |
| link_directories(directory)                           | 把目錄directory 添加到linker的搜索路徑中                     |
| add_custom_target(Name COMMAND COMMENT USES_TERMINAL) | 添加一个没有輸出的並且總會被編譯的目標, COMMAND 为一些待执行的命令, USES_TERMINAL 代表是否可以直接獲取到終端 |



