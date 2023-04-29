# profanOS main-line convention

The latest profanOS kernel must respect all of the following conventions.
Why conventions? It allows to have regular and harmonious code as well as to prevent some bugs

### 1 - skip a line after a semicolon

```c
// good code
task->regs.eflags = flags;
task->regs.eip = (uint32_t) main;
task->regs.cr3 = (uint32_t) pagedir;

// bad code
task->regs.eflags = flags; task->regs.eip = (uint32_t) main; task->regs.cr3 = (uint32_t) pagedir;
```


### 2 - use snake_case for variables and functions
```c
// good code
int my_var = 0;

// bad code
int myVar = 0;
int myvar = 0;
int My_Var = 0;
```


### 3 - your code must tab with 4 spaces (except Makefile)
```c
// good code
void sys_reboot() {
    uint8_t good = 0x02;
    while (good & 0x02)
        good = port_byte_in(0x64);
    port_byte_out(0x64, 0xFE);
    asm volatile("hlt");
}

// bad code
void sys_reboot() {
    uint8_t good = 0x02;
  while (good & 0x02)
      good = port_byte_in(0x64);
   port_byte_out(0x64, 0xFE);
   asm volatile("hlt");
}
```


### 4 - use dynamic memory for variable size
```c
// good code
char *copy = malloc(strlen(str) + 1);
strcpy(copy, str);

// bad code
char copy[strlen(str) + 1];
strcpy(copy, str);
```


### 5 - use kernel functions for management
```c
// good code
sys_fatal("out of memory");

// bad code
fskprint("$3fatal: out of memory\n");
asm volatile("cli");
asm volatile("hlt");
```


### 6 - use compact syntax
```c
// good code
val = (k == debut) ? 1 : debut;

// bad code
if (k == debut) {
    val = 1;
} else {
    val = debut;
}
```


### 7 - put spaces between operators
```c
// good code
for (int i = 0; i < index + 1; i++) {
    last = (last != -1) ? (last - last % 3) / 3 : imm;
}

// bad code
for (int i=0;i<index+1;i++) {
    last=(last!=-1)?(last-last%3)/3:imm;
}
```


### 8 - use the library and not the driver
```c
// good code
int temps = 10;
ms_sleep(temps * 1000);

// bad code
int temps = 10;
uint32_t start_time = timer_get_tick();
while (timer_get_tick() < start_tick + (uint32_t) temps * 100) {
    do_nothing();
}
```


### 9 - follow the nomenclature of public functions
```c
// good code
int mem_alloc(int size);
int mem_get_usage();
int mem_get_usable();
int mem_get_alloc_count();

// bad code
int alloc_mem(int size);
int usage_of_memory();
int usable_memory();
int count_of_alloc();
```


### 10 - your code must not exceed 4 indentation tabs
```c
// good code
int start(int addr, int arg) {
    ...

    for (int i = 0; i < max; i++) {
        ...
        if (str[str_index] != '\n') continue;
        ...
        if (line % 14) continue;
        for (j = 0; str[j] != '\n'; j++)
            temps[j] = str[j];
        ...
    }
}

// bad code
int start(int addr, int arg) {
    ...

    for (int i = 0; i < max; i++) {
        ...
        if (str[str_index] == '\n') {
            ...
            if (line % 14 == 0) {
                for (j = 0; str[j] != '\n'; j++)
                    temps[j] = str[j]; // 5 tabs
                ...
            }
        }
    }
}
```


### 11 - comment magic numbers
```c
// good code
if (new_pos >= 3998)    // (row * col + (col - 1)) * 2
    old_cursor -= 160;  // row * 2

// bad code
if (new_pos >= 3998)
    old_cursor -= 160;
```


### 12 - commentary conventions
```c
// good one line comment

/* good long multi
 * line comment */

/***********************
 * GOOD TITLE COMMENT *
***********************/
```


### 13 - pointer initialization
```c
// good code
void *ptr = malloc(10);

// bad code
void * ptr = malloc(10);
void* ptr = malloc(10);
```


### 14 - don't use memory after free
```c
// good code
void *ptr = malloc(10);
USING(ptr);
free(ptr);

// bad code
void *ptr = malloc(10);
free(ptr);
USING(ptr);
```
