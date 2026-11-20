# CRM Cobranza: GitHub Pages + Google Sheets

**Interfaz:** sólo búsqueda de clientes y ficha para registrar gestiones.
**Base única:** Google Sheets. Toda persona que abre el sitio ve la misma cartera y el mismo historial de gestiones. **No usa IndexedDB ni CSV en GitHub.**

## Instalación paso a paso

1. Abre Google Sheets, crea un documento nuevo y llámalo `CRM COBRANZA PUEBLA`.
2. Importa el CSV `COBRANZA TOTAL DE PUEBLA.csv` desde **Archivo > Importar > Subir**, preferiblemente en una pestaña nueva. Renombra la pestaña con los clientes como **`CARTERA`**. La primera fila debe tener `CLIENTE_UNICO`, `NOMBRE`, `SEMANA_DE_ATRASO`, etc. No cambies los nombres de columnas.
3. En el menú **Extensiones > Apps Script**, pega el contenido de **`Code.gs`**.
4. En `Code.gs`, sustituye `PEGA_AQUI_ID_DE_TU_GOOGLE_SHEETS` por el ID que aparece entre `/d/` y `/edit` en la URL de tu Google Sheets.
5. Guarda. En Apps Script ve a **Implementar > Nueva implementación > Aplicación web**; ejecuta como **yo** (propietario) y da acceso a **Cualquier persona**. Autoriza los permisos. Copia la URL terminada en **`/exec`**. No uses la URL `/dev`.
6. Abre **`index.html`** en cualquier editor y sustituye `PEGA_AQUI_LA_URL_DE_APPS_SCRIPT_EXEC` por esa URL `/exec`. No incluyas los CSV en GitHub.
7. Reemplaza el `index.html` de tu repositorio de GitHub Pages por el de este paquete. Asegúrate de tener Pages habilitado en **Settings > Pages > Deploy from a branch > main > /(root)**.
8. Abre la página y busca un cliente único. Al registrar una gestión se crea la pestaña **`GESTIONES`**. Desde entonces los cambios quedan visibles para cualquiera que abra el CRM.

## Columnas de GESTIONES

`FECHA_REGISTRO`, `CLIENTE_UNICO`, `GESTOR`, `TIPIFICACION`, `OBSERVACIONES`, `PROXIMA_GESTION`, `MONTO_PROMESA`, `ID_GESTION`.

## Cómo funciona

- El HTML busca desde Google Sheets mediante un Web App de Apps Script.
- No descarga los ~80 mil registros al navegador. Busca por **cliente único** o **nombre** dentro de la hoja `CARTERA` y muestra 25 coincidencias como máximo.
- Consulta los datos del cliente y las últimas 40 gestiones registradas.
- Las gestiones se escriben en `GESTIONES`, con un bloqueo que evita interferencia entre registros simultáneos.
- Para verificar el guardado, el navegador vuelve a consultar el historial y busca el ID de la nueva gestión; no muestra éxito sólo por haber enviado la solicitud.

## Consideraciones

- Un repositorio público de GitHub no guardará el CSV. No hace falta cargar el archivo CSV nuevamente desde cada navegador.
- Si publicas Apps Script como **Cualquier persona** y ejecutas como propietario, cualquiera que conozca la dirección de tu CRM/API podrá buscar los datos y registrar gestiones con tus permisos. El mecanismo evita una clave expuesta en HTML, pero **no ofrece control de usuarios ni protección de datos**. Úsalo sólo cuando tengas autorización para compartir esos datos.
- La primera búsqueda puede tardar unos segundos con carteras grandes. Google Sheets tiene límites de tamaño, cuota y tiempo; esta solución está pensada para un CRM simple, no para miles de consultas concurrentes.
- Al modificar `Code.gs`, publica una nueva versión del despliegue de Apps Script. Modificar el HTML requiere republicar el index de GitHub Pages.
- Si no ves la nueva gestión, comprueba la pestaña GESTIONES antes de reintentar. Una conexión lenta puede retrasar la confirmación.

## Archivos a subir

- **GitHub:** `index.html` únicamente.
- **Apps Script:** contenido de `Code.gs`.
- **Google Sheets:** datos CSV importados en `CARTERA`; `GESTIONES` se crea automáticamente.
