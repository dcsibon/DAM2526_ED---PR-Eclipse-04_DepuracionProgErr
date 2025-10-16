
# Guía completa: Breakpoints condicionales en Eclipse

## 1) Crear un breakpoint “normal”

1. Abre el código fuente *(.java)*.
2. Haz **doble clic** en el margen izquierdo de la línea onde quieras pausar la ejecución de tu programa → aparece un círculo azul (breakpoint de línea).
3. Ejecuta en modo **Debug** (icono del bicho). El programa se parará cada vez que pase por esa línea.

> Esto ya funciona, pero se detiene **en todas las iteraciones**. Vamos a condicionarlo.

---

## 2) Convertirlo en **condicional**

1. Clic derecho sobre el círculo azul → **Breakpoint Properties…**
2. Marca **Enabled** *(activo)* y **Conditional**.
3. Elige uno de los dos modos:

   * **Suspend when 'true'** y escribe una `expresión booleana` que debe cumplir para que tu `breakpoint` se active y tu programa se pare *(por ejemplo `suma > 5`)*.
   * **Suspend when value changes** y pon una expresión cuyo **valor** quieras vigilar (p. ej. `maxima`).

Pulsa **OK**.

---

## 3) ¿Qué significan las opciones que aparecen en la ventana `Breakpoint Properties`?

<img width="600" alt="image" src="https://github.com/user-attachments/assets/a29be2a8-ef38-482f-883d-4d847b8de8a1" />


### Sección principal

* **Enabled**
  Activa/desactiva el breakpoint sin borrarlo.
* **Trigger Point**
  Marca este breakpoint como “disparador”. En escenarios complejos puede habilitar otros breakpoints al alcanzarlo. Útil en depuraciones avanzadas; lo normal es **no usarlo**.
* **Disable on hit**
  Se desactiva automáticamente tras activarse una vez. Útil para “parar solo la primera vez”.
* **Suspend thread / Suspend VM**

  * **Suspend thread** (recomendado): pausa **solo el hilo actual**.
  * **Suspend VM**: pausa **toda** la máquina virtual Java (todos los hilos). Úsalo solo si lo necesitas.

### Hit count (contador)

* **Hit count**
  Se detiene cuando la línea se ha ejecutado **N** veces.
  Ej.: Hit count = 5 → se para la **quinta** vez que pase por ahí.

### Conditional (condición)

Activa la evaluación de una **expresión Java** en el contexto de esa línea.

* **Suspend when 'true'**
  Se detiene **solo si la expresión booleana vale `true`**.
  Ej.: `temperatura < 0 || temperatura > 50` → para en temperaturas fuera de rango.
* **Suspend when value changes**
  Se detiene **cuando cambia el valor** de la expresión respecto a la última vez.
  Ej.: `temperaturaMaxima` → se parará **solo cuando se actualice la variable temperaturaMaxima**.

> Las expresiones se evalúan **con las variables visibles en esa línea** (parámetros, locales, campos accesibles).
> Puedes llamar métodos, pero evita los que tengan **efectos secundarios**.

### Filtering / Scope *(si tu Eclipse lo muestra)*

* Permite limitar el breakpoint a **ciertas clases, paquetes o hilos**.
  Útil en proyectos grandes para no parar en ejecuciones que no te interesan.

---

## 4) Menú contextual de los *Breakpoints* en Eclipse *(opciones interesantes o más utilizadas)*

<img width="400" alt="image" src="https://github.com/user-attachments/assets/22b2f1bf-61a2-4f7d-8e36-f220476e13f4" />


Cuando haces clic derecho sobre el punto de interrupción (círculo azul del margen izquierdo), Eclipse muestra un menú con diversas opciones que permiten **controlar su comportamiento**.
Estas son las más importantes:

### 🔹 **Toggle Breakpoint**

**(Ctrl + Shift + B)**
Activa o desactiva un *breakpoint* en la línea actual.

* Si no existe, lo crea.
* Si ya existe, lo elimina.

👉 Es el método más rápido para añadir o quitar puntos de interrupción.

### 🔹 **Disable Breakpoint**

**(Shift + Doble clic)**
Desactiva temporalmente el *breakpoint* (sin borrarlo).

* El círculo azul se convierte en un **círculo vacío** (gris).
* Puedes volver a activarlo repitiendo la acción.

💡 *Muy útil cuando no quieres detener la ejecución en ese punto, pero tampoco deseas perder la configuración condicional.*

### 🔹 **Toggle Triggerpoint**

Convierte el *breakpoint* seleccionado en un **punto de disparo (trigger point)**.

* Un *trigger point* **activa** otros *breakpoints deshabilitados* cuando se alcanza.
* Se usa en depuraciones complejas, por ejemplo, cuando solo quieres que se activen ciertos *breakpoints* **después** de pasar por un punto concreto.

**Ejemplo:**
Activa el *breakpoint* de un método `calcularMedia()` **solo después** de haber pasado por `leerNotas()`.

### 🔹 **Toggle Breakpoint with Hit Count**

Permite especificar un **contador de ejecuciones** (*hit count*).

* El *breakpoint* se activará únicamente cuando se haya ejecutado **N veces**.
* Es equivalente a abrir las *Breakpoint Properties* y marcar “Hit count”.

💡 Ejemplo:
Si pones *Hit count = 5*, Eclipse detendrá la ejecución **la quinta vez** que el flujo alcance esa línea.

### 🔹 **Toggle Tracepoint**

Un *tracepoint* **no detiene la ejecución**, pero **registra información** (por ejemplo, imprime valores o mensajes en la consola o log).
Es similar a un *System.out.println()* temporal, pero gestionado por el depurador. Debes modificarlo en la ventana `Breakpoint Properties`.

### 🔹 **Run to Line**

**(Ctrl + Alt + Clic)**
Ejecuta el programa **hasta la línea seleccionada**, sin necesidad de crear un *breakpoint permanente*.
Es una ejecución *temporal* que se detiene justo antes de esa línea.
Para que se habilite el programa debe estar en modo Debug y detenido.

💡 Perfecto cuando quieres “saltar” rápidamente hasta un punto del código.

### 🔹 **Add Bookmark… / Add Task…**

Permiten marcar líneas del código para recordatorios o tareas.

* **Bookmark:** marca visual sin impacto funcional (solo para navegar).
* **Task:** permite añadir comentarios tipo “TODO” gestionables desde la vista *Tasks*.

### 🔹 **Show Quick Diff / Show Line Numbers / Folding**

Opciones del editor para mostrar diferencias, numerar líneas o contraer bloques de código.
No están relacionadas directamente con la depuración, pero son útiles durante el análisis.

### 🔹 **Preferences…**

Abre directamente el panel de configuración global de Eclipse, normalmente en:

```
Window → Preferences → Java → Debug
```

Desde ahí puedes ajustar:

* Colores de los *breakpoints*.
* Comportamiento del depurador.
* Opciones de suspensión de hilos, vistas, etc.

### 🔹 **Breakpoint Properties…**

**(Ctrl + Doble clic sobre el círculo azul)**
Abre la ventana de propiedades detalladas del *breakpoint*.

💡 Es la herramienta clave para convertir un *breakpoint normal* en uno **condicional o avanzado**.

---
