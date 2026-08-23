# 05 — Recuperación y seguridad

## `restore`, `reset` y `revert`

Son herramientas distintas.

### `git restore`

Descarta cambios del working tree:

```bash
git restore archivo.txt
```

Saca del staging sin borrar modificaciones:

```bash
git restore --staged archivo.txt
```

### `git revert`

Revierte un commit creando otro commit:

```bash
git revert <sha>
```

Es la alternativa preferida para deshacer cambios ya compartidos en ramas públicas.

### `git reset`

Mueve la referencia actual.

```bash
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
```

- `--soft`: conserva staging y working tree.
- `--mixed`: conserva working tree y reconstruye staging.
- `--hard`: alinea branch, staging y working tree; puede eliminar cambios locales.

## Reflog

```bash
git reflog
```

Ejemplo de recuperación:

```bash
git reflog
git switch -c recovery/lost-work <sha>
```

## Stash

```bash
git stash push -m "wip: payment form"
git stash list
git stash show -p stash@{0}
git stash pop
```

Incluir untracked:

```bash
git stash push -u -m "wip with untracked"
```

## Limpiar archivos no trackeados

Previsualizar primero:

```bash
git clean -nd
```

Eliminar:

```bash
git clean -fd
```

> Nunca uses `git clean -fd` sin revisar primero con `-n` si hay archivos que necesitás conservar.

## Force push

Si reescribiste intencionalmente una rama propia:

```bash
git push --force-with-lease
```

`--force-with-lease` verifica que el remoto siga en el estado esperado y reduce el riesgo de pisar commits ajenos.

## SSH

Generar clave moderna:

```bash
ssh-keygen -t ed25519 -C "tu@email.com"
```

Agregar al agente:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

Probar GitHub:

```bash
ssh -T git@github.com
```

Nunca compartas:

```text
~/.ssh/id_ed25519
```

La clave `.pub` sí puede cargarse en GitHub.

## Secretos

Nunca versionar:

- passwords;
- API keys;
- tokens;
- private keys;
- `.env` reales;
- credenciales cloud;
- connection strings con secretos.

Si un secreto fue publicado:

1. revocarlo o rotarlo inmediatamente;
2. reemplazarlo en la aplicación;
3. revisar logs y accesos;
4. limpiar el historial si corresponde.

Borrarlo del último commit no lo convierte mágicamente en secreto otra vez.

## `.gitignore`

```gitignore
.env
.env.*
!.env.example
*.pem
*.key
node_modules/
dist/
coverage/
```

## Recuperar un archivo de otro commit

```bash
git restore --source=<sha> -- path/al/archivo
```

## Recuperar una rama borrada

```bash
git reflog
# identificar último SHA
git switch -c recovery/branch <sha>
```

## Commit en rama equivocada

Si todavía no hiciste push:

```bash
git branch feat/correct-branch
git reset --hard HEAD~1
git switch feat/correct-branch
```

Una alternativa más explícita es crear primero la nueva rama apuntando al commit y luego mover la rama original.

## Deshacer un merge publicado

En una rama compartida suele ser preferible:

```bash
git revert -m 1 <merge_sha>
```

El parámetro `-m` indica qué padre debe considerarse línea principal. Revisá el resultado antes de publicar.

## Diagnóstico antes de actuar

```bash
git status
git branch -vv
git log --oneline --graph --decorate --all -20
git reflog -20
git remote -v
```

Estos comandos suelen dar contexto suficiente para evitar una recuperación destructiva innecesaria.
