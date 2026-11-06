# Home-Assistant-Realejos

Configuración y recursos del Home Assistant de casa.

## Plano 3D interactivo (`www/plano3d.html`)

Plano 3D de la vivienda (Three.js) para el dashboard de la tablet. Muestra las habitaciones, el mobiliario, la terraza y los dispositivos, y se conecta a Home Assistant:

- Tocar una habitación → enciende/apaga su luz (el suelo se ilumina).
- Tocar o mantener pulsado un dispositivo → abre su detalle en HA.
- Botones: vista 3D / planta, paredes bajas, ocultar nombres.
- Fuera de HA se abre en **modo demo** (estados simulados).

### Instalación

1. Copia `www/plano3d.html` a `/config/www/plano3d.html` del Home Assistant (si `www` no existía, reinicia HA).
2. Añade una tarjeta **Página web** al dashboard (mejor en una vista tipo *Panel*):

   ```yaml
   type: iframe
   url: /local/plano3d.html?v=1
   aspect_ratio: 60%
   ```

   Sube el número de `?v=` cada vez que actualices el archivo para evitar la caché.

Parámetros opcionales de la URL: `view=top` (abre en planta), `walls=low` (paredes bajas), `bg=transparent` (fondo transparente).

Si el iframe no puede acceder a la sesión de HA, añade `&token=TOKEN_DE_LARGA_DURACION` para conectar por WebSocket (ten en cuenta que el token queda visible en la configuración del dashboard).

### Configuración

Al principio del archivo, en el bloque `CONFIGURACIÓN`:

- `ROOMS` → nombre de cada habitación y su entidad de luz (`light.*`).
- `DEVICES` → TV LG, Sonos, Chromecast, termo Ariston, cargador V2C, altavoces IKEA: entidad, icono y posición.
- `WALLS` / `FURNITURE` → tabiques, puertas, ventanas y muebles (en metros).

Las entidades que no existen en HA aparecen con borde rojo.

### Pendiente

- Sustituir los nombres de entidad genéricos por los reales.
- Versión realista: texturas a partir de fotos e iluminación horneada con Blender (exportar a `.glb`).
