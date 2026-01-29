# RubiksTimer Project 🧩

## Descripción del Proyecto
Aplicación web para cronometrar resoluciones del Cubo de Rubik, almacenar estadísticas y analizar el progreso del usuario.
Este proyecto sigue una arquitectura **MVC (Modelo-Vista-Controlador)** y una metodología de desarrollo ágil e incremental.

## 📂 Estructura del Proyecto
Para facilitar el trabajo en equipo, hemos dividido el código siguiendo el patrón MVC. Por favor, respetad la ubicación de los ficheros:

rubikstimer_project/
├── app/
|   ├── __init__.py   → Inicializador de la app
|   ├── config.py     → Configuración (Bases de datos, claves)
│   |
|   ├── models/       → [BACKEND] Lógica de datos (BD). Aquí van las Clases (Solve, Session).
|       ├── __init__.py
|       ├── solve.py
|       └── session.py
│   ├── templates/    → [FRONTEND] Vistas HTML. Usad Jinja2 para los datos dinámicos.
|       ├── base.html
|       ├── index.html
|       └── stats.html
│   ├── static/       → [FRONTEND] Archivos públicos (CSS, Imágenes y JS del cliente).
│       ├── css/
|       │   └── style.css
|       ├── js/
|       │   ├── timer.js   <-- Lógica del cronómetro (Cliente)
|       │   └── stats.js
|       └── img/
│   └── controllers/  → [BACKEND] Rutas de Flask. Aquí se reciben las peticiones y se llama al   
|       |                Modelo.
|       ├── __init__.py
|       └── main_controller.py             
|
├── run.py            → Punto de entrada. Ejecutar este archivo para iniciar el servidor local.
├── requirements.txt  → Lista de dependencias. Si instalas algo nuevo, actualiza este fichero.
└── .gitignore        → Configuración para ignorar archivos basura (no tocar sin avisar).


## Guía Detallada de Ficheros y Carpetas

1. Raíz del Proyecto (Gestión y Configuración)
Estos archivos son para la gestión del proyecto, no contienen lógica del cronómetro.

.gitignore: Le dice a Git qué archivos NO subir al repositorio (como archivos temporales, carpetas de compilación __pycache__ o contraseñas locales). Es vital para evitar conflictos entre los 3 compañeros.

requirements.txt: Lista de librerías necesarias (ej: Flask, SQLAlchemy). Permite que tus compañeros instalen todo con un comando (pip install -r requirements.txt) y tengan el mismo entorno de desarrollo.

run.py: El archivo que "enciende" el servidor. Importa la aplicación de la carpeta app y la ejecuta.

README.md: Documentación básica. Explica cómo instalar y ejecutar el proyecto.

2. Carpeta app/ (El Núcleo del Software)
__init__.py: Transforma la carpeta en un paquete. Aquí se inicializa la base de datos y se conectan el Modelo, la Vista y el Controlador.

3. Carpeta app/models/ (El Modelo - M)
Contiene la representación de la información y reglas de negocio, independiente de la interfaz.

solve.py: Clase Solve. Define la estructura de la tabla de base de datos para un intento (ID,   tiempo en milisegundos, scramble, fecha).

session.py: Lógica para agrupar intentos y métodos de cálculo (media de 5, media de 12). Aquí reside la "lógica pesada" del backend.

4. Carpeta app/templates/ (La Vista - V)
Contiene los archivos HTML. En Flask, las vistas interactúan con el modelo a través del motor de plantillas (Jinja2).

base.html:Plantilla maestra. Contiene el menú de navegación, el pie de página y los imports de CSS/JS que se repiten en todas las páginas. Evita duplicar código (principio DRY mencionado en apuntes de XP ).

index.html: La pantalla principal. Hereda de base.html y contiene el contenedor donde se mostrarán los números grandes del cronómetro.

stats.html: Página para visualizar tablas de tiempos y gráficas de progreso.

5. Carpeta app/static/ (Recursos del Cliente)
Archivos que el navegador descarga tal cual. Importante: Aquí va la lógica "en tiempo real".

css/style.css: Estilos visuales (colores, fuentes, diseño responsive).

js/timer.js: CRÍTICO. Contiene el código JavaScript que escucha el evento keydown (barra espaciadora), cuenta los milisegundos en el navegador y, al parar, envía los datos al servidor mediante una petición POST.

js/stats.js: Código para renderizar gráficas (usando librerías como Chart.js) basado en los datos que envía el backend.

6. Carpeta app/controllers/ (El Controlador - C)
Gestiona la entrada del usuario y orquesta la respuesta.

main_controller.py: Define las rutas URL (Endpoints).

@route('/'): Carga el modelo necesario y renderiza index.html.

@route('/save-time', methods=['POST']): Recibe el tiempo del timer.js, valida que sea correcto, llama a models/solve.py para guardarlo en la base de datos y devuelve "OK".

## 🚀 Cómo empezar (Setup)

TODO (Clonar repositorio, Crear entorno virtual, instalar dependencias y ejecutar el servidor)

