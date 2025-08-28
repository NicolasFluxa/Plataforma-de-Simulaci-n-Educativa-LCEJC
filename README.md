# Plataforma de Simulación Educativa: LCEJC

![Laravel](https://img.shields.io/badge/Laravel-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![MySQL](https://img.shields.io/badge/MySQL-005C84?style=for-the-badge&logo=mysql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

Este es el monorepo oficial para los proyectos **PCIS4 (Administración de Personal)** y **PCIS5 (Gestión Comercial)**, desarrollados por Conecta+ para el Complejo Educacional Javiera Carrera.

## 🚀 Arquitectura del Proyecto

Este repositorio utiliza una arquitectura de monorepo para gestionar el código de múltiples aplicaciones que comparten una base común (autenticación, base de datos, componentes de UI).

* `/backend`: Contiene la aplicación principal de Laravel.
* `/frontend`: Contiene la aplicación principal de React (Vite).
* `/packages`: Contiene los módulos específicos de cada simulador y el código compartido.

## ⚙️ Instalación y Puesta en Marcha Local

1.  **Clonar el repositorio:**
    ```bash
    git clone [https://github.com/tu-usuario/lcejc-simulador.git](https://github.com/tu-usuario/lcejc-simulador.git)
    cd lcejc-simulador
    ```

2.  **Configurar el Backend (Laravel):**
    * Navega a la carpeta del backend: `cd backend`
    * Crea tu archivo de entorno: `cp .env.example .env`
    * Vuelve a la raíz del proyecto: `cd ..`

3.  **Instalar TODAS las dependencias:**
    * Desde la raíz del proyecto, levanta Docker para que Composer y NPM estén disponibles:
        ```bash
        docker-compose up -d --build
        ```
    * Instala dependencias de Composer:
        ```bash
        docker-compose run --rm composer install
        ```
    * Instala dependencias de NPM (esto instalará los `node_modules` en `/frontend` y en cada paquete que lo requiera):
        ```bash
        docker-compose run --rm npm install
        ```

4.  **Ejecutar las migraciones de la base de datos:**
    * La migración inicial creará las tablas compartidas (como `users`) y las tablas específicas de cada proyecto.
    ```bash
    docker-compose run --rm artisan migrate --seed
    ```

5.  **¡Listo!**
    * El frontend de React estará disponible en `http://localhost:5173`
    * El backend de Laravel estará disponible en `http://localhost:8000`

## 🚀 Flujo de Despliegue (CI/CD)

El despliegue a Hostinger está automatizado con GitHub Actions. Cualquier `push` a la rama `main` disparará un flujo que compilará ambos proyectos y los desplegará en el subdominio `desarrollo.lcejc.cl`.

