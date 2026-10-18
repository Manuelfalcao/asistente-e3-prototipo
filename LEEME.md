# PROTOTIPO descartable: formato de distribución

Prototipo para [Prototipo instalable para elegir el formato](../../issues/07-prototipo-formato.md). **No es el Asistente**: es una Calculadora de reactancia, un Inventario y un panel de Diagnóstico, todo en un solo `index.html` autocontenido.

El mismo `index.html` sirve para las dos pruebas:

- **PWA:** la carpeta completa publicada en GitHub Pages (HTTPS).
- **HTML suelto:** el archivo `index.html` solo, mandado como documento por WhatsApp.

## Qué ya se probó (Chrome en PC, `localhost`)

- La reactancia calcula bien: 145 MHz y 100 nH dan XL = 91,11 Ω.
- El Inventario sobrevive a la recarga (localStorage e IndexedDB).
- Con el servidor apagado, la página abre igual desde la caché del service worker.
- Al pasar de v1 a v2 aparece el aviso amarillo "Hay una versión nueva". Al tocar Recargar se ve v2, se borra la caché vieja y el Inventario sigue.
- Exportar e importar por código funcionan.
- `persist()` fue **denegada** en una pestaña común de Chrome. Es lo esperable: Chrome la concede a sitios instalados o con mucho uso. Hay que verlo instalado.

## Publicar en GitHub Pages

1. Crear un repositorio **público** (por ejemplo `asistente-e3-prototipo`) y subir el contenido de esta carpeta a la raíz de `main`.
2. Settings › Pages › Source: "Deploy from a branch", `main`, `/ (root)`.
3. El link queda `https://<usuario>.github.io/asistente-e3-prototipo/`.

## Pruebas en dispositivos

Después de cada prueba, tocar **Compartir diagnóstico** y mandárselo a uno mismo por WhatsApp. Ese texto es el resultado.

### A. PWA en Android (Chrome)

1. Mandar el link por WhatsApp y tocarlo. Anotar si abre en la vista web de WhatsApp o en Chrome.
2. Instalar: aviso automático, o menú ⋮ › "Instalar app" / "Agregar a pantalla principal".
3. Abrir desde el ícono. Agregar 2 o 3 valores al Inventario. Tocar "Pedir persistencia".
4. **Modo avión**, cerrar la app desde Recientes, reabrir. ¿Abre? ¿Está el Inventario? → Compartir diagnóstico.

### B. PWA en iPhone (Safari, iOS 26)

1. Mandar el link por WhatsApp y tocarlo. Si abre dentro de WhatsApp, pasarlo a Safari.
2. Antes de instalar, agregar un valor al Inventario **en Safari** (para ver que no pasa a la app).
3. Compartir › "Agregar a inicio". Abrir desde el ícono.
4. ¿El Inventario está vacío? (esperado: sí, almacenamiento separado). Agregar valores e **importar** el código exportado desde Safari.
5. Pedir persistencia. **Modo avión**, cerrar la app, reabrir → Compartir diagnóstico.
6. **Dentro de 7 a 10 días**, abrir otra vez y anotar si el Inventario sigue (mirar "Primer valor guardado" y "aperturas").

### C. Aviso de versión nueva (Android y iPhone)

1. Con la app ya instalada en los dos, cambiar `VERSION` a `'v2'` en `index.html` **y** en `sw.js` y subirlo.
2. Esperar un par de minutos a que Pages despliegue. Abrir la app con conexión.
3. ¿Aparece el aviso amarillo? ¿Al tocar Recargar dice v2 y conserva el Inventario? Si no aparece, cerrar y reabrir una vez y anotar cuántas aperturas hicieron falta.

### D. HTML suelto por WhatsApp

Mandar `index.html` como **documento** a los dos teléfonos y a WhatsApp Desktop o Web en la PC. En cada uno anotar:

- Qué app lo abre (o qué ofrece el teléfono).
- ¿Calcula la reactancia? (si sí, corre el JavaScript).
- Fila **localStorage** del Diagnóstico: `ok` o `FALLA · …`.
- Agregar un valor, cerrar, volver a abrir el archivo **desde el chat**: ¿sigue el valor?

## Resultados

| Prueba | Android | iPhone | PC |
|---|---|---|---|
| Abre el link desde WhatsApp en… | | | — |
| Instalación (pasos reales) | | | |
| Sin conexión tras cerrar | | | |
| Inventario tras cerrar | | | |
| `persist()` / `persisted()` instalada | | | |
| Inventario Safari → app (vacío / importado ok) | — | | — |
| Inventario a los 7–10 días | | | |
| Aviso de versión nueva | | | |
| HTML suelto: qué app lo abre | | | |
| HTML suelto: corre JS | | | |
| HTML suelto: localStorage | | | |
| HTML suelto: Inventario al reabrir | | | |
