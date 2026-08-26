> 🇬🇧 [Read in English](README.md)

# Simona

**Sistema de gestión de escritorio para cafeterías y comercios gastronómicos chicos** — punto de venta, stock, producción, caja y turnos de personal en una sola app de Windows que funciona sin depender de internet.

Desarrollado de punta a punta (decisiones de producto, UI, lógica de backend, despliegue) y entregado a un cliente real que lo usa a diario en producción.

> 🛠️ **Esto no es una plantilla genérica.** Simona se diseñó 100% a medida de una cafetería específica — su flujo de trabajo, sus productos, su forma de hacer el cierre de caja. Hago este mismo tipo de software a medida para otros negocios: si tenés un flujo de trabajo específico que las herramientas genéricas no te resuelven, [escribime](#contacto) y armo algo pensado para lo que necesitás vos, no al revés.

> 📌 **Este es un repositorio vidriera/portafolio.** El código fuente completo es propietario y no está publicado acá — ver [Por qué el código no es público](#por-qué-el-código-no-es-público) más abajo. Abajo hay capturas de pantalla, el detalle de funcionalidades y el stack técnico. Si querés ver el código en una entrevista técnica o evaluación, lo muestro en vivo o doy acceso privado.

---

## Capturas de pantalla

| | |
|---|---|
| ![Dashboard](screenshots/01-dashboard.jpg) | ![Punto de venta](screenshots/02-pos.jpg) |
| ![Mesas](screenshots/03-mesas.jpg) | ![Stock](screenshots/04-stock.jpg) |

*Dashboard, punto de venta, gestión de mesas y stock. Se muestran con datos de ejemplo/vacíos — sin información real del cliente.*

---

## Qué hace

Simona maneja la operación diaria de una cafetería: toma pedidos, controla qué hay en stock, calcula el costo real de cada producto según su receta, cierra la caja, y le dice al dueño qué necesita atención *hoy* — sin necesitar conexión a internet ni pagar una suscripción.

**Punto de venta**
- Carga rápida de pedidos para mostrador, mesas y delivery
- Gestión de pedidos por mesa (Mesas)
- Múltiples formas de pago, incluida integración real con Mercado Pago (generación de QR + polling automático de aprobación del pago, y detección de transferencias entrantes)

**Cocina y producción**
- Vista de kitchen display para que cocina vea los pedidos entrantes en tiempo real, separada de la caja
- Producción basada en recetas: los productos terminados se costean según sus ingredientes, así el margen se actualiza solo cuando cambia el costo de los insumos

**Stock**
- Control de stock completo sobre un catálogo real de ~80 productos en 4 categorías
- Alertas automáticas de reposición ("qué deberías hacer hoy" muestra exactamente lo que está bajo)

**Caja y finanzas**
- Apertura/cierre de caja diaria y arqueo formal de caja
- Seguimiento de pagos pendientes (Pagos) con proyección de liquidez según fecha de vencimiento
- Ganancia bruta estimada por período, calculada sobre ventas reales menos el costo actual de los insumos — no un margen fijo
- Objetivos de facturación mensual con seguimiento de avance
- Cuentas por cobrar de clientes con saldo corriente

**Personal y turnos**
- Login de turno por PIN, para separar la sesión y las acciones de cada empleado sin el peso de un sistema de usuarios completo

**Reportes y datos propios**
- Reportes mensuales en PDF
- Todos los datos viven en un archivo JSON local que el dueño controla directamente — backup y restauración con un clic, sin depender de la nube ni de un proveedor externo

---

## Por qué se construyó así

El cliente necesitaba algo que funcione de forma confiable en una sola PC con Windows en el mostrador, que no dependa de que haya internet, y que no venga con una suscripción mensual para un negocio chico de una sola sucursal. Eso descartó el enfoque típico de SaaS en la nube y definió la mayoría de las decisiones técnicas de abajo.

## Stack técnico

- **Electron** — empaquetado como app nativa de Windows (instalador NSIS), no una pestaña de navegador
- UI en **JavaScript vanilla**, sin overhead de framework — mantiene la app rápida y la superficie de dependencias chica
- Proceso principal en **Node.js** manejando lectura/escritura de archivos, impresión silenciosa e IPC con el renderer aislado (`contextIsolation` activado, `nodeIntegration` desactivado)
- **electron-store** para persistencia local (último archivo abierto, configuración, credenciales de Mercado Pago)
- **electron-builder** para el instalador de Windows y el empaquetado
- Integración con la **API de Mercado Pago** para pagos con QR y detección de transferencias
- **JSON** local como capa de datos, con backup/restauración integrados en la UI — el cliente es dueño de sus datos como archivo, no como una fila en la base de datos de otro

## Por qué el código no es público

Simona se construyó y se entregó como software comercial para un cliente real y pago, dentro de una relación de negocio en curso (Celfar) — no como proyecto open-source. Publicar el código completo regalaría un producto funcional gratis, y no es algo que pueda hacer sin el acuerdo del cliente y del negocio.

Este repositorio existe para que el trabajo se pueda verificar: capturas reales, una lista honesta de funcionalidades, y un relato directo de las decisiones técnicas detrás. Si querés ver el código en sí — para una postulación laboral, una entrevista técnica o una evaluación de contratación — escribime y lo muestro en vivo o doy acceso privado.

## Contacto

**Juan Farias** — juanfarias8213@gmail.com

---

© 2026 Celfar. Todos los derechos reservados. Ver [LICENSE](LICENSE).
