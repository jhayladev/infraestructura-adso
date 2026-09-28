# Entorno de Desarrollo

Guía oficial para que **todos** instalemos las mismas herramientas, en las mismas versiones y en las mismas rutas. Si sigues los pasos en orden, al final todo debe quedar funcionando igual en todos los equipos.

> **Sistema operativo:** Windows 10/11 de 64 bits.
> **Versiones verificadas el:** 28 de septiembre de 2026.
> **Regla de oro:** no cambies rutas ni versiones "porque sí". Si algo no coincide con esta guía, avisa antes de seguir.

---

## 1. Herramientas y versiones

| # | Herramienta | Versión | Tipo de versión |
| --- | --- | --- | --- |
| 1 | Microsoft Visual C++ Redistributable (x64) | Última | Requisito de Apache, PHP y Workbench |
| 2 | Git for Windows | 2.55.0 (x64) | Fija |
| 3 | Visual Studio Code | Última estable (referencia: 1.139.1) | Se actualiza sola |
| 4 | PHP (Thread Safe, x64) | 8.5.11 | Fija |
| 5 | Apache HTTP Server (Apache Lounge) | 2.4.68 (Win64) | Fija |
| 6 | Composer | 2.9.x (la última estable) | Fija a la descarga |
| 7 | MySQL Community Server | 26.7.0 | Fija |
| 8 | MySQL Workbench | 26.7.0 | Fija |
| 9 | Visual Studio Community | 2026 | Última |
| 10 | SQL Server Management Studio (SSMS) | 22 (última) | Se actualiza sola |
| 11 | Brave Browser | Última | Se actualiza sola |
| 12 | Android Studio | Quail 4 — 2026.1.4 Patch 1 | Fija |
| 13 | Flutter SDK | 3.47.3 (stable) | Fija |

> **Nota:** las versiones "Fijas" afectan la compatibilidad entre herramientas (por ejemplo PHP, Apache y MySQL). Instala exactamente esa versión. Las que "se actualizan solas" no necesitan coincidir al número.

### ¿Para qué sirve cada una?

- **Git** — Control de versiones para registrar y gestionar los cambios de los proyectos.
- **Visual Studio Code** — Editor de código para programar con diferentes tecnologías.
- **PHP** — Lenguaje para aplicaciones web y lógica del lado del servidor.
- **Apache** — Servidor web que ejecuta las páginas PHP en `http://localhost`.
- **Composer** — Gestor de dependencias y autoload (PSR-4) para PHP.
- **MySQL Server** — Sistema gestor de bases de datos de las aplicaciones.
- **MySQL Workbench** — Interfaz gráfica para diseñar, consultar y administrar MySQL.
- **Visual Studio Community** — IDE para desarrollo con C# y .NET.
- **SSMS** — Herramienta para administrar SQL Server y ejecutar consultas.
- **Brave** — Navegador estándar del equipo para probar aplicaciones web.
- **Android Studio** — Entorno oficial de Android: SDK, emuladores y dispositivos.
- **Flutter** — Framework para desarrollar aplicaciones móviles multiplataforma.

---

## 2. Carpetas estándar

Todos usamos **estas rutas exactas**. Crea primero las carpetas base (una sola vez):

1. Abre el Explorador de archivos y entra a `C:\`.
2. Crea la carpeta `dev`.
3. Dentro de `C:\dev` crea la carpeta `www` (aquí van los proyectos web).

| Elemento | Ruta |
| --- | --- |
| PHP | `C:\dev\php` |
| Apache | `C:\dev\Apache24` |
| Flutter SDK | `C:\dev\flutter` |
| Android SDK | `C:\dev\android-sdk` |
| Proyectos web (DocumentRoot de Apache) | `C:\dev\www` |
| Git, VS Code, Composer, MySQL, Visual Studio, SSMS, Brave, Android Studio | Ruta por defecto del instalador |

> **Importante:** no uses rutas con espacios, tildes ni la ñ para PHP, Flutter y el SDK de Android. Por eso no se instalan dentro de la carpeta de tu usuario de Windows.

---

## 3. Orden de instalación

Sigue este orden. Cada herramienta depende de las anteriores.

### Paso 1. Microsoft Visual C++ Redistributable (x64)

1. Descarga: https://aka.ms/vs/17/release/vc_redist.x64.exe
2. Ejecútalo, acepta la licencia y presiona **Instalar**.
3. Si dice que ya está instalado, presiona **Cerrar** y continúa.

### Paso 2. Git for Windows

1. Entra a https://git-scm.com/install/windows
2. En **Standalone Installer** descarga **Git for Windows/x64 Setup**.
3. Ejecuta el instalador y deja **todo por defecto**, excepto estas pantallas:
   - **Choosing the default editor:** selecciona **Visual Studio Code**.
   - **Adjusting the name of the initial branch:** elige **Override the default branch name → `main`**.
   - **Adjusting your PATH environment:** deja **Git from the command line and also from 3rd-party software**.
4. Presiona **Install** y luego **Finish**.
5. Abre **Git Bash** o **PowerShell** y configura tu identidad (cambia los datos):

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu-correo@ejemplo.com"
git config --global init.defaultBranch main
```

