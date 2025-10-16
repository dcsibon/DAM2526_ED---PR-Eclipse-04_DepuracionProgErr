
# 🐞 Práctica: Depuración de código en Eclipse

## Objetivo

* Usar el **depurador** de Eclipse (breakpoints, Resume, Step Over/Into/Return).
* Observar **variables** y **flujo** de ejecución.
* **Encontrar y describir** errores (compilación, ejecución o lógica) y corregirlos.
* Entregar evidencias (capturas) + código corregido.

---

## 1) Crear el proyecto y la clase

1. Crea el proyecto **DepuracionErrores**.
2. Crea el paquete: `tema2_debug`. *(vamos a simplificarlo por ahora)*
3. Crea la clase: `MediaNotas`.

Pega **exactamente** este código:

```java
package tema2_debug;

import java.util.Scanner;

public class MediaNotas {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int contador = 0;
        double suma = 0;

        System.out.print("Introduce el número de alumnos: ");
        int numAlumnos = sc.nextInt();

        while (contador <= numAlumnos) {
            System.out.print("Introduce la nota del alumno " + contador + ": ");
            double nota = sc.nextDouble();

            if (nota < 0 || nota > 10)
                System.out.println("Error: la nota debe estar entre 0 y 10");

            suma = suma + nota;
            contador++;
        }

        double media = suma / numAlumnos;
        System.out.println("La media del grupo es: " + media);

        sc.close();
    }
}
```

> Nota: **no modifiques** el código antes de depurar. Primero ejecuta e identifica los errores del programa ().

---

## 2) Guía rápida de depuración en Eclipse

1. **Coloca breakpoints** (doble clic en el margen izquierdo) al menos en:

   * La lectura de cada nota.
   * El cálculo de la media.

2. **Inicia la depuración** con el icono del **bicho verde** (Debug).
   Acepta cambiar a la perspectiva *Debug*.

3. Usa los controles:

* **F6 Step Over**: ejecuta la línea actual.
* **F5 Step Into**: entra en el método llamado.
* **F7 Step Return**: vuelve al método llamador.
* **F8 Resume**: continúa hasta el siguiente breakpoint.

4. Observa en las **vistas**:

* **Variables**: valores de `contador`, `suma`, `nota`, `numAlumnos`.
* **Console**: lo que imprime el programa.
* **Breakpoints**: lista y configuración (puedes activar *Conditional* o *Hit count* si te ayudan).
* **Expressions** (opcional): añade `suma / (contador == 0 ? 1 : contador)` para ver una “media parcial”.

---

## 3) Tareas

1. **Ejecuta y depura** el programa introduciendo varios datos (incluye al menos un valor fuera de rango).
2. **Localiza y explica** con tus palabras **todos** los problemas que observes (de flujo, validación, cálculo, etc.).

   * No te decimos cuáles son: **tú debes detectarlos con el depurador**.
3. **Corrige** el código para que:

   * Pida exactamente el número de notas indicado.
   * **No acepte** notas fuera de 0..10 (vuelve a pedir hasta que sea válida).
   * Calcule la **media correcta**.
4. Mantén `sc.close();` al final del `main`.

> Pista: si te ayuda, puedes reescribir el bucle con `for` y control de reintentos.

---

## 4) Entrega *(GitHub)*

Crea tu repositorio público: **PR-Eclipse-04-DebugProgErr**

Estructura sugerida:

```
PR-Eclipse-03-Debug/
 ├── src/tema2_debug/MediaNotas.java         (versión corregida)
 ├── capturas/
 │    ├── 01_breakpoints.png                 (breakpoints colocados)
 │    ├── 02_variables_iteracion.png         (valores en Variables durante el bucle)
 │    ├── 03_console_comportamiento.png      (salida que evidencia un problema)
 │    ├── 04_expressions_opcional.png        (si usas Expressions a parte de las pedidas en el punto 5)
 │    ├── 05_media_corregida.png             (resultado correcto tras corregir)
 │    ├── 06_breakpoint_condicional.png      (breakpoint properties del breakpoint condicional que se pide)
 │    ├── 04_expressions_obligatorias.png    (expresiones pedidas en el punto 5)
 │    └── 05_plantilla_pedirnota.png         (definición de la plantilla en `Templates`)
 └── README.md
```

Contenido del **README.md**:

Detalla los siguientes apartados:

1. **Descripción de los errores encontrados** (qué pasaba y por qué).

2. **Cómo los detectaste** (qué breakpoint/qué vista/qué valor te lo mostró).

3. **Qué cambios hiciste** para corregirlos.

4. Configura un **breakpoint condicional** que se dispare solo cuando la nota sea inválida.

[Guía: Breakpoints en Eclipse](breakpoint.md)
  
5. Añade las siguientes expresiones en **Expressions** que muestren el valor de la `suma`, el `contador` y la `media parcial` en cada iteración.

6. Escribe una **plantilla** (Template) llamada `pedirnota` que genere:

  ```java
  double nota;
  do {
      System.out.print("Introduce la nota del alumno ${index}: ");
      nota = sc.nextDouble();
  } while (nota < 0 || nota > 10);

  ${cursor}
  ```
[Guía: Cómo crear una Plantilla de Código (Template) en Eclipse](template.md)
