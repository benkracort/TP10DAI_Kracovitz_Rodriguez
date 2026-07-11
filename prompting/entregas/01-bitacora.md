# 📓 Bitácora de Prompts — Ejercicio N° ___

> Copiá este archivo por cada ejercicio que entregues. Nombralo, por ejemplo, `entregas/01-bitacora.md`.
> Esta bitácora **es parte de la nota**. Un ejercicio sin bitácora no se corrige.

---

## Datos

- **Alumno/as:** Benjamin Kracovitz y Catalina Rodriguez
- **Ejercicio:** N° 01 — Nueva tabla y su CRUD
- **Fecha:** 11/07/2026
- **Modelo de IA usado:** ChatGPT

---

## 1. 🎯 Qué me pidieron

Resumí en 2–3 líneas el objetivo del ejercicio con tus palabras (no copiado del enunciado).

```
El objetivo del ejercicio es incorporar una nueva entidad llamada materias a la API existente, respetando la arquitectura y el estilo del proyecto. Se tiene que implementar su CRUD completo (controller, service y repository), conectarlo a PostgreSQL y exponer sus endpoints sin modificar la estructura ya utilizada para alumnos y cursos.
```

---

## 2. 💬 Mis prompts (en orden)

Pegá **todos** los prompts que usaste, en orden, con la respuesta resumida y qué hiciste con ella. Agregá tantos como necesites.

### Prompt #1

**Lo que escribí:**
```
# ROL
Actuá como un desarrollador backend senior especializado en Node.js, Express y PostgreSQL. Tenés experiencia trabajando con arquitecturas en capas (Controller → Service → Repository), escribiendo código limpio y consistente con proyectos ya existentes.

# CONTEXTO
Estoy haciendo un TP de una API REST con:
Node.js
Express
PostgreSQL
paquete pg
ES Modules (import/export)
Arquitectura:
controllers
services
repositories
NO usamos ORM (Prisma, Sequelize, TypeORM, etc.).

Ya existen las entidades alumnos y cursos, cada una con:
controller
service
repository

También existe una clase DbPg que encapsula el acceso a la base mediante métodos como:
queryAll()
queryOne()
queryReturnId()
queryRowCount()

Quiero que todo el código nuevo siga exactamente el mismo estilo que el proyecto existente.

Después de este mensaje voy a pegar los siguientes archivos para que los uses como referencia:
db-pg.js
cursos-repository.js
cursos-service.js
cursos-controller.js
Esos archivos son la única referencia válida de estilo.
No inventes otra arquitectura ni otra forma de programar.

# TAREA
Necesito agregar una nueva entidad llamada materias.

La tabla es:
CREATE TABLE materias (
    id SERIAL PRIMARY KEY,
    nombre VARCHAR(75) NOT NULL
);

También existe otra tabla:
CREATE TABLE calificaciones (
    id SERIAL PRIMARY KEY,
    id_alumno INT NOT NULL REFERENCES alumnos(id),
    id_materia INT NOT NULL REFERENCES materias(id),
    nota INT NOT NULL,
    fecha DATE NOT NULL DEFAULT CURRENT_DATE,
    UNIQUE(id_alumno, id_materia)
);

En este ejercicio NO hay que programar nada relacionado con calificaciones. Solo necesito el CRUD completo para materias, igual al de cursos.

Los endpoints finales deberán permitir:
GET
GET por id
POST
PUT
DELETE

# RESTRICCIONES
NO uses ORM.
NO agregues dependencias.
NO cambies la arquitectura existente.
NO simplifiques el código.
NO cambies nombres de métodos.
NO cambies el estilo.
Usá exclusivamente la clase DbPg.
Usá queries parametrizadas ($1, $2, etc.).
Conservá los console.log si el proyecto ya los utiliza.
Respetá la organización Repository → Service → Controller.
Escribí código listo para copiar y pegar.
Si detectás que falta información, preguntá antes de asumir.

# ITERACIÓN
Quiero hacerlo paso a paso. Primero analizá los archivos que te pase. Después generá únicamente materias-repository.js. Esperá mi revisión. Cuando te diga "seguí", recién generá materias-service.js. Cuando vuelva a decir "seguí", recién generá materias-controller.js. Finalmente, cuando todo esté correcto, indicame exactamente qué debo agregar en server.js para registrar: 
app.use("/api/materias", ...); 
No avances a la siguiente capa hasta que yo lo autorice.
```

