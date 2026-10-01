# Respuestas — Laboratorio: Pull Requests, Merge Conflict y Release

## 1. ¿Qué es una Pull Request (PR) y por qué es importante en el flujo de trabajo colaborativo?

Una Pull Request es una solicitud para fusionar los cambios de una rama en otra, normalmente de una rama de característica hacia `main`. Es importante porque permite revisar, discutir y probar los cambios antes de integrarlos en la rama principal, dejando un historial visible de la revisión.

## 2. ¿Qué son los conflictos de fusión en Git?

Los conflictos de fusión ocurren cuando dos ramas modifican las mismas líneas de un archivo (o una rama borra contenido que la otra editó) y Git no puede decidir automáticamente qué versión conservar. Hace falta intervención manual para resolverlos.

## 3. ¿Qué es un flujo de trabajo de Git?

Un flujo de trabajo de Git es el conjunto de reglas y procedimientos que el equipo sigue al usar Git: cómo se crean ramas, cómo se integran los cambios (Pull Requests, merge o rebase), cómo se revisa el código y cómo se publican versiones (tags y releases).

## 4. ¿Por qué es importante utilizar ramas en Git?

Las ramas aíslan el trabajo en curso de la línea principal. Permiten desarrollar una característica o corrección sin romper `main`, trabajar en paralelo, abrir una Pull Request para revisión y descartar o posponer un experimento sin afectar lo ya publicado.

## 5. ¿Qué es un conflicto de fusión y cómo se resuelve en Git?

Un conflicto de fusión es el estado en el que Git detiene un merge (o rebase) porque las mismas líneas cambiaron en ambas ramas. Git marca el archivo con `<<<<<<<`, `=======` y `>>>>>>>`. Se edita el archivo para dejar una sola versión válida (eligiendo un lado o combinando ambos), se quitan los marcadores, y luego:

```bash
git add app.js
git commit -m "fix: resuelve conflicto en app.js"
```

## 6. ¿Qué es un release en Git?

Un release es una versión publicada del proyecto. En Git se marca con una etiqueta (tag), a menudo anotada, que apunta a un commit concreto. En GitHub, el Release asocia esa etiqueta con notas de la versión y, si hace falta, con archivos adjuntos.

## 7. ¿Cómo se puede revertir una fusión en Git?

Si el merge ya está en el historial publicado, se revierte con un nuevo commit que deshace el resultado del merge, indicando el padre que se conserva (normalmente el de `main`):

```bash
git revert -m 1 <hash-del-merge-commit>
```

Si el merge todavía no se ha compartido, se puede volver al commit anterior con `git reset --hard <commit-anterior>` y no volver a publicar ese merge. `revert` es la opción segura cuando la fusión ya está en el remoto.

## 8. Clona un repositorio remoto desde GitHub en tu máquina local.

```bash
git clone https://github.com/alonso3107/s8hd.git
```

## 9. Crea una nueva rama llamada feature/nueva-caracteristica.

```bash
git checkout -b feature/nueva-caracteristica
```

## 10. Haz algunos cambios en el archivo index.html, añádelos al área de preparación y realiza un commit.

```bash
git add index.html
git commit -m "feat: agrega diseño a la página de inicio"
```

## 11. Sube tus cambios a la rama remota feature/nueva-caracteristica.

```bash
git push -u origin feature/nueva-caracteristica
```

## 12. Crea una Pull Request (PR) para fusionar la rama feature/nueva-caracteristica a la rama main.

En GitHub:

1. Abre el repositorio `alonso3107/s8hd`.
2. Pulsa **Compare & pull request** (o **New pull request**).
3. Base: `main`. Compare: `feature/nueva-caracteristica`.
4. Escribe título y descripción de los cambios en `index.html`.
5. Pulsa **Create pull request**.

## 13. Fusión de la Pull Request realizada con la rama main.

En la página de la Pull Request:

1. Revisa los cambios y, si corresponde, aprueba la revisión (**Approve**).
2. Pulsa **Merge pull request**.
3. Confirma con **Confirm merge**.

## 14. Elimina la rama feature/nueva-caracteristica después de fusionarla.

En GitHub, tras el merge, pulsa **Delete branch**. Desde la terminal:

```bash
git push origin --delete feature/nueva-caracteristica
git checkout main
git branch -d feature/nueva-caracteristica
```

## 15. Resuelve un conflicto de fusión en el archivo app.js.

1. Crea dos ramas que diverjan y modifiquen las mismas líneas de `app.js`.
2. Fusiona la primera en `main`.
3. Abre una Pull Request de la segunda hacia `main`. GitHub indicará que no se puede fusionar automáticamente.
4. En local, actualiza `main` e integra:

```bash
git checkout feature/cambio-b
git fetch origin
git merge origin/main
```

5. Abre `app.js`, quita los marcadores de conflicto y deja una sola versión válida de `saludo()`.
6. Marca el archivo como resuelto y confirma:

```bash
git add app.js
git commit -m "fix: resuelve conflicto en app.js"
git push
```

7. Completa el merge de la Pull Request en GitHub.

## 16. Crea una etiqueta (tag) llamada v1.0 para marcar el primer release del proyecto.

```bash
git checkout main
git pull origin main
git tag -a v1.0 -m "Primera versión estable"
git push origin v1.0
```

En GitHub se puede crear además el Release **v1.0** a partir de esa etiqueta.

## 17. Actualiza tu repositorio local con los últimos cambios de la rama main.

```bash
git checkout main
git pull origin main
```
