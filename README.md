# CRM Cobranza · Búsqueda y Gestión

CRM de GitHub Pages para **Cobranza Total de Puebla**, con 79,706 clientes y dos apartados.

## Acceso
- Repositorio: https://github.com/ciserondavidg-ui/crm_quitas
- Sitio GitHub Pages: https://ciserondavidg-ui.github.io/crm_quitas/

## Archivos CSV
Por el tamaño del archivo original (~12 MB), los clientes se subieron al propio repositorio en 16 archivos:
`cartera/parte_01.csv` hasta `cartera/parte_16.csv`.

El `index.html` los descarga automáticamente y los combina en memoria; **no hay que cargar manualmente el CSV en cada equipo**. Si más adelante se añade `clientes.csv` a la raíz del repositorio, el CRM usa ese archivo con prioridad.

## Funciones
- **Búsqueda:** nombre, cliente único, división, zona y estatus.
- **Ficha:** deudas, quitas, capital, saldo a pagar y datos de la cartera.
- **Gestión:** estatus, gestor, contacto, promesa, fecha de seguimiento, notas e historial.
- **Exportación:** gestiones a un CSV.

## Dónde se guardan las gestiones
Las gestiones **solo se almacenan en cada navegador** mediante IndexedDB y se pueden exportar. **No se sincronizan entre agentes.** GitHub Pages no es una base de datos. Para compartir actividades, promesas y estados en tiempo real entre usuarios, necesitarás un servicio de datos adicional.

## Publicación
En GitHub ve a **Settings > Pages** y activa el despliegue desde `main`, carpeta raíz `/(root)`. La publicación del CSV deja la cartera **públicamente descargable**, incluidos nombres y saldos.
