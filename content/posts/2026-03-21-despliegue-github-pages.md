---
title: "Despliegue del Blog en GitHub Pages"
date: 2026-03-21
author: "Arturo"
draft: false
type: "posts"
categories: ["proyecto", "deployment"]
tags: ["github-pages", "git", "github", "hugo"]
---

## Introducción

Desplegar un blog estático en **GitHub Pages** es uno de los métodos más simples y económicos para publicar contenido web. En esta entrada, veremos cómo configurar y desplegar nuestro blog hecho con **Hugo** en GitHub Pages de forma automática mediante acciones de CI/CD.

## ¿Qué es GitHub Pages?

GitHub Pages es un servicio de hosting estático gratuito proporcionado por GitHub que permite publicar sitios web directamente desde un repositorio. Es ideal para:

- 📚 Blogs personales y profesionales
- 📖 Documentación de proyectos
- 🎨 Portafolios
- 📊 Landing pages

## Requisitos previos

Antes de comenzar, necesitas tener:

- Una cuenta en **GitHub**
- Un repositorio con tu proyecto Hugo
- Git instalado en tu máquina local
- Conocimientos básicos de Git y GitHub

## Paso 1: Configurar el repositorio

### 1.1 Crear un repositorio en GitHub

1. Ve a [GitHub](https://github.com/new) y crea un nuevo repositorio
2. Nombra tu repositorio como `<username>.github.io` si deseas que sea tu sitio principal
3. Inicializa con un README si lo prefieres

### 1.2 Clonar el repositorio localmente

```bash
git clone https://github.com/<username>/<nombre-repo>.git
cd <nombre-repo>
```

## Paso 2: Configurar Hugo para GitHub Pages

### 2.1 Actualizar `hugo.toml`

En tu archivo `hugo.toml`, asegúrate de que la URL base sea correcta:

```toml
baseURL = "https://<username>.github.io/<repo-name>/"
languageCode = "es"
```

> **Nota:** Si usas un repositorio `<username>.github.io`, la baseURL será simplemente `https://<username>.github.io/`

### 2.2 Ignorar la carpeta `public`

El directorio `public` contiene archivos generados. Añade esto a tu `.gitignore`:

```
public/
resources/_gen/
```

## Paso 3: Configurar GitHub Actions

GitHub Actions permite automatizar el despliegue cada vez que hagas push a la rama principal. Crea el archivo `.github/workflows/deploy.yml`:

```yaml
name: Deploy Hugo site

on:
  push:
    branches:
      - main
      - master

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          submodules: true
          fetch-depth: 0

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: latest
          extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          cname: tudominio.com  # Opcional: si usas dominio personalizado
```

## Paso 4: Hacer push y desplegar

```bash
# Añade todos los cambios
git add .

# Commit
git commit -m "Configurar despliegue en GitHub Pages"

# Push a la rama principal
git push origin main
```

GitHub Actions ejecutará automáticamente el workflow y tu sitio estará disponible en `https://<username>.github.io/<repo-name>/`

## Paso 5: Verificar el despliegue

1. Ve a la pestaña **Actions** de tu repositorio
2. Observa que el workflow se está ejecutando
3. Una vez completado, accede a tu URL para verificar que el sitio está en línea

## Solución de problemas comunes

### ❌ El sitio no aparece después de desplegar

- Verifica que GitHub Pages esté habilitado en **Settings → Pages**
- Comprueba que la rama de despliegue esté configurada como `gh-pages`
- Espera 5-10 minutos después del primer despliegue

### ❌ El sitio se ve desalineado o sin estilos

- Asegúrate de que `baseURL` en `hugo.toml` es correcto
- Limpia la caché del navegador (Ctrl+Shift+Delete)
- Verifica que los paths relativos en tus assets son correctos

### ❌ Los cambios no se actualizan

- Confirma que el workflow finalizó exitosamente en la pestaña Actions
- Haz push a la rama correcta (main o master)

## Ventajas del despliegue en GitHub Pages

✅ **Gratuito** - Sin costes de hosting

✅ **Automático** - Se despliega al hacer push

✅ **Seguro** - HTTPS incluido

✅ **Integrado** - Control de versiones y despliegue en un solo lugar

✅ **Escalable** - Soporta tráfico alto sin problemas

## Alternativas: Azure Static Web Apps

Si prefieres más funcionalidades avanzadas, también puedes desplegar en **Azure Static Web Apps**, que ofrece:
- Staging environments automáticos para pull requests
- Funciones serverless
- API management integrado
- Mayor control de la infraestructura

## Conclusión

El despliegue en GitHub Pages es ideal para proyectos estáticos como blogs y documentación. Combinado con Hugo y GitHub Actions, obtienes un workflow eficiente y automatizado. Para nuestro proyecto colaborativo EQ20, esto nos permite compartir nuestro trabajo de forma rápida y profesional.

¡Ahora tu blog está disponible para el mundo! 🚀
