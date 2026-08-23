# 03 — Branches, merge y rebase

## Crear y cambiar ramas

```bash
git switch -c feat/payments
git switch main
```

Equivalente histórico:

```bash
git checkout -b feat/payments
git checkout main
```

## Inspeccionar ramas

```bash
git branch
git branch -a
git branch -vv
```

## Integrar con merge

```bash
git switch main
git merge feat/payments
```

### Fast-forward

Si `main` no avanzó desde que nació la feature, Git puede mover simplemente el puntero.

### Merge commit

Si las ramas divergieron, Git puede crear un commit con dos padres.

```bash
git merge --no-ff feat/payments
```

## Rebase

Reaplicar commits de una rama sobre otra base:

```bash
git fetch origin
git switch feat/payments
git rebase origin/main
```

Rebase cambia los SHAs de los commits reaplicados.

### Conflictos

```bash
git status
# resolver archivos
git add archivo
git rebase --continue
```

Abortar:

```bash
git rebase --abort
```

Omitir el commit conflictivo:

```bash
git rebase --skip
```

Usalo sólo si realmente querés descartar ese commit.

## Rebase interactivo

```bash
git rebase -i HEAD~5
```

Acciones frecuentes:

- `pick`: conservar;
- `reword`: cambiar mensaje;
- `edit`: pausar para modificar;
- `squash`: combinar preservando mensajes;
- `fixup`: combinar descartando el mensaje secundario;
- `drop`: eliminar commit.

## Merge vs rebase

### Merge

Ventajas:

- no reescribe commits existentes;
- refleja explícitamente la integración;
- es seguro para historial compartido.

### Rebase

Ventajas:

- historial lineal;
- útil para actualizar una feature antes del PR;
- permite limpiar commits antes de compartirlos.

Regla práctica: **no reescribas historial público compartido sin coordinación**.

## Cherry-pick

```bash
git cherry-pick <sha>
```

Abortar:

```bash
git cherry-pick --abort
```

Continuar después de resolver:

```bash
git add .
git cherry-pick --continue
```

## Conflictos

Marcadores:

```text
<<<<<<< HEAD
versión actual
=======
versión entrante
>>>>>>> branch
```

Secuencia de resolución:

```bash
git status
# editar
git add archivo
```

En merge:

```bash
git commit
```

En rebase:

```bash
git rebase --continue
```

## Eliminar ramas

Local segura:

```bash
git branch -d feat/payments
```

Local forzada:

```bash
git branch -D feat/payments
```

Remota:

```bash
git push origin --delete feat/payments
```

## Nombres recomendados

```text
feat/customer-notifications
fix/login-timeout
refactor/payment-service
chore/update-dependencies
docs/api-guide
```

## Estrategia pragmática

Para la mayoría de equipos de producto:

```text
main
 ├── feat/*
 ├── fix/*
 ├── refactor/*
 └── chore/*
```

Ramas cortas, PRs pequeños y CI rápido suelen ser más sostenibles que modelos con muchas ramas permanentes.
