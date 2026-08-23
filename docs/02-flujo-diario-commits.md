# 02 — Flujo diario y commits

## Inspeccionar antes de modificar

```bash
git status
git diff
git diff --staged
```

`git status` indica qué está modificado, staged, untracked o en conflicto.

## Staging Area

Agregar un archivo:

```bash
git add src/app.js
```

Agregar un directorio:

```bash
git add src/
```

Agregar todos los cambios visibles:

```bash
git add .
```

Seleccionar hunks interactivos:

```bash
git add -p
```

Esto permite construir commits más pequeños aunque hayas trabajado sobre varios cambios simultáneamente.

## Sacar algo del staging

```bash
git restore --staged archivo.txt
```

El contenido permanece en el working tree.

## Restaurar cambios locales

```bash
git restore archivo.txt
```

Esto descarta modificaciones no commitadas en ese archivo.

## Commit

```bash
git commit -m "fix: validate empty email"
```

Abrir editor para un mensaje extendido:

```bash
git commit
```

## Anatomía recomendada

```text
<tipo>(<scope opcional>): <resumen>

<cuerpo opcional>

<footer opcional>
```

Ejemplo:

```text
fix(auth): reject expired reset tokens

Validate token expiration before changing the password.

Refs: #123
```

## Amend

Corregir el último commit local:

```bash
git add archivo-olvidado.txt
git commit --amend
```

Cambiar sólo el mensaje:

```bash
git commit --amend -m "docs: correct setup instructions"
```

> `amend` cambia el SHA. Si el commit ya fue compartido, evaluá el impacto antes de reescribirlo.

## Historial

```bash
git log
git log --oneline
git log --oneline --graph --decorate --all
git show <sha>
```

Últimos cinco commits:

```bash
git log -5 --oneline
```

## Diff entre referencias

```bash
git diff main..feat/login
git diff <sha1>..<sha2>
```

## Ignorar archivos

`.gitignore` típico:

```gitignore
.env
.env.*
node_modules/
dist/
coverage/
*.log
.DS_Store
```

Comprobar por qué un archivo está ignorado:

```bash
git check-ignore -v archivo
```

## Archivos ya trackeados

Agregar un path al `.gitignore` no deja de trackearlo automáticamente.

```bash
git rm --cached archivo
```

Para directorios:

```bash
git rm -r --cached directorio/
```

## Eliminar y renombrar

```bash
git rm archivo.txt
git mv viejo.txt nuevo.txt
```

Git detecta renames por similitud; no almacena una operación de rename como entidad independiente.

## Workflow diario recomendado

```bash
git switch main
git pull --ff-only
git switch -c feat/nueva-tarea

# editar

git status
git diff
git add -p
git diff --staged
git commit -m "feat: implement new task"
git push -u origin feat/nueva-tarea
```

## Anti-patrones

- `git add .` sin mirar qué entra.
- Commits como `cambios`, `fix`, `cosas`.
- Mezclar refactor, feature y format masivo en un único commit.
- Versionar `.env`, tokens, claves o dumps sensibles.
- Hacer `amend` o rebase sobre historial compartido sin coordinar.
