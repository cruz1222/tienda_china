# Mapeo de Pantallas, Flujos y Definición de Requerimientos — GroStop

**Proyecto:** GroStop (E-Commerce Grocery Store)  
**Autor:** Andrea Dalith Zavala Barbosa (Desarrollador Líder / Core)  
**Equipo:** Syntax Squad  

---

## 1. Mapeo de Pantallas y Flujos de Usuario

### A. Módulo del Cliente / Usuario Final
- **`/` (Inicio / Home):** Despliega el catálogo general de abarrotes, banners promocionales y la barra de navegación.
- **`/login` y `/register` (Autenticación):** Formularios para acceso de usuarios existentes y registro de nuevos clientes.
- **`/product/<id>` (Detalle de Producto):** Muestra precio, descripción, stock disponible y botón para agregar al carrito.
- **`/cart` (Carrito de Compras):** Muestra el resumen de artículos seleccionados, permite modificar cantidades y calcular el total.
- **`/checkout` (Procesamiento de Pago/Pedido):** Recopila la dirección de entrega y confirma la orden de compra.
- **`/orders` (Historial de Pedidos):** Consulta del estado y detalle de compras previas del cliente.

### B. Módulo del Administrador
- **`/admin/login` (Acceso Administrativo):** Autenticación de usuarios con rol de administrador.
- **`/admin/dashboard` (Panel de Control):** Vista general de métricas clave (ventas totales, pedidos pendientes, alertas de stock).
- **`/admin/products` (Gestión de Inventario):** Alta, baja, modificación y actualización de stock de productos.
- **`/admin/orders` (Gestión de Pedidos):** Actualización del estado de los pedidos de los clientes (Pendiente, Enviado, Entregado).

---

## 2. Definición de Requerimientos Funcionales (RF)

* **RF01 - Autenticación de Usuarios:** El sistema debe permitir el registro e inicio de sesión seguro para clientes y administradores.
* **RF02 - Visualización del Catálogo:** El sistema debe listar los productos disponibles recuperando imagen, nombre, precio y stock desde MySQL.
* **RF03 - Gestión del Carrito:** El cliente debe poder agregar, modificar la cantidad o eliminar productos de su sesión de carrito.
* **RF04 - Creación de Pedidos:** El sistema debe registrar la transacción en la base de datos al completar el proceso de checkout.
* **RF05 - Administración de Inventario:** El administrador debe poder crear, editar y eliminar registros en la tabla de productos (CRUD).
* **RF06 - Control de Pedidos:** El administrador debe poder cambiar el estado de procesamiento de cada compra.

---

## 3. Definición de Requerimientos No Funcionales (RNF)

* **RNF01 - Arquitectura:** Desarrollo basado en el patrón MVC/Rutas modulares sobre el framework Flask (Python 3.x).
* **RNF02 - Persistencia:** Base de datos relacional MySQL para garantizar la integridad referencial de usuarios, productos y pedidos.
* **RNF03 - Interfaz de Usuario:** Diseño adaptativo (Responsive Web Design) implementado con Bootstrap y CSS3.
* **RNF04 - Seguridad Básica:** Consultas SQL parametrizadas para evitar inyecciones SQL y manejo seguro de sesiones HTTP.
