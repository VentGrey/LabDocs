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
        printf(" Las llaves cómo se ven aquí :) ");
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
#### 3.1 - Espacios

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


