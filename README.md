# Home-Assistant-Realejos

Configuración de Home Assistant (automatizaciones y dashboards) mantenida con Claude.

## Estructura

```
packages/     Automatizaciones, scripts y ayudantes agrupados por zona/función
dashboards/   Dashboards en YAML (tablet.yaml, movil.yaml)
docs/         Utilidades (plantilla para sacar el inventario de entidades)
```

El repo se clona en `/config/realejos` dentro de Home Assistant, así no toca la configuración existente.

## Instalación en Home Assistant (una sola vez)

1. **Copia de seguridad**: Ajustes → Sistema → Copias de seguridad → Crear copia.
2. **Add-on Studio Code Server**: Ajustes → Complementos → Tienda → "Studio Code Server" → Instalar → Iniciar → Abrir.
3. En Studio Code Server abre un terminal (menú ☰ → Terminal → New Terminal) y ejecuta:
   ```bash
   cd /config
   git clone https://github.com/juancbr9/home-assistant-realejos.git realejos
   cd realejos && git checkout claude/home-assistant-integration-fr0ujh
   ```
   (Si el repo es privado, Git pedirá usuario y un *token* personal de GitHub como contraseña.)
4. Añade esto a `/config/configuration.yaml` (si ya existe la clave `homeassistant:` o `lovelace:`, añade solo lo de dentro):
   ```yaml
   homeassistant:
     packages: !include_dir_named realejos/packages

   lovelace:
     dashboards:
       casa-tablet:
         mode: yaml
         title: Tablet
         icon: mdi:tablet
         show_in_sidebar: true
         filename: realejos/dashboards/tablet.yaml
       casa-movil:
         mode: yaml
         title: Móvil
         icon: mdi:cellphone
         show_in_sidebar: true
         filename: realejos/dashboards/movil.yaml
   ```
5. Herramientas para desarrolladores → YAML → **Comprobar configuración** → si está OK, **Reiniciar**.

## Actualizar tras cada cambio de Claude

```bash
cd /config/realejos && git pull
```
Después: Herramientas para desarrolladores → YAML → recargar *Automatizaciones* (o reiniciar si hay paquetes nuevos). Los dashboards se refrescan recargando la página.

## Inventario de dispositivos

Pega el contenido de `docs/inventario_template.jinja` en Herramientas para desarrolladores → Plantilla y pásale el resultado a Claude.
