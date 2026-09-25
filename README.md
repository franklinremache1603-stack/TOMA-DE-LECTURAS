# Toma de Lecturas EEQ

Aplicación web progresiva (PWA) para registrar lecturas de medidores desde celular o computador.

## Funciones

- Carga de rutas desde XLSX, XLS o CSV.
- Búsqueda por medidor, cuenta, cliente, dirección o secuencia.
- Lectura actual y cálculo de consumo.
- Novedades y observaciones.
- Validación de lectura menor o igual a la anterior.
- Fecha/hora automática.
- Captura de GPS.
- Foto del medidor comprimida en el dispositivo.
- Guardado local con IndexedDB.
- Respaldo y recuperación JSON.
- Exportación XLSX y CSV.
- Filtros por pendientes, leídos y novedades.
- PWA instalable en Android.
- Funcionamiento offline después de la primera carga y cacheo de recursos.

## Archivos

- `index.html` interfaz
- `styles.css` diseño responsive
- `app.js` lógica de la aplicación
- `manifest.webmanifest` configuración PWA
- `sw.js` cache/offline
- `icons/` iconos
- `ejemplo_ruta.csv` ejemplo para pruebas

## Formato recomendado de la ruta

La aplicación intenta reconocer nombres equivalentes, pero las únicas columnas recomendadas son:

```text
MEDIDOR;CLIENTE
```

Ejemplo:

```text
12345678;CLIENTE UNO
87654321;CLIENTE DOS
11223344;CLIENTE TRES
```

Si el archivo contiene otras columnas adicionales, la aplicación también intentará reconocerlas automáticamente y utilizarlas cuando sea posible.

## Publicar en GitHub Pages

1. Cree un repositorio, por ejemplo `lecturas-eeq`.
2. Suba todos los archivos y carpetas de este proyecto.
3. Abra `Settings`.
4. Entre a `Pages`.
5. En `Build and deployment`, seleccione:
   - Source: `Deploy from a branch`
   - Branch: `main`
   - Folder: `/ (root)`
6. Guarde.
7. GitHub mostrará una dirección similar a:
   `https://TU-USUARIO.github.io/lecturas-eeq/`

## Instalar en Android

1. Abra la dirección publicada con Chrome.
2. Espere la primera carga completa.
3. Abra el menú de Chrome.
4. Seleccione `Agregar a pantalla de inicio` o `Instalar aplicación`.
5. Después de la primera carga, gran parte de la aplicación funcionará sin internet.

## Privacidad

Los registros, lecturas, GPS y fotografías se almacenan localmente en el navegador del dispositivo mediante IndexedDB.

No suba archivos de rutas con datos reales al repositorio público de GitHub.

El repositorio debe contener únicamente el código de la aplicación.


## Persistencia automática de la ruta

La última ruta cargada queda guardada localmente en el dispositivo mediante IndexedDB.

- Al cerrar la aplicación, navegador o pestaña, la ruta NO se pierde.
- Al volver a abrir la aplicación, la última ruta y sus lecturas se recuperan automáticamente.
- No es necesario volver a seleccionar el archivo.
- La ruta solo se reemplaza cuando el usuario selecciona manualmente un archivo nuevo.
- Antes de reemplazar una ruta existente, la aplicación solicita confirmación.
- Se recomienda crear un respaldo JSON antes de reemplazar una ruta de trabajo.

## Importante sobre Excel

La lectura/escritura XLSX utiliza SheetJS desde jsDelivr. La primera vez conviene abrir la aplicación con internet para que el navegador y el Service Worker puedan almacenar ese recurso. CSV funciona sin esa dependencia.

## Recomendación operativa

Antes de borrar datos del teléfono o cambiar de dispositivo, use `Crear respaldo JSON`.


## Identificación y fotografía

- La aplicación muestra la leyenda **“Realizada por Jesus Remache”** en la interfaz.
- Cada registro dispone de un apartado específico para tomar o cargar una fotografía del medidor.
- La imagen se guarda localmente junto con el registro y puede visualizarse o eliminarse antes de exportar.


## Interfaz simplificada del ítem 3

En el ítem **3. Medidor seleccionado** únicamente se muestran:

- MEDIDOR
- CLIENTE
- LECTURA ACTUAL
- NOVEDAD
- OBSERVACIÓN

La fotografía queda en un apartado independiente. La información adicional puede mantenerse internamente para compatibilidad y exportación, pero no se muestra en el ítem 3.


## GPS ligado automáticamente a la fotografía

En esta versión el GPS ya no requiere una acción separada.

Cuando el usuario toma o carga una fotografía:

1. La aplicación guarda la fotografía.
2. Solicita automáticamente la ubicación GPS del dispositivo.
3. Guarda latitud, longitud, precisión, fecha y hora junto con esa fotografía y el registro del medidor.
4. La ubicación se muestra dentro del apartado de fotografía.
5. Al eliminar la fotografía también se eliminan sus coordenadas GPS asociadas.

Si el usuario bloquea el permiso de ubicación, la fotografía se conserva, pero la aplicación informa que no pudo asociar el GPS.
