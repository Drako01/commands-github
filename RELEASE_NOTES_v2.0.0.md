# Git & GitHub Guide v2.0.0 — Professional Edition

Esta versión transforma el repositorio en una guía profesional de Git y GitHub, pensada tanto para aprendizaje como para consulta diaria en proyectos reales.

## Highlights

- Tutorial modular desde fundamentos hasta workflows profesionales.
- Flujo diario con `status`, `diff`, staging y commits.
- Uso moderno de `git switch` y `git restore`.
- Branches, merge, rebase, cherry-pick y resolución de conflictos.
- Pull Requests, forks, reviews y GitHub CLI.
- Recuperación con `reflog`, `reset`, `revert` y stash.
- SSH, secretos y `.gitignore`.
- Conventional Commits y Semantic Versioning.
- Tags, releases y GitHub Actions.
- Cheat sheet de comandos frecuentes.
- Buenas prácticas para equipos y ramas protegidas.

## Breaking documentation change

La documentación fue reorganizada por completo. El README anterior acumulaba comandos y un tutorial en la misma página; desde `v2.0.0`, el README funciona como entrada principal y los temas detallados viven en `docs/`.

## Correcciones importantes

- Se eliminan duplicaciones de contenido.
- Se corrigen typos y comandos inconsistentes.
- Se reemplazan recetas antiguas basadas exclusivamente en `checkout` por alternativas actuales donde corresponde.
- Se aclara el riesgo de `reset --hard`, `clean -fd`, `branch -D` y force push.
- Se diferencia el tratamiento del historial local respecto del historial ya compartido.
- Se recomienda `git push --force-with-lease` cuando una reescritura remota sea necesaria.

## Autor

**[Alejandro Di Stefano](https://github.com/Drako01)**

## Tag propuesto

```text
v2.0.0
```

## Título sugerido del GitHub Release

```text
Git & GitHub Guide v2.0.0 — Professional Edition
```
