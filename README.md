# Online Store 🛒

Sistema web de comercio electrónico desarrollado con **Python (Flask)** y **MySQL**, diseñado para gestionar productos, categorías, carritos de compras, pedidos, clientes, administradores, vendedores y repartidores.

---

## 🛠️ Tecnologías Utilizadas

* **Lenguaje:** Python 3
* **Framework Web:** Flask, Flask-SQLAlchemy, Flask-WTF
* **Base de Datos:** MySQL / MariaDB (vía XAMPP)
* **Otras Librerías:** PyYAML, PyMySQL, mysqlclient, Flask-SocketIO

---

## 📋 Requisitos Previos

Asegúrate de tener instalados los siguientes componentes en tu sistema:

* [Python 3.x](https://www.python.org/)
* [XAMPP](https://www.apachefriends.org/) (con los servicios de Apache y MySQL)
* Visual Studio Code (u otro editor de texto)

---

## 🚀 Instalación y Configuración

### 1. Entorno Virtual de Python

Abre la terminal en la raíz de tu proyecto y ejecuta los siguientes comandos:

```powershell
# Crear el entorno virtual
python -m venv venv

# Activar el entorno virtual (PowerShell)
.\venv\Scripts\Activate.ps1

# Instalar todas las dependencias requeridas
pip install -r rec.txt
```

---

## 🗄️ Configuración de la Base de Datos (XAMPP)

1. Abre el **Panel de Control de XAMPP** e inicia los módulos **Apache** y **MySQL**.
2. Entra a phpMyAdmin desde tu navegador: `http://localhost/phpmyadmin`.
3. Crea una nueva base de datos llamada **`online_store`**.
4. Importa el archivo `Dump.sql`:
   * Selecciona la base de datos `online_store`.
   * Ve a la pestaña **Importar**.
   * Selecciona el archivo `Dump.sql` y presiona **Continuar**.

> ⚠️ **Nota de Compatibilidad (Error #1273 - Collation desconocida):**  
> Si usas MariaDB en XAMPP y recibes un error al importar, abre el archivo `Dump.sql` en tu editor, busca la cadena `utf8mb4_0900_ai_ci` y reemplázala completamente por `utf8mb4_unicode_ci`. Guarda el archivo y vuelve a intentar la importación.

---

## ⚙️ Configuración de Conexión (`database.yaml`)

Verifica que el archivo `database.yaml` contenga las credenciales correctas para conectarse a XAMPP (por defecto, XAMPP no requiere contraseña en el usuario `root`):

```yaml
mysql_host : '127.0.0.1'
mysql_user: 'root'
mysql_password : ''
mysql_db : 'online_store'
```

---

## 🏁 Ejecución de la Aplicación

Con el entorno virtual activado y los servicios de XAMPP corriendo, inicia el servidor web ejecutando:

```bash
python run.py
```

Accede a la aplicación ingresando desde tu navegador a `http://127.0.0.1:5000` o la dirección asignada en la consola.

---

## 🔑 Credenciales de Prueba (Cargadas desde el Dump)

### 👤 Cliente (`customer`)
* **Email:** `sahilgoyal@gmail.com`
* **Contraseña:** `sahil@2002`

### 🛡️ Administrador (`admin`)
* **ID / Usuario:** `1`
* **Contraseña:** `akgoel@283`

<img width="1600" height="880" alt="login_screen" src="https://github.com/user-attachments/assets/18fef4ad-922d-45eb-9551-5b54aa5cf340" />
### alumnos:
---
cruz angel velazquez guel,

andrea dalith zavala barbosa,

ximena zepeda ruiz,

roberto alexis cisneros vazquez 
