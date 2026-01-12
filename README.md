
## Práctica 3 – Validación lógica de formulario

**Repositorio:** `pr03_js_validacion_logica`

### 📌 Enunciado

Crea una página web con un formulario que contenga **exactamente estos campos**:

1. **Nombre** (texto)
2. **Apellidos** (texto)
3. **Email** (email)
4. **Contraseña** (password)
5. **Repetir contraseña** (password)
6. **Edad** (número)
7. **Acepto las condiciones** (checkbox)

### Validaciones a realizar (todas con JavaScript)

* **Nombre** y **Apellidos**:

  * no pueden estar vacíos
  * deben tener **al menos 3 caracteres**

* **Email**:

  * debe contener **un `@`**
  * debe contener **un `.`**
  * y el **punto debe estar después de la @**

* **Contraseña** y **Repetir contraseña**:

  * la contraseña debe tener **al menos 6 caracteres**
  * ambas contraseñas deben ser **exactamente iguales**

* **Edad**:

  * debe ser un número dentro de un rango razonable (por ejemplo **0–120**)

* **Condiciones**:

  * el formulario solo será válido si el checkbox está marcado

### Requisitos obligatorios

* Al pulsar “Enviar”, el formulario **no debe recargar la página**.
* Si hay errores, deben mostrarse **agrupados en un único mensaje** (un solo bloque).
* El mensaje debe mostrarse **en la propia web**, no mediante `alert`.

### Entrega

* enlace al repositorio
* enlace a la web (GitHub Pages)

### HTML y CSS para la práctica

#### `index.html`

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Práctica 3 - Validación lógica</title>
  <link rel="stylesheet" href="styles.css" />
  <script src="app.js" defer></script>
</head>
<body>
  <main class="card">
    <h1>Formulario</h1>

    <form id="formulario" novalidate>
      <label>Nombre
        <input id="nombre" type="text">
      </label>

      <label>Apellidos
        <input id="apellidos" type="text">
      </label>

      <label>Email
        <input id="email" type="email">
      </label>

      <label>Contraseña
        <input id="password" type="password">
      </label>

      <label>Repetir contraseña
        <input id="password2" type="password">
      </label>

      <label>Edad
        <input id="edad" type="number">
      </label>

      <label class="check">
        <input id="condiciones" type="checkbox">
        Acepto las condiciones
      </label>

      <button type="submit">Enviar</button>
    </form>

    <section id="mensajes" class="mensajes" aria-live="polite"></section>
  </main>
</body>
</html>
```

#### `styles.css`

```css
body {
  margin: 0;
  padding: 40px;
  font-family: system-ui, Arial, sans-serif;
  background: #f3f4f6;
}

.card {
  max-width: 520px;
  margin: 0 auto;
  background: white;
  padding: 24px;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(0,0,0,.10);
}

form {
  display: grid;
  gap: 12px;
}

label {
  display: grid;
  gap: 6px;
}

input {
  padding: 10px;
}

.check {
  display: flex;
  gap: 10px;
  align-items: center;
}

button {
  padding: 10px 14px;
  cursor: pointer;
}

.mensajes {
  margin-top: 14px;
  padding: 12px;
  border-radius: 10px;
  min-height: 1.2em;
}

.mensajes.ok {
  background: #f0fff4;
  border: 1px solid #b7e4c7;
}

