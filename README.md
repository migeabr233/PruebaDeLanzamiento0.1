# B.caapi - Documentación del Proyecto

## Visión general
Este proyecto es una página estática con React UMD y Tailwind CSS cargados desde CDN. La página principal es `index.html` y usa `js/index.js` para renderizar toda la interfaz mediante componentes de React.

El archivo `index2.html` es una copia de seguridad de la versión anterior del sitio y no se usa en el flujo principal.

---

## Estructura de archivos

- `index.html`
  - Página principal actual.
  - Carga el CSS desde `css/index.css`.
  - Carga React, ReactDOM y Babel desde CDN.
  - Importa `js/index.js` con `type="text/babel"`.

- `index2.html`
  - Versión antigua conservada como respaldo.

- `css/index.css`
  - Estilos personalizados globales y utilidades para la página.

- `js/index.js`
  - Lógica del sitio.
  - Define los datos del catálogo, las colecciones, testimonios, galería y la marca.
  - Contiene el componente principal `App` y componentes secundarios como `Header`, `HeroSection`, `ProductsSection`, `CartDrawer`, `ProductModal`, `Footer`, entre otros.

- `bcappi.jpeg`
  - Imagen usada en el header.

- `serve-local.bat` y `serve-local.ps1`
  - Scripts opcionales para iniciar un servidor local si se desea.

---

## Cómo ejecutar el proyecto

### 1. Abrir directamente en navegador
- Puedes abrir `index.html` directamente en el navegador.
- Sin embargo, algunos navegadores bloquean la carga de `type="text/babel"` cuando se usa `file://`.
- Si al abrirlo directamente la página no carga, usa una versión servida por HTTP.

### 2. Servir con un servidor local (recomendado para desarrollo)

Desde la carpeta del proyecto:

```powershell
python -m http.server 8000
```

Después abre:

```text
http://localhost:8000/index.html
```

Si necesitas, puedes usar los scripts:

- `serve-local.bat`
- `serve-local.ps1`

---

## Cómo mantener la página

### Datos y contenido
- El contenido de la página está centralizado en `js/index.js` dentro de la constante `B_CAAPI_DATA`.
- Para cambiar productos, colecciones, testimonios, contactos, o textos generales, edita los objetos dentro de `B_CAAPI_DATA`.
- Ejemplo:
  - Cambia `brandInfo.whatsapp` para actualizar el número de WhatsApp.
  - Agrega nuevos productos en la lista `products`.
  - Ajusta `collections` para cambiar las categorías.

### Componentes clave
- `App`
  - Maneja los estados del carrito, producto seleccionado, filtro activo, formulario de contacto y toast.
  - Renderiza todas las secciones de la página.

- `Header`
  - Barra superior con navegación y acceso al carrito.

- `ProductsSection`
  - Lista productos filtrables por colección.
  - Usa `FilterButton` y `ProductCard`.

- `ProductCard`
  - Muestra cada producto y permite ver detalles o añadir al carrito.

- `CartDrawer`
  - Ventana lateral que muestra los productos en el carrito.

- `ProductModal`
  - Modal que muestra detalles de un producto seleccionado.

- `ContactSection`
  - Formulario de contacto que redirige a WhatsApp.

---

## Qué revisar antes de un cambio importante

1. **Dependencias en HTML**
   - React y ReactDOM se cargan desde CDN.
   - Babel transpila JSX en el navegador.
   - Si se hace un cambio mayor, considera precompilar JSX con un bundler.

2. **Rutas de archivos**
   - `index.html` carga `css/index.css` y `js/index.js`.
   - Si renuevas nombres de archivos, actualiza esas referencias.

3. **Clases Tailwind**
   - El proyecto usa Tailwind vía CDN, por lo que todas las clases de utilidad se usan directamente en JSX.
   - Si se necesita escalar, puede ser buena idea migrar a un `postcss`/`tailwind.config.js` real.

4. **Imágenes y recursos externos**
   - Muchas imágenes usan URLs de Unsplash.
   - Si deseas hacer el sitio más estable, almacena las imágenes localmente o usa un CDN propio.

---

## Recomendaciones para escalar la página

### Opción 1: Mantener como página estática ligera
- Sigue usando `index.html`, `css/index.css` y `js/index.js`.
- Mantén el contenido en `B_CAAPI_DATA` si no necesitas un CMS.
- Buena opción para GitHub Pages o Vercel como sitio estático.

### Opción 2: Migrar a un proyecto React moderno
- Usa `create-react-app`, Vite o Next.js.
- Convierte `js/index.js` en componentes `.jsx` separados.
- Mueve los datos a archivos JSON o a un backend si la tienda crece.
- Facilita mantenimiento, testing y despliegue profesional.

### Opción 3: Agregar build y minificación
- Elimina `type="text/babel"` para producción.
- Compila JSX a JS con un bundler (Vite, Webpack, Rollup, esbuild).
- Usa Tailwind con PostCSS para un CSS más óptimo.

---

## Cómo agregar una nueva sección

1. Crea un nuevo componente funcional en `js/index.js`.
2. Inserta el componente dentro de `<main>` en el `return` de `App`.
3. Añade datos a `B_CAAPI_DATA` si necesitas contenido estructurado.
4. Si el estilo es nuevo, agrégalo a `css/index.css`.

---

## Notas finales

- `index2.html` es un respaldo de la versión anterior.
- El código actual es fácil de mantener si se maneja bien el bloque `B_CAAPI_DATA`.
- Si buscas escalar de verdad, la mejor práctica es migrar a una configuración de build y separar componentes en archivos individuales.

---

## Contacto de mantenimiento
- Revisa primero `js/index.js` para cambios de contenido
- Revisa `css/index.css` para cambios visuales
- Revisa `index.html` para cambios en dependencias o carga de scripts
- Mantén `index2.html` como respaldo antes de hacer grandes cambios
