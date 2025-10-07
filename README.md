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

Auth::routes();
Route::get('/home', [App\Http\Controllers\HomeController::class, 'index'])->name('home');

