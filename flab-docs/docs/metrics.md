# Estándares de código para Future Lab

En esta página se mostrarán los estandares de código utilizados por Future Lab.

Los lenguajes soportados (actualmente) por miembros de Future Lab son:

 * C (Cristofer Nava, Oliver López, Omar Purata).
 * Python 3 (Luis Sustaita, Rodolfo Ferro, Ricardo Mirón, Anthony Smith, etc.)
 * Rust (Omar Purata)
 * JavaScript (Oliver López, Adolfo Ramírez)

## ¿Por qué un estándar?

En Future Lab nuestros desarrolladores constantemente colaboran entre sí para realizar
proyectos dentro de las instalaciones, es importante establecer medidas para que el
código enviado a producción sea legible, modular y fácil de mantener.

-------

## C

El código escrito en el lenguaje de programación C deberá seguir los siguientes
criterios:

**Los estándares están escritos para C11.**

### 1- Indentación

Las tabulaciones son de 8 carácteres, por lo tanto los indents del código serán
de 8 carácteres.

**Cita sobre los indents de 8 espacios:**

> *Algunas personas podrían decir que tener indents de 8 espacios hace que el*
> *código se mueva mucho hacia la derecha y que ésto hace que sea difícil leer*
> *en terminales de 80 carácteres. La respuesta a ello es simple, si necesitas*
> *más de 3 niveles de indentación en tu código, estás frito y deberías de*
> *reescribir tu programa.*

**EVITE** poner múltiples sentencias en una línea:

```c
if (condición) hacer_esto:
        hacer_algo_cada_vez;
```
### 2- Rompe líneas y cadenas largas

El estílo de código se hizo para facilitar la lectura y mantenimiento del
código.

El límite de la longitud de las líneas en el código es de `80` columnas.

Todas las sentencias mayores a 80 columnas deberán ser "partidas" en trozos
sensibles, a menos que exceder las 80 columnas incremente la facilidad de
lectura.

Los descendientes de las líneas o cadenas deberán ser menores al padre y
se acomodarán a la derecha.

Lo mismo aplica para las cabeceras de las funciones con varios argumentos.

Nunca rompa cadenas visibles al usuario ya que se dificultaría su búsqueda.


### 3- Sobre las llaves y los espacios

Otro de los problemas que viene con C es el lugar donde se colocarán las
llaves y los espacios. A diferencia del tamaño de los indents existe una
razón técnica de porque se deberia de elegir una colocación sobre otra, aun
así, la manera que adoptaremos sera la mostrada por los maestros Kernighan &
Dennis Ritchie, la cual consiste en poner la llave inicial hasta el final de
la línea y colocar la llave de cierre al inicio:

```c
int main() {
        printf("Las llaves cómo se ven aquí :)");
}
```

lo mismo aplica para toda sentencia que no sea una función como:

 * `if`
 * `switch`
 * `for`
 * `while`
 * `do`

Ej:

```c
switch (acción) {
case caso_1:
        return 0;
case caso_2:
        return 0;
case caso_3:
        return 0;
default:
        return NULL;
}
```

Existe un caso especial (funciones), en las cuales, algunos programadores
colocan la llave de apertura al inicio de la siguiente línea:

```c
int func_suma(int x, int y)
{

        //Cuerpo de la función.

}
```

Muchos han tachado ésta forma de inconsistente, normalmente por que la gente
piensa en 2 cosas:
  * K & R están bien.
  * K & R están bien.
(Tampoco es que importe mucho ya que no puedes anidar funciones en C).

Nótese que la llave de cierre se considera "vacía" cuando se encuentra sola
en una línea, **excepto** en casos donde se continúa una sentencia previa.

Por ejemplo un `while` en una sentencia `do` o un `else` en una sentencia `if`.

```c

do {
        //Cuerpo de el ciclo do.
} while (condición);
```

Y

```c
if (x == y) {
        ..
} else if (x > y) {
        ...
} else {
        ....
}
```

Además, nótese que éste tipo de acomodo en las llaves minimiza el número de
líneas vacías (o casi vacías) sin perder nada de facilidad de lectura.

**Evite** poner llaves donde no son necesarias, ergo, donde una sola sentencia
es mas que suficiente:

```c
if (condicion)
        acción();
```

y

```c
if (condicion)
        acción();
else
        acción2();
```

Ésto no aplica si solo una de las ramas de la sentencia condicional es una
es una sentencia sola, en otros casos las llaves serán necesarias:

```c
if (condición) {
        acción();
        acción2();
} else {
        otracosa();
}
```
#### 3.1- Espacios

Use un espacio después de (la mayoría) de las palabras reservadas de C.

Las excepciones notables con `sizeof`, `typeof`, `aligof` y `__attribute__`,
las cuales parecen funciones, así que use espacios después de éstas palabras:

```c
if, switch, case, for, do, while
```
Pero no en las palabras anteriormente mencionadas

```c
s = sizeof(struct file);
```

**NO** agregue espacios dentro de las expresiones con paréntesis:
**El siguiente ejemplo es lo que NO debe hacer**

