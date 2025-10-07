# Laboratorio #2 – Implementación del Login en Laravel
> Repositorio académico documentado con **toda** la información requerida (requisitos, instalación, autenticación, MVC, migraciones, evidencia, respaldo BD, dificultades/soluciones, referencias, footer y fecha).

![PHP](https://img.shields.io/badge/PHP-8%2B-777BB4) ![Composer](https://img.shields.io/badge/Composer-latest-orange) ![Laravel](https://img.shields.io/badge/Laravel-10-red) ![MySQL](https://img.shields.io/badge/MySQL-MariaDB-blue) ![Node.js](https://img.shields.io/badge/Node.js-npm-brightgreen) ![Bootstrap](https://img.shields.io/badge/Bootstrap-5-7952B3) ![VSCode](https://img.shields.io/badge/VSCode-Editor-007ACC)

---

## Tabla de Contenidos
- [Descripción General](#descripción-general)
- [Demo Local](#demo-local)
- [Requisitos Previos](#requisitos-previos)
- [Instalación y Arranque](#instalación-y-arranque)
- [Autenticación (UI / Breeze)](#autenticación-ui--breeze)
- [Configuración de Entorno (.env)](#configuración-de-entorno-env)
- [Base de Datos: Migraciones y Respaldo](#base-de-datos-migraciones-y-respaldo)
- [Arquitectura MVC y Estructura de Carpetas](#arquitectura-mvc-y-estructura-de-carpetas)
- [Rutas Principales](#rutas-principales)
- [Evidencia (capturas)](#evidencia-capturas)
- [Dificultades y Soluciones](#dificultades-y-soluciones)
- [Referencias](#referencias)
- [Footer (Créditos)](#footer-créditos)
- [Fecha de Ejecución](#fecha-de-ejecución)
- [Checklist de Entrega](#checklist-de-entrega)
- [Comandos Útiles](#comandos-útiles)
- [Notas y Licencia](#notas-y-licencia)

---

## Descripción General
Este repositorio contiene la implementación de un **módulo de autenticación (login/registro)** en **Laravel**, aplicando el patrón **Modelo–Vista–Controlador (MVC)**. La documentación explica **todo el flujo**: requisitos, comandos, configuración de entorno, migraciones, resultado visual, dificultades/soluciones y **respaldo de la base de datos**, tal como se solicita en la asignación académica.

## Demo Local
- URL local por defecto (Artisan): **http://127.0.0.1:8000/**
- Comando de ejecución: `php artisan serve`

---

## Requisitos Previos
**Prerrequisitos del entorno**
- PHP **8.0+**
- **Composer** (última versión estable)
- **Laravel Installer** o `composer create-project`
- **XAMPP / WampServer / Laragon** (Apache o Nginx) con **MySQL/MariaDB**
- Editor: **Visual Studio Code**
- **Node.js + npm**
- Sistema Operativo: **Windows 10/11** (equivalente en Linux/Mac)

**Iconos/Tecnologías**: ver badges al inicio.

---

## Instalación y Arranque
> Si ya tienes el proyecto clonado, ejecuta solo `composer install`, `npm install` y configura el `.env`.

```bash
# 1) Crear proyecto (si comienzas desde cero)
composer create-project laravel/laravel login-lab
cd login-lab

# 2) Dependencias
composer install
npm install

# 3) Archivo de entorno y clave de app
cp .env.example .env
php artisan key:generate
