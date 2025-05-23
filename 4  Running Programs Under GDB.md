以下是 **GDB 启动程序（Starting your Program）** 核心用法的提炼总结，按功能分类：

---

### **1. 运行程序（run / r）**
#### **基本用法**
```gdb
(gdb) run                  # 启动程序
(gdb) run arg1 arg2        # 带参数启动
```
- **前提条件**：需提前用 `file` 或启动时指定程序（如 `gdb ./program`）。
- **注意**：若调试远程目标（如 `target remote`），可能需改用 `continue` 或 `load`。

#### **关键点**
- 参数会通过 Shell 传递（支持通配符和变量替换），可通过 `set startup-with-shell off` 禁用 Shell。
- 程序环境继承自 GDB，可通过 `set env` 和 `unset env` 修改。

---

### **2. 从主函数开始调试（start）**
```gdb
(gdb) start arg1 arg2      # 停在 main 函数入口，并传递参数
```
- **等效操作**：临时断点 `main` + `run`。
- **适用场景**：快速跳过语言相关的初始化阶段（如 C++ 全局对象构造）。
- **注意**：某些语言（如 Ada）的“主函数”名称可能非 `main`。

---

### **3. 从程序第一条指令开始调试（starti）**
```gdb
(gdb) starti               # 停在程序的第一条指令
```
- **用途**：调试初始化阶段（如动态库加载、静态对象构造）。
- **对比**：`start` 停在 `main`，而 `starti` 停在程序入口点（如 `_start`）。

---

### **4. 程序运行控制**
| 命令                | 作用                               |
|---------------------|-----------------------------------|
| `kill`             | 终止正在运行的程序                 |
| `set args arg1`    | 设置程序参数（下次 `run` 生效）    |
| `show args`        | 查看当前设置的参数                 |
| `tty /dev/pts/1`   | 重定向程序输入输出到指定终端       |



---

### **速查表**
| 场景                     | 命令                          |
|--------------------------|-------------------------------|
| 普通启动                 | `run`                         |
| 调试初始化代码           | `starti`                      |
| 跳过语言初始化           | `start`                       |
| 设置环境变量             | `set env VAR=value`           |
| 禁用地址随机化           | `set disable-randomization on`|

通过以上命令组合，可覆盖大多数调试启动需求。更多细节参考 [GDB 官方文档](https://sourceware.org/gdb/current/onlinedocs/gdb.html/Starting.html#Starting)。
