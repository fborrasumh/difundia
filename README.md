# DifundIA

La comunicación de una asociación de pacientes, hecha en un paso. Aplicación web de un solo fichero, del curso «IA para asociaciones de pacientes» del Instituto ProPatiens y la Cátedra del Paciente de la Universidad Miguel Hernández de Elche.

**Usar la app:** https://fborrasumh.github.io/difundia/ · **Portal del curso:** https://fborrasumh.github.io/propatiens/

**Idiomas:** castellano (por defecto), català, euskara, galego, English y português; selector en la barra superior (o `?lang=ca`, `?lang=eu`, `?lang=gl`, `?lang=en`, `?lang=pt` en la URL).

## Qué hace

Tres pasos pensados para el voluntariado:

1. **Lo que ya tenéis.** Subir el perfil de la asociación (JSON) y, si se quiere, documentos, folletos o boletines anteriores (Word, PDF, PowerPoint, texto o imágenes). Todo es opcional.
2. **La idea.** Escribirla en una o dos frases y, si la hay, la fecha. Si hace falta inscribirse, se pega el enlace del formulario (Google Forms u otro) o se crea uno en Google con un botón (ver «Inscripción online»).
3. **Listo.** En una sola llamada a la IA salen: publicación para Facebook e Instagram, publicación corta (X, Bluesky o Threads), WhatsApp, boletín, noticia para la web, nota de prensa, versión de lectura fácil, briefing para Canva y calendario de publicación. Cada texto se copia con un botón y todo se descarga en Word. Con «¿Cambiar algo?» se rehacen todos los textos con una indicación en palabras normales.

**Imágenes y documentos listos, sin IA y sin red.** Con el kit de marca del perfil (logo, color principal, color secundario y eslogan), la app:

- dibuja en PNG la publicación cuadrada (1080 × 1080), la story (1080 × 1920), un cartel A4 para imprimir y la cabecera del boletín (1200 × 400), siempre con la misma plantilla;
- maqueta el boletín en HTML como un correo (tablas y estilos en línea, 600 px) y la nota de prensa en A4 con membrete;
- abre cualquiera de ellos en una ventana de impresión para guardarlo como PDF (texto nítido y seleccionable);
- si hay enlace de inscripción, añade su código QR a la publicación cuadrada, la story y el cartel A4;
- redacta el texto alternativo de las imágenes y avisa si los colores elegidos no dan contraste suficiente (WCAG 4,5:1).

La tipografía (Poppins, SIL Open Font License) va incrustada para que imágenes y PDF salgan iguales en cualquier ordenador.

Si el perfil está vacío, la app lo completa con lo que digan los documentos (solo los campos vacíos) y se puede descargar para las demás apps.

## Inscripción online

En el paso de la idea, el recuadro «Inscripción online» admite el enlace de cualquier formulario. El enlace va a la IA, que lo copia tal cual en las publicaciones, no se marca como ajeno y sale como código QR en las imágenes (el QR se dibuja en el navegador, sin red).