**Auto-chequeo de las 5 partes EFSI** (marcá lo que incluiste):
- [✅] Rol
- [✅] Contexto (¿pegaste código del proyecto?)
- [✅] Tarea
- [✅] Restricciones
- [✅] Iteración

**Qué me devolvió (resumen):**
```
Perfecto. Entendí las restricciones y voy a respetarlas.

No voy a:

* cambiar la arquitectura;
* introducir patrones distintos;
* usar ORM;
* renombrar métodos;
* "mejorar" el código por mi cuenta;
* avanzar a la siguiente capa hasta que me autorices.

El flujo va a ser exactamente este:

1. Analizo los archivos que me pases.
2. Genero únicamente `materias-repository.js`.
3. Espero tu revisión.
4. Cuando digas **"seguí"**, genero `materias-service.js`.
5. Cuando vuelvas a decir **"seguí"**, genero `materias-controller.js`.
6. Cuando todo esté aprobado, te indico exactamente qué agregar en `server.js` para registrar:

app.use("/api/materias", ...);

Antes de escribir una sola línea de código necesito ver los archivos de referencia, porque dijiste que **son la única referencia válida de estilo**.

Pegame, en este orden si puede ser:

1. `db-pg.js`
2. `cursos-repository.js`
3. `cursos-service.js`
4. `cursos-controller.js`

Con eso analizaré el estilo (nombres de métodos, manejo de errores, SQL, logs, respuestas, etc.) y recién después generaré **únicamente** `materias-repository.js`.

```

**¿Me sirvió tal cual, o tuve que corregir/repreguntar?**
```
Por el momento no
```

### Prompt #2

**Lo que escribí:**
```
db-pg.js:
[todo el código de db-pg.js, innecesario ponerlo de nuevo aca]
cursos-repository.js:
[todo el código de cursos-repository.js, innecesario ponerlo de nuevo aca]
cursos-service.js:
[todo el código de cursos-service.js, innecesario ponerlo de nuevo aca]
cursos-controller.js:
[todo el código de cursos-controller.js, innecesario ponerlo de nuevo aca]
```
**Por qué necesité este segundo prompt** (qué falló o faltó en el anterior):
```
En el anterior prompt le dije que le iba a pasar despues de ese mensaje los 4 archivos para que tenga las bases del proyecto.
```

---

## 3. 🔧 Qué hizo la IA y qué hice yo

Marcá esto **también en el código** con comentarios `// [IA]` y `// [YO]`. Acá resumilo:

| Archivo / función | Lo generó la IA | Lo modifiqué/escribí yo | Por qué |
|---|---|---|---|
| | | | |
| | | | |

---

## 4. 🐛 Errores o cosas mal que detecté en la respuesta de la IA

> Si ponés "ninguno", probablemente no las viste. **Siempre** hay algo (un import de más, un estilo distinto, un caso borde olvidado, una mala práctica de seguridad).

```
...
```

---

## 5. ✅ Verificación

Pegá el checklist de verificación del ejercicio y marcá lo que comprobaste **vos** (con qué evidencia: captura de Postman, salida de `npm test`, número de ms, etc.).

```
...
```

---

## 6. ✍️ Reflexión (300–600 palabras)

Cubrí: qué proceso seguiste, qué decisiones tomaste y por qué, qué aprendiste, y —lo más importante— **qué corregiste de lo que te dio la IA**. Escribí con tus palabras; esto se contrasta con el oral.

```
...
```

---

## 7. 🔗 Adjuntos

- [ ] Link/PDF de la conversación completa con la IA
- [ ] Commit(s) en GitHub: `____________`
- [ ] Capturas / evidencias de verificación
