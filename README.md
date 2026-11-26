# III Unidad ISC305: API de Personas

API REST construida con Laravel 13 para gestionar personas (CRUD) mediante respuestas JSON. Práctica de la asignatura ISC-305 Programación Web. Los datos son ficticios y los endpoints todavía no tienen autenticación.

## Requisitos

- PHP 8.3 o superior, con las extensiones requeridas por Laravel y `pdo_mysql`
- Composer 2
- MySQL 8.x activo (o MariaDB equivalente)
- Git
- Postman (para probar los endpoints)

## Estructura del repositorio

```text
III-UNIDAD-ISC305/
├── backend/      Proyecto Laravel (API)
├── postman/      Colección de Postman exportada
└── README.md
```

El proyecto Laravel está en la carpeta `backend/`. Todos los comandos de Artisan y Composer se ejecutan desde esa carpeta.

## Configuración de MySQL

Cree la base de datos:

```sql
CREATE DATABASE isc305_unidad3
CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

Copie `backend/.env.example` como `backend/.env` y configure sus propias credenciales locales:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=isc305_unidad3
DB_USERNAME=<su_usuario_mysql>
DB_PASSWORD=<su_clave_mysql>
```

> El archivo `.env` no se sube al repositorio, porque contiene credenciales y la clave de la aplicación. Sus valores reales deben permanecer solo en su equipo.

## Instalación y ejecución

Desde la carpeta `backend/`:

```bash
cd backend
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate
php artisan config:clear
php artisan serve
```

La API queda disponible en `http://127.0.0.1:8000/api`.

## Reconstruir en otro equipo

1. Clonar el repositorio: `git clone https://github.com/VemaFest/III-UNIDAD-ISC305.git`
2. Entrar a `backend/` y ejecutar `composer install`.
3. Copiar `.env.example` como `.env` y ajustar las credenciales de MySQL.
4. Ejecutar `php artisan key:generate` para generar la clave de esa nueva instalación.
5. Crear la base `isc305_unidad3` y ejecutar `php artisan migrate`.
6. Ejecutar `php artisan serve`.

## Endpoints

Base URL: `http://127.0.0.1:8000/api`

| Método | Ruta                | Controlador@método              | Descripción                     | Código de éxito | Errores |
|--------|---------------------|---------------------------------|---------------------------------|-----------------|---------|
| GET    | /hola               | Closure (respuesta de prueba)   | Mensaje de bienvenida           | 200             |         |
| GET    | /personas           | PersonaController@index         | Listar todas las personas       | 200             |         |
| GET    | /personas/{id}      | PersonaController@show          | Consultar una persona           | 200             | 404     |
| POST   | /personas           | PersonaController@store         | Crear una persona               | 201             | 422     |
| PUT    | /personas/{id}      | PersonaController@update        | Actualizar una persona          | 200             | 404, 422|
| DELETE | /personas/{id}      | PersonaController@destroy       | Eliminar una persona            | 204             | 404     |

### Campos de Persona

| Campo              | Tipo      | Reglas                                              |
|--------------------|-----------|-----------------------------------------------------|
| id                 | entero    | Generado automáticamente                            |
| dni                | texto(13) | Obligatorio, 13 dígitos, único                      |
| nombre             | texto(100)| Obligatorio, máximo 100 caracteres                  |
| fecha_nacimiento   | fecha     | Obligatoria, no puede ser futura                    |

## Colección de Postman

La colección se encuentra en `postman/III-UNIDAD-ISC305.postman_collection.json`.

Para usarla:

1. Abra Postman y seleccione **Import**.
2. Elija el archivo JSON de la carpeta `postman/`.
3. Revise que la variable de URL apunte a `http://127.0.0.1:8000/api`.

La colección no incluye credenciales ni datos privados.