Si la asociación aún no tiene formulario, «Crear mi formulario en Google» abre una aplicación web de Google Apps Script con los datos de la actividad (nombre, día y hora, lugar, precio, plazas y fecha límite) y de la asociación (nombre, dirección, correo y web del perfil). La aplicación se ejecuta con la cuenta de Google de quien la usa, así que el formulario y sus respuestas quedan en el Drive de la asociación. Crea las preguntas de inscripción, la información básica de protección de datos y las autorizaciones de imagen y de comunicaciones, lo publica y vuelve a DifundIA con el enlace (`?formulario=…`). El código y la guía para implementarla están en [fborrasumh/propatiens/materiales/formulario_webapp](https://github.com/fborrasumh/propatiens/tree/main/materiales/formulario_webapp); su dirección va en la constante `FORM_APP` (vacía: solo se puede pegar el enlace).

## Qué comprueba el código (la IA propone, el código comprueba)

- **Legibilidad** con el índice de Fernández-Huerta (solo en castellano y en textos de 25 palabras o más).
- **Longitud** de la publicación corta (280 caracteres).
- **Expresiones estigmatizantes** («sufre», «padece», «los diabéticos», metáforas de lucha…), con alternativa centrada en la persona, en los seis idiomas.
- **Enlaces ajenos**: los que no son de la web, las redes o las fuentes aprobadas del perfil, ni aparecen en el material.
- **Cifras nuevas**: números que no están en los documentos, la idea, el perfil ni la fecha.
- **Huecos `[COMPLETAR]`** que la IA deja cuando falta un dato, en lugar de inventarlo.
- **Afirmaciones de salud**: cada una debe tener una cita literal de los documentos (✓, comprobada por código) o una fuente aprobada del perfil (◐, la cita no se puede comprobar en el navegador); si no, se marca (⚠).
- **Calendario**: la IA propone los días relativos y el código calcula las fechas; las fechas clave del perfil (dd/mm) se calculan por código.

## Perfil común de la asociación

El mismo archivo JSON sirve en JuntIA, DifundIA, SubvencIA y EncuestIA: se rellena en cualquiera, se descarga y se sube en la siguiente.

```json
{
  "formato": "perfil-asociacion-pacientes",
  "version": 1,
  "actualizado": "2026-11-06",
  "app": "DifundIA",
  "nombre": "", "ambito": "", "territorio": "", "web": "", "email": "", "direccion": "",
  "mision": "", "publicos": "", "tono": "", "redes": "", "hashtags": "", "evitar": "",
  "fuentes": ["https://…"],
  "fechas": ["14/11 Día Mundial de la Diabetes"],
  "eslogan": "", "color1": "#1F6FB2", "color2": "#F2A541",
  "logo": "data:image/png;base64,…"
}
```

`ambito` es la enfermedad o condición; `email` y `direccion`, los datos de contacto que usa la cláusula de protección de datos del formulario de inscripción; `color1`, `color2` y `logo` forman el kit de marca (el logo va dentro del JSON, reducido a 600 px, y nunca se envía a la IA); `fuentes`, las fuentes aprobadas para afirmaciones de salud; `fechas`, una por línea con `dd/mm` y nombre. Al subirlo se aceptan también listas escritas como texto (una por línea) y se ignoran los campos desconocidos.

## Cómo se usa la IA

Con la propia clave de OpenAI, Google Gemini o Anthropic Claude. La clave se guarda solo en el navegador y cada persona paga su propio uso. No hace falta servidor.

## Privacidad

Perfil, documentos y textos creados se guardan solo en el navegador (IndexedDB). Al crear, la idea, el perfil y el texto de los documentos salen hacia el proveedor de IA con correos, DNI/NIE, teléfonos e IBAN enmascarados; antes del primer envío se muestra lo que sale y se avisa de posibles nombres de personas. Las imágenes no se pueden enmascarar: se avisa antes de enviarlas. Solo documentación anonimizada.

## Límites

- No publica nada: copiar y publicar lo hace la persona.
- No da consejos clínicos ni dosis, y no garantiza que un texto sea correcto: hay que revisarlo siempre.
- La comprobación de estigma es una lista de expresiones, no un juicio: puede no detectar todas ni acertar siempre.
- Las cifras pequeñas (hasta 12) no se comprueban, para no marcar horas o cantidades corrientes.
- Una fuente aprobada se reconoce por su dirección o su nombre; el contenido de la página no se comprueba.
- Las plantillas de imagen son fijas: no se pueden mover elementos como en Canva (para eso está el briefing).
- En el boletín HTML el logo va incrustado: algunos programas de correo (Gmail, por ejemplo) no muestran imágenes incrustadas. Para enviarlo por correo, sustituid el logo por la dirección de una imagen alojada en vuestra web o en vuestro programa de envíos.
- La app no comprueba quién aparece en las fotos: si añadís fotos de personas, necesitáis su consentimiento.
- Probada con IA simulada de los tres proveedores; no con una clave real.

## Autoría

Fernando Borrás Rocher (Universidad Miguel Hernández de Elche) · ORCID [0000-0002-5519-4573](https://orcid.org/0000-0002-5519-4573)

Licencia MIT.
