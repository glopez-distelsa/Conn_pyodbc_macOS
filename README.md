# Conn_pyodbc_macOS👨‍💻🚀☕️ 

* Fuente: 🗃️

[GitHub - Connecting to SQL Server from Mac OSX](https://pages.github.com/)
```
https://github.com/mkleehammer/pyodbc/wiki/Connecting-to-SQL-Server-from-Mac-OSX
```
[Install the Microsoft ODBC driver for SQL Server (macOS)](https://learn.microsoft.com/en-us/sql/connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos?view=sql-server-ver16#17)
```
https://learn.microsoft.com/en-us/sql/connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos?view=sql-server-ver16#17
```

* Pasos
  
- [ ] Instalar `Homebrew`
      
    ```
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
    ```
- [ ] Instalar Controladores ODBC
      
* MICROSOFT
    
  1 - Agregar `repositorio de Microsoft`
  
      ```
      brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
      ```
      
  2 - Actualizar `Homebrew`
    
      ```
      brew update
      ```
      
  3 - Instalar `msodbcsql18` y `mssql-tools18`
      
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
    - Agrega la ruta de las bibliotecas de `Homebrew` a `DYLD_LIBRARY_PATH`:
    ```
    export DYLD_LIBRARY_PATH=/opt/homebrew/lib:$DYLD_LIBRARY_PATH
    ```

> [!IMPORTANT]
> Tener instalado pyodbc en nuestro ambiente de python: 
> `pip install pyodbc`






> [!TIP]
> Helpful advice for doing things better or more easily.

> [!WARNING]
> Urgent info that needs immediate user attention to avoid problems.

> [!CAUTION]
> Advises about risks or negative outcomes of certain actions.
