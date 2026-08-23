# 06 — Automatización, tags y releases

## Tags

Listar:

```bash
git tag
```

Crear tag anotado:

```bash
git tag -a v2.0.0 -m "Release v2.0.0"
```

Verlo:

```bash
git show v2.0.0
```

Publicarlo:

```bash
git push origin v2.0.0
```

Todos los tags:

```bash
git push origin --tags
```

Eliminar local:

```bash
git tag -d v2.0.0
```

Eliminar remoto:

```bash
git push origin :refs/tags/v2.0.0
```

## Semantic Versioning

Formato:

```text
MAJOR.MINOR.PATCH
```

- **MAJOR**: cambio incompatible o reestructuración mayor.
- **MINOR**: nueva funcionalidad compatible.
- **PATCH**: bugfix compatible.

Ejemplos:

```text
1.4.2 -> 1.4.3  patch
1.4.2 -> 1.5.0  minor
1.4.2 -> 2.0.0  major
```

## GitHub Release vs tag

Un tag es una referencia Git. Un GitHub Release es una capa de publicación asociada a un tag que puede contener:

- título;
- release notes;
- assets;
- binaries;
- indicación de prerelease;
- información orientada al usuario.

## Conventional Commits

```text
feat: nueva funcionalidad
fix: bugfix
docs: documentación
refactor: refactorización
perf: performance
test: tests
build: build/dependencies
ci: CI/CD
chore: mantenimiento
```

Breaking change:

```text
feat!: change authentication contract
```

O mediante footer:

```text
BREAKING CHANGE: old endpoint was removed
```

## GitHub Actions

Workflow mínimo:

```yaml
name: CI

on:
  pull_request:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run checks
        run: echo "Agregar lint, tests o build"
```

Los workflows viven en:

```text
.github/workflows/
```

## CI profesional

Checks frecuentes:

- lint;
- format check;
- unit tests;
- integration tests;
- build;
- type checking;
- security scanning;
- dependency audit;
- smoke tests.

La rama principal debería quedar protegida cuando el proyecto lo requiera, haciendo obligatorios los checks críticos.

## Releases automatizados

Con una política consistente de commits es posible automatizar:

- cálculo de versión;
- changelog;
- tag;
- GitHub Release;
- publicación de paquetes.

Herramientas habituales incluyen Release Please, semantic-release y Changesets. La elección depende del stack y del tipo de distribución.

## Versionar documentación

Una guía técnica también puede usar SemVer. Un cambio como transformar una lista básica de comandos en un tutorial completo justifica un `MAJOR` porque cambia sustancialmente el alcance y la estructura de consumo.

## Checklist de release

Antes de publicar:

- `main` estable;
- CI verde;
- changelog actualizado;
- versión definida;
- breaking changes documentados;
- secretos ausentes;
- documentación actualizada;
- tag apuntando al commit correcto;
- release notes comprensibles para una persona que no vio los commits.

## Ejemplo manual

```bash
git switch main
git pull --ff-only

git tag -a v2.0.0 -m "Release v2.0.0"
git push origin v2.0.0
```

Luego se crea el GitHub Release tomando `v2.0.0` como tag y usando notas preparadas para esa versión.
