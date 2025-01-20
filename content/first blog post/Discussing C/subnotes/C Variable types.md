### Variables
- varType varName = value

#### **Types**:

| Datentyp             | Wertebereich (min.)                                          | Formatzeichen                        | Größe (Bits)       |
| -------------------- | ------------------------------------------------------------ | ------------------------------------ | ------------------ |
| **signed char**      | -128<br>bis +127                                             | `%hhd` (für dezimal), `%c` (für Zeichen) | 8                |
| **unsigned char**    | 0<br>bis 255                                                 | `%hhu`                               | 8                |
| **short**            | -32.768<br>bis +32.767                                       | `%hd` oder `%hi`                     | 16               |
| **unsigned short**   | 0<br>bis 65.535                                              | `%hu`                                | 16               |
| **int**              | -32.768<br>bis +32.767 (auf einigen Systemen -2.147.483.648 bis +2.147.483.647) | `%d` oder `%i`                  | 16/32 (plattformabhängig) |
| **unsigned int**     | 0<br>bis 65.535 (auf einigen Systemen bis 4.294.967.295)     | `%u`                                 | 16/32 (plattformabhängig) |
| **long**             | -2.147.483.648<br>bis +2.147.483.647                         | `%ld` oder `%li`                     | 32               |
| **unsigned long**    | 0<br>bis 4.294.967.295                                       | `%lu`                                | 32               |
| **long long (seit C99)** | -9.223.372.036.854.775.808<br>bis +9.223.372.036.854.775.807 | `%lld` oder `%lli`             | 64               |
| **unsigned long long** | 0<br>bis 18.446.744.073.709.551.615                        | `%llu`                               | 64               |
| **bool (seit C99)**  | 0 und 1                                                      | `%u`                                 | 1 (in der Praxis oft 8) |
| **float**            | 1.2E-38<br>bis 3.4E+38                                       | `%f`                                 | 32               |
| **double**           | 2.3E-308<br>bis 1.7E+308                                     | `%f` (`%lf` für `scanf`)             | 64               |
| **long double**      | 3.4E-4932<br>bis 1.1E+4932                                   | `%Lf`                                | 80/128 (plattformabhängig) |

signed vs. unsigned
- the variable is signed
- the key difference is the value range
  same amount of values, but unsigned vars include negative values as well. Because of that the positive range of a signed variable is twice as much compared to unsigned variables



constants are unchangeable vars 
```c
const int num = 5;
//the var num cant be changed in the following program
```