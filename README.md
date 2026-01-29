# RubiksTimer Project 🧩

## Descripción del Proyecto
Aplicación web para cronometrar resoluciones del Cubo de Rubik, almacenar estadísticas y analizar el progreso del usuario.
Este proyecto sigue una arquitectura **MVC (Modelo-Vista-Controlador)** y una metodología de desarrollo ágil e incremental.

## 📂 Estructura del Proyecto
Para facilitar el trabajo en equipo, hemos dividido el código siguiendo el patrón MVC. Por favor, respetad la ubicación de los ficheros:

```text
rubikstimer_project/
├── app/
│   ├── __init__.py           # Inicializador de la app (Factoría de aplicación)
│   ├── config.py             # Configuración global (Bases de datos, claves secretas)
│   │
│   ├── models/               # [M] MODELO (Backend/Datos)
│   │   ├── __init__.py
│   │   ├── solve.py          # Clase 'Solve': define el intento (tiempo, scramble)
│   │   └── session.py        # Clase 'Session': lógica de medias (Ao5, Ao12)
│   │
│   ├── templates/            # [V] VISTA (Frontend/HTML)
│   │   ├── base.html         # Plantilla base (menú y estructura común)
│   │   ├── index.html        # Página principal (Cronómetro)
│   │   └── stats.html        # Página de estadísticas y gráficas
│   │
│   ├── static/               # [V] RECURSOS ESTÁTICOS (Frontend)
│   │   ├── css/
│   │   │   └── style.css     # Estilos visuales
│   │   ├── js/
│   │   │   ├── timer.js      # Lógica del cronómetro (Ejecutado en navegador)
│   │   │   └── stats.js      # Renderizado de gráficas (Chart.js)
│   │   └── img/
│   │
│   └── controllers/          # [C] CONTROLADOR (Backend/Rutas)
│       ├── __init__.py
│       └── main_controller.py # Define las rutas (@app.route) y conecta M con V
│
├── run.py                    # Punto de entrada (Ejecutar para iniciar servidor)
├── requirements.txt          # Dependencias (Flask, SQLAlchemy, etc.)
└── .gitignore                # Archivos ignorados por Git (no tocar)
```

## Guía Detallada de Ficheros y Carpetas

### 1. Raíz del Proyecto (Gestión y Configuración)
Estos archivos son para la gestión del proyecto, no contienen lógica del cronómetro.

__.gitignore__: Le dice a Git qué archivos NO subir al repositorio (como archivos temporales, carpetas de compilación __pycache__ o contraseñas locales). Es vital para evitar conflictos entre los 3 compañeros.

__requirements.txt__: Lista de librerías necesarias (ej: Flask, SQLAlchemy). Permite que tus compañeros instalen todo con un comando (pip install -r requirements.txt) y tengan el mismo entorno de desarrollo.

__run.py__: El archivo que "enciende" el servidor. Importa la aplicación de la carpeta app y la ejecuta.

__README.md__: Documentación básica. Explica cómo instalar y ejecutar el proyecto.

### 2. Carpeta app/ (El Núcleo del Software)
__init__.py: Transforma la carpeta en un paquete. Aquí se inicializa la base de datos y se conectan el Modelo, la Vista y el Controlador.

### 3. Carpeta app/models/ (El Modelo - M)
Contiene la representación de la información y reglas de negocio, independiente de la interfaz.

__solve.py__: Clase Solve. Define la estructura de la tabla de base de datos para un intento (ID,   tiempo en milisegundos, scramble, fecha).

__session.py__: Lógica para agrupar intentos y métodos de cálculo (media de 5, media de 12). Aquí reside la "lógica pesada" del backend.

### 4. Carpeta app/templates/ (La Vista - V)
Contiene los archivos HTML. En Flask, las vistas interactúan con el modelo a través del motor de plantillas (Jinja2).

__base.html__:Plantilla maestra. Contiene el menú de navegación, el pie de página y los imports de CSS/JS que se repiten en todas las páginas. Evita duplicar código (principio DRY mencionado en apuntes de XP ).

__index.html__: La pantalla principal. Hereda de base.html y contiene el contenedor donde se mostrarán los números grandes del cronómetro.

__stats.html__: Página para visualizar tablas de tiempos y gráficas de progreso.

### 5. Carpeta app/static/ (Recursos del Cliente)
Archivos que el navegador descarga tal cual. Importante: Aquí va la lógica "en tiempo real".

__css/style.css__: Estilos visuales (colores, fuentes, diseño responsive).

__js/timer.js__: CRÍTICO. Contiene el código JavaScript que escucha el evento keydown (barra espaciadora), cuenta los milisegundos en el navegador y, al parar, envía los datos al servidor mediante una petición POST.

__js/stats.js__: Código para renderizar gráficas (usando librerías como Chart.js) basado en los datos que envía el backend.

### 6. Carpeta app/controllers/ (El Controlador - C)
Gestiona la entrada del usuario y orquesta la respuesta.

__main_controller.py__: Define las rutas URL (Endpoints).

@route('/'): Carga el modelo necesario y renderiza index.html.

@route('/save-time', methods=['POST']): Recibe el tiempo del timer.js, valida que sea correcto, llama a models/solve.py para guardarlo en la base de datos y devuelve "OK".

## 🚀 Cómo empezar (Setup)

TODO (Clonar repositorio, Crear entorno virtual, instalar dependencias y ejecutar el servidor)