### Paso 3. Visual Studio Code

1. Entra a https://code.visualstudio.com/download
2. En **Windows** descarga **User Installer (x64)**.
3. Ejecuta el instalador. En la pantalla **Seleccionar tareas adicionales** marca:
   - Agregar la acción "Abrir con Code" al menú contextual de archivos.
   - Agregar la acción "Abrir con Code" al menú contextual de directorios.
   - Registrar Code como editor de tipos de archivo compatibles.
   - **Agregar a PATH** (requiere reiniciar el shell).
4. Presiona **Instalar** y luego **Finalizar**.
5. Extensiones recomendadas (opcional, pero igual para todos): **Dart**, **Flutter**, **PHP Intelephense**.

### Paso 4. PHP 8.5.11 (Thread Safe)

> Usamos la versión **Thread Safe** porque Apache carga PHP como módulo. La versión Non Thread Safe no sirve para este entorno.

1. Entra a https://windows.php.net/download/
2. En la sección **PHP 8.5**, busca **VS17 x64 Thread Safe** y descarga el **Zip** (no el Debug Pack ni el Development package).
3. Descomprime el contenido del ZIP directamente en `C:\dev\php`. Debe quedar así: `C:\dev\php\php.exe` (no `C:\dev\php\php-8.5.11\php.exe`).
4. Entra a `C:\dev\php`, copia el archivo `php.ini-development` y pégalo en la misma carpeta. Renombra la copia a **`php.ini`**.
5. Abre `C:\dev\php\php.ini` con VS Code y busca estas líneas (usa `Ctrl + F`). Quita el `;` del inicio para activarlas y ajusta los valores:

```ini
extension_dir = "C:/dev/php/ext"
date.timezone = America/Bogota

extension=curl
extension=fileinfo
extension=mbstring
extension=mysqli
extension=openssl
extension=pdo_mysql
extension=zip
```

6. Guarda el archivo.

### Paso 5. Variables de entorno de PHP

1. Presiona `Windows + R`, escribe `sysdm.cpl` y presiona Enter.
2. Ve a **Opciones avanzadas → Variables de entorno…**
3. En **Variables del sistema**, selecciona **Path** y presiona **Editar**.
4. Presiona **Nuevo** y agrega: `C:\dev\php`
5. Presiona **Aceptar** tres veces.
6. Cierra y vuelve a abrir cualquier terminal. Prueba con:

```powershell
php -v
```

Debe mostrar `PHP 8.5.11`.

### Paso 6. Apache HTTP Server 2.4.68

1. Entra a https://www.apachelounge.com/download/
2. En **Apache 2.4 VS18 Windows Binaries**, descarga **Apache 2.4.68 Win64** (archivo `httpd-2.4.68-...-win64-VS18.zip`).
3. Abre el ZIP y copia la carpeta **`Apache24`** dentro de `C:\dev`. Debe quedar `C:\dev\Apache24\bin\httpd.exe`.
4. Abre `C:\dev\Apache24\conf\httpd.conf` con VS Code y haz estos cambios:

**a) Ruta base** (cerca del inicio del archivo):

```apache
Define SRVROOT "C:/dev/Apache24"
```

**b) Nombre del servidor** (busca `ServerName`):

```apache
ServerName localhost:80
```

**c) Carpeta de proyectos.** Busca `DocumentRoot` y el bloque `<Directory ...>` que lo sigue, y déjalos así:

```apache
DocumentRoot "C:/dev/www"
<Directory "C:/dev/www">
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
</Directory>
```

**d) Módulo de reescritura** (necesario para rutas amigables y APIs). Quita el `;`... en este caso el `#` de esta línea:

```apache
LoadModule rewrite_module modules/mod_rewrite.so
```

