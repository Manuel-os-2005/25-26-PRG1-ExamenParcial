# Examen Parcial - Manuel-os-2005

**Usuario GitHub:** Manuel-os-2005
**Fecha:** 4 de noviembre de 2025
**Retos tenidos en cuenta:** Reto 001, Reto 002

---

## Instrucciones

A continuación encontrarás fragmentos de código extraídos de tus entregas. Cada fragmento contiene una o más situaciones relacionadas con los conceptos vistos en clase.

Para cada pregunta debes:
1) Identificar a qué se refiere la observación
2) Explicar si es o no un error y por qué
3) Proponer la corrección

Nota: Responde 5 de las 9 preguntas (en función a lo indicado en el examen).


---

## Pregunta 1

Archivo: `CalculadoraDePrecio.java` — [Ver archivo](https://github.com/mmasias/25-26-PRG1/blob/1876fbf4f06a47bf6d7997067adf1984538ee87c/evaluaciones/retos/CalculadoraDePrecio.java) (Reto 001)

```java
double descuento=0;
descuento=(unidades<10?0:(unidades<50?0.05:(unidades<100?0.10:0.15)));
```

¿Qué observas en este código?

Observación

En este fragmento se utiliza un operador ternario anidado para calcular el valor del descuento según la cantidad de unidades. Aunque el cálculo es correcto, este tipo de estructura hace que el código sea más difícil de leer y de mantener, sobre todo cuando hay varios rangos de condiciones.
Antes del cálculo, se declara y asigna la variable double descuento = 0;, lo cual es innecesario porque en la siguiente línea se vuelve a asignar un valor. Esto genera una redundancia que no aporta nada al código.
También se puede ver que las variables usan formato camelCase en lugar del estilo acordado en clase, que es minúsculas_con_barras_bajas.
Los mensajes de consola no son del todo correctos: hay un paréntesis sin cerrar en la línea del IVA y una “O” mayúscula que puede confundirse con el número cero.
Por otro lado, el uso de double para valores monetarios es aceptable, aunque sería más recomendable trabajar con céntimos (enteros) o formatear la salida a dos decimales para evitar errores de precisión.
En general, el código funciona, pero no cumple del todo con las normas de claridad, formato y estilo vistas en clase.

¿Es error?

No es un error de ejecución, ya que el programa se ejecuta correctamente y da los resultados esperados.
Sin embargo, sí se considera un error de estilo y de mantenimiento porque el uso del operador ternario anidado y la asignación redundante van en contra de los criterios de código limpio y legible.

Justificación

En clase se insistió en que es mejor utilizar estructuras condicionales if/else if cuando existen varios casos posibles. Estas estructuras facilitan la lectura y la modificación del código.
La legibilidad debe ser prioritaria frente a la concisión, ya que un código claro se entiende mejor y se puede mantener sin dificultad.
Mantener una nomenclatura coherente y usar un formato uniforme en las variables y mensajes de salida mejora la comprensión general del programa.
Además, formatear la salida numérica para mostrar solo los decimales necesarios hace que los resultados sean más precisos y fáciles de interpretar.

-- Propuesta corregida 

import java.util.Scanner;

public class CalculadoraDePrecio {
    public static void main(String[] args) {
        Scanner entrada = new Scanner(System.in);
        System.out.println("precio unitario base (centimos)?");
        int precio_base_centimos = entrada.nextInt();
        System.out.println("cantidad de unidades?");
        int unidades = entrada.nextInt();
        System.out.println("tipo de iva (21, 10 o 4)?");
        int iva = entrada.nextInt();

        double precio_unitario = precio_base_centimos / 100.0;
        double descuento;
        if (unidades < 10) {
            descuento = 0.0;
        } else if (unidades < 50) {
            descuento = 0.05;
        } else if (unidades < 100) {
            descuento = 0.10;
        } else {
            descuento = 0.15;
        }

        double precio_unitario_con_iva = precio_unitario + (precio_unitario * iva / 100.0);
        double precio_unitario_final = precio_unitario_con_iva - (precio_unitario_con_iva * descuento);
        double precio_total = precio_unitario_final * unidades;

        System.out.printf("precio unitario base: %.2f euros%n", precio_unitario);
        System.out.printf("iva aplicado: %d%%%n", iva);
        System.out.printf("descuento aplicado: %.0f%%%n", descuento * 100);
        System.out.printf("precio unitario con iva: %.2f euros%n", precio_unitario_con_iva);
        System.out.printf("precio unitario final: %.2f euros%n", precio_unitario_final);
        System.out.printf("precio total: %.2f euros%n", precio_total);
    }
}

---## Pregunta 2

Archivo: `DevolucionCambio.java` — [Ver archivo](https://github.com/mmasias/25-26-PRG1/blob/1876fbf4f06a47bf6d7997067adf1984538ee87c/evaluaciones/retos/DevolucionCambio.java) (Reto 001)

```java
int billetes=cambio/100;
int resto=cambio%100;
// ...
System.out.println(billetes+" monedas de 1");
```

¿Qué observas en este código?

---Observación

Se reutiliza la variable billetes para diferentes denominaciones, incluyendo las monedas de 1 euro, sin recalcular su valor.
El mensaje "monedas de 1" no coincide con el contenido real de la variable, ya que billetes contiene el valor del cálculo anterior.
Hay una falta de coherencia entre el nombre de la variable, el valor que almacena y el texto mostrado en pantalla.
No se respeta el principio de una variable = un significado, lo que rompe las normas de código limpio.

¿Es error?

Sí, es un error lógico y de salida: el código muestra un valor incorrecto al usuario.

Justificación

Cada denominación debe tener su propia variable para mantener claridad y trazabilidad.
El mensaje de salida debe coincidir con el cálculo realizado.
Es importante no reutilizar variables para distintos propósitos, ya que esto reduce la legibilidad y puede generar errores en la salida.

--Codigo propuesto: 

package evaluaciones.retos;

import java.util.Scanner;

public class DevolucionCambio {
    public static void main(String[] args) {
        Scanner entrada = new Scanner(System.in);
        System.out.println("cuantos euros debe pagar?");
        int euros = entrada.nextInt();
        System.out.println("cuantos euros paga?");
        int euros_recibidos = entrada.nextInt();

        int cambio = euros_recibidos - euros;
        int billetes_100 = cambio / 100;
        int resto = cambio % 100;
        int billetes_50 = resto / 50;
        resto = resto % 50;
        int billetes_20 = resto / 20;
        resto = resto % 20;
        int billetes_10 = resto / 10;
        resto = resto % 10;
        int monedas_5 = resto / 5;
        resto = resto % 5;
        int monedas_2 = resto / 2;
        resto = resto % 2;
        int monedas_1 = resto;

        System.out.println(billetes_100 + " billetes de 100");
        System.out.println(billetes_50 + " billetes de 50");
        System.out.println(billetes_20 + " billetes de 20");
        System.out.println(billetes_10 + " billetes de 10");
        System.out.println(monedas_5 + " monedas de 5");
        System.out.println(monedas_2 + " monedas de 2");
        System.out.println(monedas_1 + " monedas de 1");
    }
}

## Pregunta 3

Archivo: `ConversorDeDuracion.java` — [Ver archivo](https://github.com/mmasias/25-26-PRG1/blob/1876fbf4f06a47bf6d7997067adf1984538ee87c/evaluaciones/retos/ConversorDeDuracion.java) (Reto 001)

```java
int dias=segundos/SEGUNDOS_POR_DIA;
int resto=segundos%SEGUNDOS_POR_DIA;
int horas=resto/SEGUNDOS_POR_HORA;
resto=resto%SEGUNDOS_POR_HORA;
int minutos=resto/SEGUNDOS_POR_MINUTO;
resto=resto%SEGUNDOS_POR_MINUTO;
```

¿Qué observas en este código?

---Observación

En este código se realiza la conversión de una cantidad total de segundos a días, horas, minutos y segundos, utilizando correctamente las operaciones de división y módulo. La lógica de cálculo es correcta, ya que el programa va actualizando el valor del resto en cada paso para no perder información.
Sin embargo, el código puede mejorarse en legibilidad y estructura. Las variables no siguen el formato acordado en clase, ya que deberían escribirse en minúsculas_con_barras_bajas en lugar de camelCase.
Aunque las constantes están bien declaradas en mayúsculas, lo cual facilita su identificación, sería recomendable mantener una organización más clara del bloque de código, dejando espacios entre las partes del proceso para una lectura más fluida.
También se podría mejorar la interacción con el usuario añadiendo un texto de salida más explicativo, para que los resultados sean más fáciles de interpretar.
En general, el programa cumple con su objetivo, pero no se ajusta completamente a las normas de estilo y presentación establecidas.

¿Es error?

No hay error lógico ni sintáctico, el código cumple su función.
Aun así, presenta errores de estilo que afectan a la claridad, la presentación y la legibilidad general del programa.

Justificación

La forma en que se aplican las divisiones y los módulos es correcta y respeta el orden lógico de conversión: primero días, luego horas, después minutos y finalmente los segundos restantes.
En clase se insistió en mantener una estructura clara, donde las variables tengan nombres descriptivos, coherentes y adaptados a las normas de formato.
Se debe buscar siempre que el código sea entendible sin necesidad de comentarios, priorizando la legibilidad y la organización visual.
Mantener consistencia en la nomenclatura y en la forma de presentar los resultados facilita la depuración y la comprensión del código por parte de otros compañeros.

Codigo propuesto; package evaluaciones.retos;

import java.util.Scanner;

public class ConversorDeDuracion {
    public static void main(String[] args) {
        Scanner entrada = new Scanner(System.in);
        System.out.println("cuantos segundos desea convertir?");
        int total_segundos = entrada.nextInt();

        final int segundos_por_minuto = 60;
        final int segundos_por_hora = 3600;
        final int segundos_por_dia = 86400;

        int dias = total_segundos / segundos_por_dia;
        int resto = total_segundos % segundos_por_dia;

        int horas = resto / segundos_por_hora;
        resto = resto % segundos_por_hora;

        int minutos = resto / segundos_por_minuto;
        resto = resto % segundos_por_minuto;

        System.out.println("resultado de la conversion:");
        System.out.println(dias + " dias");
        System.out.println(horas + " horas");
        System.out.println(minutos + " minutos");
        System.out.println(resto + " segundos");
    }
}
## Pregunta 4

Archivo: `Reto_002.java` — [Ver archivo](https://github.com/mmasias/25-26-PRG1/blob/1876fbf4f06a47bf6d7997067adf1984538ee87c/evaluaciones/retos/Reto_002.java) (Reto 002)

```java
boolean vampiroVivo = true;
// ...
vampiroVivo = vidaVampiro <= 0;
if (vampiroVivo) {
    // turno del vampiro
}
```

¿Qué observas en este código?

---

## Pregunta 5

Archivo: `Reto_002.java` — [Ver archivo](https://github.com/mmasias/25-26-PRG1/blob/1876fbf4f06a47bf6d7997067adf1984538ee87c/evaluaciones/retos/Reto_002.java) (Reto 002)

```java
final int ATAQUE_1 = 7;
final double ATAQUE_PROBABILIDAD_1 = 0.5;
// ...
final int ATAQUE_3 = 30;
final double ATAQUE_PROBABILIDAD_3 = 0.12;
```

¿Qué observas en este código?

---Observación

En este fragmento se declaran varias constantes individuales para los ataques y sus probabilidades:
ATAQUE_1, ATAQUE_PROBABILIDAD_1, ATAQUE_2, ATAQUE_PROBABILIDAD_2, ATAQUE_3, ATAQUE_PROBABILIDAD_3.
Aunque el código funciona correctamente, el diseño es repetitivo y poco escalable. Si en el futuro se quisieran añadir más ataques o modificar alguno, habría que editar múltiples líneas y bloques condicionales, aumentando el riesgo de errores.
Se rompe el principio de no repetición (DRY) y se pierde cohesión entre datos relacionados (daño y probabilidad), ya que ambos dependen del mismo índice pero están definidos por separado.
Además, los nombres en mayúsculas son válidos para constantes, pero no respetan las normas establecidas en clase, donde se recomendó el uso de minúsculas_con_barras_bajas para variables y una organización más uniforme para mejorar la legibilidad.
El fragmento podría optimizarse agrupando la información de cada ataque dentro de un array o estructura que relacione directamente daño y probabilidad, reduciendo el código repetido y facilitando la extensión del programa.

¿Es error?

No es un error de ejecución, ya que el código compila y produce el resultado esperado.
Sin embargo, es un error de diseño y de estilo, porque va en contra de las buenas prácticas de programación que fomentan el mantenimiento, la claridad y la escalabilidad del código.

Justificación

En clase se trabajó la idea de modularidad y código limpio, buscando evitar repeticiones innecesarias.
La creación de múltiples variables similares es un síntoma de que el código puede beneficiarse de una estructura de datos más adecuada, como un array o lista.
Agrupar los datos en colecciones permite recorrerlos con bucles, reduciendo la posibilidad de inconsistencias entre los valores de daño y probabilidad.
Además, mantener una nomenclatura clara y homogénea facilita que el código sea comprensible sin depender de comentarios.

-Codigo propuesto; 

import java.util.Scanner;

public class Reto002 {
    public static void main(String[] args) {
        Scanner entrada = new Scanner(System.in);

        int vida_guerrero = 20;
        int vida_vampiro = 10;

        int[] ataques_vampiro_danio = {7, 15, 30};
        double[] ataques_vampiro_probabilidad = {0.5, 0.25, 0.12};

        System.out.println("turno del vampiro");
        int indice_ataque = (int) (Math.random() * ataques_vampiro_danio.length);

        if (Math.random() < ataques_vampiro_probabilidad[indice_ataque]) {
            vida_guerrero = vida_guerrero - ataques_vampiro_danio[indice_ataque];
            System.out.println("el guerrero recibe dano");
        } else {
            System.out.println("el guerrero esquiva el ataque");
        }

        System.out.println("vida guerrero [" + vida_guerrero + "] / vida vampiro [" + vida_vampiro + "]");
    }
}
## Pregunta 6

Archivo: `DevolucionCambio.java` — [Ver archivo](https://github.com/mmasias/25-26-PRG1/blob/1876fbf4f06a47bf6d7997067adf1984538ee87c/evaluaciones/retos/DevolucionCambio.java) (Reto 001)

```java
billetes=resto/2;
resto=resto%2;
System.out.println(billetes+" monedas de 2");

System.out.println(billetes+" monedas de 1");
```

¿Qué observas en este código?

---Observación

Se reutiliza la variable billetes para diferentes cálculos, incluyendo monedas de 2 y monedas de 1 sin recalcular su valor.
El nombre billetes no es adecuado cuando también se usa para monedas, lo que genera confusión entre el cálculo y el mensaje mostrado.
Esto provoca que el número de monedas de 1 sea incorrecto y que la salida no coincida con los valores reales.
El código funciona, pero incumple las normas de claridad y de nombres coherentes vistas en clase.

¿Es error?

Sí, es un error lógico y de salida.
La variable billetes se reutiliza para diferentes valores, generando una salida incorrecta aunque el programa no falle.

Justificación

Cada variable debe representar un solo dato y no cambiar de función en el mismo bloque.
Los nombres deben reflejar con precisión su contenido, manteniendo coherencia entre el cálculo y la salida.
Separar los cálculos por denominación mejora la legibilidad, la trazabilidad y el mantenimiento del código.

--Codigo propuesto; package evaluaciones.retos;

import java.util.Scanner;

public class DevolucionCambio {
    public static void main(String[] args) {
        Scanner entrada = new Scanner(System.in);
        System.out.println("cuantos euros debe pagar?");
        int euros = entrada.nextInt();
        System.out.println("cuantos euros paga?");
        int euros_recibidos = entrada.nextInt();

        int cambio = euros_recibidos - euros;
        int billetes_100 = cambio / 100;
        int resto = cambio % 100;
        int billetes_50 = resto / 50;
        resto = resto % 50;
        int billetes_20 = resto / 20;
        resto = resto % 20;
        int billetes_10 = resto / 10;
        resto = resto % 10;
        int monedas_5 = resto / 5;
        resto = resto % 5;
        int monedas_2 = resto / 2;
        resto = resto % 2;
        int monedas_1 = resto;

        System.out.println(billetes_100 + " billetes de 100");
        System.out.println(billetes_50 + " billetes de 50");
        System.out.println(billetes_20 + " billetes de 20");
        System.out.println(billetes_10 + " billetes de 10");
        System.out.println(monedas_5 + " monedas de 5");
        System.out.println(monedas_2 + " monedas de 2");
        System.out.println(monedas_1 + " monedas de 1");
    }
}
## Pregunta 7

Archivo: `Reto_002.java` — [Ver archivo](https://github.com/mmasias/25-26-PRG1/blob/1876fbf4f06a47bf6d7997067adf1984538ee87c/evaluaciones/retos/Reto_002.java) (Reto 002)

```java
vampiroVivo = vidaVampiro <= 0;

if (vampiroVivo) {
    int ataque = (int) (Math.random() * 3) + 1;
    if (ataque == 1) {
        if (Math.random() < ATAQUE_PROBABILIDAD_1) {
            vidaVampiro = vidaVampiro - ATAQUE_1;
            System.out.println("El vampiro recibe daño");
```

¿Qué observas en este código?

---

## Pregunta 8

Archivo: `Reto_002.java` — [Ver archivo](https://github.com/mmasias/25-26-PRG1/blob/1876fbf4f06a47bf6d7997067adf1984538ee87c/evaluaciones/retos/Reto_002.java) (Reto 002)

```java
final int DAÑO_ESPADA = 2;
int vidaGuerrero = 20;
final double PORCENTAJE_EXITO_GUERRERO = 0.5;

// Estas constantes nunca se usan en el código
```

¿Qué observas en este código?

---

## Pregunta 9

Archivo: `CalculadoraDePrecio.java` — [Ver archivo](https://github.com/mmasias/25-26-PRG1/blob/1876fbf4f06a47bf6d7997067adf1984538ee87c/evaluaciones/retos/CalculadoraDePrecio.java) (Reto 001)

```java
System.out.println("Descuento aplicado: "+(descuento*100+"%"));
```

¿Qué observas en este código?


