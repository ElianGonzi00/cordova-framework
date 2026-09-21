# Calendario trazable — Captura de imagen (Apache Cordova)

Aplicación **híbrida** desarrollada con **Apache Cordova** que implementa el acceso a la **cámara del dispositivo** para capturar y mostrar una imagen. Es la evidencia del **Trabajo Práctico N.º 4** de *Programación Cliente-Servidor*, donde se adapta una funcionalidad pendiente del caso trazable (servicio de calendario) a una app móvil construida con tecnología web.

## Funcionalidad implementada

- **Capturar foto**: invoca la cámara mediante `cordova-plugin-camera` y muestra la imagen en pantalla.
- **Enviar foto**: acción prevista para el envío al servidor (actualmente como *stub*, lista para conectarse al back-end).
- **Multiplataforma**: el mismo código funciona en la plataforma `browser` (data URI completo) y en dispositivos nativos Android/iOS (base64 crudo), resolviendo la diferencia de formato en tiempo de ejecución.

## Stack técnico

| Componente | Detalle |
|---|---|
| Framework | Apache Cordova (plataforma `browser`) |
| Plugin | `cordova-plugin-camera` ^8.0.0 |
| Front-end | HTML5, CSS3 (tokens propios), JavaScript |
| Estilos | Bootstrap 4.3.1 + `css/index.css` |

## Requisitos

- [Node.js](https://nodejs.org/) (incluye npm)
- Apache Cordova CLI **10.0.0 o superior**:
  ```bash
  npm install -g cordova
  ```

## Ejecución (plataforma browser)

Desde la carpeta `myproject/`:

```bash
npm install                  # instala dependencias y el plugin de cámara
cordova platform add browser # agrega la plataforma browser
cordova run browser          # compila y sirve la app
```

La aplicación queda disponible en **http://localhost:8000**.

> Nota: la plataforma `browser` es para desarrollo y prueba rápida (no requiere el SDK de Android). Para una entrega nativa se agregaría la plataforma `android` / `ios` y se generaría el APK/IPA correspondiente.

## Estructura del proyecto

```
myproject/
├── config.xml            # Configuración de la app Cordova (id, nombre, plugins)
├── package.json          # Dependencias y plataformas declaradas
└── www/                  # Código de la aplicación (lo que corre en el WebView)
    ├── index.html        # Estructura: título, botones y contenedor de la foto
    ├── css/index.css     # Estilos (tokens de diseño, responsive, dark mode)
    ├── js/index.js       # Lógica: deviceready, captura y render de la imagen
    └── img/logo.png
```

## Notas técnicas

La captura se resuelve en `www/js/index.js`. El plugin devuelve la imagen en formatos distintos según la plataforma, por eso el `src` se arma condicionalmente:

```js
photo.src = imageData.indexOf("data:") === 0
    ? imageData                              // browser: ya viene como data URI completo
    : "data:image/jpeg;base64," + imageData; // nativo: base64 crudo, se antepone la cabecera
```

Este detalle es lo que garantiza la **trazabilidad multiplataforma** de la funcionalidad sin duplicar código.

## Autor

**Elian González** — Licenciatura en Informática, Universidad Empresarial Siglo 21.
Trabajo Práctico N.º 4 — *Programación Cliente-Servidor*.

---

*Basado en el proyecto de inicio de Apache Cordova. Licencia Apache-2.0.*
