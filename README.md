# Actividad Branching Git
Integrantes:
Diego Pena
Brandon Inostroza
Renato Campos
Victor Erazo
Bruno Bustos
Christopher Contreras
Alonso Morales
Julio Oyarzun

Objetivo
Practicar branching, fork, pull request y merge.
## Tema investigado
¿Qué diferencia hay entre branch y fork?

## Definición
BRANCH es una rama, que te sirve para manejar un código distinto al de la rama principal. En caso de un FORK haces una copia exacta de un repositorio.

## Respuestas
1. BRANCH: es una línea de trabajo independiente y paralela a la rama principal.

2. FORK: creación de una copia independiente de un proyecto de software a partir de una versión existente

3. DIFERENCIAS:  BRANCH es una rama, que te sirve para manejar un código distinto al de la rama principal. En caso de un FORK haces una copia exacta de un repositorio.

## Ejemplo

Si creas un branch, por ejemplo llamado "nueva-funcion", sigues trabajando dentro del mismo repositorio, pero en una versión separada del código. Luego puedes unir esos cambios a la rama principal (main).

Si haces un fork, creas una copia del repositorio en tu propia cuenta. Desde ahí puedes hacer cambios sin afectar el repositorio original, y si quieres, puedes enviar una solicitud (pull request) para que el dueño original revise tus cambios.

## Conclusión personal

En mi opinión, los branch son útiles cuando trabajas dentro de un mismo equipo y repositorio, mientras, que los fork son más útiles cuando quieres contribuir a proyectos externos o experimentar sin afectar el original.

---
## Alumno 3 — ¿Qué es `main` y por qué se protege?

---

## Parte 1: Investigación

### 1. ¿Qué representa la rama `main`?

La rama `main` (anteriormente conocida como `master`) es la **rama principal** de un repositorio Git. Representa la **línea base oficial** del proyecto y contiene el código que se considera **estable, probado y listo para producción**.

En términos prácticos:

- Es el **punto de partida** desde donde se crean todas las demás ramas de trabajo (feature branches, hotfix, etc.).
- Es la rama que refleja el **estado actual del producto en producción** o la versión más reciente y confiable del software.
- Todos los cambios que eventualmente se integran al proyecto deben pasar por `main` como destino final.
- Cuando alguien clona un repositorio, por defecto obtiene el contenido de la rama `main`.

En resumen, `main` actúa como la **"fuente de verdad"** del proyecto: cualquier desarrollador puede confiar en que lo que está en `main` funciona correctamente.

### 2. ¿Por qué `main` suele ser la rama estable?

`main` se mantiene como la rama estable por convención y por diseño del flujo de trabajo. Las razones principales son:

- **Flujo de trabajo basado en ramas (branching workflow):** Los desarrolladores no trabajan directamente en `main`. En su lugar, crean ramas separadas (por ejemplo, `feature/login`, `bugfix/error-404`) donde realizan sus cambios. Solo cuando esos cambios han sido revisados y probados, se fusionan (*merge*) a `main`.
- **Revisión de código (Code Review):** Antes de integrar cambios a `main`, se abren **Pull Requests (PR)** o **Merge Requests (MR)**, donde otros miembros del equipo revisan el código, sugieren mejoras y aprueban los cambios.
- **Pruebas automatizadas (CI/CD):** En equipos profesionales, se configuran pipelines de integración continua que ejecutan pruebas automáticas (tests unitarios, de integración, etc.) cada vez que alguien intenta fusionar código a `main`. Si las pruebas fallan, el merge se bloquea.
- **Despliegue a producción:** Muchos equipos tienen configurado un despliegue automático (*deploy*) que se activa cada vez que se actualiza `main`. Por esta razón, es crítico que `main` siempre contenga código funcional.
- **Historial limpio:** Mantener `main` estable garantiza un historial de commits ordenado y confiable, lo que facilita la depuración de errores y el seguimiento de cambios.

### 3. ¿Qué significa proteger la rama principal?

Proteger una rama en Git (a través de plataformas como **GitHub**, **GitLab** o **Bitbucket**) significa **aplicar reglas y restricciones** que controlan quién puede modificarla y bajo qué condiciones. Esto se logra mediante las llamadas **Branch Protection Rules** (reglas de protección de rama).

Las protecciones más comunes incluyen:

- **Prohibir commits directos (push directo):** Nadie puede hacer `git push` directamente a `main`. Todos los cambios deben llegar a través de un Pull Request.
- **Requerir revisiones aprobadas:** Se exige que al menos uno o más revisores aprueben el PR antes de que se pueda fusionar.
- **Requerir que pasen las pruebas automáticas (status checks):** Los pipelines de CI/CD deben completarse exitosamente antes de permitir el merge.
- **Prohibir force push:** Se impide que alguien reescriba el historial de la rama con `git push --force`, lo cual podría borrar o alterar commits existentes.
- **Prohibir la eliminación de la rama:** Se evita que alguien borre accidentalmente la rama `main`.
- **Requerir historial lineal:** Se puede exigir que los merges mantengan un historial lineal (sin merge commits innecesarios).
- **Requerir commits firmados:** Para mayor seguridad, se puede exigir que los commits estén firmados digitalmente.