**e) Índice por defecto.** Busca `<IfModule dir_module>` y déjalo así:

```apache
<IfModule dir_module>
    DirectoryIndex index.php index.html
</IfModule>
```

**f) Conectar PHP con Apache.** Agrega este bloque **al final** del archivo:

```apache
# --- PHP 8.5 ---
LoadModule php_module "C:/dev/php/php8apache2_4.dll"
PHPIniDir "C:/dev/php"
<FilesMatch "\.php$">
    SetHandler application/x-httpd-php
</FilesMatch>
```

5. Guarda el archivo.

### Paso 7. Variable de entorno de Apache y arranque como servicio

1. Repite el procedimiento del Paso 5 y agrega al **Path** del sistema: `C:\dev\Apache24\bin`
2. Abre **PowerShell como administrador** (clic derecho → *Ejecutar como administrador*) y ejecuta:

```powershell
httpd -t
httpd -k install
net start Apache2.4
```

- `httpd -t` debe responder **Syntax OK**. Si da error, revisa el archivo `httpd.conf`.
- Si el puerto 80 está ocupado (por ejemplo por IIS), detén ese servicio o avisa al grupo antes de cambiar el puerto.

3. Prueba que PHP funciona con Apache. Crea el archivo `C:\dev\www\index.php` con este contenido:

```php
<?php phpinfo();
```

4. Abre el navegador en http://localhost. Debes ver la página de información de PHP 8.5.11.

> **Si Apache no arranca y menciona `php8apache2_4.dll`:** confirma que instalaste el Visual C++ Redistributable (Paso 1) y que usaste PHP **Thread Safe** x64. Si el problema continúa, avisa al grupo y no cambies versiones por tu cuenta.

### Paso 8. Composer

1. Entra a https://getcomposer.org/ y presiona **Download**.
2. En **Windows Installer** descarga **Composer-Setup.exe**.
3. Ejecútalo con estas opciones:
   - **Install for all users** (recomendado).
   - **Developer mode:** déjalo **desmarcado**.
   - Cuando pida la ruta de PHP, elige `C:\dev\php\php.exe`.
   - Proxy: déjalo **vacío**.
4. Finaliza y **cierra y abre una terminal nueva**. Prueba con:

```powershell
composer -V
```

### Paso 9. MySQL Community Server 26.7.0

1. Entra a https://dev.mysql.com/downloads/mysql/
2. En **Select Version** deja **26.7.0** y en **Select Operating System** deja **Microsoft Windows**.
3. Descarga el primero de la lista: **Windows (x86, 64-bit), MSI Installer** y en la siguiente pantalla presiona **No thanks, just start my download**.
4. Ejecuta el instalador. Elige el tipo de instalación **Server only** o **Typical** y presiona **Install**.
5. En la configuración del servidor usa **estos valores para todos**:

| Opción | Valor |
| --- | --- |
| Tipo de configuración | Development Computer |
| Puerto | `3306` |
| Autenticación | Use Strong Password Encryption (recomendada, por defecto) |
| Usuario | `root` |
| Contraseña de `root` | `Adso2026*` (solo para uso local del curso) |
| Servicio de Windows | Activado, iniciar con el sistema, nombre por defecto |

6. Finaliza y aplica la configuración hasta que todos los pasos digan **Complete**.

### Paso 10. Variable de entorno de MySQL

