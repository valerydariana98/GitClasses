# Apuntes de Git

**Nombre:** Valery Dariana Ortuño Panozo

Repositorio creado para registrar el avance diario de la materia.

---

## Clase 1 – Introducción a Git

### ¿Qué es Git?

Git es un Sistema de Control de Versiones Distribuido (VCS).

Permite:

* Guardar archivos
* Mantener un historial de cambios
* Trabajar de manera local sin depender de internet

---

### ¿Cómo nació Git?

Git fue creado por **Linus Torvalds**.

---

### Instalación de Git

Para instalar Git:

1. Ir a la página oficial:
   https://git-scm.com/install/

2. Descargar según tu sistema operativo

3. Verificar instalación en terminal:

```bash
git --version
```

---

### Configuraciones básicas

Configurar nombre de usuario:

```bash
git config --global user.name "Tu Nombre"
```

Configurar correo:

```bash
git config --global user.email "tu@correo.com"
```

Configuración recomendada:

```bash
git config --global core.autocrlf true
```

---

### Archivos importantes en un repositorio

Todo repositorio debería tener:

* `README.md` → Documentación del proyecto
* `.gitignore` → Archivos que Git debe ignorar

---

## Clase 2 – Estados y Commits

### Los 3 estados de Git

Los archivos en Git pasan por tres estados:

| Estado | Zona | Descripción |
|---|---|---|
| Modificado | Directorio de Trabajo | Cambios locales que Git aún no tiene registrados |
| Preparado | Stage Area | Cambios seleccionados listos para el próximo commit |
| Confirmado | Repositorio Local | Cambios guardados en el historial con un hash único |

---

### Directorio de Trabajo

Git observa los archivos y los clasifica en:

* **Untracked:** Archivo nuevo que Git nunca ha visto
* **Modified:** Archivo que Git ya conoce y fue modificado, eliminado o renombrado

Comandos útiles:

```bash
# Revertir un archivo a su estado original (cuidado: borra los cambios)
git restore <archivo>
```

> Para que Git ignore un archivo nuevo, agrega su nombre al `.gitignore`.

---

### Stage Area

Es el área de preparación donde seleccionas qué cambios irán en el próximo commit.

```bash
# Agregar un archivo específico
git add <archivo>

# Agregar todos los archivos observados por Git
git add .

# Sacar un archivo del stage (vuelve a "Modified")
git restore --staged <archivo>
```

---

### Repositorio Local

Una vez en stage, se confirman los cambios con un commit, que crea un punto en el historial.

```bash
# Crear un commit
git commit -m "mensaje"

# Deshacer el último commit (los cambios vuelven a stage)
git reset --soft HEAD~1
```

---

### Buenas prácticas con commits

#### ¿Cada cuánto hacer un commit?

Usa **commits atómicos**: cada commit representa un único cambio lógico, pequeño y completo. Es mejor varios commits pequeños con sentido que uno grande con todo.

#### Cómo escribir un buen mensaje de commit

1. **Usa verbos imperativos en inglés:**

   * `Add` → se añade un nuevo archivo
   * `Change` → se modifica un archivo existente
   * `Fix` → se corrige un bug
   * `Remove` → se elimina un archivo

2. **Sin punto final ni puntos suspensivos**

3. **Máximo 50 caracteres** — si tienes mucho que explicar, probablemente debas separar el commit

4. **Usa prefijos semánticos:**

```bash
git commit -m "<tipo>: <descripción>"
```

| Prefijo | Cuándo usarlo |
|---|---|
| `feat` | Nueva funcionalidad para el usuario |
| `fix` | Bug que afecta al usuario |
| `perf` | Mejora de rendimiento |
| `build` | Cambios en el sistema de build o despliegue |
| `ci` | Cambios en integración continua |
| `docs` | Cambios en documentación |
| `refactor` | Renombrar variables, funciones, reestructurar código |
| `style` | Formato, espacios, tabulaciones (sin impacto funcional) |
| `test` | Tests nuevos o refactorización de tests |

5. **Agrega cuerpo si necesitas más contexto:**

```bash
git commit
# Primera línea: título (prefijo + descripción)
# Desde la segunda línea: cuerpo con la explicación detallada
```

---

## Clase 3 – GitHub y SSH

### ¿Qué es GitHub?