.mensajes.err {
  background: #fff0f3;
  border: 1px solid #ffb3c1;
}
```

---

## 📘 Contenidos necesarios para realizar la práctica

A continuación se explican **conceptos nuevos** que necesitarás para poder resolver esta práctica.

### 1️⃣ `event.preventDefault()`

#### ¿Para qué sirve?

Cuando se envía un formulario, el navegador realiza automáticamente estas acciones:

* envía los datos
* recarga la página
* pierde el contenido que se estaba mostrando

Esto ocurre **aunque el formulario tenga errores**.

`event.preventDefault()` sirve para:

> **Evitar el comportamiento automático del navegador**
> y permitir que JavaScript controle lo que ocurre.

#### Uso básico

```js
form.addEventListener("submit", function (event) {
  event.preventDefault();
  // aquí va nuestro código
});
```

Gracias a esto:

* la página **no se recarga**
* JavaScript puede validar los datos
* podemos mostrar mensajes de error o éxito en la web

#### ¿Y si el formulario es correcto?

Usar `event.preventDefault()` **no significa que el formulario no pueda enviarse**.

Significa simplemente que:

> **el envío automático queda desactivado**
> y ahora JavaScript decide cuándo enviar el formulario.

Si todas las validaciones son correctas, podemos enviar el formulario manualmente desde JavaScript:

```js
form.submit();
```

#### Comportamiento final

1. El usuario pulsa **Enviar**
2. JavaScript bloquea el envío automático
3. Se realizan las validaciones
4. Si hay errores:

   * se muestran en la página

5. Si todo es correcto:

   * JavaScript envía el formulario

### 2️⃣ `.className`

#### ¿Para qué sirve?

`.className` permite:

* **leer**
* **cambiar**
  la clase CSS de un elemento.

Ejemplo:

```js
mensaje.className = "error";
```

Esto equivale a escribir en HTML:

```html
<p class="error"></p>
```

En la práctica se usa para:

* aplicar estilos distintos
* mostrar mensajes de error o éxito
* cambiar el aspecto según lo que ocurra

#### Ejemplo sencillo

```js
mensaje.className = "mensajes err";
```

Significa:

> “A este elemento aplícale estas clases CSS”.

## 3️⃣ `.trim()`

### ¿Para qué sirve?

`.trim()` elimina los **espacios en blanco al principio y al final** de un texto.

Ejemplo:

```js
let nombre = "   Ana   ";
nombre = nombre.trim();
```

Resultado:

```
"Ana"
```

Sirve para:

* evitar que el usuario “engañe” al programa escribiendo solo espacios
* validar correctamente campos de texto

### 4️⃣ `indexOf()`

#### ¿Para qué sirve?

`indexOf()` busca un texto dentro de otro texto.

Ejemplo:

```js
"hola@correo.com".indexOf("@");
```

Resultado:

```
4
```

Devuelve:

* la **posición** donde aparece el texto
* `-1` si **no existe**

Ejemplo:

```js
"hola".indexOf("@"); // -1
```

### 5️⃣ `lastIndexOf()`

#### ¿Para qué sirve?

Hace lo mismo que `indexOf()`, pero:

* busca **desde el final**

Ejemplo:

```js
"hola@correo.com".lastIndexOf(".");
```

Resultado:

```
11
```

Sirve para:

* encontrar el último punto de un email
* comprobar que está después de la `@`

### 6️⃣ `.length`

#### ¿Para qué sirve?

`.length` indica la **longitud** de un texto (o de otros elementos más adelante).

Ejemplo:

```js
"hola".length; // 4
```

En formularios se usa para:

* comprobar longitud mínima
* validar contraseñas
* evitar textos demasiado cortos

### 🧠 Resumen

| Elemento                 | Para qué sirve                             |
| ------------------------ | ------------------------------------------ |
| `event.preventDefault()` | Evita que el formulario recargue la página |
| `submit()`               | Envía el formulario manualmente desde JS   |
| `.className`             | Cambiar clases CSS desde JS                |
| `.trim()`                | Quitar espacios al principio y al final    |
| `indexOf()`              | Buscar texto desde el inicio               |
| `lastIndexOf()`          | Buscar texto desde el final                |
| `.length`                | Saber cuántos caracteres tiene un texto    |

---

### Curiosidades del HTML sobre la ACCESIBILIDAD

#### ¿Qué es `aria-live`?

`aria-live` es un **atributo de accesibilidad** (ARIA) que se usa para indicar a los **lectores de pantalla** que el contenido de un elemento puede **cambiar dinámicamente**.

Sirve para que personas con discapacidad visual sepan que **ha aparecido un nuevo mensaje**, aunque no se haya recargado la página.

#### ¿Qué significa `aria-live="polite"`?

```html
<section id="mensajes" aria-live="polite"></section>
```

Significa:

> “Cuando el contenido de este elemento cambie,
> avisa al lector de pantalla **de forma educada**,
> **sin interrumpir** lo que el usuario esté escuchando.”

Es decir:

* el lector de pantalla **espera** a terminar la frase actual
* luego lee el nuevo contenido

#### Diferencia entre `polite` y `assertive`

| Valor       | Comportamiento                                                                |
| ----------- | ----------------------------------------------------------------------------- |
| `polite`    | Lee el cambio cuando puede (recomendado para mensajes informativos)           |
| `assertive` | Interrumpe inmediatamente lo que se esté leyendo (solo para errores críticos) |

En un formulario:

* mensajes de error → `polite` es lo correcto
* alertas graves → `assertive` (muy pocas veces)

