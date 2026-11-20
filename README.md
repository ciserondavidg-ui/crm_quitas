# CRM de cobranza para GitHub Pages

CRM de un solo archivo (`index.html`) para consultar una cartera CSV y registrar gestiones en el navegador.

## Publicar en GitHub

1. Crea un repositorio nuevo. Si lo publicarás mediante GitHub Pages, considera que el sitio será público, incluso si los datos se mantienen locales.
2. Sube **solo `index.html`** al repositorio, en la rama `main` y en la carpeta raíz.
3. En **Settings > Pages > Build and deployment**, elige **Deploy from a branch**, rama `main` y carpeta `/(root)`. Guarda.
4. Abre la dirección que GitHub Pages te indique (normalmente `https://TU_USUARIO.github.io/TU_REPOSITORIO/`).
5. En el CRM pulsa **Cargar cartera** y selecciona tu archivo CSV en tu propia computadora.

## Funciones incluidas

- Importación de CSV (comillas y saltos de línea compatibles).
- Búsqueda por `CLIENTE_UNICO` y `NOMBRE`.
- Filtros por división, zona, estado de gestión; orden y paginación.
- Indicadores de deuda, saldo por pagar y quita promedio.
- Ficha por cliente y los 15 campos de origen.
- Estado, gestor, teléfono adicional, observaciones, fecha de seguimiento e historial de gestiones.
- Agenda de seguimientos pendientes, vencidos y futuros.
- Exportación de clientes filtrados a CSV y gestiones a CSV.
- Respaldo completo y restauración con JSON.
- Persistencia local mediante IndexedDB, sin servidor externo ni bibliotecas remotas.

## Seguridad y límites

**Nunca subas el archivo de clientes CSV, las gestiones exportadas ni los respaldos JSON a un repositorio público.** GitHub Pages no es una base de datos privada ni un CRM multiusuario con autenticación. El archivo `index.html` contiene solamente la aplicación, no las cuentas.

El navegador almacena localmente la cartera y las anotaciones. Si se borra el almacenamiento del sitio, se pierden sus datos, salvo que exista respaldo. Los registros **no se comparten entre computadoras ni usuarios**. Para una operación multiusuario con autenticación, auditoría y sincronización debe implementarse un backend protegido y políticas de acceso.

El CSV debe incluir las columnas `CLIENTE_UNICO`, `NOMBRE`, `DEUDA_TOTAL` y `SALDO_A_PAGAR`. El archivo original incluye 15 columnas, que se mantienen en la ficha. Si vuelves a importar una cartera, se conservan las gestiones locales asociadas al mismo `CLIENTE_UNICO`.
