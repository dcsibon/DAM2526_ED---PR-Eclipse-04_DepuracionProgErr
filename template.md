
# **Guía: Cómo crear una Plantilla de Código (Template) en Eclipse**

Las **plantillas de código** son una funcionalidad muy útil del IDE Eclipse.
Permiten escribir una palabra clave (como `pedirnota`) y que Eclipse la sustituya automáticamente por un bloque de código completo, como un bucle, una condición o incluso varios fragmentos de programa.

---

## 🪜 **Pasos para crear una nueva plantilla**

### 🔹 1. Abrir el menú de plantillas

Ve a:

```
Window → Preferences → Java → Editor → Templates
```

Ahí verás una lista de plantillas predefinidas (por ejemplo `sysout`, `for`, `main`, etc.), que Eclipse usa para autocompletar código al pulsar **Ctrl + Espacio**.

---

### 🔹 2. Crear una nueva

Haz clic en el botón **New...**

Se abrirá una ventana llamada **New Template** con varios campos que debes rellenar.

---

### 🔹 3. Completar los campos principales

| Campo                    | Qué poner                                                                                               |
| ------------------------ | ------------------------------------------------------------------------------------------------------- |
| **Name**                 | Nombre de tu plantilla (por ejemplo `pedirnota`). Es lo que escribirás en el editor para insertarla.    |
| **Context**              | Elige `Java statements` (para que pueda insertarse dentro de métodos).                                  |
| **Description**          | Una breve descripción de lo que hace (por ejemplo “Plantilla para pedir una nota válida entre 0 y 10”). |
| **Automatically insert** | ✅ Déjalo activado (inserta automáticamente al pulsar Intro).                                            |
| **Pattern**              | Aquí escribes el código que se insertará cuando se use la plantilla.                                    |

---

### 🔹 4. Escribir el patrón (Pattern)

Por ejemplo, para crear la plantilla `pedirnota`:

```java
double nota;
do {
    System.out.print("Introduce la nota del alumno ${index}: ");
    nota = sc.nextDouble();
} while (nota < 0 || nota > 10);

${cursor}
```

---

## 🧠 **Explicación de las variables dentro del patrón**

Dentro de las plantillas se pueden usar **variables de plantilla**.
Van entre `${}` y permiten personalizar o automatizar partes del código.

| Variable            | Qué hace                                                                                                                                                        |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `${cursor}`         | Indica dónde quedará el cursor al terminar de insertar el código. Es recomendable colocarla **al final** del bloque para poder seguir escribiendo justo debajo. |
| `${index}`          | Variable editable. Cuando insertas la plantilla, Eclipse te deja escribir directamente el valor (por ejemplo, el número del alumno).                            |
| `${word_selection}` | Se reemplaza por el texto seleccionado antes de insertar la plantilla.                                                                                          |
| `${date}`           | Inserta la fecha actual.                                                                                                                                        |
| `${time}`           | Inserta la hora actual.                                                                                                                                         |
| `${user}`           | Inserta el nombre de usuario configurado en Eclipse.                                                                                                            |

---

## 🔧 **Cómo crear variables personalizadas**

1. En la ventana “New Template”, haz clic en **Insert Variable...**
2. Aparecerá una lista de variables disponibles.
3. Puedes escribir directamente en el código `${nombre_variable}` si quieres una variable editable nueva (como `${index}` en el ejemplo).
4. Al usar la plantilla, Eclipse te permitirá escribir un valor para cada variable editable y moverte entre ellas con la tecla **Tab**.

---

## 💬 **Por qué aparece “i” por defecto al usar `${index}`**

Eclipse intenta **adivinar un valor inicial** para las variables comunes.
En este caso:

* Detecta que estás dentro de un método o bucle,
* Y asigna automáticamente el valor `"i"` (por convención, el típico nombre de índice en bucles).

👉 No es un error: simplemente puedes **sobrescribirlo** al insertar la plantilla (escribe otro texto y pulsa Tab).

Si quieres evitar ese valor inicial, puedes renombrar la variable a otra más específica, por ejemplo `${numAlumno}`.
Así Eclipse no intentará sugerir “i”.

---

## 🧩 **Ejemplo final completo**

**Name:** `pedirnota`
**Context:** `Java statements`
**Description:** Plantilla para pedir una nota válida entre 0 y 10
**Pattern:**

```java
double nota;
do {
    System.out.print("Introduce la nota del alumno ${numAlumno}: ");
    nota = sc.nextDouble();
} while (nota < 0 || nota > 10);

${cursor}
```

---

## ▶️ **Cómo usar tu plantilla**

1. En cualquier método, escribe el nombre de la plantilla:

   ```
   pedirnota
   ```
2. Pulsa **Ctrl + Espacio**
   → Aparece tu plantilla en la lista de autocompletado.
3. Pulsa **Enter**
   → Se inserta el bloque de código completo.
4. Rellena los valores de las variables (por ejemplo `${numAlumno}`) y pulsa **Tab** para moverte entre ellas.

---

