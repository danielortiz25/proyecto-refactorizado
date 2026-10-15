# Proyecto refactorizado: portfolio personal

Taller práctico **"El Refactor"** del módulo Diseño de Interfaces Web (DIW), UD2 - Uso de Estilos (RA2).

Sitio web personal de tres páginas (Inicio, Sobre mí y Contacto) que partía de un código "sucio" con estilos en línea (`index.html`) y estilos internos (`sobre.html`). Se ha refactorizado para centralizar toda la apariencia en una única hoja de estilos generada con Sass.

## Estructura

```
proyecto-refactorizado/
├── index.html
├── sobre.html
├── contacto.html
├── css/
│   └── estilos.css        # CSS compilado (el que enlazan las páginas)
├── scss/
│   ├── estilos.scss       # Punto de entrada: importa los parciales
│   ├── _colores.scss      # Paleta de colores y fuentes (variables)
│   ├── _fuentes.scss      # Importación de Google Fonts
│   ├── _mixins.scss       # Mixin reutilizable para campos de texto
│   ├── _base.scss         # body, títulos, párrafos
│   ├── _header.scss
│   ├── _nav.scss
│   ├── _contenido.scss
│   ├── _formulario.scss
│   ├── _botones.scss
│   └── _footer.scss
└── .vscode/
    └── settings.json      # Configuración de Live Sass Compiler
```

## Qué se ha hecho

- **Refactorización:** eliminados todos los atributos `style=""` y el bloque `<style>`. Las tres páginas quedan sin estilos propios y enlazan `css/estilos.css`.
- **HTML semántico:** `header`, `nav`, `main`, `section`, `footer`, y formulario con `label` asociados a sus campos.
- **Sass:** variables, anidamiento y un mixin (`campo-texto`), organizados en parciales.
- **Identidad visual:**
  - Paleta: azul petróleo `#0A4F60` (primario), ámbar `#E8A33D` (secundario), texto `#1B2A30` y fondo claro `#F4F8F9`.
  - Tipografías: Montserrat para los encabezados y Open Sans para el cuerpo.
- **Menú:** flexbox, sin subrayado y con efecto `hover`. El enlace de la página actual se marca con la clase `activo`.
- **Formulario de contacto:** campos al 100% de ancho, con `padding` y `margin`, y botón con el color primario (solo estructura, sin funcionalidad).
- **Validación:** `css/estilos.css` validado en el [W3C CSS Validator](https://jigsaw.w3.org/css-validator/) sin errores.

## Cómo compilar el Sass

1. Instala la extensión **Live Sass Compiler** (Glen Marks) en VS Code.
2. Abre `scss/estilos.scss` y pulsa **Watch Sass** en la barra de estado.
3. Al guardar cualquier archivo `.scss`, el CSS se regenera en `css/estilos.css` (la ruta está configurada en `.vscode/settings.json`).

## Sobre la carpeta `.vscode`

La actividad no pide esta carpeta; la he añadido por una razón práctica.

Por defecto, Live Sass Compiler guarda el CSS compilado **junto al SCSS** (en `scss/estilos.css`). Yo prefiero mantener el SCSS y el CSS en carpetas separadas, y que las tres páginas enlacen `css/estilos.css`. Para eso hay que indicarle a la extensión dónde guardarlo, y lo he hecho en `.vscode/settings.json`:

```json
{
  "liveSassCompile.settings.formats": [
    { "format": "expanded", "extensionName": ".css", "savePath": "/css" }
  ],
  "liveSassCompile.settings.generateMap": false
}
```

- `savePath: "/css"` hace que el CSS se genere en `css/estilos.css`.
- `format: "expanded"` genera el CSS con una regla por línea, fácil de leer.
- `generateMap: false` evita crear el archivo `.map` (source map), que no hace falta.

La carpeta `.vscode` solo afecta a este proyecto, no a otros proyectos de VS Code. Si no se quiere usar, el proyecto funciona igual, pero habría que cambiar el `<link>` de las páginas a `scss/estilos.css` o mover el CSS a mano después de compilar.

## Cómo verlo

Abre `index.html` en el navegador (por ejemplo, con la extensión Live Server de VS Code).