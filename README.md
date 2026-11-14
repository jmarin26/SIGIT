# SIGIT

Sistema Integral de Gestión de Incidencias y Tickets. Aplicación web para técnicos informáticos de campo, orientada al registro de incidencias y partes de intervención desde el móvil.

## Estado del Sprint 1

El entorno de desarrollo está operativo. Django arranca en local y las migraciones iniciales se han aplicado en PostgreSQL. Las pantallas de gestión de empresas y sedes aún no están implementadas.

## Requisitos

- Python 3.13.
- PostgreSQL 18 en ejecución en `127.0.0.1:5432`.
- Una base de datos `sigit` cuyo propietario sea `sigit_user`. Este usuario debe poder iniciar sesión en PostgreSQL.

## Arranque local en Windows

Abre PowerShell en la carpeta que contiene `manage.py`. Si ya tienes el entorno `.venv` creado y las dependencias instaladas, puedes saltarte este bloque.

```powershell
py -3.13 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

En la misma ventana, ejecuta estas líneas una por una. La primera te pedirá la contraseña de `sigit_user`. Escríbela y espera a que vuelva el indicador de PowerShell antes de ejecutar la siguiente línea. No guardes la contraseña ni la clave de Django en el repositorio.

```powershell
$sigitPassword = Read-Host "Contraseña de sigit_user" -AsSecureString
$env:SIGIT_DB_PASSWORD = [pscredential]::new('sigit_user', $sigitPassword).GetNetworkCredential().Password
$env:SIGIT_SECRET_KEY = .\.venv\Scripts\python.exe -c "import secrets; print(secrets.token_urlsafe(48))"
.\.venv\Scripts\python.exe manage.py migrate
.\.venv\Scripts\python.exe manage.py runserver
```

Abre [http://127.0.0.1:8000/](http://127.0.0.1:8000/) para comprobar que Django arranca. Si cierras PowerShell, tendrás que volver a configurar las variables antes del siguiente arranque.
