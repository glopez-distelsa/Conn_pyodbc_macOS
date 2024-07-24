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
        
- [ ] Configuracion del entorno:
      
    - Agrega la ruta de las bibliotecas de `Homebrew` a `DYLD_LIBRARY_PATH` en macOS:
      
  ```
  export DYLD_LIBRARY_PATH=/opt/homebrew/lib:$DYLD_LIBRARY_PATH
  ```

> [!IMPORTANT]
> Tener instalado pyodbc en nuestro ambiente de python: 
> `pip install pyodbc`

- [ ] Codigo prueba en python para conexión:

> [!WARNING]
> Es necesario hablar con los DBAs para que puedan crearte un usuario especial para poderte conectar con python desde macOS

```python
import pyodbc

conn_str = (
    'DRIVER={ODBC Driver 18 for SQL Server};'
    'SERVER=<TU_SERVIDOR>;'
    'DATABASE=<TU_BASE_DE_DATOS>;'
    'UID=<TU_USUARIO>;'
    'PWD=<TU_CONTRASEÑA>;'
    'Authentication=ActiveDirectoryIntegrated;'
)

try:
    connection = pyodbc.connect(conn_str)
    print("Conectado a la base de datos!")
    connection.close()
except Exception as e:
    print(f"Error al conectar a la base de datos: {e}")
```
