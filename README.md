# Laboratorio #2 — Implementación del Login en Laravel

![PHP](https://img.shields.io/badge/PHP-8%2B-777BB4)
![Composer](https://img.shields.io/badge/Composer-latest-orange)
![Laravel](https://img.shields.io/badge/Laravel-10-red)
![MySQL](https://img.shields.io/badge/MySQL-MariaDB-blue)
![Node.js](https://img.shields.io/badge/Node.js-npm-brightgreen)
![Bootstrap](https://img.shields.io/badge/Bootstrap-5-7952B3)
![VSCode](https://img.shields.io/badge/Editor-VSCode-007ACC)

> Repositorio académico con la implementación de **autenticación (login/registro)** en **Laravel**, aplicando el patrón **Modelo–Vista–Controlador (MVC)** y documentando el flujo completo de instalación, configuración, ejecución y respaldo.

---

## Tabla de contenidos
- [Descripción general](#descripción-general)
- [Demo local](#demo-local)
- [Requisitos previos](#requisitos-previos)
- [Instalación y arranque](#instalación-y-arranque)
- [Autenticación (UI / Breeze)](#autenticación-ui--breeze)
- [Configuración de entorno (.env)](#configuración-de-entorno-env)
- [Base de datos: migraciones y respaldo](#base-de-datos-migraciones-y-respaldo)
- [Arquitectura MVC y estructura del proyecto](#arquitectura-mvc-y-estructura-del-proyecto)
- [Rutas principales](#rutas-principales)
- [Evidencia (capturas)](#evidencia-capturas)
- [Dificultades y soluciones](#dificultades-y-soluciones)
- [Referencias](#referencias)
- [Créditos (footer)](#créditos-footer)
- [Fecha de ejecución](#fecha-de-ejecución)
- [Checklist de entrega](#checklist-de-entrega)
- [Comandos útiles](#comandos-útiles)
- [Notas](#notas)

---

## Descripción general
Este proyecto implementa un módulo de **login y registro de usuarios** con Laravel. El objetivo es:
1) Consolidar el uso de **MVC** en un entorno real.
2) Documentar **requisitos, comandos y configuración** del entorno.
3) Mostrar **evidencias visuales** del resultado.
4) Incluir **respaldo de la base de datos** dentro del repositorio.

---

## Demo local
- URL por defecto (Artisan): **http://127.0.0.1:8000/**
- Arranque del servidor: `php artisan serve`

---

## Requisitos previos
- **PHP 8.0+**
- **Composer** (última versión)
- **Laravel Installer** o `composer create-project`
- **XAMPP / WampServer / Laragon** con **Apache** y **MySQL/MariaDB**
- **Node.js + npm**
- **Visual Studio Code**
- **Windows 10/11** (o equivalente en Linux/Mac)

> Si clonas un repo existente, normalmente necesitas: `composer install`, `npm install`, crear `.env`, `php artisan key:generate`, configurar BD y `php artisan migrate`.

---

## Instalación y arranque
```bash
# 1) Crear proyecto (si inicias desde cero)
composer create-project laravel/laravel login-lab
cd login-lab

# 2) Dependencias
composer install
npm install

# 3) Archivo de entorno y clave de app
cp .env.example .env
php artisan key:generate

# 4) Compilar assets (Mix o Vite)
npm run dev

# 5) Servidor local
php artisan serve
# abre http://127.0.0.1:8000/
