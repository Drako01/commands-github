# Git & GitHub — Guía Profesional

<p align="center">
  <img src="https://git-scm.com/images/logos/downloads/Git-Icon-1788C.png" alt="Git" width="120" />
</p>

<p align="center">
  Guía práctica en español para aprender Git desde los fundamentos y trabajar con GitHub usando flujos profesionales, seguros y mantenibles.
</p>

<p align="center">
  <strong>Autor:</strong> <a href="https://github.com/Drako01">Alejandro Di Stefano</a>
</p>

<p align="center">
  <img alt="Release" src="https://img.shields.io/badge/release-v2.0.0-blue" />
  <img alt="Git" src="https://img.shields.io/badge/Git-version%20control-F05032?logo=git&logoColor=white" />
  <img alt="GitHub" src="https://img.shields.io/badge/GitHub-collaboration-181717?logo=github&logoColor=white" />
</p>

---

## Objetivo

Este repositorio no es una lista aislada de comandos. Está organizado como una **guía de estudio, referencia y operación diaria** para entender Git, colaborar en GitHub y resolver problemas habituales sin depender de recetas memorizadas.

Incluye:

- fundamentos de Git y su modelo de objetos;
- instalación y configuración inicial;
- working tree, staging area, commits y `HEAD`;
- branches y estrategias de integración;
- remotes, fetch, pull y push;
- merge, rebase y cherry-pick;
- stash, restore, reset y revert;
- resolución de conflictos;
- tags y releases;
- forks y Pull Requests;
- autenticación SSH;
- `.gitignore` y manejo de secretos;
- GitHub CLI;
- Conventional Commits;
- GitHub Actions y automatización;
- recuperación ante errores;
- troubleshooting;
- cheat sheet de uso diario.

> La guía prioriza comandos actuales como `git switch` y `git restore`, sin omitir `git checkout` cuando sigue siendo útil o aparece en proyectos existentes.

---

## Índice

| Capítulo | Contenido |
| --- | --- |
| [01 — Fundamentos y configuración](docs/01-fundamentos-configuracion.md) | Modelo mental, instalación, config, init, clone y estructura interna |
| [02 — Flujo diario y commits](docs/02-flujo-diario-commits.md) | status, add, diff, commit, restore, log y buenas prácticas |
| [03 — Branches e integración](docs/03-branches-merge-rebase.md) | branches, merge, rebase, cherry-pick y conflictos |
| [04 — GitHub y colaboración](docs/04-github-colaboracion.md) | remotes, PRs, forks, reviews, GitHub CLI y estrategias de equipo |
| [05 — Recuperación y seguridad](docs/05-recuperacion-seguridad.md) | reset, revert, reflog, stash, SSH, secretos y errores frecuentes |
| [06 — Automatización y releases](docs/06-automatizacion-releases.md) | tags, releases, Conventional Commits, SemVer y GitHub Actions |
| [Cheat Sheet](docs/cheatsheet.md) | Comandos frecuentes para consulta rápida |
| [CHANGELOG](CHANGELOG.md) | Evolución de la guía |

---

# Git en 60 segundos

Git es un sistema de control de versiones distribuido. Cada clon contiene el historial del repositorio y permite crear commits, ramas y comparaciones localmente.

El flujo mental más importante es:

```text
Working Tree
    ↓ git add
Staging Area / Index
    ↓ git commit
Local Repository
    ↓ git push
Remote Repository
```

Tres preguntas resuelven buena parte del trabajo diario:

```bash
git status
git diff
git log --oneline --graph --decorate --all
```

---

## Configuración inicial

```bash
git --version

git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"

git config --global init.defaultBranch main
```

Ver configuración efectiva:

```bash
git config --list --show-origin
```

Configurar editor por defecto, por ejemplo VS Code:

```bash
git config --global core.editor "code --wait"
```

---

## Crear o clonar un repositorio

### Crear uno nuevo

```bash
mkdir mi-proyecto
cd mi-proyecto
git init
```

### Clonar uno existente

```bash
git clone https://github.com/usuario/repositorio.git
```

Con SSH:

```bash
git clone git@github.com:usuario/repositorio.git
```

---

## Flujo diario

### Estado

```bash
git status
```

### Ver cambios no staged

```bash
git diff
```

### Ver cambios staged

```bash
git diff --staged
```

### Agregar archivos

```bash
git add archivo.txt
git add src/
git add .
```

Para seleccionar cambios por fragmentos:

```bash
git add -p
```

### Commit

```bash
git commit -m "feat: agregar validación de usuarios"
```

Un commit profesional debería representar una unidad lógica de cambio. Evitá commits gigantes con múltiples objetivos no relacionados.

---

## Conventional Commits

Una convención simple ayuda a leer el historial y automatizar releases.

