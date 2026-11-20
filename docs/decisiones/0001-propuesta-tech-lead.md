# Propuesta del Tech Lead: tecnología, datos y división del trabajo

**Estado:** propuesta, pendiente de aprobación del stakeholder.

## 1. Tecnología

| Opción | Pros | Contras |
|---|---|---|
| **A. App web instalable (PWA)**, p. ej. React + Vite | Un solo código para Android e iPhone. Se instala desde un enlace. Actualizaciones instantáneas. Hosting gratis (Vercel, Netlify, GitHub Pages). Fácil de aprender. | Las notificaciones en iPhone son limitadas. El temporizador puede fallar con la pantalla bloqueada. Instalarla requiere "Agregar a pantalla de inicio" (una vez). |
| **B. App nativa multiplataforma** (React Native con Expo, o Flutter) | Se siente como una app de verdad. Notificaciones y temporizador confiables. | Instalación permanente vía tienda: en Android un APK es fácil; en iPhone hace falta Apple Developer (USD 99/año) o TestFlight. Más compleja y con actualizaciones más lentas. |
| **C. Sin código** (Glide, FlutterFlow, AppSheet) | Muy rápido, sin programar. | La lógica de nutricionista y chef queda limitada. Suscripciones pagas, dependencia del proveedor y poco aprendizaje. |

**Recomendación: A.** El temporizador se resuelve con un aviso sonoro mientras
la app está abierta y la API Wake Lock mantiene la pantalla encendida durante
la receta. Si después las notificaciones son indispensables, se puede migrar
a B, reutilizando el catálogo y la lógica del chef.

## 2. Datos

Las **recetas y el catálogo** van en un archivo JSON dentro del código,
versionado en git. No necesitan base de datos.

Los **datos de ella** (gustos, metas, historial):

| Opción | Pros | Contras |
|---|---|---|
| **A. Solo en el teléfono** (IndexedDB/localStorage) | Gratis, sin cuentas ni contraseñas, funciona sin internet, máxima privacidad. | Si cambia de teléfono o borra los datos del navegador, se pierden. Nadie puede ayudarla a distancia. |
| **B. En la nube** (Supabase o Firebase, plan gratis) | Respaldo, varios dispositivos, tú puedes ajustarle las metas a distancia, y a futuro su nutricionista podría entrar. | Necesita inicio de sesión. Más complejidad. Son datos de salud, así que hay que cuidar la privacidad (Ley 19.628 y Ley 21.719). |
| **C. Local primero, nube después** | Se parte simple y no se cierra la puerta a la nube. | Hay que diseñar bien la capa de datos desde el inicio, y la migración es trabajo extra. |

**Recomendación: C.** En el MVP los datos se guardan en el teléfono, con un
botón "Guardar respaldo" y una capa de datos aislada. Si la prueba de 2
semanas funciona, se conecta Supabase.

## 3. División del trabajo

| Opción | Pros | Contras |
|---|---|---|
| **A. Por capas** (datos → lógica → pantallas) | Base técnica sólida. | No hay nada usable hasta el final y mamá no puede probar temprano. |
| **B. Por rebanadas verticales** (cada tarea entrega algo usable) | Mamá puede probar desde la primera semana y el feedback llega temprano. | Algo de reorganización del código en el camino. |
| **C. Por pantallas** | Fácil de entender. | La lógica compartida, como la del chef, queda repartida y duplicada. |

**Recomendación: B.** Rebanadas propuestas:

1. Esqueleto: app instalable, publicada en internet, con pantalla "Hola".
2. Catálogo de 18 platos + botón "¿Qué hago hoy?" + "Dame otra opción".
3. Onboarding de gustos que filtra las propuestas.
4. "Lo cociné" + historial + no repetir.
5. Receta paso a paso con íconos.
6. Nutricionista: metas semanales que guían al chef.
7. Temporizador + pantalla siempre encendida durante la receta.
8. Respaldo de datos.

Flujo por tarea: rama → Desarrollador → pull request → QA → merge → se
publica sola. Desde la rebanada 2, mamá ya puede usarla.
