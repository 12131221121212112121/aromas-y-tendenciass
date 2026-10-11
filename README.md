# Aromas y Tendencias

Catálogo web en español: Centro, San Miguel y Kennedy 1; 178 esencias iniciales, productos complementarios, carritos independientes por sucursal y solicitud de cotización por WhatsApp. Precios y disponibilidad se confirman con la tienda. No integra facturación ni valida transferencias bancarias.

## Desarrollo
Node.js 22.13 o superior. Ejecutar `npm ci`, `npm run dev`. Verificación: `node --test tests/catalog.test.mjs`, `npx tsc --noEmit`, `npm run build`.

La aplicación utiliza React/Vinext y Cloudflare D1 a través de Sites. Para desplegar en otro proveedor se debe adaptar el servidor y la base de datos; no basta con subir archivos HTML a GitHub Pages.

## Encargadas
`/admin` utiliza el inicio de sesión de ChatGPT proporcionado por Sites. La autenticación no concede por sí sola permiso de editar. Cada encargada debe iniciar sesión y comunicar su identificador de usuario (visible en el panel) al administrador. Configurar la variable de entorno del servidor `CATALOG_EDITORS` como un objeto JSON que relacione identificadores con sucursales autorizadas. Ejemplo de estructura, con identificadores ficticios: `{"ID_ENCARGADA_CENTRO":["centro"],"ID_ADMINISTRADORA":["centro","san-miguel","kennedy"]}`. Aplicar la configuración mediante un nuevo despliegue. No incluir esta configuración en el JavaScript del navegador. No hay contraseñas compartidas ni cuentas autorizadas por defecto.

Las encargadas pegan el listado completo, revisan la vista previa y publican el reemplazo. Se conserva el historial en D1 y se detectan cambios simultáneos para evitar sobreescribir otra actualización. Los apartados complementarios se mantienen en `lib/catalog.ts`; el editor de pegado actual reemplaza las esencias. La tienda puede regresar al listado inicial o cargar una versión anterior y publicarla.

## Datos y contenido
Sucursales, cuentas bancarias, esencias y productos: `lib/catalog.ts`. Imágenes: `public/assets/`. No se incluyen números de identidad. Los nombres ambiguos del listado se conservaron para revisión del negocio. Las imágenes de fragancias originales son referencias, no una afirmación de vender perfumes originales. Las fotos de recipientes con contenido sin identificación confirmada no se asignan a productos de limpieza específicos. Los videos recibidos no se incorporaron en esta primera versión.

## Persistencia
Carritos: almacenamiento local del navegador. Listados: tabla D1 `catalog_versions`, migración en `drizzle/`. La versión inicial se usa cuando una sucursal aún no tiene actualizaciones. Si falla la consulta, el catálogo muestra un aviso de listado de referencia. El envío a WhatsApp abre un mensaje que el cliente debe enviar; no se transmite automáticamente.

## Pendientes de negocio
Asignar las cuentas reales de las encargadas; revisar nombres ambiguos, presentaciones no confirmadas y fotografías; confirmar los precios si se desean mostrar. Kennedy 2 no forma parte de esta versión. El sitio se entrega privado para revisión y necesita una decisión posterior de acceso público para recibir clientes.
