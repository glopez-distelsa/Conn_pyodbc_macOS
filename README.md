# Conn_pyodbc_macOS👨‍💻🚀☕️ 

## Fuente: 🗃️

[GitHub - Connecting to SQL Server from Mac OSX](https://pages.github.com/)
```
https://github.com/mkleehammer/pyodbc/wiki/Connecting-to-SQL-Server-from-Mac-OSX
```
[Install the Microsoft ODBC driver for SQL Server (macOS)](https://learn.microsoft.com/en-us/sql/connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos?view=sql-server-ver16#17)
```
https://learn.microsoft.com/en-us/sql/connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos?view=sql-server-ver16#17
```
  
> [!IMPORTANT]
> Antes de comenzar, es fundamental tener un entorno de Python configurado adecuadamente. En el repositorio [conda_environments_install](https://github.com/glopez-distelsa/conda_environments_install), proporciono una guía detallada sobre cómo configurar entornos conda según el proyecto en el que estés trabajando, asegurando que todas las dependencias necesarias se encuentren dentro del mismo. Si aún no estás familiarizado con el uso de entornos, te recomiendo revisarlo.


## Pasos a seguir para instalacion 
  
- [ ] Instalar `Homebrew`
    ```
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
    ```
    
- [ ] Instalar Controladores ODBC
* MICROSOFT
  
  1 - Agregar `repositorio de Microsoft`:
  
  ```
  brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
  ```
      
  2 - Actualizar `Homebrew`:
  
  ```
  brew update
  ```
      
  3 - Instalar `msodbcsql18` y `mssql-tools18`:

   ```
  HOMEBREW_ACCEPT_EULA=Y brew install msodbcsql18 mssql-tools18
  ```

> [!NOTE]
> `msodbcsql18:` Es el controlador ODBC específico para SQL Server, proporcionando conectividad ODBC a bases de datos SQL Server.
> `mssql-tools18:` Incluye herramientas como sqlcmd y bcp para interactuar con SQL Server desde la línea de comandos.
> Compatibilidad otros sitemas
> - MySQL `brew install mysql-connector-odbc`
> - PostgreSQL `brew install psqlodbc`
> - SQLite `brew install qliteodbc`
        
- [ ] Configuracion del entorno
      
    - Agrega la ruta de las bibliotecas de `Homebrew` a `DYLD_LIBRARY_PATH` en macOS
      
  ```
  export DYLD_LIBRARY_PATH=/opt/homebrew/lib:$DYLD_LIBRARY_PATH
  ```

## Codigo prueba en python para conexión

> [!WARNING]
> Es necesario hablar con los DBAs para que puedan crearte un usuario fuera de red para poderte conectar con python desde macOS

- [ ] Creacion de archivo `odbc.ini`
      
    - Este archivo nos ayuda a crear las credenciales en el y no quemarlas dentro del codigo python, lo mas recomendable seria poder utilizar una boveda compartida o cloud para gestionarlas desde ahi, pero de momento podriamos hacerlo de la siguiente forma: `crear el archivo /usr/local/etc/odbc.ini`
      
  ```
  [SQLSERVER113]
  Description = My SQL Server
  Driver = ODBC Driver 18 for SQL Server
  Server = <TU_SERVIDOR> #.113
  Database = <TU_BASE_DE_DATOS>
  UID = <TU_USUARIO>
  PWD = <TU_CONTRASEÑA>
  TrustServerCertificate = yes
  ```

    - Codigo python

```python
import pyodbc
import configparser

config = configparser.ConfigParser()
config.read('/usr/local/etc/odbc.ini')
db_config = config['SQLSERVER113']

conn_str = (
    f'DRIVER={db_config["Driver"]};'
    f'SERVER={db_config["Server"]};'
    f'DATABASE={db_config["Database"]};'
    f'UID={db_config["UID"]};'
    f'PWD={db_config["PWD"]};'
    f'TrustServerCertificate={db_config["TrustServerCertificate"]};'
)

try:
    connection = pyodbc.connect(conn_str)
    print("Connected to the database!")
    connection.close()
except Exception as e:
    print(f"Failed to connect to the database: {e}")
```
