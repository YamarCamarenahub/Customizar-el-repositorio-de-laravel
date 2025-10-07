# Laboratorio #2 — Implementación de **Login** en Laravel (Repositorio Documentado)

> **Universidad Tecnológica de Panamá — Ingeniería Web**  
> **Instructor:** Ing. Irina Fong

---

## Tabla de contenido
1. [Requisitos Previos (ecosistema y comandos base)](#1-requisitos-previos-ecosistema-y-comandos-base)
2. [Introducción (MVC), comandos de migración y objetivo](#2-introducción-mvc-comandos-de-migración-y-objetivo)
3. [Resultados visibles (capturas)](#3-resultados-visibles-capturas)
4. [Base de datos: `.env`, migraciones y respaldo](#4-base-de-datos-env-migraciones-y-respaldo)
5. [Dificultades y soluciones](#5-dificultades-y-soluciones)
6. [Referencias](#6-referencias)
7. [Footer de autoría](#7-footer-de-autoría)
8. [Fecha de ejecución](#8-fecha-de-ejecución)
9. [Entrega en el repositorio](#9-entrega-en-el-repositorio)
10. [Anexo A — Bitácora exacta de comandos ejecutados](#anexo-a--bitácora-exacta-de-comandos-ejecutados)
11. [Anexo B — Estructura del proyecto](#anexo-b--estructura-del-proyecto)

---

## 1. Requisitos Previos (ecosistema y comandos base)

**Tecnologías utilizadas en este proyecto (detectadas):**
- **Laravel Framework** ^8.75
- **laravel/ui** ^3.4 (scaffolding de autenticación con **Bootstrap**)
- **Bootstrap** ^5.1.3 (vía npm)
- **Laravel Mix (Webpack)** ^6.0.6
- **PHP** ^7.3 | ^8.0
- **MySQL/MariaDB**
- **Node.js + npm**

**Badges (opcional):**  
![PHP](https://img.shields.io/badge/PHP-%5E7.3%20%7C%20%5E8.0-blue) ![Laravel 8](https://img.shields.io/badge/Laravel-8.x-red) ![Laravel UI](https://img.shields.io/badge/laravel%2Fui-^3.4-orange) ![Bootstrap](https://img.shields.io/badge/Bootstrap-5.x-purple) ![Laravel%20Mix](https://img.shields.io/badge/Laravel%20Mix-6.x-brightgreen) ![MySQL](https://img.shields.io/badge/MySQL-Running-lightgrey) ![Node.js](https://img.shields.io/badge/Node.js-npm-green)

**Instalación rápida (comandos base):**
```bash
# 1) Clonar el repositorio (si aplica) y entrar a la carpeta del proyecto
git clone <URL_DE_TU_REPO> login-lab
cd login-lab

# 2) Dependencias PHP
composer install

# 3) Variables de entorno
cp .env.example .env
php artisan key:generate

# 4) Configurar Base de Datos (editar .env) y ejecutar migraciones
php artisan migrate

# 5) Dependencias Frontend y compilación de assets (Laravel Mix)
npm install
npm run dev   # o: npm run production

# 6) Ejecutar el servidor de desarrollo
php artisan serve
# Acceder a: http://127.0.0.1:8000  (Login: /login, Registro: /register)