```text
feat: nueva funcionalidad
fix: corrección de bug
docs: documentación
refactor: cambio interno sin alterar comportamiento
test: pruebas
chore: mantenimiento
ci: integración continua
perf: performance
```

Ejemplos:

```bash
git commit -m "feat(auth): add password reset flow"
git commit -m "fix(api): prevent duplicate requests"
git commit -m "docs: document local setup"
```

---

## Branches

Crear una rama y cambiarse a ella:

```bash
git switch -c feat/user-profile
```

Listar ramas:

```bash
git branch
git branch -a
```

Cambiar de rama:

```bash
git switch main
```

Eliminar una rama local ya integrada:

```bash
git branch -d feat/user-profile
```

Forzar eliminación local:

```bash
git branch -D feat/user-profile
```

> `-D` descarta la protección de Git. Usalo sólo cuando verificaste que no necesitás los commits exclusivos de esa rama.

---

## Remotes

Listar remotes:

```bash
git remote -v
```

Agregar `origin`:

```bash
git remote add origin git@github.com:usuario/repositorio.git
```

Cambiar URL:

```bash
git remote set-url origin git@github.com:usuario/repositorio.git
```

Ver información:

```bash
git remote show origin
```

---

## Fetch, pull y push

### `git fetch`

Descarga referencias remotas sin integrar cambios en tu rama actual.

```bash
git fetch origin
```

### `git pull`

Equivale conceptualmente a descargar e integrar.

```bash
git pull --ff-only origin main
```

`--ff-only` evita merges automáticos inesperados cuando el historial divergió.

### `git push`

Primera publicación de una rama:

```bash
git push -u origin feat/user-profile
```

Luego:

```bash
git push
```

---

## Merge

Desde la rama que recibe los cambios:

```bash
git switch main
git merge feat/user-profile
```

Tipos frecuentes:

- **fast-forward**: Git mueve el puntero de la rama;
- **merge commit**: crea un commit de integración;
- **squash merge**: combina los cambios de una rama en un único commit, normalmente desde GitHub.

---

## Rebase

Actualizar una feature branch sobre el estado actual de `main`:

```bash
git fetch origin
git switch feat/user-profile
git rebase origin/main
```

Si aparece un conflicto:

```bash
# resolver archivos
git add archivo-resuelto
git rebase --continue
```

Abortar:

```bash
git rebase --abort
```

> Evitá reescribir con rebase commits públicos que otras personas ya estén usando, salvo que el equipo haya acordado explícitamente ese flujo.

---

## Resolver conflictos

Git marca las zonas conflictivas así:

```text
<<<<<<< HEAD
cambio actual
=======
cambio entrante
>>>>>>> otra-rama
```

Proceso:

```bash
git status
# editar y resolver
git add archivo
```

Si estabas haciendo merge:

```bash
git commit
```

Si estabas haciendo rebase:

```bash
git rebase --continue
```

---

## Deshacer cambios de forma segura

### Restaurar un archivo no staged

```bash
git restore archivo.txt
```

### Sacar un archivo del staging sin perder cambios

```bash
git restore --staged archivo.txt
```

### Revertir un commit publicado

```bash
git revert <sha>
```

`revert` crea un nuevo commit inverso y suele ser la opción correcta en ramas compartidas.

### Reset local

```bash
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
```

`--hard` modifica índice y working tree. Puede eliminar trabajo no guardado.

---

## Reflog: la red de seguridad de Git

Si moviste una rama o hiciste un reset incorrecto:

```bash
git reflog
```

Luego podés inspeccionar o recuperar un commit:

```bash
git switch -c recovery/<nombre> <sha>
```

En muchos casos un commit “perdido” sigue siendo recuperable mientras permanezca referenciado por el reflog.

---

## Stash

Guardar cambios temporales:

```bash
git stash push -m "wip: formulario"
```

Listar:

```bash
git stash list
```

Recuperar y eliminar del stash:

```bash
git stash pop
```

Aplicar sin eliminar:

```bash
git stash apply stash@{0}
```

---

## Cherry-pick

Aplicar un commit puntual sobre otra rama:

```bash
git cherry-pick <sha>
```

Es útil para hotfixes o para trasladar un cambio aislado. No debería convertirse en el mecanismo normal de integración de ramas enteras.

---

# Pull Requests en GitHub

Un flujo habitual:

```bash
git switch main
git pull --ff-only
git switch -c feat/nueva-funcionalidad

# trabajar
git add .
git commit -m "feat: implement new feature"
git push -u origin feat/nueva-funcionalidad
```

Luego se crea un Pull Request hacia `main`.

Un PR profesional debería explicar:

- problema u objetivo;
- solución implementada;
- alcance;
- riesgos;
- cómo probarlo;
- screenshots si modifica UI;
- migraciones o variables de entorno si corresponden.