---

## Parte 2: Respuestas

### 1. ¿Qué representa `main` en un proyecto?

La rama `main` representa la **versión oficial y estable del proyecto**. Es la rama principal del repositorio y funciona como la fuente de verdad del código. Todo lo que está en `main` se considera **probado, revisado y listo para ser utilizado o desplegado en producción**. Cuando un nuevo miembro del equipo clona el repositorio, recibe automáticamente el contenido de `main`, por lo que esta rama debe reflejar siempre el estado más confiable del software.

### 2. ¿Por qué no debería usarse para cambios directos?

Realizar cambios directamente en `main` es riesgoso por varias razones:

- **Introducción de errores:** Sin revisión ni pruebas previas, un cambio directo podría introducir bugs que afecten a todos los miembros del equipo o incluso a los usuarios finales si hay despliegue automático.
- **Pérdida de trazabilidad:** Los cambios directos no pasan por un proceso formal de revisión, lo que dificulta entender quién hizo qué cambio y por qué.
- **Conflictos con otros desarrolladores:** Si varias personas hacen push directo a `main`, se pueden generar conflictos difíciles de resolver y se puede corromper el historial.
- **Riesgo de sobrescritura:** Un `force push` accidental podría borrar el trabajo de otros desarrolladores.
- **Rompe el flujo de CI/CD:** Los pipelines de integración continua están diseñados para validar cambios *antes* de que lleguen a `main`. Un push directo salta esta validación.

Por estas razones, el estándar de la industria es que **todos los cambios lleguen a `main` exclusivamente a través de Pull Requests revisados y aprobados**.

### 3. ¿Por qué es importante mantenerla estable?

Mantener `main` estable es fundamental porque:

- **Es la base para todo el equipo:** Todos los desarrolladores crean sus ramas de trabajo a partir de `main`. Si `main` tiene errores, esos errores se propagarán a todas las ramas nuevas.
- **Despliegue continuo:** En muchos proyectos, `main` está conectada directamente al entorno de producción. Un error en `main` puede significar un error visible para los usuarios finales.
- **Confianza del equipo:** Un equipo que confía en que `main` siempre funciona puede trabajar más rápido y con menos fricción. No necesitan perder tiempo verificando si la rama base está rota.
- **Facilita la depuración:** Si `main` siempre es estable, cuando aparece un bug se puede comparar fácilmente con versiones anteriores para identificar qué cambio lo introdujo (usando herramientas como `git bisect`).
- **Profesionalismo y buenas prácticas:** Mantener `main` estable es un indicador de madurez en el proceso de desarrollo de software. Es una práctica estándar en la industria que demuestra disciplina y organización en el equipo.

---

# Alumno 4  ¿Qué es un commit y por qué es importante?

## ¿Qué es un commit?

Un commit es un punto de guardado que captura los cambios realizados en un proyecto en un momento específico.

## ¿Por que se deben hacer commits pequeños?

Porque al hacer commits pequeños las revisiones de código resultan ser mas fáciles de entender entre colaboradores y mantener el historial del proyecto de forma ordenada.

## ¿Cómo ayudan los commits a entender la historia del trabajo?

Los commits se utilizan para explicar que parte del proyecto se realizaron los cambios, quien hizo cada cambio, corregir errores de la versión actual regresando a la anterior para arreglar el origen.

---

## 📚 Fuentes

1. [About protected branches — GitHub Docs](https://docs.github.com/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches)
2. [Managing a branch protection rule — GitHub Docs](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/managing-a-branch-protection-rule)
3. [Best Practices for Branch Protection — DEV Community](https://dev.to/n3wt0n/best-practices-for-branch-protection-2pe3)
4. [GitHub Branch Protection Rules: Why and How to Use Them — Medium](https://medium.com/@techeazy.consulting/github-branch-protection-rules-why-and-how-to-use-them-07ecfdb003cf)
5. [GitHub Branch Protection Guide: Preventing Direct Commits to Main — Paradime Docs](https://docs.paradime.io/app-help/concepts/working-with-git/github-branch-protection-guide-preventing-direct-commits-to-main)
6. [Protected branches — GitLab Docs](https://docs.gitlab.com/user/project/repository/branches/protected/)
7. [GitHub Branch Protection Guide: Keys for Developers — Arnica](https://www.arnica.io/blog/what-every-developer-needs-to-know-about-github-branch-protection)