1. Abre `C:\Program Files\MySQL\` y confirma el nombre exacto de la carpeta del servidor (por ejemplo `MySQL Server 26.7`).
2. Repite el procedimiento del Paso 5 y agrega al **Path** del sistema la carpeta `bin` de esa ruta, por ejemplo:

```text
C:\Program Files\MySQL\MySQL Server 26.7\bin
```

3. Abre una terminal nueva y prueba:

```powershell
mysql --version
mysql -u root -p
```

Escribe la contraseña y debes entrar al prompt `mysql>`. Para salir escribe `exit`.

### Paso 11. MySQL Workbench 26.7.0

1. Entra a https://dev.mysql.com/downloads/workbench/
2. Descarga **Windows (x86, 64-bit), MSI Installer** (`mysql-workbench-26.7.0-winx64.msi`) y presiona **No thanks, just start my download**.
3. Ejecuta el instalador con las opciones por defecto (*Complete*).
4. Abre Workbench. En la conexión **Local instance** usa: host `127.0.0.1`, puerto `3306`, usuario `root` y la contraseña definida en el Paso 9.
5. Presiona **Test Connection**. Debe responder con éxito.

### Paso 12. Visual Studio Community 2026

1. Entra a https://visualstudio.microsoft.com/es/downloads/
2. En **Visual Studio 2026**, ubica **Community** y presiona **Descarga gratuita**.
3. Ejecuta el instalador descargado.
4. En **Cargas de trabajo** marca:
   - **Desarrollo de escritorio con .NET** (obligatoria).
   - **ASP.NET y desarrollo web** (obligatoria).
   - **Desarrollo de la interfaz de usuario multiplataforma de .NET (.NET MAUI)** (opcional, solo si el proyecto lo pide).
5. Presiona **Instalar** y espera a que finalice. Puede tardar.

### Paso 13. SQL Server Management Studio (SSMS) 22

> SSMS es solo la herramienta de administración. **No** necesitas tener instalado Visual Studio Community para usarlo.

1. Entra a https://learn.microsoft.com/es-es/ssms/install/install
2. Descarga el instalador de SSMS 22 (`vs_SSMS.exe`).
3. Ejecuta el archivo. Se abrirá el instalador de Visual Studio (es normal).
4. Selecciona los componentes necesarios y presiona **Instalar**.
5. Al terminar, abre SQL Server Management Studio y configura la conexión con tu servidor.

### Paso 14. Brave Browser

1. Entra a https://brave.com/es/download/
2. Presiona **Descargar Brave** y ejecuta `BraveBrowserSetup.exe`.
3. El instalador funciona automáticamente. Al terminar se abre Brave.
4. Opcional: en **Configuración → Navegador predeterminado**, ponlo como predeterminado.

### Paso 15. Android Studio (Quail 4 — 2026.1.4 Patch 1)

1. Entra a https://developer.android.com/studio y presiona **Descargar Android Studio**. Acepta los términos.
2. Ejecuta el instalador con las opciones por defecto.
3. Al abrir por primera vez, en el asistente elige **Custom** (no *Standard*).
4. En **Android SDK Location** escribe: `C:\dev\android-sdk`
5. Termina el asistente y espera la descarga de componentes.
6. Ve a **More Actions → SDK Manager → pestaña SDK Tools** y marca **Android SDK Command-line Tools (latest)**. Presiona **Apply**.

Variable de entorno del SDK:

1. Abre **Variables de entorno** (Paso 5).
2. En **Variables del sistema** presiona **Nueva…** y crea:
   - Nombre: `ANDROID_HOME`
   - Valor: `C:\dev\android-sdk`

### Paso 16. Flutter SDK 3.47.3

Documentación oficial: https://docs.flutter.dev/install/manual

1. Entra a https://docs.flutter.dev/install/manual, en el paso **Download the Flutter SDK bundle** descarga el ZIP para Windows (`flutter_windows_3.47.3-stable.zip`).
2. Descomprímelo en `C:\dev` para que quede `C:\dev\flutter\bin\flutter.bat`. Por PowerShell:

```powershell
Expand-Archive -Path "$env:USERPROFILE\Downloads\flutter_windows_3.47.3-stable.zip" -DestinationPath "C:\dev"
```

3. Si falta `flutter.bat` después de descomprimir, tu antivirus lo puso en cuarentena. Agrega `C:\dev\flutter` a las exclusiones del antivirus y descomprime de nuevo.
4. Agrega al **Path** del sistema (Paso 5): `C:\dev\flutter\bin`
5. Crea esta variable del sistema para que Flutter use Brave en web:
   - Nombre: `CHROME_EXECUTABLE`
   - Valor: `C:\Program Files\BraveSoftware\Brave-Browser\Application\brave.exe`
6. Abre una terminal **nueva** y ejecuta:

```powershell
flutter --version
flutter config --android-sdk "C:\dev\android-sdk"
flutter doctor --android-licenses
flutter doctor -v
```

En `--android-licenses` escribe `y` para aceptar todas las licencias.

---

## 4. Resumen de variables de entorno

**Variables del sistema → Path (agregar):**

| Entrada |
| --- |
| `C:\dev\php` |
| `C:\dev\Apache24\bin` |
| `C:\Program Files\MySQL\MySQL Server 26.7\bin` *(confirma el nombre real de la carpeta)* |
| `C:\dev\flutter\bin` |

**Variables del sistema (crear):**

| Nombre | Valor |
| --- | --- |
| `ANDROID_HOME` | `C:\dev\android-sdk` |
| `CHROME_EXECUTABLE` | `C:\Program Files\BraveSoftware\Brave-Browser\Application\brave.exe` |

Git, VS Code y Composer agregan su propia entrada automáticamente.

---

## 5. Verificación final

Cierra todas las terminales, abre una nueva de **PowerShell** y ejecuta:

```powershell
git --version
code --version
php -v
php -m
httpd -v
composer -V
mysql --version
flutter --version
flutter doctor -v
```

Resultado esperado:

| Comando | Debe mostrar |
| --- | --- |
| `git --version` | `git version 2.55.0.windows.x` |
| `code --version` | Versión de VS Code (1.139 o superior) |
| `php -v` | `PHP 8.5.11 (cli) ... ZTS` |
| `php -m` | Incluye `curl`, `fileinfo`, `mbstring`, `mysqli`, `openssl`, `pdo_mysql`, `zip` |
| `httpd -v` | `Apache/2.4.68 (Win64)` |
| `composer -V` | `Composer version 2.9.x` |
| `mysql --version` | `mysql  Ver 26.7.0 for Win64` |
| `flutter --version` | `Flutter 3.47.3 • channel stable` |
| `flutter doctor -v` | `[√]` en Flutter, Windows, Android toolchain y Android Studio |

Además:

- http://localhost muestra la página `phpinfo()` de PHP 8.5.11.
- MySQL Workbench conecta a `127.0.0.1:3306` con el usuario `root`.
- Visual Studio 2026 abre y crea un proyecto de *Windows Forms*.
- SSMS abre sin errores.

> **Nota sobre `flutter doctor`:** puede mostrar `[!]` en *Visual Studio – develop Windows apps* si no instalaste la carga de trabajo de C++. Es normal y no afecta a las apps móviles. Tampoco debe marcar error en *Connected device*, aunque no tengas un dispositivo conectado.

---

## 6. Rutas de descarga (resumen)

Todo lo que hay que descargar, en el orden de instalación:

| Orden | Herramienta | Página de descarga | Archivo a elegir | Carpeta de instalación |
| --- | --- | --- | --- | --- |
| 1 | Visual C++ Redistributable | https://aka.ms/vs/17/release/vc_redist.x64.exe | `vc_redist.x64.exe` | Por defecto |
| 2 | Git | https://git-scm.com/install/windows | Standalone Installer → Git for Windows/x64 Setup | Por defecto |
| 3 | Visual Studio Code | https://code.visualstudio.com/download | Windows → User Installer (x64) | Por defecto |
| 4 | PHP 8.5.11 | https://windows.php.net/download/ | PHP 8.5 → VS17 x64 **Thread Safe** → Zip | `C:\dev\php` |
| 5 | Apache 2.4.68 | https://www.apachelounge.com/download/ | Apache 2.4 VS18 → Win64 (zip) | `C:\dev\Apache24` |
| 6 | Composer | https://getcomposer.org/ | Download → Composer-Setup.exe | Por defecto |
| 7 | MySQL Server 26.7.0 | https://dev.mysql.com/downloads/mysql/ | Windows (x86, 64-bit), MSI Installer (el primero) | Por defecto |
| 8 | MySQL Workbench 26.7.0 | https://dev.mysql.com/downloads/workbench/ | Windows (x86, 64-bit), MSI Installer | Por defecto |
| 9 | Visual Studio Community 2026 | https://visualstudio.microsoft.com/es/downloads/ | Community → Descarga gratuita | Por defecto |
| 10 | SSMS 22 | https://learn.microsoft.com/es-es/ssms/install/install | `vs_SSMS.exe` | Por defecto |
| 11 | Brave | https://brave.com/es/download/ | `BraveBrowserSetup.exe` | Por defecto |
| 12 | Android Studio | https://developer.android.com/studio | Android Studio para Windows | Por defecto (SDK en `C:\dev\android-sdk`) |
| 13 | Flutter 3.47.3 | https://docs.flutter.dev/install/manual | Windows → `flutter_windows_3.47.3-stable.zip` | `C:\dev\flutter` |

---

## 7. Si algo falla

1. Cierra y abre de nuevo la terminal (las variables de entorno solo se leen al abrirla).
2. Revisa que la ruta de cada carpeta sea **exactamente** la de la sección 2.
3. Vuelve a ejecutar el comando de verificación de esa herramienta.
4. Si sigue fallando, comparte el mensaje de error completo con el grupo. **No cambies versiones ni rutas por tu cuenta.**
