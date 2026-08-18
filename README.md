# Diane Nails

Sitio web para Diane Nails con landing page, galeria conectada a Firebase, panel administrativo y portal de artistas.

## Archivos principales

- `index.html`: pagina publica principal.
- `admin.html`: panel administrativo para citas, cobros, clientes, servicios, galeria y dias cerrados.
- `artistas.html`: portal interno para que las artistas vean ganancias semanales y servicios realizados.
- `firebase-config.js`: configuracion publica de Firebase usada por la web.

## Seguridad

- No pongas llaves privadas de IA, pagos ni servicios externos en HTML o JavaScript del navegador.
- El chatbot esta en modo respuesta local para evitar exponer llaves privadas. Para IA real, usa una Cloud Function o backend que proteja la llave.
- El registro publico del admin esta deshabilitado. Crea usuarios administradores desde Firebase Console.
- Revisa las reglas de Firestore antes de publicar para que solo usuarios autorizados puedan leer/escribir datos administrativos.
- El portal de artistas usa los cobros con campo `artistName`; cada cuenta solo ve sus datos si su correo esta registrado en `Admin -> Artistas`.
- La sesion del portal de artistas esta aislada de la sesion administrativa: abrir `artistas.html` siempre requiere una cuenta de artista independiente.
- Cada pestana del portal conserva su propia sesion, por lo que dos artistas pueden iniciar con correos distintos al mismo tiempo sin reemplazarse entre ellas.
- Para dar acceso a una artista: abre `Admin -> Artistas`, autoriza su correo y asigna su nombre. Luego la artista abre `Portal artistas` y usa `Crear mi contrasena` para activar su cuenta.
- Las contrasenas nunca se guardan en Firestore. Si la artista la olvida, puede usar `Olvide mi contrasena` para recibir un enlace seguro de Firebase en su correo.
- Los cobros antiguos sin artista no aparecen en una cuenta de artista hasta que se reasignen desde Firestore o se vuelvan a registrar con artista.
- El detalle semanal de cada artista incluye sus cobros y todas las citas que tenga asignadas durante esa semana, sin importar su estado.
- La seccion `Agenda semanal` agrupa las citas de la artista por cada dia, de lunes a domingo, ordenadas por hora.
- La seccion `Clientes` del panel administrativo guarda nombre, WhatsApp y atributos mediante emojis; permite buscar, editar y eliminar registros.
- Al crear una cita manual desde Administración se puede elegir una clienta del directorio para completar automáticamente su nombre, WhatsApp y atributos.
- Las artistas ven junto al nombre de cada clienta los emojis de clasificación guardados en el directorio, tanto en la agenda como en el detalle semanal.
- La seccion administrativa `Recordatorios` muestra citas de las proximas 24 horas y abre WhatsApp con un mensaje preparado. El envio es manual y no requiere una API de pago.

## Siguiente mejora recomendada

Separar CSS/JS en archivos propios y agregar fotos reales de trabajos en la galeria para mejorar conversion.
