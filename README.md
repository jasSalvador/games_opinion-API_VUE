# games_opinion_m6

# Proyecto de Opiniones de Juegos

Proyecto desarrollado con **Vue.js** que permite a los usuarios agregar, editar y eliminar opiniones sobre diferentes juegos. La lista de juegos disponibles es dinamica y proviene del consumo de una API externa. El sitio utiliza rutas dinámicas y estáticas, gestionadas por Vue Router, para navegar entre las distintas vistas de manera eficiente. El diseño y la funcionalidad están optimizados siguiendo los requerimientos establecidos.

---

## Funcionalidad

### Home
- Muestra una lista de juegos disponibles obtenida mediante el consumo de una API externa.
- Permite:
  - Acceder a la vista de opiniones de un juego mediante un botón.
  - Dar "like" a un juego, y acceder a la vista de "Administración".

2. **Opiniones**:
   - Los usuarios pueden:
     - Crear opiniones sobre un juego.
     - Editar y eliminar sus opiniones.
     - Ver todas las opiniones relacionadas con el juego.
   - Las opiniones se almacenan en el `localStorage` para persistencia de datos.

3. **Administración**:
   - Al dar "Like" a un juego, el usuario es redirigido a esta vista:
   - En esta vista los usuario pueden:
     - Ingresar su nombre y contraseña mediante un formulario.
     - "Comprar" coins asociados al juego.


## Características principales

1. **Consumo de API**:

   - Obtención dinámica de juegos desde una API para mostrarlos en la página inicial.
   - Actualización automática de la lista de juegos al cargar la página.

2. **Rutas dinámicas y estáticas**:
   - Navegación entre las vistas "Home", "Opiniones" y "Administración".
   - Ruta dinámica para identificar el juego del cual se opina o se da like.
   - Ruta `404` para URLs no válidas.

3. **Optimización**:
   - Uso de directivas de Vue.js como `v-bind`, `v-for`, `v-if`, `v-model`, `v-text` y `v-on` para gestionar datos dinámicos e interacción del usuario.


## Instalación y configuración

**Clonar el repositorio**

## Instalar dependencias:
npm install

### Ejecutar el servidor:
npm run serve

### Abrir en el navegador:
La aplicación estará disponible en http://localhost:8080.

