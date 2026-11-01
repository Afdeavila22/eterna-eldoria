# ETERNA · Crónicas de Eldoria

Una entrega web autónoma de un RPG táctico isométrico original. No usa paquetes, imágenes externas ni compilación: abre `index.html` y juega.

## Qué está implementado y se puede probar ahora

- **Fase 1 — creación:** tres clases seleccionables (Guardián, Oráculo, Explorador), nombre y apariencia/árbol de talentos por clase.
- **Fase 2 — mundo:** mapa isométrico táctil con movimiento por casillas, Puerto Lúmina y Bosque Virel, portales, NPC, diálogo, mercado y mapa regional.
- **Fase 3 — progreso:** misión guiada, encuentro táctico por turnos, victoria, nivel, monedas, inventario, equipo y talentos que se desbloquean al subir de nivel.
- **Móvil:** interfaz responsive, botones grandes, `viewport-fit`, navegación inferior y persistencia local con `localStorage`.

## Fase 4: estado realista

La pantalla de Gremio y sus personajes conectados son **una simulación de interfaz local**. Las partidas, creación de personaje, progreso e inventario se guardan solamente en el navegador actual. Aún no existe autenticación, servidor de juego, chat, combate entre jugadores ni sincronización entre dispositivos.

Para multijugador real, una ruta concreta es:

1. Crear API en Node.js (Fastify/NestJS) con PostgreSQL y Prisma para cuentas, personajes, inventario y misiones.
2. Añadir Auth.js, Clerk o Supabase Auth para registro, inicio de sesión y sesiones seguras.
3. Usar Socket.IO o Colyseus para presencia, salas, movimiento validado por servidor y encuentros cooperativos/competitivos.
4. Mover las reglas de recompensa y combate al servidor; el cliente nunca debe decidir oro, nivel o botín.
5. Desplegar la API en Render/Fly.io/Railway y la base de datos en Supabase/Neon; configurar dominio, HTTPS, CORS y variables secretas en el proveedor (nunca en este repositorio).

## Publicar la versión actual

### Netlify Drop (sin terminal)

1. Crea una carpeta que contenga `index.html`, `styles.css` y `game.js`.
2. Entra a [Netlify Drop](https://app.netlify.com/drop) y arrastra esa carpeta.
3. Netlify dará una URL HTTPS que ya funciona en móvil. No hay comando de compilación ni carpeta de publicación: el directorio raíz es el sitio.

### GitHub Pages

1. Sube estos tres archivos a la raíz de un repositorio de GitHub.
2. Abre **Settings → Pages**, selecciona **Deploy from a branch**, rama `main` y carpeta `/(root)`.
3. Guarda; GitHub mostrará la URL pública en esa misma pantalla.

### Verificación local

Al ser estático puedes abrir `index.html` directamente. Para simular el comportamiento de una web publicada, desde esta carpeta ejecuta `python3 -m http.server 8080` y abre `http://localhost:8080`.

## Estructura

- `index.html` — pantallas y estructura accesible.
- `styles.css` — arte isométrico procedural y diseño responsive.
- `game.js` — estado, interacción, combate y guardado local.

## Próxima iteración recomendada

Crear el proyecto de servidor antes de añadir más contenido. Define el contrato de datos de personaje, inventario y combate, implementa autenticación y luego sustituye `localStorage` por una API autenticada. Así el contenido de nuevos mapas no tendrá que reescribirse después.