```c
s = sizeof( struct file );
```

Cuando declare punteros utilice el operador `*` adyacente a el nombre del dato
o nombre de la funcion y no al nombre del tipo:

Bien:

```c
char *puntero;
long long super_punteros(char *puntero **punteroapuntero);
char *punteros_raros(subpuntero *s);
```

Mal:

```c
char* puntero;
long long super_punteros(char* puntero **punteroapuntero);
char* punteros_raros(subpuntero *s);
```

Utilice un espacio en cada lado de los operadores binarios y ternarios:

```c
= + - < > * / % | & ^ <= >= == != ? :
```

pero no incluya un espacio después de los operadoes unarios:

```c
& * + - ~ ! sizeof typeof alignof __attribute__ defined
```

No incluya espacios en los operadores unarios de incremento y decremento:

```c
++ --
```

Y no incluya espacios alrededor de los operadores `.` y `->`.

No deje espacios en blanco al final de las líneas. Algunos editores con
indentación "`inteligente`" van a insertar un espacio en blando al inicio de
las nuevas líneas, asi que usted podrá comenzar a tirar código de inmediato.
PERO, algunos editores no eliminan éste espacio y uno termina sin agregar
código en la línea completa, por lo que uno termina con líneas con espacios
sobrantes:

> Utilice la selección de su cursos para notar el siguiente ejemplo:

```c
int main() {
        printf("Soy un código sin espacios innecesarios :D");
}
```

VS

```c
int main() { 
        printf("Yo tengo espacios innecesarios :("); 
} 
```

### 4- Nombres

C es un lenguaje robusto y como lenguaje robusto, los nombres de tus
variables deberán ser robustos también, los programadores en C no utilizan
nombres de variables como: `EstoEsUnContadorTemporal`. Un programador de C
llama a su variable `tmp`, que es muy fácil de escribir y no más difícil de
entender.

**Sin embargo**, aunque los nombres con letras mezcladas (nomeclatura Camello)
se ven mal, los nombres descriptivos para las variables son un *must*.

Llamar a una función o variable global `foo` es una ofensa.

Las variables globales (úselas solo cuando **realmente** las necesite)
deberán tener nombres descriptivos, al igual que las funciones globales.

Si usted tiene una función que cuenta el número de usuarios activos, deberá
de llamarla `count_active_users()` o de una forma similar. **NO** deberá
llamarla `cntactsrs()`.

Las variables locales deberán de tener nombres cortos y directos al punto. Si
usted tiene un contador con de enteros la variable normalmente deberia de
llamarse `i`, llamarla `contador_ciclo` sería ineficiente (por no decir tonto)
. simplemente `tmp`, ese sería un buen nombre de variable para un temporal.

Si tiene miedo de mezclar nombres de variables entonces tiene otro problema.

### 5- Typedef

Por favor no utilice cosas como `vps_t`. Es un **horror** utilizar typedef para
estructuras y punteros, cuando vea un:

`vps_t a;`

en el código fuente significa:

`struct virtual_container *a;`

y no hace falta explicar que significa `a`.

Normalmente se piensa que los typedefs `mejoran la experiencia de lectura`,
aunque realmente se utilizan para:
    * Objetos totalmente opacos (donde typedef es para esconder el interior)
    * Tipos de enteros claros, para evitar confusiones entre `int` y `long`.
    * Nuevos tipos idénticos a los de C99.
    * Son seguros para el userspace

### 6- Funciones

El nombre de las funciones deberá de ser corto y preciso. Deberán de cabe
dentro de una o dos pantallas de texto (la pantalla del ISO/ANSI es de 80x24
como sabemos) y deberá hacer una sola cosa y hacerla bien.

La longitud máxima de una función es inversamente proporcional a la
complejidad y el nivel de indentación de dicha funcion. Asi que si tienes una
función conceptualmente simple que es una sentencia `case` larga pero simple
donde tienes que hacer muchas evaluaciones pequeñas está bien tener una
función larga.

Pero, si tuviése una función mas compleja y sospechas que un estudiante de
tu universidad un poco menos "agraciado" que tú pueda tener problemas
entendiendo el código de la función es recomendable que se apegue al máximo
con el límite. Utilice funciones "ayudantes" con nombres descriptivos.

Otra forma de "medir" una función es por el número de variables locales.
Normalmente no se deberían de exceder las 5-10 variables locales, en caso
contrario algo estará haciendo mal. Reformule su función, rómpala en pedazos
mas pequeños.

> Un cerebro humano puede rastrear fácilmente a 7 cosas diferentes, una mas
> y comienza a confundirse.

Usted puede sentir que es brillante, pero quizá le gustaría saber que hizo
hace dos semanas.

En el código fuente, separe las funciones con una línea en blanco. Si la
función es exportada entonces el macro `EXPORT` deberia seguir inmediatamente
despues de la llave de cierre, ej:

```c
int system_is_up(void)
{
        return system_state == SYSTEM_RUNNING;
}
EXPORT_SYMBOL (system_is_up);
```

