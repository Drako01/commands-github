# Changelog

Todos los cambios relevantes de este repositorio se documentan en este archivo.

El versionado sigue el criterio de [Semantic Versioning](https://semver.org/).

## [2.0.0] — 2026-08-23

### Added

- Nueva guía profesional y progresiva de Git + GitHub.
- Capítulo de fundamentos, configuración y modelo mental de Git.
- Capítulo de flujo diario, staging, commits y Conventional Commits.
- Capítulo de branches, merge, rebase, cherry-pick y conflictos.
- Capítulo completo de colaboración con GitHub, Pull Requests, forks, reviews y GitHub CLI.
- Capítulo de recuperación con `restore`, `reset`, `revert`, `reflog`, stash y clean.
- Sección de seguridad, SSH, secretos y `.gitignore`.
- Capítulo de tags, Semantic Versioning, releases y GitHub Actions.
- Cheat sheet de consulta rápida.
- Referencias oficiales y ruta de aprendizaje.
- Autoría visible de Alejandro Di Stefano enlazada al perfil de GitHub.

### Changed

- El README deja de ser una colección acumulativa y duplicada de comandos para convertirse en la landing principal de una documentación modular.
- Se priorizan comandos modernos como `git switch` y `git restore` para operaciones que históricamente se resolvían con `git checkout`.
- Se reemplazan ejemplos centrados en `master` por `main`, sin asumir que todos los repositorios deben usar necesariamente el mismo nombre.
- Se mejora la explicación de `fetch`, `pull`, `push`, branches y remotes.
- Se agrega contexto de seguridad alrededor de operaciones destructivas.
- Se diferencia correctamente el uso de `reset` frente a `revert` en historial local y compartido.
- Se recomienda `--force-with-lease` frente a `--force` cuando una reescritura remota es realmente necesaria.

### Fixed

- Typos y comandos mal escritos presentes en la documentación histórica.
- Ejemplos ambiguos de `git rebase`.
- Explicaciones incorrectas o demasiado simplificadas sobre eliminación de branches.
- Referencias inconsistentes a `master` y `main`.
- Duplicación extensa entre la sección original de comandos y el tutorial añadido posteriormente.

## Versiones anteriores

El repositorio original funcionaba como una colección de comandos, ejemplos y apuntes de Git/GitHub. La versión `2.0.0` representa una reestructuración mayor del alcance y la organización de ese material.
