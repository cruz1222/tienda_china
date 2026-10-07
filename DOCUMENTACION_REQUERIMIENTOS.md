# Mapeo de Pantallas, Flujos y Definición de Requerimientos — GroStop

**Proyecto:** GroStop (E-Commerce Grocery Store)  
**Autor:** Andrea Dalith Zavala Barbosa   

---

## Mapeo de Pantallas y Flujos de Usuario

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

## 1. Planteamiento del Proceso de Ingeniería de Software

El desarrollo del sistema abarca las **5 actividades clave del ciclo de vida de requisitos**:

1. **Elicitación (Levantamiento):** Descubrimiento y levantamiento de necesidades mediante la inspección del código fuente Flask (`run.py`, `market/`), el análisis del esquema SQL (`Dump.sql`) y la definición de flujos de usuario/administrador.
2. **Análisis:** Clasificación de necesidades en **Requisitos Funcionales** y **No Funcionales**, negociando prioridades mediante la metodología **MoSCoW** (Must, Should, Could, Won't).
3. **Especificación:** Documentación formal mediante enunciados verificables (*"El sistema debe..."*) bajo los estándares **IEEE 830 / IEEE 29148**.
4. **Validación:** Comprobación de consistencia, completitud y trazabilidad de cada requisito mediante escenarios de prueba de aceptación.
5. **Gestión de Cambios:** Control de versiones e integración continua soportados en Git y GitHub.

---

## 2. Requisitos Funcionales (RF)

Los requisitos funcionales definen los comportamientos específicos y servicios que el sistema debe ejecutar.

### Módulo 1: Autenticación y Gestión de Usuarios
* **RF-01 (Must):** El sistema debe permitir el registro de nuevos usuarios solicitando nombre de usuario, correo electrónico y contraseña.
* **RF-02 (Must):** El sistema debe validar las credenciales de acceso ingresadas contra los registros guardados en la base de datos `online_store`.
* **RF-03 (Must):** El sistema debe mantener la sesión activa del usuario autenticado a lo largo de la navegación mediante variables de sesión de Flask.
* **RF-04 (Should):** El sistema debe permitir al usuario cerrar sesión en cualquier momento, destruyendo la sesión actual.

### Módulo 2: Catálogo de Productos
* **RF-05 (Must):** El sistema debe consultar y desplegar en la interfaz web el listado completo de productos desde la base de datos MySQL.
* **RF-06 (Should):** El sistema debe mostrar una vista detallada para cada producto con su nombre, imagen, descripción, precio y disponibilidad.

### Módulo 3: Carrito de Compras y Pedidos
* **RF-07 (Must):** El sistema debe permitir a los usuarios autenticados agregar productos a un carrito de compras.
* **RF-08 (Must):** El sistema debe calcular de forma automática el total a pagar según los precios y cantidades seleccionadas en el carrito.
* **RF-09 (Should):** El sistema debe procesar la compra registrando la orden y descontando las unidades del stock en la base de datos `online_store`.

---

## 3. Requisitos No Funcionales (RNF)

Atributos de calidad, rendimiento, entorno operativo y seguridad que el sistema debe cumplir.

* **RNF-01 (Rendimiento / Verificable):** El sistema debe cargar la página principal del catálogo en menos de 2.0 segundos bajo entorno local.
* **RNF-02 (Seguridad):** Las contraseñas de los usuarios deben encriptarse mediante un algoritmo de hashing seguro antes de almacenarse en la base de datos.
* **RNF-03 (Entorno y Compatibilidad):** El backend debe ejecutarse sobre Python 3.x con el microframework Flask, usando MySQL/MariaDB (XAMPP) como gestor de base de datos a través del conector `flask_mysqldb`.
* **RNF-04 (Usabilidad):** La interfaz debe ser clara, funcional y compatible con navegadores web estándar (Chrome, Edge, Firefox).

---

## 4. Clasificación y Priorización (Método MoSCoW)

| Criterio | Requisitos Asignados |
| :--- | :--- |
| **Must have** *(Indispensables)* | RF-01, RF-02, RF-03, RF-05, RF-07, RF-08, RNF-02, RNF-03 |
| **Should have** *(Importantes)* | RF-04, RF-06, RF-09, RNF-01, RNF-04 |
| **Could have** *(Futuras iteraciones)* | Pasarela de pagos externa (Stripe/PayPal), sistema de comentarios y valoraciones por producto. |
| **Won't have** *(Fuera del alcance actual)* | Aplicación móvil nativa (Android/iOS), facturación electrónica automática. |

## 5. Diagrama de Flujo del Proceso

```mermaid
graph TD
    A([Inicio: Usuario entra a la tienda]) --> B[RF-05: Consultar Catálogo de Productos]
    B --> C[(Base de Datos MySQL: online_store)]
    C --> D[Cargar Productos en la Interfaz]
    
    D --> E{¿El usuario quiere comprar?}
    
    E -- No --> F[Explorar productos / Ver detalles RF-06]
    F --> D
    
    E -- Sí --> G{¿Sesión iniciada? RF-03}
    
    G -- No --> H[Formulario de Inicio de Sesión / Registro]
    H --> I[RF-01 / RF-02: Validar credenciales y hash RNF-02]
    I --> C
    C -- Credenciales Válidas --> J[Crear Sesión de Usuario]
    J --> K[RF-07: Agregar Producto al Carrito]
    
    G -- Sí --> K
    
    K --> L[RF-08: Calcular Total y Subtotales]
    L --> M{¿Confirmar Compra?}
    
    M -- Cancelar --> D
    M -- Confirmar --> N[RF-09: Procesar Orden y Descontar Stock]
    N --> C
    C -- Stock Actualizado --> O([Fin: Compra Exitosa y Pedido Confirmado])
    User --> UC7

    Admin --> UC2

## Diagrama de Casos de Uso

```mermaid
graph LR
    subgraph Actores
        Cliente((Cliente / Usuario))
        Admin((Administrador / Vendedor))
    end

    subgraph Sistema Tienda China
        UC1[CU01: Registrar Cuenta]
        UC2[CU02: Iniciar Sesión]
        UC3[CU03: Consultar Catálogo]
        UC4[CU04: Ver Detalle de Producto]
        UC5[CU05: Comprar / Agregar Producto]
        UC6[CU06: Cerrar Sesión]
        UC7[CU07: Registrar / Modificar Producto]
        UC8[CU08: Consultar Inventario General]
    end

    Cliente --> UC1
    Cliente --> UC2
    Cliente --> UC3
    Cliente --> UC4
    Cliente --> UC5
    Cliente --> UC6

    Admin --> UC2
    Admin --> UC7
    Admin --> UC8
    Admin --> UC6
    Admin --> UC8
    Admin --> UC7
