# 01 — Fundamentos y configuración

## Qué problema resuelve Git

Git registra la evolución de un conjunto de archivos mediante snapshots identificados por commits. Cada clon contiene un repositorio completo, por lo que la mayoría de las operaciones son locales.

## Modelo mental

```text
Working Tree -> Index/Staging Area -> Local Repository -> Remote
```

- **Working Tree**: archivos que editás.
- **Index / Staging Area**: selección exacta que formará el próximo commit.
- **Repository**: historial persistido en `.git/`.
- **Remote**: referencia a otro repositorio, normalmente GitHub.

## Objetos internos

Git trabaja principalmente con:

- **blob**: contenido de archivo;
- **tree**: estructura de directorios;
- **commit**: snapshot + metadata + padres;
- **tag**: referencia nombrada a un objeto, normalmente un commit.

`HEAD` representa la referencia actualmente checkout/switchada.

## Instalación

Descarga oficial: <https://git-scm.com/downloads>

Verificar:

```bash
git --version
```

## Configuración global

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
git config --global init.defaultBranch main
```

Consultar:

```bash
git config --global --list
git config --list --show-origin
```

Git maneja distintos niveles:

```text
system -> global -> local
```

La configuración local del repositorio tiene prioridad sobre la global.

```bash
git config user.email "email-especifico@empresa.com"
```

## Crear repositorio

```bash
mkdir demo
cd demo
git init
```

Verificar:

```bash
git status
```

## Clonar

HTTPS:

```bash
git clone https://github.com/usuario/proyecto.git
```

SSH:

```bash
git clone git@github.com:usuario/proyecto.git
```

Nombre local distinto:

```bash
git clone git@github.com:usuario/proyecto.git proyecto-local
```

## `.git`

No edites manualmente `.git/` salvo que sepas exactamente qué estás haciendo. Contiene referencias, objetos, configuración, logs y metadata esencial del repositorio.

## Primer laboratorio

```bash
mkdir git-lab
cd git-lab
git init

echo "# Git Lab" > README.md
git status
git add README.md
git commit -m "docs: initialize repository"
git log --oneline
```

## Buenas prácticas iniciales

- Usar `main` como rama principal salvo política contraria.
- Configurar identidad correctamente antes de comenzar.
- No versionar secretos.
- Crear `.gitignore` desde el inicio.
- No ejecutar comandos destructivos sin revisar `git status` y el historial.

## Diagnóstico rápido

```bash
git status
git branch --show-current
git remote -v
git log --oneline -10
```
