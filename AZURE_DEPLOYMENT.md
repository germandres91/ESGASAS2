# Guía de Despliegue en Azure Static Web Apps

## Archivos de Configuración Creados

Se han creado y optimizado los siguientes archivos para el despliegue correcto en Azure:

### 1. `staticwebapp.config.json`
- Configura las rutas de la aplicación
- Define el archivo de entrada como `index.html`
- Configura rutas específicas para páginas de casos
- Configura los tipos MIME para las imágenes
- Establece reglas de caché y manejo de errores 404

### 2. `.github/workflows/azure-static-web-apps.yml`
- Workflow de GitHub Actions para despliegue automático
- Se ejecuta cuando se hace push a la rama `main`
- Requiere el token `AZURE_STATIC_WEB_APPS_API_TOKEN` en los secrets de GitHub

### 3. `web.config`
- Configuración adicional para IIS/Azure
- Define tipos MIME para archivos especiales
- Configura compresión y reescritura de URLs

### 4. `robots.txt` y `sitemap.xml`
- Optimización SEO para motores de búsqueda
- Sitemap con todas las páginas del sitio

### 5. `.gitignore`
- Excluye archivos innecesarios del repositorio
- Incluye exclusiones específicas para Azure Static Web Apps

## Pasos para Desplegar

### 1. Subir archivos a GitHub
```bash
git add .
git commit -m "Configuración para Azure Static Web Apps"
git push origin main
```

### 2. Configurar Azure Static Web Apps
1. Ve al portal de Azure
2. Crea un nuevo recurso "Static Web App"
3. Conecta tu repositorio de GitHub
4. Configura:
   - **Source**: GitHub
   - **Repository**: Tu repositorio
   - **Branch**: main
   - **App location**: `/` (raíz del proyecto)
   - **API location**: (dejar vacío)
   - **Output location**: (dejar vacío)

### 3. Configurar GitHub Secrets
1. Ve a tu repositorio en GitHub
2. Settings → Secrets and variables → Actions
3. Agrega el secret: `AZURE_STATIC_WEB_APPS_API_TOKEN`
4. El valor lo obtienes del portal de Azure en la sección "Manage deployment token"

## Estructura del Proyecto

```
/
├── index.html                 # Página principal
├── caso-exploracion-minera.html
├── caso-ingenieria-civil.html
├── caso-recursos-hidricos.html
├── staticwebapp.config.json   # Configuración de Azure
├── web.config                 # Configuración IIS/Azure
├── robots.txt                 # SEO
├── sitemap.xml               # SEO
├── .github/
│   └── workflows/
│       └── azure-static-web-apps.yml
├── images/                    # Carpeta de imágenes
├── .gitignore
└── AZURE_DEPLOYMENT.md       # Esta guía
```

## Archivos Eliminados

Se eliminaron los siguientes archivos que podrían causar problemas en Azure:
- `generate-pdf.js` - Requiere Node.js (no compatible con Azure Static Web Apps)
- `generate_pdf.py` - Archivo Python vacío
- `package.json` - Dependencias de Node.js innecesarias
- `print-pdf.html` - Página duplicada
- `index-print.html` - Página duplicada
- `README_PDF.md` - Documentación innecesaria
- `INSTRUCCIONES_IMAGENES.md` - Documentación innecesaria

## Solución de Problemas

### Si aparece la página de bienvenida de Azure:
1. Verifica que el archivo `staticwebapp.config.json` esté en la raíz
2. Asegúrate de que `index.html` esté en la raíz del proyecto
3. Verifica que el workflow de GitHub Actions se ejecute correctamente

### Si las imágenes no se cargan:
1. Verifica que la carpeta `images/` esté incluida en el repositorio
2. Asegúrate de que las rutas en el HTML sean relativas (`images/archivo.jpg`)

## Notas Importantes

- El archivo `index.html` debe estar en la raíz del proyecto
- Todas las rutas de imágenes deben ser relativas
- El archivo `staticwebapp.config.json` configura el enrutamiento para SPA
- El workflow se ejecuta automáticamente en cada push a `main`