---

## Forks

Configurar el repositorio original como `upstream`:

```bash
git remote add upstream git@github.com:organizacion/proyecto.git
git fetch upstream
```

Actualizar tu `main`:

```bash
git switch main
git merge --ff-only upstream/main
git push origin main
```

---

# GitHub CLI (`gh`)

Autenticarse:

```bash
gh auth login
```

Crear PR:

```bash
gh pr create --fill
```

Ver PRs:

```bash
gh pr list
```

Revisar checks:

```bash
gh pr checks
```

Ver PR actual:

```bash
gh pr view --web
```

---

## Tags y releases

Crear tag anotado:

```bash
git tag -a v2.0.0 -m "Release v2.0.0"
```

Publicarlo:

```bash
git push origin v2.0.0
```

Versionado SemVer:

```text
MAJOR.MINOR.PATCH
```

- `MAJOR`: cambios incompatibles o reestructuración mayor;
- `MINOR`: nuevas funcionalidades compatibles;
- `PATCH`: correcciones compatibles.

Los tags identifican commits. Los **GitHub Releases** agregan metadata, notas, assets y una presentación orientada a usuarios.

---

## SSH con GitHub

Recomendado actualmente:

```bash
ssh-keygen -t ed25519 -C "tu@email.com"
```

Iniciar agente:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

Ver clave pública:

```bash
cat ~/.ssh/id_ed25519.pub
```

Probar conexión:

```bash
ssh -T git@github.com
```

Nunca compartas la clave privada.

---

## `.gitignore`

Ejemplo genérico:

```gitignore
.env
.env.*
node_modules/
dist/
build/
coverage/
*.log
.DS_Store
.vscode/
```

> `.gitignore` no elimina archivos que ya están versionados.

Para dejar de trackear uno sin borrarlo localmente:

```bash
git rm --cached .env
```

Si un secreto ya fue publicado, borrarlo del último commit no invalida la credencial. Primero hay que **rotarla o revocarla** y luego limpiar el historial si corresponde.

---

## Historial útil

```bash
git log --oneline --graph --decorate --all
```

Buscar por texto del commit:

```bash
git log --grep="auth"
```

Buscar commits que agregaron o eliminaron una cadena:

```bash
git log -S "TOKEN_AUTH" --oneline
```

Ver quién modificó líneas:

```bash
git blame archivo.txt
```

---

## Comandos que conviene tratar con respeto

```bash
git reset --hard
git clean -fd
git push --force
git branch -D
git rebase
```

No son comandos “malos”; simplemente pueden reescribir referencias o destruir cambios si se ejecutan sin entender el estado actual.

Para ramas propias que ya fueron publicadas y reescritas intencionalmente, preferí:

```bash
git push --force-with-lease
```

antes que:

```bash
git push --force
```

---

# Estrategia recomendada para equipos pequeños y medianos

Una base pragmática:

```text
main
 ├── feat/...
 ├── fix/...
 ├── refactor/...
 └── chore/...
```

Flujo:

1. `main` siempre estable;
2. rama corta por tarea;
3. commits pequeños y comprensibles;
4. Pull Request obligatorio para cambios importantes;
5. CI ejecutándose sobre el PR;
6. squash o merge según política del equipo;
7. eliminar branch después del merge.

No hace falta imponer GitFlow completo si el producto no necesita ramas de release mantenidas en paralelo.

---

## Diagrama histórico del repositorio

El recurso original se conserva como referencia:

<p align="center">
  <img src="git-desarrollo-EdIT.png" alt="Diagrama de desarrollo con Git" width="700" />
</p>

---

## Ruta de aprendizaje

```text
Modelo mental de Git
       ↓
status / diff / add / commit
       ↓
branches
       ↓
merge y conflictos
       ↓
remotes / fetch / pull / push
       ↓
Pull Requests
       ↓
rebase / cherry-pick
       ↓
reset / revert / reflog
       ↓
SSH / seguridad
       ↓
tags / releases / CI
```

---

## Recursos oficiales

- Git: <https://git-scm.com/>
- Pro Git: <https://git-scm.com/book/en/v2>
- Git Reference: <https://git-scm.com/docs>
- GitHub Docs: <https://docs.github.com/>
- GitHub CLI: <https://cli.github.com/>
- Semantic Versioning: <https://semver.org/>
- Conventional Commits: <https://www.conventionalcommits.org/>

---

## Autor

**[Alejandro Di Stefano](https://github.com/Drako01)**

Repositorio mantenido como material práctico de referencia y formación sobre Git y GitHub.

---

## Licencia y uso

Podés utilizar este material como referencia de estudio. Si lo reutilizás públicamente, mantené la atribución correspondiente al autor y al repositorio original.
