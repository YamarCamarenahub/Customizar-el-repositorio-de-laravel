# Laboratorio #2 — Implementación de **Login** en Laravel (Repositorio Documentado)
> **Universidad Tecnológica de Panamá — Ingeniería Web**  
> **Instructor:** Ing. Irina Fong

---

## Índice
- [1. Requisitos previos (ecosistema y comandos base)](#sec-1)
- [2. Introducción (MVC), migraciones y objetivo](#sec-2)
- [3. Resultados visibles (capturas)](#sec-3)
- [4. Base de datos: `.env`, migraciones y respaldo](#sec-4)
- [5. Dificultades y soluciones](#sec-5)
- [6. Personalización de estilos (fondo con Bootstrap 5)](#sec-6)
- [7. Referencias](#sec-7)
- [8. Footer de autoría](#sec-8)
- [9. Fecha de ejecución](#sec-9)
- [Anexo A — Bitácora exacta de comandos ejecutados](#anexo-a)
- [Anexo B — Estructura del proyecto](#anexo-b)

---

<a id="sec-1"></a>
## 1. Requisitos previos (ecosistema y comandos base)

**Versiones detectadas en este proyecto**
- **Laravel**: 8.x (constraint ^8.75)
- **laravel/ui**: ^3.4
- **PHP**: ^7.3|^8.0
- **Laravel Mix**: ^6.0.6
- **Bootstrap**: ^5.1.3
- **@popperjs/core**: ^2.10.2
- **Node.js + npm** (requerido para compilar assets)
- **MySQL/MariaDB** en ejecución

**Instalación rápida**
```bash
# Clona el repositorio y entra al proyecto
git clone <URL_DE_TU_REPO> login-lab
cd login-lab

# Dependencias PHP
composer install

# Variables de entorno y clave de app
cp .env.example .env
php artisan key:generate

# Configura la BD en .env y ejecuta migraciones
php artisan migrate

# Dependencias Frontend y compilación (Laravel Mix)
npm install
npm run dev        # o: npm run production

# Servidor de desarrollo
php artisan serve
# URL: http://127.0.0.1:8000  (Login: /login, Register: /register)
```

**Scaffolding de autenticación (ya aplicado)**
```bash
composer require laravel/ui
php artisan ui bootstrap --auth
npm install
npm run dev
php artisan migrate
```

> **Nota:** La carpeta `bootstrap/` del proyecto **no** es el framework CSS **Bootstrap**. Bootstrap (CSS/JS) se instala por npm (ya declarado en `package.json`) y se compila con **Laravel Mix**.

---

<a id="sec-2"></a>
## 2. Introducción (MVC), migraciones y objetivo

**Arquitectura MVC (Laravel 8)**
- **Modelos (`app/Models`)**: Representan tablas y reglas de negocio. Ej.: `User`.
- **Controladores (`app/Http/Controllers`)**: Orquestan la lógica. Este proyecto incluye:
  - `Auth/LoginController.php`, `Auth/RegisterController.php`, `Auth/ForgotPasswordController.php`, `Auth/ResetPasswordController.php`, `Auth/VerificationController.php`, `Auth/ConfirmPasswordController.php`.
  - `HomeController.php` para el *dashboard* posterior al login.
- **Vistas (`resources/views`)**: Plantillas Blade generadas por `laravel/ui` en:
  - `resources/views/auth/*` (login, register, passwords)
  - `resources/views/layouts/app.blade.php` (layout base)
- **Rutas (`routes/web.php`)**: Autenticación y dashboard:
  ```php
  Auth::routes();
  Route::get('/home', [App\Http\Controllers\HomeController::class, 'index'])->name('home');
  ```

**Comandos de migración esenciales**
```bash
php artisan migrate
php artisan migrate:status
php artisan migrate:fresh --seed   # recrea tablas (si tienes seeders)
```

**Objetivo del laboratorio**
Implementar un módulo de **Login** totalmente funcional y documentado: prerrequisitos, MVC, capturas, `.env` y migraciones, respaldo de BD, dificultades/soluciones, referencias, footer, fecha y entrega.

---

<a id="sec-3"></a>
## 3. Resultados visibles (capturas)

Incluye capturas reales en `docs/img/` con estos nombres:

- `docs/img/home.png` — Home (visitante)
- `docs/img/login.png` — Pantalla de Login
- `docs/img/register.png` — Pantalla de Registro
- `docs/img/dashboard.png` — Dashboard autenticado

*(Opcional)* Agrega evidencia de:
- `php artisan route:list`
- Migraciones exitosas en consola

---

<a id="sec-4"></a>
## 4. Base de datos: `.env`, migraciones y respaldo

**Ejemplo de `.env`**
```dotenv
APP_NAME="LoginLab"
APP_ENV=local
APP_KEY=base64:GENERADA_POR_ARTISAN
APP_DEBUG=true
APP_URL=http://127.0.0.1:8000

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=login_lab
DB_USERNAME=root
DB_PASSWORD=
```

**Migraciones y seeders**
```bash
php artisan migrate
php artisan db:seed          # si definiste seeders
php artisan migrate:status
```

**Respaldo de BD con `mysqldump`**
```bash
# Ajusta usuario, contraseña y nombre de la BD
mysqldump -u root -p login_lab > db/backup/login_lab_backup.sql
```
> Versiona el archivo de respaldo en `db/backup/`. No subas `.env` al repositorio (usa `.env.example`).

---

<a id="sec-5"></a>
## 5. Dificultades y soluciones

**Pantallas de Login/Register sin estilos o “en blanco”**
- Verifica compilación: `npm install && npm run dev` (Laravel Mix).
- En `resources/views/layouts/app.blade.php`, confirma que se referencien `{{ mix('css/app.css') }}` y `{{ mix('js/app.js') }}` o `asset()` según tu layout generado por UI.
- No elimines `@csrf` en formularios.

**`http://localhost/login` no abre**
- Usa `php artisan serve` y entra a `http://127.0.0.1:8000/login`.
- Revisa que exista `Auth::routes()` en `routes/web.php`.

**Errores de migración / conexión a BD**
- Revisa credenciales en `.env` y que MySQL esté activo.
- Si cambiaste esquema, `php artisan migrate:fresh --seed` (si tienes seeders).

**Cachés “pegadas” tras cambiar configuración**
```bash
php artisan cache:clear
php artisan config:clear
php artisan view:clear
php artisan route:clear
```

---

<a id="sec-6"></a>
## 6. Personalización de estilos (fondo con Bootstrap 5)

> Objetivo: aplicar un **fondo con imagen** solo a `/login` y `/register`.

**1) Coloca tu imagen**
- Copia tu imagen a: `public/img/laravel-bg.jpg`

**2) Agrega CSS personalizado**
- En **Laravel Mix**, el CSS principal suele ser `resources/sass/app.scss` (o `resources/css/app.css`).  
  - Si usas `app.scss`, confirma que importe Bootstrap (ya viene por defecto con UI):
    ```scss
    // resources/sass/app.scss
    // Bootstrap
    @import "~bootstrap/scss/bootstrap";
    
    // Estilos personalizados
    body.auth-bg {
      min-height: 100vh;
      background: url('/img/laravel-bg.jpg') no-repeat center center fixed;
      background-size: cover;
    }
    ```
  - Si usas `app.css`, agrega al final:
    ```css
    /* resources/css/app.css */
    body.auth-bg {
      min-height: 100vh;
      background: url('/img/laravel-bg.jpg') no-repeat center center fixed;
      background-size: cover;
    }
    ```

**3) Aplica la clase condicionalmente en el layout**
- Edita `resources/views/layouts/app.blade.php` y agrega la clase `auth-bg` al `<body>` cuando la ruta sea `login` o `register`:
  ```blade
<!doctype html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>{{ config('app.name', 'Laravel') }}</title>
    <link href="{{ mix('css/app.css') }}" rel="stylesheet">
</head>
<body class="{{ request()->is('login') || request()->is('register') ? 'auth-bg' : '' }}">
    <div id="app">
        @yield('content')
    </div>
    <script src="{{ mix('js/app.js') }}" defer></script>
</body>
</html>
  ```

**4) Reconstruye assets**
```bash
npm run dev     # o: npm run production
```

> Con esto, las vistas de login y register heredan el layout y muestran el fondo. Si deseas **oscurecer** la imagen, agrega un pseudo-elemento overlay en CSS.

---

<a id="sec-7"></a>
## 7. Referencias
- **Laravel Docs (8.x, Auth)**: https://laravel.com/docs/8.x/authentication  
- **laravel/ui (Bootstrap Auth Scaffolding)**: https://github.com/laravel/ui  
- **Laravel Mix 6**: https://laravel-mix.com/  
- **Bootstrap 5**: https://getbootstrap.com/  

---

<a id="sec-8"></a>
## 8. Footer de autoría

- **Estudiante:** Yamar Camarena  
- **Carrera:** Ingeniería de Software — UTP  
- **Curso:** Ingeniería Web  
- **Instructor:** Ing. Irina Fong

---

<a id="sec-9"></a>
## 9. Fecha de ejecución

- **Fecha:** 07/10/2025

---

<a id="anexo-a"></a>
## Anexo A — Bitácora exacta de comandos ejecutados
```bash
# Preparación del entorno
composer install
cp .env.example .env
php artisan key:generate

# Scaffolding de autenticación con Bootstrap
composer require laravel/ui
php artisan ui bootstrap --auth

# Compilación de assets (Laravel Mix)
npm install
npm run dev        # o npm run production

# Base de datos
php artisan migrate
php artisan migrate:status

# Servidor de desarrollo
php artisan serve
# URL: http://127.0.0.1:8000/login
```

---

<a id="anexo-b"></a>
## Anexo B — Estructura del proyecto
```
login-lab/
├─ app/
│  └─ Http/Controllers/
│     ├─ Auth/ (LoginController, RegisterController, etc.)
│     └─ HomeController.php
├─ resources/
│  └─ views/
│     ├─ auth/
│     │  ├─ login.blade.php
│     │  ├─ register.blade.php
│     │  └─ passwords/ (reset, email, confirm)
│     └─ layouts/app.blade.php
├─ routes/
│  └─ web.php          # Auth::routes(); /home
├─ public/
│  ├─ css/app.css      # generado por Mix
│  ├─ js/app.js        # generado por Mix
│  └─ img/laravel-bg.jpg
├─ database/
│  └─ migrations/      # tablas de users, password_resets, etc.
├─ db/
│  └─ backup/
│     └─ login_lab_backup.sql   # tu respaldo
├─ package.json         # Bootstrap 5 + Laravel Mix 6
├─ composer.json        # laravel/framework 8.x + laravel/ui
├─ webpack.mix.js
└─ README.md
```
