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