En los prototipos de las funciones, incluya los nombres de los parámetros con
los tipos de dato. Aunque ésto no es requerido por C, es preferible dentro
de los sistemas tipo Unix porque es una manera mas simple de proporcionale
información al lector.

### 7- Salida de funciones centralizada

Aunque sea muy odiado por los buenos programadores, el equivalente de la
sentencia `goto` usada frecuentemente por los compiladores en la forma de
una instrucción de salto sin condición.

La sentencia `goto` es útil cuando la función tiene múltiples salidas y
el mismo trabajo de mantenimiento (como limpieza de memoria) se necesita hacer

Si no se necesita hacer limpieza alguna simplemente salga de la función.

Elija nombres de identificador que indique qué hace `goto` o porque `goto`
existe. Un buen nombre sería `out_free_buffer:` si es que el `goto` libera
el buffer. **EVITE** utilizar nombres como los de GW-BASIC por ejemplo:
`err1:` y `err2:`. porque tendría que re-enumerarlos si es que agrega o
elimina caminos de salida.

Las justificaciones para usar `goto` son:
 * Las sentencias incondicionales son mas fáciles de leer y seguir.
 * Se reduce el anidado.
 * Los errores que se dan al no actualizar puntos de salida cuando se hacen modificaciones se evitan.
 * Le ahorra el trabajo al compilador de optimizar código redundante.

```c
int func(int a)
{
        int resultado = 0;
        char *buffer;

        buffer = kmalloc(SIZE, GFP_KERNEL);
        if (!buffer)
                return -ENOMEM;

        if (condicional1) {
                while (loop1) {
                        ...
                }
                result = 1;
                goto out_free_buffer;
        }
        ...
out_free_buffer:
        kfree(buffer);
        return resultado;
}
```

Un tipo de error común a tener en cuenta es el bug `one err` que se ve así:

```c
err:
        kfree(foo->bar);
        kfree(foo);
        return ret;
```

El error de éste código es que algunos caminos de salida para `foo` son `NULL`.
Normalmente la manera de arreglar ésto es "romper" el código en 2 identificadores
de error `err_free_bar:` y `err_free_foo:`:

```c
err_free_bar:
        kfree(foo->bar);
err_free_foo:
        kfree(foo);
        return ret;
```

Igual evite confiarse y trate de simular errores para probar TODOS sus caminos
de salida.

### 8- Comentarios

Los comentarios en el código siempre son buenos, aunque siempre existe el
riesgo de sobre-comentar un código.
**NUNCA** trate de explicar cómo funciona su código en un comentario:
es mucho mejor escribir el código de manera en la que la funcionalidad sea
obvia, ademas es una pérdida de tiempo explicar mal código.

Generalemente usted querrá explicar **QUE** hace su código y no **COMO**
lo hace. Además, evite poner comentarios dentro del cuerpo de una función:

Si la función es tan compleja al punto en el que tiene que separarla y poner
comentarios para cada parte, probablemente necesite leer el capítulo 6 por un
buen rato antes de continuar con su código. Puede hacer pequeños comentarios
para notas o para advertir acerca de algo genial (o muy feo), pero evite
excederse. En su lugar ponga los comentarios antes de la función, indicando
que hace y posiblemente por que lo hace.

Para comentarios multilinea el estilo preferente es:

```c
/*
* Este es el estilo preferido para
* los comentarios multilinea
* dentro de Future Lab
* Y los códigos en C que se hagan
*
* Descripción: Un montón de asteriscos en el lado
* izquierdo de la pantalla.
*/
```

También es importante comentar los datos, sean tipos básicos o derivados.


### 9- Hiciste un atascadero...

Está bien, todos lo hacemos. Probablemente tus queridos amigos te han dicho que
editores como `Gnu EMACS` o `GitHub Atom` formatean el código de C de manera
automática y probablemente te hayas dado cuenta de que efectivamente lo hacen
pero los valores por defecto que usan van mas allá de lo "horrible". De hecho
son peor que escribir con la cabeza, un número infinito de simios escribiendo
en éstos editores con sus valores por defecto jamás harían un buen programa.

> Lo mismo aplica a cualquier editor del cual se conserven sus valores de
> edición por defecto.

Así que usted puede eliminar `Atom` o `Gnu EMACS` o simplemente cambiar sus
valores por unos mas "correctos".

Incluso si falla en hacer que EMACS o Atom hagan un buen trabajo no todo está
perdido, puede usar `indent`.

`GNU indent` tiene las mismas opciones feas de `GNU emacs`. Sin embargo indent
es dócil y fácil de modificar ya que los autores de éste saben reconocer la
autoridad de K&R así que, si le damos al programa las opciones `-kr -i8` éste
indentará nuestro código de una manera correcta.

`indent` tiene un montón de opciones, sobre todo cuando se refiere a
re-formatear el código, solo hace falta un vistazo al manual.

Recuerde que `indent` no es una solución para **Ser un mal programador**.


