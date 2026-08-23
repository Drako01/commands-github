# 04 — GitHub y colaboración profesional

## Remotes

```bash
git remote -v
git remote add origin git@github.com:usuario/repositorio.git
git remote set-url origin git@github.com:usuario/repositorio.git
```

## Fetch

```bash
git fetch origin
```

Descarga referencias remotas sin integrar cambios.

Limpiar referencias de ramas remotas eliminadas:

```bash
git fetch --prune
```

## Pull

```bash
git pull --ff-only origin main
```

`--ff-only` evita merges locales implícitos si la rama divergió.

Otra política válida es rebase explícito:

```bash
git pull --rebase origin main
```

El equipo debería acordar una estrategia.

## Push

Primera publicación:

```bash
git push -u origin feat/customer-search
```

Luego:

```bash
git push
```

## Pull Requests

Un PR es una unidad de revisión e integración, no sólo un botón de merge.

### Contenido recomendado

```text
## Objetivo
Qué problema resuelve.

## Cambios
Qué se modificó.

## Cómo probar
Pasos reproducibles.

## Riesgos
Regresiones, migraciones, flags, compatibilidad.

## Evidencia
Screenshots, logs o resultados cuando aplique.
```

## Tamaño de PR

PRs pequeños suelen tener:

- menor tiempo de review;
- menor superficie de regresión;
- conflictos más simples;
- rollback más fácil.

## Estrategias de merge en GitHub

### Merge commit

Conserva la estructura de la rama.

### Squash and merge

Genera un único commit en la rama destino. Muy útil cuando una feature contiene commits intermedios de trabajo.

### Rebase and merge

Reaplica commits de forma lineal en la rama destino.

No existe una única política universal; debe elegirse según trazabilidad y operación del equipo.

## Reviews

Una revisión útil evalúa:

- corrección funcional;
- legibilidad;
- seguridad;
- performance;
- testing;
- compatibilidad;
- observabilidad;
- mantenibilidad.

Evitar reviews centradas exclusivamente en estilo si un formatter o linter puede resolverlo automáticamente.

## Forks

```bash
git clone git@github.com:tu-usuario/proyecto.git
cd proyecto
git remote add upstream git@github.com:organizacion/proyecto.git
```

Actualizar desde upstream:

```bash
git fetch upstream
git switch main
git merge --ff-only upstream/main
git push origin main
```

## GitHub CLI

Instalación y documentación: <https://cli.github.com/>

Autenticación:

```bash
gh auth login
```

Crear PR:

```bash
gh pr create --fill
```

Listar:

```bash
gh pr list
```

Ver:

```bash
gh pr view
gh pr view --web
```

Checks:

```bash
gh pr checks
```

Checkout de un PR:

```bash
gh pr checkout 123
```

## Issues

Crear desde CLI:

```bash
gh issue create
```

Listar:

```bash
gh issue list
```

## Branch protection

En repositorios importantes conviene proteger `main` con políticas como:

- Pull Request obligatorio;
- checks de CI requeridos;
- reviews requeridas;
- bloqueo de force push;
- resolución de conversaciones antes del merge;
- branch actualizada cuando el riesgo lo justifique.

## CODEOWNERS

GitHub permite definir propietarios por paths:

```text
# .github/CODEOWNERS
/backend/ @backend-team
/frontend/ @frontend-team
/.github/ @platform-team
```

## Plantillas

Un repositorio maduro puede incluir:

```text
.github/
  PULL_REQUEST_TEMPLATE.md
  ISSUE_TEMPLATE/
```

Esto estandariza la información mínima necesaria para colaborar.

## Flujo recomendado

```bash
git switch main
git pull --ff-only
git switch -c feat/task-name
# trabajo
git add -p
git commit -m "feat: implement task"
git push -u origin feat/task-name
gh pr create --fill
```