GitHub es una plataforma en la nube y red social para desarrolladores que permite alojar, gestionar y colaborar en proyectos de software usando Git.

> **Git ≠ GitHub:** Git es el sistema que crea los puntos de guardado. GitHub es el servidor donde esos puntos se almacenan y comparten. GitHub usa Git, pero no son lo mismo.

---

### SSH vs HTTPS

| | HTTPS | SSH |
|---|---|---|
| Autenticación | Te la pide cada vez (incluso con token) | Se configura una vez con una key |
| Comodidad | ❌ Tedioso | ✅ Sin interrupciones |
| Recomendado | No | **Sí, siempre usar SSH** |

---

### Configuración de SSH

Ejecuta estos comandos en tu terminal (Linux) o Git Bash (Windows):

```bash
# 1. Generar la clave SSH
ssh-keygen -t ed25519 -C "tu-correo@email.com"

# 2. Copiar el contenido de la clave pública
cat ~/.ssh/id_ed25519.pub
```

Luego en GitHub: **Perfil → Settings → SSH and GPG Keys → New SSH Key**, pega el contenido copiado, ponle un nombre a tu PC y click en **Add SSH Key**.

```bash
# 3. Verificar la conexión
ssh -T git@github.com
```

---

### Crear un repositorio en GitHub

1. Ve a `https://github.com/Tu-user?tab=repositories` y click en **New**
2. Pon el nombre y descripción del repositorio
3. Click en **Create Repository**

---

### Conectar un repositorio local con GitHub

> Requisito: ya debes tener el repo local inicializado (`git init`) y al menos un commit.

```bash
# Agregar el repositorio remoto (origin es el apodo por defecto de la URL)
git remote add origin git@github.com:TuUser/TuRepo.git

# Renombrar la rama principal a "main"
git branch -M main

# Subir los cambios por primera vez
git push -u origin main
```

---

### Clonar un repositorio

```bash
# Clonar con SSH (recomendado)
git clone "git@github.com:TuUser/TuRepo.git"

# Si lo clonaste con HTTPS por error, cambia el puntero a SSH
git remote set-url origin "git@github.com:TuUser/TuRepo.git"

# Ver a qué repositorio remoto está conectado tu repo
git remote -v
```

---

### Subir y bajar cambios

```bash
# Subir commits al servidor remoto
git push origin <rama>

# Traer commits del servidor remoto
git pull origin <rama>
```

| Comando | Acción |
|---|---|
| `git push` | "Empuja" tus commits hacia GitHub |
| `git pull` | "Trae" los commits de GitHub a tu máquina |
| `origin` | Apodo del repositorio remoto (GitHub) |
| `<rama>` | La rama que quieres subir o bajar |

---

## Clase 4 – Git Remote, SSH Múltiple y Checkout

### Git Remote

`git remote` gestiona las conexiones con repositorios remotos: le dice a Git local de dónde traer o hacia dónde enviar información.

```bash
# Ver las URLs a las que apunta el repositorio
git remote -v

# Vincular el repo local con uno remoto
git remote add origin <url>

# Cambiar la URL del repositorio remoto
git remote set-url origin <url>
```

---

### SSH Múltiple (varias cuentas de GitHub)

Cada cuenta de GitHub necesita su propia llave SSH. Una llave da acceso a una cuenta, no a varias.

**Paso 1 — Generar una nueva llave con nombre distinto:**

```bash
ssh-keygen -t ed25519 -C "micorreo@gmail.com" -f ~/.ssh/id_miname
```

**Paso 2 — Crear el archivo `~/.ssh/config` para que no choquen las llaves:**

```
# Cuenta principal
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519

# Cuenta secundaria
Host github-miname
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_miname
```

| Campo | Descripción |
|---|---|
| `Host` | Alias que le pones a la conexión (lo que escribes después de `git@`) |
| `HostName` | Dirección real del servidor, siempre `github.com` |
| `User` | Usuario del sistema remoto, siempre `git` en GitHub |
| `IdentityFile` | Ruta exacta a la llave privada que usar para ese Host |

**Paso 3 — Verificar que funciona:**

```bash
ssh -T git@github-miname
```

> ⚠️ Al clonar, usa el Host correcto para cada cuenta:
> ```bash
> git clone git@github-miname:usuario/repo.git
> ```

---

### Configuraciones locales (por repositorio)

Las configuraciones locales se aplican solo al repositorio actual y tienen prioridad sobre las globales.

```bash
# Sin el flag --global → aplica solo al repo actual
git config user.name "Mi Nombre"
git config user.email "micorreo@gmail.com"
```

---

### Git Checkout

`git checkout` mueve el **HEAD** (el puntero que indica dónde estás) hacia un commit o rama específica.

Sirve para:

* **Inspeccionar** → ver cómo era el código en un commit antiguo
* **Restaurar** → recuperar archivos eliminados o modificados
* **Experimentar** → probar cambios sin tocar la rama principal
* **Cambiar de rama** → moverse entre ramas

```bash
# Ir a un commit específico (por su hash)
git checkout <hash>

# Volver a la rama principal
git checkout main
```

---

### Estado "Detached HEAD"

Normalmente el HEAD apunta a una **rama** (que avanza con cada commit). Al hacer checkout a un commit, el HEAD apunta directamente a ese commit fijo — quedas en estado **Detached HEAD**.

> Es como ser un espectador en el pasado: puedes ver todo, pero si te vas sin "encarnar" en una rama, los cambios que hagas se pierden.

Si hiciste cambios en este estado y no quieres perderlos:

```bash
# Crear una rama nueva desde ese punto para conservar los cambios
git checkout -b rama_nueva
```

---

### Buenas prácticas con Checkout

* Antes de viajar al pasado, asegúrate de tener todo commiteado — Git no te dejará moverte con cambios sin guardar
* Si vas a escribir más de dos líneas en un commit antiguo, crea una rama de una vez
* No trabajes mucho tiempo en estado Detached HEAD
* Úsalo para aprender: hacer checkout a commits de proyectos grandes es excelente para entender cómo crecieron

---

## Clase 5 – Ramas y Gitflow Básico

### ¿Qué son las ramas?

Una rama es una bifurcación del estado del código que crea un camino paralelo de desarrollo. Permiten trabajar en nuevas funcionalidades o correcciones sin afectar el código principal.

---

### Git Branch

```bash
# Listar todas las ramas y ver dónde está el HEAD
git branch

# Crear una nueva rama desde la rama actual
git branch <rama>

# Eliminar una rama
git branch -D <rama>
```

---

### Git Checkout enfocado en ramas

```bash
# Cambiar a una rama existente (requiere tener el directorio limpio)
git checkout <rama>

# Crear una rama y moverse a ella en un solo paso
git checkout -b <rama>
```

---

### Git Checkout vs Git Switch

En 2019 (Git 2.23) se introdujo `git switch` para separar la navegación de ramas del resto de funciones de `checkout`.

| | `git checkout` | `git switch` |
|---|---|---|
| Propósito | Multipropósito: ramas, commits, archivos | Especializado solo en ramas |
| Riesgo | Puede dejarte en Detached HEAD fácilmente | Evita errores accidentales |
| Cuándo usarlo | Comando clásico y universal | Comando moderno recomendado |

```bash
# Cambiar de rama (moderno)
git switch <rama>

# Crear y moverse a una nueva rama (moderno)
git switch -c <rama>
```

---

### Gitflow Básico

Gitflow es un flujo de trabajo que establece reglas y convenciones para el uso de ramas, permitiendo trabajar de forma ordenada en equipo.

#### Ramas principales

| Rama | Propósito |
|---|---|
| `main` | Código en producción, siempre estable |
| `develop` | Pre-producción, donde se integran las funcionalidades antes de lanzar |

#### Ramas de apoyo

| Rama | Nace de | Muere en | Propósito |
|---|---|---|---|
| `feature/*` | `develop` | `develop` | Desarrollar una tarea o funcionalidad específica |
| `release/*` | `develop` | `main` y `develop` | Preparar y pulir una nueva versión (QA) |
| `hotfix/*` | `main` | `main` y `develop` | Arreglar bugs urgentes en producción |

#### Convención de nombres

```
feature/add-search-bar
feature/new-user-form

release/v1.0.0
release/v2.1.0-beta

hotfix/fix-login-error
hotfix/security-patch-v1.0.2
```

> **¿Por qué hotfix nace de `main` y no de `develop`?** Porque `develop` puede tener cambios inestables. Un parche de producción debe partir de un estado estable.