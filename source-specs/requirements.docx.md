**Scope General del Proyecto Woppa (MVP)**

**Perspectiva: Desarrollo de Software**

**Descripción General:**

El presente documento define el alcance funcional y técnico del desarrollo de la Fase 1 \- MVP de Woppa, una aplicación móvil y un panel web básico para conectar consumidores con comercios mediante promociones tipo 2x1 y descuentos simples. El enfoque de este MVP es validar hipótesis de negocio y adopción, sin implementar aún automatizaciones avanzadas o funciones de fidelización.

Alcance Incluido (In-Scope)

1\. Frontend Mobile (Usuarios Finales \- iOS & Android):

* Visualización de mapa con promociones geolocalizadas sin necesidad de registro.

* Filtros por categoría (ej.: Gastronomía, Farmacia).

* Listado de promociones.

* Visualización de detalle de la promoción.

* Registro e inicio de sesión (email/contraseña o Google OAuth).

* Redención de promociones mediante cupón digital con código único.

2\. Frontend Web (Comercios):

* Formulario de carga de promociones por los comercios (datos básicos, imágenes, ubicación, tipo de descuento).

* Dashboard simple para visualizar promociones activas, estado y redenciones.

3\. Backend & APIs:

* Autenticación de usuarios y comercios.

* Gestión CRUD de promociones.

* Generación de códigos únicos de redención.

* Almacenamiento de imágenes de productos.

* Métricas básicas de redención y visualización.

4\. Validación Manual (Equipo Woppa):

* Backoffice o herramienta interna mínima para validar o rechazar promociones antes de su publicación.

Fuera de Alcance (Out of Scope)

* Pagos digitales o integración con sistemas de pago.

* Automatización de redención en punto de venta (ej.: QR, NFC, POS).

* Notificaciones push o email masivo.

* Gestión avanzada de usuarios o perfiles (favoritos, historial).

* Dashboard avanzado con reportes, exportaciones o gráficas.

* Programa de referidos, gamificación o viralización (fase futura).

* IA para análisis automático de contenido.

Assumptions (Supuestos)

1. El MVP está enfocado en validación rápida del modelo de negocio, no en escalabilidad masiva.

2. La redención será manual por parte del comercio, sin integraciones tecnológicas en el local.

3. El uso de OAuth con Google se limita a simplificar el registro de usuarios y no se requiere integración con otros servicios de Google.

4. Los códigos de redención se validarán visualmente y no requieren verificación en tiempo real en el comercio.

5. Las promociones estarán limitadas a un número acotado de categorías y subcategorías en esta primera fase.

Constrains (Restricciones)

* El proyecto debe ajustarse a un tiempo de desarrollo acotado para su entrega inicial.

* El stack tecnológico debe priorizar agilidad y bajo costo operativo (ej.: frameworks híbridos, Firebase, Google Forms para validación).

* Cumplimiento con LGPD (Ley General de Protección de Datos de Brasil) y mejores prácticas de seguridad de datos.

* El sistema debe ser accesible para comercios con bajo nivel de digitalización.

* Las imágenes de productos deben ser optimizadas para bajo consumo de datos en móviles.

**Riesgos Técnicos y Operativos**

| Riesgo | Impacto | Mitigación |
| :---: | ----- | :---: |
| Baja adopción de comercios o desinterés en subir promociones. | Alto | Implementar onboarding simple \+ acompañamiento manual. |
| Dependencia de geolocalización en móviles (usuarios sin permisos). | Alto | Definir comportamiento en caso de denegación (zona por defecto). |
| Validación manual ineficiente o insuficiente si el volumen crece. | Alto | Definir criterios claros y evaluar automatización en futuras fases. |
| Dificultad de escalado sin un backend robusto si la demanda crece rápidamente. | Alto | Elegir arquitectura modular y escalable desde el inicio. |
| Fricción en el registro o desconfianza del usuario para redimir ofertas. | Medio | Minimizar datos requeridos, mostrar valor antes del registro. |
| Riesgo de fraude o uso indebido de cupones. | Medio | Limitar generación de códigos por usuario y sesión. |

**Requerimientos**

**Épica 1: Visualización de promociones sin login (exploración geolocalizada)**

**2\. Requerimientos del Wiframe 1** 

**![Map View](/woppa-wireframe-1-mapa.png)**

**Descripción General:**

**Permitir a los usuarios explorar promociones geolocalizadas cercanas sin necesidad de registrarse o iniciar sesión, reduciendo la fricción inicial y aumentando la probabilidad de conversión al mostrar valor inmediato.**

**2.1 Geolocalización**

* La aplicación debe solicitar permiso de ubicación al usuario al acceder a esta pantalla – Sí

* El mapa debe centrarse automáticamente en la ubicación actual del usuario si se concede el permiso  \- R. Hacer una comparación con las aplicaciones similares y ver cuál radio quieren incluir, hacer una opción para expandir o disminuir el radio – puede ser una barra.

* Si el usuario no otorga permisos, se debe mostrar una ubicación por defecto (por ejemplo: São Paulo centro). Si – A determinar el Código Postal de la zona que queremos ver por default 

**2.2 Visualización del Mapa**

* El mapa debe mostrar una cuadrícula urbana simplificada, optimizada para identificar fácilmente los puntos de promoción.

* Los íconos de promociones deben colocarse en el mapa según su ubicación geográfica.

**2.3 Promociones Geolocalizadas**

* Las promociones deben visualizarse mediante íconos circulares diferenciados por categoría:

  * Gastronomía: ícono de tenedor y cuchillo, color rosa (\#E573E2).

  * Farmacia: ícono de cápsulas o cruz médica, color verde (\#3AD4AC). – Ajustar el ícono de la categoría de la farmacia, un símbolo más universal. Los colores se pueden cambiar en cualquier momento. (Backlog)

* Cada ícono puede incluir un pequeño número indicando cuántas promociones hay en esa ubicación.

* Al hacer clic en un ícono, debe abrirse una previsualización (tooltip o modal) con detalles básicos de la promoción (nombre del comercio, tipo de oferta).

**2.4 Filtros por Categoría**

* En la parte superior del mapa deben incluirse dos botones de filtro: “Gastronomía” y “Farmacia”.

* Al activar o desactivar estos filtros, el mapa debe mostrar solo las promociones correspondientes a la categoría seleccionada. El estado seleccionado debe de permanecer durante toda la sección no se olvida una vez accedemos a otras partes de la app.

  * *Toni: Está extraño que tenga que clickear el opuesto, para ver por ej sólo gastronomía debería de clickear farmacia (para desactivarlo).*

* El estado activo del filtro debe estar visualmente resaltado.

* Si no se selecciona ninguna categoría vemos todas las promociones por defecto 

**2.5 Contador de Descuentos**

* En la parte inferior de la pantalla debe aparecer un mensaje que indique la cantidad de descuentos disponibles (ej: “12 descuentos cerca”, cambiar wording ya que no son realmente los cercanos). – Cambiar el símbolo de porcentaje pro algún otro que represente ahorro. 

**2.6 Botón de Registro**

* Debe incluirse un botón “Registrarse” visible en la parte superior derecha. – Cambiar el lenguaje a más amigable – ex. Quiero registrarme, que sea más cercano con el usuario. 

* Este botón debe redirigir al flujo de onboarding, pero su interacción no debe ser obligatoria para explorar las promociones.

* El diseño debe resaltar el botón sin distraer del contenido principal.

**2.7. Requerimientos de Experiencia de Usuario (UX)**

* La navegación debe ser fluida, sin pantallas de carga extensas ni interrupciones.

* No debe solicitarse ninguna acción obligatoria antes de mostrar las promociones.

* La interfaz debe ser clara, limpia, con buena jerarquía visual y colores consistentes con el branding de Woppa.

* El diseño debe transmitir confianza, beneficio inmediato y facilidad de uso.

**2.8. Consideraciones Técnicas**

* Debe garantizarse un tiempo de carga rápido del mapa, incluso en conexiones móviles.

* La app debe manejar correctamente los estados sin conexión o sin permisos de geolocalización.

* Toda lógica de filtrado, renderizado de íconos y contador debe ejecutarse en tiempo real sin recargar la pantalla.

**Dudas**

Comportamiento de los íconos en el mapa

* ¿Qué debe ocurrir al tocar un ícono de promoción? (tooltip, modal) – Incluir uno de los dos. 

* ¿Cómo se muestran múltiples promociones en la misma ubicación? Modal o Tooltip o Bottom sheet

Lógica del contador de descuentos

* ¿"Descuentos cerca" significa dentro de qué radio o zona? – Revisar otras aplicaciones con sevricios similares y la opción expandir o disminuir ese radio. 

* ¿El contador refleja solo lo visible en pantalla o todo lo disponible geográficamente? Al inicio el contador muestra TODAS los descuentos disponibles en tiempo real, con el objetivo de despertar la curiosidad del usuario. Si se selecciona un filtro se muestra el total de ofertas para esa categoría solamente

Filtros por categoría

* ¿Se pueden activar ambas categorías al mismo tiempo o son excluyentes? Sí, se pueden activar ambas categorías. 

* ¿Se planea escalar a más categorías en el futuro? (¿diseño flexible?) Sí, se quiere escalar a más categorías. 

Escenario sin permisos de geolocalización

* ¿Cuál es la ciudad predeterminada si no se otorgan permisos? Sao Pablo 

* ¿Debe mostrarse un mensaje que invite a activar ubicación? Sí – Se muestra solamete si no la tenés activa, si ya la tenés activa te pide permiso la primera vez para acceder a la misma 

* Incluir un botón flotante para regresar a la ubicación actual, 

* Permitir al usuario activar la ubicación desde la aplicación desde ese botón mostrando un estilo distinto para los 2 estados.

Botón “Registrarse”

* ¿Hacia dónde redirige el botón de registro? (pantalla interna)

* ¿Debe explicitarse algún incentivo para registrarse desde esta pantalla? Por ahora no, para que el usuario pueda explorar.

 Visualización de múltiples íconos

* ¿Cómo se evita la sobreposición de íconos en zonas densas? (Número de promociones por ícono)

  * *Toni: Ok, son clusters a nivel cercanía, y luego a nivel comercio va a haber un momento que no se puede separar mas (cuando un comercio tiene varias promos por ej)*

**Supuestos**

* El usuario puede visualizar y explorar el mapa completo sin necesidad de registrarse.

* Los datos de geolocalización se solicitan al iniciar, pero la app funciona sin ellos (con ubicación por defecto).

* Solo existen dos categorías (gastronomía y farmacia) en esta etapa del MVP.

* Cada categoría tiene un color e ícono asignado y fijo.

* Ambas categorías están activadas por defecto en la primera carga.

* Si hay más de una promoción en la misma ubicación exacta, se muestra un número sobre el ícono.

* No se requiere ningún paso adicional para visualizar los detalles básicos de una promoción al tocar el ícono.


**3\. Requerimientos del Wiframe 2**

**![Offers List](/woppa-wireframe-2-listado-ofertas.png)**

**Descripción General**

Esta pantalla muestra al usuario una lista de promociones disponibles cerca de su ubicación actual. El objetivo es facilitar la exploración detallada de cada oferta con foco en claridad, simplicidad y urgencia para redimir. Es una alternativa complementaria a la vista de mapa.

**3.1 Geolocalización y cabecera**

* La ubicación actual del usuario debe mostrarse en la parte superior, junto con un ícono de geolocalización.

* El contador de “descuentos cerca” debe estar sincronizado con las promociones listadas en pantalla. – Cambiar el wording, porque queremos mostrar todos los descuentos existentes en tiempo real, y la palabra cerca hace alusión al radio elegido. 

* Se debe incluir un botón visible de "Registrarse", que redirige al flujo de onboarding sin bloquear la navegación.

**3.2 Listado de promociones**

Cada promoción en la lista debe incluir los siguientes elementos:

**Componentes visibles por promoción:**

* Imagen del comercio o del producto en miniatura (placeholder si no hay imagen disponible).

* Categoría del comercio mediante ícono en esquina superior derecha del recuadro:

  * Gastronomía: ícono tenedor y cuchillo.

  * Farmacia: ícono de cápsulas. – Cambiar por un símbolo más universal 

* Etiqueta de urgencia o destaque si aplica (ej: “🔥 Solo por hoy”), en color naranja. (Incluir, últimos disponibles \*si quedan pocos\*, \*popular\*, \*mejor calificado\* \- Analizar y definir la lista de etiquetas/urgentes que queremos incluir

  * Toni: Quizás Highlight es un mejor nombre en vez de etiqueta y tener distintos tipos y que sean fijos por ej:

    * Highlight 

    *    \- tipo: 'urgency' | 'popularity' | 'quality' | 'new' | 'exclusive' | 'limitedTime';

    *    \- label

    *    \- color

* Nombre del comercio.

* Detalle de condiciones de uso (ej: días, horarios, exclusiones).

* Etiqueta visual “2x1” (beneficio principal). – Cambiar el “2x1” por “1+1”. Es como les funciona y como lo utilizan en Brasil. 

* Botón de acción **“Obtener oferta”** en color primario (morado), que lleva al flujo de redención.

**3.3 Diseño y organización**

* Las promociones deben estar organizadas verticalmente y priorizar las más cercanas y/o urgentes (referirse a lista de etiquetas) Se va a analizar otras aplicaciones con servicios similares.  

  * 

* El diseño debe ser limpio, con separación clara entre bloques de promociones.

* El botón “Obtener oferta” debe ser claramente visible y estar disponible para todas las ofertas.

**3.5 Requerimientos de Experiencia de Usuario (UX)**

* La información crítica debe ser escaneable: título del comercio, beneficio (1+1), y botón de acción visibles sin necesidad de interacción adicional.

* El diseño debe transmitir urgencia y simplicidad, especialmente en promociones con límite de tiempo.

* No se requiere login para visualizar ni interactuar con los botones de “Obtener oferta”, salvo en el paso de redención.

**3.6 Consideraciones Técnicas**

* La lista debe poder renderizarse dinámicamente desde una API de backend con datos actualizados.

* Debe contemplarse paginación o scroll infinito si la cantidad de promociones excede una cantidad predeterminada.

* El botón de “Obtener oferta” debe redirigir al flujo de redención y, si aplica, verificar si el usuario está registrado (gateo condicional).

* La interfaz debe ser responsive y optimizada para móviles de gama media.

**3.7. Accesibilidad**

* Todos los botones y etiquetas deben ser legibles con contraste suficiente.

* Se deben usar atributos de accesibilidad para lectores de pantalla (ej: alt text para imágenes, roles de botones).

**Dudas:**

**Contenido de las promociones**

* ¿Qué campos son obligatorios para mostrar una promoción en el listado? (¿Imagen, texto, condiciones?)

* ¿Las promociones pueden tener múltiples beneficios o solo se permite un formato fijo tipo “1+1”? – Toda la aplicación es solo ofertas 1+1, es el distintivo 

* ¿Las condiciones de uso pueden ocupar más de una línea? ¿Se debe limitar su longitud? – Solo que se aclare el horario de disponibilidad. De entrada se debe saber cuántas hay disponibles, el comercio y WOPPA van haciendo – Cuando se agota se muestra igual la oferta, pero con un mensaje que diga algún mensaje tipo: Agotado, vuelve pronto, etc. Por cuánto tiempo se quiere seguir mostrando una oferta una vez agotada? – El resto del día. 

**Imágenes de promociones**

* ¿Qué sucede si un comercio no sube imagen? ¿Se usa un placeholder genérico? ¿Por categoría? – Es obligatorio. 

* ¿La imagen es del producto específico o del local/comercio? – La imagen pasa por un equipo de servicio al cliente para revisar los datos de la promoción. Un QA previo a publicar la oferta. 

**Botón “Obtener oferta” – Cambiar el wornding por algo más cercano y amigable ex. “Quiero la oferta”**

* ¿El botón requiere login para funcionar o solo en el paso de redención? – Solo en el paso de la redención 

* ¿Qué flujo exacto sigue el botón: modal, nueva pantalla, redirección condicional? – Vamos directamente a la siguiente pantalla. 

**Etiquetas como “Solo por hoy”**

* ¿Se genera automáticamente según la validez de la promoción o lo define el comercio?  \- Generado por el equipo de WOPPA, el equipo decide internamente cuales promociones quiere etiquetar para evitar que ciertos comercios “abusen” de las etiquetas. 

  * *Toni: Necesidad de backoffice*

* ¿Habrá más etiquetas destacadas como “Novedad”, “Últimos días”, etc.? – Si, hay más etiquetas, analizarlas y definirlas proximamente. 

**Orden y prioridad del listado**

* ¿Cuál es el criterio de orden por defecto? (proximidad geográfica, caducidad, relevancia) – Por cercanía y por la definicón de las etiquetas. 

* ¿Se permitirá ordenar o filtrar las promociones desde esta vista en el MVP? Sí, trabajar en el filtro. 

* Con el botón de registrarse, si el usuario ya tiene cuenta, se mostrará automáticamente la opción de Log in? El app va a reconocer el móvil del usuario? Qué wording se vá a utilizar en este caso en el botón de arriba a la derecha? – Incluir registrarse / Log in – Utilizar el mismo CTA pero con los colores opuestos al botón del registro – El app debe recordar al usuario. / El wording puede ser algo como mi cuenta. 

**Estado de promociones inactivas**

* ¿Qué debe ocurrir con promociones expiradas o agotadas? ¿Se ocultan, se muestran atenuadas, o se eliminan? – Las promociones expiradas o agotadas se muestran disponibles el resto de ese día.

  * *Toni: Vamos a mostrar también promociones expiradas/agotadas en el mapa, o sólo en el listado?*

* ¿Se planea mostrar un aviso tipo “agotado”? Sí – para generar curiosidad

**Supuestos** 

* El usuario no necesita estar registrado para visualizar esta pantalla ni para tocar el botón “Obtener oferta”; se solicitará login o el registro más adelante si es necesario al momento de redimir la oferta. 

* El diseño asume que todas las promociones tendrán al menos un título, condiciones y una etiqueta de beneficio (ej: “1+1”).

* Las imágenes de los comercios son obligatorias.

* Las etiquetas como “Solo por hoy” son opcionales y destacadas manualmente por el equipo de operaciones de WOPPA y no por el comercio.

* Las promociones listadas están activas y disponibles en tiempo real; promociones vencidas o deshabilitadas se muestran durante el resto del día. 

* El botón “Obtener oferta” abre el flujo de redención; si el usuario no tiene cuenta, se le pedirá registrarse en ese momento, si tiene cuenta, y por algún motivo el app no está reconociendo al usuario (cambio de celular, actualización de la app, etc) la aplicación pedirá que se identifique el usuario  (Log in)

* La lista está ordenada por cercanía o relevancia de las etiquetas (por definir).

**4\. Requerimientos del Wiframe 3**

**![Offer Detail](/woppa-wireframe-3-detalle-oferta.png)**

Esta pantalla permite al usuario consultar la información completa de una promoción específica. Su objetivo es brindar claridad, aumentar la confianza del usuario en la oferta, y facilitar la decisión de redención. Representa un paso clave previo a la conversión.

**4.1 Cabecera**

* Incluir barra superior con botón de retorno (flecha hacia atrás).

* Mostrar el nombre del comercio como título de la pantalla.

* Incluir botón de "Registrarse" en la esquina superior derecha, visible pero no obligatorio ó “mi cuenta” si ya está registrado. 

**4.2 Imagen de la promoción**

* Visualizar una imagen representativa del producto o comercio. \- Obligatorio

**4.3 Etiqueta de urgencia**

* Si aplica, debe mostrarse una etiqueta visual como "Solo por hoy" en color naranja. 

* Este elemento es opcional y debe poder controlarse desde el backend – Lo controla el equipo interno de WOPPA, para evitar abusos de los comercios. 

**4.4 Información de la oferta**

**Nombre del comercio:**

* Debe mostrarse de forma destacada.

**Categorías:**

* Etiquetas visuales para categoría principal (ej. Gastronomía) y subcategoría (ej. Sushi y poke).

**Condiciones de uso:**

* Incluir detalle de días y horarios de validez.

* Aclarar exclusiones o restricciones relevantes (por ejemplo, si no incluye bebidas o si no se aceptan reservas).

**Ubicación:**

* Mostrar la dirección del comercio en texto.

* Debe incluirse un mapa con la ubicación marcada. Puede ser un mapa estático o interactivo??? – Discutir la opción del mapa estático y si es posible integrar un botón con la opción de “cómo llegar?”que te redirija a google maps. 

**Beneficio:**

* Mostrar etiqueta visual con el tipo de promoción,  SIEMPRE es "1+1", en una cápsula visible.

**4.5 Acción principal: "Obtener oferta"**

* Incluir botón destacado con el texto "Obtener oferta", ubicado en la parte inferior de la pantalla.- Cambiar el wording por algo más cercano al usuario

* El botón debe estar disponible para todos los usuarios.

* Si el usuario no está registrado, al hacer clic se redirige al flujo de registro antes de continuar con la redención.

**4.6 Requerimientos de Experiencia de Usuario (UX)**

* La disposición de los elementos debe favorecer la lectura rápida y escaneable.

* Toda la información clave debe ser visible sin necesidad de múltiples desplazamientos.

* El diseño debe mantener coherencia visual con el resto del producto.

**4.7. Consideraciones Técnicas**

* Toda la información se debe cargar dinámicamente desde el backend.

* El mapa puede implementarse inicialmente como componente estático por simplicidad, con opción de un botón de “cómo llegar” que te redirija a google maps

* El botón "Obtener oferta" debe incluir lógica condicional según el estado de autenticación del usuario.

**4.8 Accesibilidad**

* Garantizar contraste adecuado entre texto y fondo.

* Asegurar que todos los elementos interactivos cumplan con tamaños táctiles mínimos.

* El mapa debe contar con alternativas accesibles según su implementación (texto alternativo o equivalentes).

**Dudas** 

**Imagen de la oferta**

* ¿La imagen es obligatoria para publicar una promoción? Sí, es obligatorio por parte de los comercios brindar la imagen

**Etiquetas de urgencia**

* ¿La etiqueta “Solo por hoy” se genera automáticamente desde el backend según fecha de vigencia, o se marca manualmente? – Se marca manualmente, lo decide el equipo de WOPPA. Se coordina con el comercio? Ellos pueden “pedir” que se incluya una etiqueta de este tipo? Coordinar la etiqueta de “Solo por hoy”, en un futuro se puede elegir categorías de “los más vendidos” relacionado con tus compras – que el alrgoritmo se base en tu historial de compras. Proponer una lista de 3 etiquetas. 

  * ¿Se prevén otras etiquetas de urgencia como “Últimos días”, “Nuevo”, etc.? – Sí, se analizarán como se menciona previamente: “Solo por hoy”, “Agotado”, “Los más vendidos”(relacionados con tus compras)

**Etiquetas de categoría y subcategoría**

* ¿Las categorías y subcategorías son fijas o deben poder escalar a más opciones en el futuro? – Se pretende escalar en el futuro 

  * ¿Se puede mostrar más de una subcategoría por promoción? Ex. Sushi\&poke/saludable  \- Sí, se puede con base a la oferta 

**Mapa de ubicación**

* ¿El mapa debe ser estático o interactivo en esta fase del MVP? – Rerefirse al requirement del mapa.

  * ¿Qué fuente se usará para la geolocalización (ej. Google Maps, Mapbox)? – Google Maps

**Contenido de la sección de condiciones**

* ¿Existen lineamientos sobre la longitud del texto de condiciones? – Se incluye el horario disponible, condiciones de la promoción (Qué incluye o que no incluye) 

  * ¿Debe mostrarse algún aviso si las condiciones son demasiado extensas (por ejemplo, ver más)? – Solamente se permite dos líneas para que sea más digerible para el usuario. 

**Botón “Obtener oferta”**

* ¿El usuario debe estar registrado para poder redimir la oferta? – Sí 

  * ¿El botón muestra el cupón directamente o navega a otra pantalla? ¿Qué flujo exacto se espera? – Pendiente definir método de pago

**Promociones vencidas**

* ¿Qué debe ocurrir si el usuario accede a esta pantalla con una promoción que ya expiró? Una promoción **expirada NO** se debe mostrar en el listing, una promoción **agotada** se muestra por el resto del día actual  (con etiqueta de “Agotado”-  La oferta queda grayed out. No se puede hacer click, se muestra solo para generar curiosidad. 

  * Agregar la opción de obtener más de una oferta del mismo comercio por parte del mismo usuario (considerando familias, grupos de amigos, estudiantes, compañeros de trabajo, etc) 

  * Para las consdiciones – Inlcuir si se requiere reserva, un mensaje tipo: **Supuestos** Para reservas consultar directamente con el proveedor, se incluyen dos íconos, que lleve a google maps donde se ve la información de,l comercio (número, ubi, etc), y un ícono de IG. \-  Es viable agregar el IG, no tiene complejidad as per Toni, se debe pedir al comercio que ingrese su IG en el form, en un campo específico. 

  * 

* El usuario puede acceder a esta pantalla sin estar registrado, y se le solicitará registro solo al momento de redimir la oferta. (Si aún no es usuario)

* Las etiquetas de categoría y subcategoría se definen por el comercio al momento de cargar la promoción y son gestionadas por un equipo interno de QA de WOPPA 

* La promoción enviada por el comercio se revisa por el equipo de WOPPA – SLA de 12 hrs para hacer la oferta pública. 

* La promoción está activa y vigente al momento de mostrar esta pantalla; promociones vencidas no son accesibles.

* El mapa es un componente embebido que puede inicialmente ser una imagen estática, con opción a de boton de como llegar – redirigir a google maps 

* El botón “Obtener oferta” ejecuta una acción condicional: si el usuario está logueado (El app recuerda al usuario) se le muestra la oferta; si no, se le redirige al registro.

* Todas las condiciones visibles en esta pantalla son de solo lectura y no requieren interacción adicional.

**5\. Requerimientos del Wiframe 4**

![Registration](/woppa-wireframe-4-register.png)

**Descripción General**

Esta pantalla permite al usuario crear una cuenta para redimir ofertas dentro de la app. Debe ofrecer una experiencia simple, confiable y ágil, con validaciones claras y múltiples métodos de acceso.

Confirmar si quieren validar email \- recomendado para evitar abusos 

**4.1 Encabezado y bienvenida**

* Mostrar mensaje de bienvenida personalizado: “¡Qué bueno tenerte por acá\!”.

* Incluir el logotipo o marca visual distintiva de Woppa (representado como “W\!” en el diseño) – Conversarlo con Alfredo y Ana. 

**4.2 Selector de pestañas: Registro / Ingreso**

* Mostrar un conmutador que permita al usuario alternar entre los modos de **Registro** e **Ingreso** sin abandonar la pantalla.

* El estado activo debe estar claramente diferenciado visualmente (por ejemplo, botón resaltado).

**4.3 Registro con Google**

* Incluir un botón para **registro con Google** mediante OAuth.

* Este botón debe tener el logotipo de Google y estar destacado en la parte superior del formulario.

* Al hacer clic, debe iniciarse el flujo de autenticación de Google y, al completarse, crear automáticamente una cuenta en Woppa si el usuario no existe.

**4.4 Registro manual con correo y contraseña**

**Campos requeridos:**

* **Correo electrónico**

  * Campo obligatorio.

  * Validación de formato estándar de email.

  * Placeholder visible con ejemplo ("mariaperez@gmail.com").

* **Contraseña**

  * Campo obligatorio.

  * Debe mostrar el texto "Al menos 8 caracteres: 1 mayúscula, 1 número, 1 caracter especial".

  * Debe incluir ícono para mostrar/ocultar contraseña (eye icon).

* **Nombre y Apellido**   
* **Teléfono celular** 

**Validaciones:**

* Mostrar errores en tiempo real si el correo es inválido o la contraseña no cumple los criterios.

* Bloquear el botón de envío si los campos no están completos o válidos.

* *Toni: Más allá del formato del correo, no vamos a validar que este sea valido, es decir, de un usuario real?*

**4.5 Diseño y estructura visual**

* Espaciado generoso entre campos y elementos.

* Tipografía clara y jerarquía visual coherente.

* Paleta de colores consistente con la marca Woppa.

* Mensajes de error y confirmación visibles y accesibles.


**4.6 Requerimientos de Experiencia de Usuario (UX)**

* La pantalla debe cargar rápidamente y no presentar bloqueos visuales.

* El formulario debe poder ser completado fácilmente con una sola mano (diseño mobile-first).

* Al finalizar el registro, el usuario debe ser redirigido automáticamente a la pantalla donde estaba (por ejemplo, retorno al detalle de la promoción si venía desde ahí).

**4.7 Consideraciones Técnicas**

* El botón “Registro con Google” debe integrarse vía API de Google OAuth 2.0.

* Las contraseñas deben ser enviadas de forma segura (encriptadas, sin almacenarse en frontend).

* Debe incluirse lógica para prevenir registros duplicados por correo.

* Debe implementarse lógica de detección de errores comunes (correo ya registrado, error en red, contraseña insegura).

**4.8. Accesibilidad**

* Campos de entrada deben estar correctamente etiquetados.

* Todos los elementos interactivos deben ser accesibles por teclado y lectores de pantalla.

* Debe indicarse visualmente el foco en cada campo activo.

**Dudas**  

Registro con Google

* ¿El botón de "Registro con Google" también debe permitir login si el correo ya está registrado? – Sí: acceder con. 

  * ¿Qué datos se deben capturar del perfil de Google además del correo (nombre, foto, etc.)? Nombre apellido, ubicación, edad, sexo, fecha de nacimiento (promoción por el cumpleaoños)

    1. *Toni: Al hacer login con google no permite obtener directamente ubicación, sexo, edad de la interaccion Oauth*

       1. *Aca dejo lo que se obtiene normalmente (name, given\_name, family\_name, picture, email) [https://accounts.google.com/.well-known/openid-configuration](https://accounts.google.com/.well-known/openid-configuration)* 

       2. *Requiere implementación extra usando las apis de google (de [People](https://developers.google.com/people/api/rest/v1/people/get?hl=es-419)) para obtener esos datos, e incluso así podría venir el date of birth sin año*

          1. *Requiere de scopes sensibles, tienen que pasar por revisión de google al crear la app. Se tiene que cumplir con politicas de privacidad estrictas.*

       3. *Por otra parte los usuarios que no se registren con Google no tendrían esta información, pero si tendrían el teléfono por ej. Quizás lo mejor es tener un register (email \+ password) \-\> onboarding centralizado (names, gender, date of birth, phone, location)?*

  * ¿Debe mostrarse alguna notificación al usuario después de autenticarse con Google? – Cuando se registra un mail de bienvenida, al hacer log in no hace falta. 

Conmutador Registro / Ingreso

* ¿Ambos flujos estarán completamente disponibles desde esta misma pantalla? Sí 

  * ¿Se requiere una transición visual al cambiar entre “Registro” e “Ingreso”? – Sí, porque el registro lleva más campos. 

Validaciones del formulario

* ¿Debe mostrarse validación en tiempo real mientras el usuario escribe, o solo al intentar enviar?  \- Mostrar la validación en tiempo real (para email, número de teñefono, y contraseña) 

  * ¿Qué mensaje exacto se debe mostrar si el correo ya está registrado? \- ¨Ups, este usuario ya existe¨, ¨parece que ya estás registrado¨ \- algo cercano al cliente. 

  * ¿El campo de contraseña debe tener una barra visual de “fuerza de contraseña”? No, no va con el diseño, solo el mensaje de los requisitos de la contraseña. 

Errores y feedback

* ¿Cómo deben manejarse errores comunes de red o validaciones del backend? ¿Alerta modal, mensajes en línea? – Pending de revisar. 

  * ¿Debe haber una pantalla de error genérico o reintento? Devolver inmediatamente a la pantalla de registro para reintentar. 

Redirección tras registro

* ¿A qué pantalla debe redirigirse al usuario después de registrarse correctamente? – Un wireframe intermedio, que te dé el link de mercado pago, o un mensaje que te diga¨ tenés equis cantidad de tiempo para ir acercarte a una red de cobranza para hacer tu pago con el siguiente código xxxxx. El tiempo para hacer el pago¨En gastronomía 2 hrs. En farmacia hasta el final del día.  – Revisar con la diseñadora, y con Alfredo. 

  De aquí se generan dos flujos, 

  1.cuando haces el pago con el link, termina el pago y te dirige a la siguiente pantalla ya existente, con el código listo para redimir la oferta 

  2\. Cuando se piensa hacer el pago por medio de la red de cobranza se genera un código y se muestra la pantalla con el mensaje del tiempo disponible para hacer el pago, una vez se haga el pago en la red con el código, este se vuelve válido para el comercio. 

  Se da la opción de enviar email con la confirmación del pago si no se puede usar el mismo códgo, o si es más económico. \- La implementación técnica de enviar un email de confirmación no es costosa, pero hay que considerar el costo operativo o de infraestructura asociado al envío de emails (por ejemplo, proveedores externos). Se puede usar el mismo cupón, solo se debe definir el flujo que siga el cupón. 

  * ¿Debe mantenerse el contexto anterior (por ejemplo, si venía desde una oferta)? – Referirse al punto anterior para definir esto. 

Política de privacidad y términos

* ¿Debe incluirse un enlace a términos y condiciones y política de privacidad en esta pantalla? Sí, se debe redactar, revisar compliance local. LGPD – Ley de protección de datos en Brazil. 

  * ¿Se requiere aceptación activa (checkbox)? – Sí. (considerar que a futuro se pretende incluir otros métodos de pago) 

Supuestos 

* El usuario puede registrarse con Google o mediante nombre y apellido, numero celular, correo y contraseña. Ambas opciones están disponibles desde el inicio.

* El botón “Registro con Google” detecta automáticamente si el correo ya está registrado y redirige al login si corresponde.

* El formulario está disponible sin fricción adicional, **requiere** confirmación de correo electrónico para crear la cuenta.

* Las contraseñas deben tener mínimo 8 caracteres, incluyendo al menos 1 mayúscula, 1 número y 1 carácter especial, tal como se indica debajo del campo.

* La contraseña ingresada puede mostrarse u ocultarse mediante un ícono de visibilidad.

* Si el usuario ya estaba navegando una oferta o pantalla específica antes del registro, será dirigido a la pantalla del código de promoción listo para redimir. 

* No se considera por ahora el registro mediante redes sociales adicionales (ej. Facebook, Apple ID) fuera de Google. – Considerar IG & FB. – Consultar con el team el budget de incorporar las redes sociales?????????

  * Toni: Register con IG no existe, podemos estimar Register con FB, aunque comenzaría con Google para simplificar (implementación extra, otra app que gestionar y configurar ahora en facebook, scopes sensibles).

* El diseño actual contempla un checkbox de aceptación de términos y Privacidad. 

**6.Requerimientos del Wiframe 5**

![Coupon](/woppa-wireframe-5-obtained-cupon.png)

**Descripción General**

Esta pantalla confirma al usuario que ha obtenido exitosamente una promoción, mostrando el código de redención único. Tiene un rol funcional (mostrar el código) y emocional (reforzar el valor obtenido). Permite redireccionar al usuario hacia la acción deseada (usar el beneficio o explorar más ofertas).

**6.1 Encabezado**

* Mostrar ícono de cierre (X) en la esquina superior derecha para salir de la pantalla.

* No incluir navegación adicional; esta vista funciona como modal de confirmación.

**6.2 Mensaje principal**

* Incluir mensaje de celebración o refuerzo positivo: "¡Esperamos que disfrutes tu beneficio\!". – Revisa rel mensaje 

* Acompañar con un ícono gráfico alusivo (ej: confeti, fiesta) para reforzar positivamente la experiencia. – Revisar el ícono, se puede incluir una ¨mascota¨ de la marca, para reforzar la identidad de la marca, por ejemplo se ha pensando en cambiar el nombre a un nombre que incluya una ¨U¨ y que el macaquito esté colgando de la ¨U¨, una vez que haces el pago y obtienes el código, el macaquito se vé celebrando la oferta. Todo esto refeurza el rol emocional de esta pantalla, y refuerza la identidad. 

**6.3 Código de redención**

* Mostrar el código único de forma central, en mayúsculas y con diseño destacado.

* El código debe ser generado dinámicamente y estar vinculado a la promoción específica.

* Debajo del código debe mostrarse:

  * Nombre del comercio (ej: “Sushi Go”)

  * Etiqueta con tipo de beneficio (ej: “1+1”)

    

**6.4 Instrucciones de uso**

* Incluir una leyenda instructiva del tipo:  
  "Mostrá este código para obtener tu pedido en el comercio." – Considerar un tono amistoso y cercano siempre a la hora de la traducción. Stephanie habla portugués, podría encargarse de la traducción. 

**6.5 Botones de acción**

* Botón principal (morado): “Ir al disfrutar de la oferta”  
  Redirige al usuario a google maps a la ubicación del comercio. 

* Botón secundario (bordeado): “Buscar más ofertas” – Sugerencia con relación a la marca: ¨Seguir woppeando¨ \- considerar algo similar si se cambia el nombre de la marca – refuerzo de la identidad de la marca.   
   \- Redirige al usuario nuevamente a la pantalla de exploración de promociones.

**6.6. Requerimientos de Experiencia de Usuario (UX)**

* La jerarquía visual debe poner foco absoluto en el código.

* El tono visual debe ser alegre, confiable y claro.

* El usuario no debe sentirse forzado a usar el beneficio inmediatamente; se permite explorar más si lo desea.

**6.7. Consideraciones Técnicas**

* El código debe ser generado desde backend, con lógica de unicidad y trazabilidad.

* Debe implementarse lógica para evitar duplicados o reuso del mismo código.

* La pantalla debe ser accesible aún sin conexión si ya fue cargada (considerar almacenamiento local).

  * *Toni: El usuario debería de recibir el código por mail al confirmarse la compra, no deberíamos de agregar esta complejidad (offline) en el mvp.*

* La acción de redención debe registrarse en backend como evento (para métricas).

**6.8. Accesibilidad**

* El código debe estar en texto real (no imagen) para permitir lectura por pantalla.

* Asegurar contraste alto entre texto y fondo.

* Botones con foco visual claro y etiquetas ARIA.

**Dudas** 

**Código de redención**

* ¿El código es alfanumérico aleatorio o sigue una lógica específica? Alfanumérico aleatorio. 

  * ¿Tiene fecha de vencimiento o cantidad limitada de usos? – Fecha de vencimiento se aplican las condiciones de la oferta. 

**Rastro del cupón**

* ¿Se almacena una copia del cupón en un historial para el usuario? Sí, ver sus compras 

  * Creación del perfil para el MVP  \- Consumidor \- Datos personales, Incluir Historial de compras, favoritos, Métodos de pago (más adelante) Confirguración (notificaciones), abajo, T\&C, cerrar sesion/log out

  * Perfil Para los proveedores: Mi negocio, mis ventas por rango de fechas  para el MVP, para má adelante puede ser un mini dashboard, con un poco más de análisis 

  * ¿Qué pasa si el usuario cierra la app y vuelve luego?  \- Dev team – Log out automático después de un tiempo determinado 

**Botón “Ir al disfrutar de la oferta”**

* ¿A qué pantalla debe llevar este botón? ¿Mapa, instrucciones específicas, página de comercio?  \- Lleva a google maps 

  * ¿Debe marcar la oferta como “en uso” o “redimida” al hacer clic? – Cambio de Status, cuando recién se compra, “pago” y “redimido” (buscar palabras que se asocien con la identidad de marca, siempre cercanas) 

**Estado del cupón**

* ¿Es posible invalidar un cupón una vez generado? – El comercio marca el estado  \- depende el tipo de oferta, si tenemos un stock predeterminado por el comercio, una vez se consumen esas ofertas, WOPPA lo marca como agotado automáticamente. Si el comercio ofrece una condición tipo “hasta agotar existencias” el comercio debe comunicar al equipo de WOPPA una vez se agote para que se retire la oferta. 

  1. *Toni: Que el comercio le comunique al staff de Woppa, y Woppa lo marca como agotado en el backoffice.*

  * ¿Se requiere verificación por parte del comercio? (ej. marcar como “canjeado”)  \- Una vez se completa el pago, se reduce el stock automáticamente, el comercio verifica el código de compra generado por la aplicación. 

**Trazabilidad y métricas**

* ¿Este evento cuenta como una redención efectiva o solo cuando el comercio lo valida? – Una vez se completa el pago, se reduce el stock automáticamente, el comercio verifica el código de compra generado por la aplicación.

  1. *Toni: deberíamos tener un estado de redimido que se llega una vez el comercio valida el código en el backoffice.*

  * ¿Debe generarse un ID de redención para seguimiento en backend? – Desarrollo, se acordó con el cliente usar un mismo código, se maneja por status o eqtiquetas. 

**Supuestos**

* El código mostrado es único, generado por backend y no puede reutilizarse por otros usuarios.

* La acción de generar el cupón queda registrada como una “intención de redención” incluso si no se canjea físicamente.

* El botón “Buscar más ofertas” redirige al usuario a la pantalla de mapa o listado de promociones.

* El código se puede volver a visualizar si el usuario ingresa a mi perfil e ingresa a su historial de compras. 

* El usuario debe estar Log in para ver su historial de compra, o salvar el cupón / código  \- Descargar el código en PDF o enviar un correo con el código consultar con desarrollo. 

**7.Requerimientos del Wireframe del comercio** 

**![Merchant View](/woppa-wireframe-comerciante-1.png)**

**Descripción General**

Esta pantalla permite a los comercios cargar promociones 1+1 indicando toda la información relevante para que la oferta pueda mostrarse correctamente en la app Woppa. La pantalla está pensada para facilitar la autogestión, con validaciones visuales, campos obligatorios y lógica de clasificación por categorías.

Separar los flujos del comercio: uno para crear el negocio y otro para crear la promoción. 

Preguntar si es necesario el form si o sí 

Cuando se paga el cod el status se cambia en el backoffice del comercio  automáticamente

Cuando se entrega el prod se cambia el cod a canjeado, pero MANUALMENTE 

 **7.1Encabezado**

* Título: “Crear publicación”.

* Flecha para regresar a la pantalla anterior sin guardar cambios.

* Enlace a “¿Necesitás ayuda?” ubicado arriba a la derecha, que abre guía o soporte externo. – Link de whatsapp, para el MVP 

Se crea una web, en esta web el comercio se registra y sube sus ofertas, en esta misma web se crea un espacio de bakcoffice, donde se visualiza información para que el equipo de WOPPA pueda hacer aprobación de las publciaciones y llevar el control de la data (integrar un superadmin) 

* *Toni: me imagino el mismo backoffice con distintos roles (admin?, woppa staff, comercio), ej:*  
  * *Los woppa staff:*   
    * *Login básico*  
    * *Registro de comercios (por si un usuario no tiene friccion a usar el backoffice aún)*  
      * *Si los comercios son pocos podríamos ingreasarlos directo en la base de datos de manera manual para el MVP*  
    * *Validación de promociones*  
    * *Gestión de estado de stock*   
      * *Marcar como agotadas*  
    * *Historial de actividad (quizás fuera de MVP si hay confianza?)*  
      * *Acciones realizadas por el staff*  
  * *Los comercios:*   
    * *Login básico*  
    * *Registro básico*  
    * *Carga de promociones (si hubiese fricción se podría tener tamb el gform y enviar esa data al db de woppa)*  
    * *Confirmación de redención de un cupón*  
    * *Historial de promociones*  
    * *Historial de ventas*  
* *El problema con los formularios es que no escalan, ya que tenemos una necesidad de lectura por parte de los comercios como tamb de gestión y lectura por parte del woppa staff. Es mejor concentrar el backoffice ahí directamente, aunque se podría seguir teniendo la carga de promociones con google form si eso fuera una fricción.*   
* *Quizas para el panel de woppa se podría usar algo como [https://docs.adminjs.co/](https://docs.adminjs.co/) que se conecta directo con la db y ya permite el crud de todas las entidades*

**7.2 Campos y Componentes del Formulario**

**Crear nueva pantalla:** 

**Página inicial: Registro o Log in** 

**Registro:** 

**Nombre del comercio** 

**Nombre y apellido de la persona responsable** 

**Teléfono Contacto comercial y contacto financiero** 

**TAX ID: CNPJ en Brazil para el MVP** 

**Correo eletrónico** 

**Dirección** 

**Contraseña** 

**Log in:** 

**Correo y contraseña**

**Perfil o Usuario**

**Historial de ventas: códigos pagos, códigos redimidos, ganancia del comercio, códigos ya pagos de parte de WOPPA y códigos pendientes.** 

**Status de la publicación: en revision, te falta info, aprobada,** 

**Revisar con el cliente y especificar si quieren algo más para el comercio**

**1\. Nombre de publicación**\*

* Campo de texto obligatorio.

* Solamente con el nombre del Producto (Alimento, producto de farmacia)

**2\. Tipo de descuento**\*

* Selector de una sola opción entre los siguientes:

  * 1+1

**3\. Categoría principal**\*

* Selector obligatorio entre dos verticales:

  * Gastronomía

  * Farmacia 

**4\. Subcategoría**\*

* Muestra opciones distintas según la categoría elegida.

* El usuario puede seleccionar solo una subcategoría.

**Subcategorías oficiales:** Revisar apps de comidad en Brazil y ajustar la lista  que quede a 10 opciones**,** mostrar un top 5\. Y después ver más.. 

Para más adelante, según el horario del día se muestran subctaegorías distintas tipo: empezando bien tu día – desayunos, almuerzos, cenas, etc. 

* **Gastronomía**

  1. Cafetería y Bakery

  2. Heladería

  3. Sushi & Asiática

  4. Steak houses

  5. Burgers

  6. Pizza y Pasta (Italian)

  7. Carnicería gourmet

  8. Boutique de vinos

  9. Saludable (alimentos naturales)

  10. Otros 

* **Farmacia y Perfumería – Revisar aplicaciones en Brazil y proponer la lista de subctagoría** 

  1. Beauty

  2. Perfumería

  3. Higiene personal

  4. Medicamentos de venta libre

  5. Homeopatía

  6. Suplementos

  7. Productos de limpieza

**7.3. Fotos del producto**\*

* Obligatorio subir al menos una imagen.

* Permite subir hasta 2 imágenes.

* Deben previsualizarse en miniaturas antes de publicar.

* Incluir instrucciones para las fotos: "debe tener buena iluminación y el producto se debe ver correctamente."

* Incluir imágenes de ejemplo 

* Considerar el uso de IA para ayudar a los comercios a validar las fotos \-Desarrollo 

  * *Toni: En un futuro*

* La publicación para por QA, y el equipo de WOPPA aprueba las fotos 

**7.4. Tiempo para canjear beneficio**\*

* Opciones únicas, visuales tipo botón:

  * 6 horas

  * 12 horas

  * 1 día

  * 3 días

  * 1 semana

  * Si no lo canjeas dentro de los tiempos marcados por el comercio que se acumule como crédito WOPPA 

**7.5 Descripción**\*

* Campo obligatorio.

* Instrucción visible: “Describí la oferta en menos de X caracteres”.

* Debe permitir indicar condiciones, restricciones y horario de validez (incluyendo fines de semana, o días festivos, horas de alto consumo, etc) 

**7.6. Precio final**

* Campo numérico con símbolo de moneda.

* Representa el valor real final que verá el usuario (no el precio base original).


**7.8. Ubicación**\*

* Campo obligatorio.

* Debe aceptar texto libre con autocompletado sugerido por integración con Google Maps

  * *Toni: En otra parte se menciona la opción de agregar un link directo a Google Maps, pero esto parece contradecirse.*

  * *Además, por qué cada promoción debería tener una ubicación si ya tenemos la del comercio?*

  * *Habría que pensar cómo asociar cada promoción al comercio correspondiente. En un Google Form no es sencillo identificar a qué comercio pertenece cada carga (y tener un formulario distinto por comercio no escala a futuro). Esto se resolvería mejor desde el backoffice.*

  * *También nos surge la duda de cómo evitar que un comercio cargue promociones que no le corresponden (desde un google form). El QA manual del equipo de Woppa no tendría herramientas para validarlo*

  * *Por otro lado, es posible que un comercio legítimamente quiera publicar promociones en distintas ubicaciones? Asumo que no hay sucursales por el momento. Se permitirían sucursales en un futuro? Esto influye en el modelo de datos*

  * *Para el MVP, lo ideal sería que la promoción tome automáticamente la ubicación del comercio asociado, siempre que esta esté validada de alguna manera.*

**7.9. ¿Por qué está en oferta?**\*

* Selector tipo tag múltiple, permite elegir uno o más motivos:

  * Promoción/Marketing

  * Próximo a vencer

  * Pocas unidades

**7.10. ¿Cuándo vence?**\*

* Campo obligatorio con formato de fecha DD/MM/AAAA.

* Representa la fecha final de disponibilidad de la promoción.

**7 Acciones y Validaciones**

**Botón "Pre Publicar"**

* Debe permanecer deshabilitado hasta completar todos los campos obligatorios.

* Al activarse, lleva a una vista previa/resumen antes de publicación. – Vista Previsa de la publicación como se verá en la aplicación de WOPPA

* Una vez se visualice la vista previa, sale otro botón de publicar, se muestra un mensaje tipo “gracias por enviar tu publicación, estamos revisándola, te daremos más detalles pronto”

* Se envía un mensaje o un correo con los status de la publicación: en revisión, “falta algo”, aprobada. 

**Botón "Cancelar y eliminar"**

* Elimina los datos ingresados hasta ese momento y retorna a la pantalla anterior.

**3\. Requerimientos de UX**

* Diseño claro y segmentado por grupos lógicos.

* Visualizaciones limpias, etiquetas visibles y componentes accesibles.

* Validaciones visuales inmediatas (ej. campos en rojo si faltan datos).

* Para el MVP  \- Optimizado para escritorio y tabletas (prioridad en web de laptops, pero si es necesario que tenga la opción para hacerlo desde el navegador del celular, no mobile first). – Consultar con desarrollo la funcionalidad de la WEB abierta desde el celular. 

**4\. Consideraciones Técnicas**

* Las subcategorías deben cargarse dinámicamente según la categoría seleccionada.

* Las imágenes deben ser validadas por tamaño, formato y peso (Aún está pendiente definir internamente si el equipo de WOPPA va a tomar las fotos, o va a poner instrucciones y especificaciones) hacer algún research de cómo se puede empezar con las fotos de manera que sea escalable. – Allan y Stephanie lo definen y confirman 

* El sistema debe prevenir duplicaciones de publicaciones idénticas dentro del mismo día.

* Se debe validar que el campo de ubicación coincida con un punto geográfico reconocido.

**5\. Accesibilidad**

* Navegación fluida con teclado. (ya sea desde laptop o desde el navegador del celular)

* Textos descriptivos en todos los campos.

* Contraste adecuado en botones, bordes y campos obligatorios.

**Dudas**

1. **Precio final y forma de pago**

   * ¿Debe indicarse alguna forma de pago específica en la publicación (efectivo, QR, tarjeta)? – WOPPA le paga al comercio. – WOPPA quiere pagar cada dos semanas al inicio para motivar al comercio, más adelante puede ser una vez al mes. 

   * ¿El precio debe estar expresado con decimales? Sí. ¿Se requiere validación regional de moneda (ej. SR, ARS, USD)? Sí, en cada país moneda local. 

   

2. **Caracteres de la descripción**

   * ¿Cuál es el número máximo exacto de caracteres permitidos en la descripción? – Revisar con desarrollo

   * ¿Qué sucede si se supera ese límite? ¿Debe mostrarse un contador en tiempo real? Revisar con desarrollo

3. **Ubicación**

   * ¿El campo debe validar automáticamente con Google Maps y rechazar entradas que no estén geolocalizadas?  \- No permitir entrada manual 

   * ¿Debe permitirse cargar direcciones personalizadas como “Envío a domicilio” o solo direcciones físicas verificables? \- \`Por ahora solo recolectar en el MVP 

4. **Carga de imágenes**

   * ¿Cuál es el peso máximo permitido por imagen? – Revisar con desarrollo – tipo de storage 

   * ¿Qué tipos de archivo están permitidos (.jpg, .png, .webp, otros)? Revisar con desarrollo – tipo de storage

   * ¿Se permite recorte o edición básica de la imagen antes de publicar? Revisar con desarrollo – tipo de storage

5. **Validación de duplicados**

   * ¿Qué parámetros se consideran para detectar duplicación de publicaciones (nombre \+ ubicación \+ fecha)? Revisar con desarrollo 

   * ¿Se debe notificar al usuario si hay duplicación, o bloquear la publicación directamente? Revisar con desarrollo

6. **Subcategorías dinámicas**

   * ¿Se pueden agregar nuevas subcategorías en el futuro? ¿Cómo se gestionaría esto en producción? Sí, más adelante se pueden agregar subcategorías 

7. **Estado de la publicación luego de “Pre-publicar”**

   * ¿La publicación queda en estado “borrador” hasta que el comercio confirme? – Queda en status de ¨ en revisión¨ revisar el wording 

   * ¿Existe un paso de moderación/manual review por parte de Woppa o se publica automáticamente? – Sí, el equpo de WOPPA hace un QA antes de la publicación 

8. **Nombre de la aplicación en versiones públicas**

   * ¿Debe aparecer el nombre “Woppa” en todas las interfaces, o es un nombre interno del proyecto? – Sí va a ser el nombre público, justo cuando sepamos el nombre definitivo se hace el logo y demás para registrar el nombre oficial. 

**Supuestos**

1. **Validaciones front-end y back-end**

   * Todos los campos obligatorios serán validados en frontend con mensajes visuales (rojo, tooltips), y validados nuevamente en backend.

   * El botón “Pre-publicar” solo se habilita si todos los campos requeridos están completos y válidos.

2. **Control de imágenes**

   * Permitiremos solo formatos .jpg y .png de hasta 5MB por imagen. Revisar con desarrollo

   * Se permitirán 2 imágenes por publicación, previsualizadas como miniaturas.

3. **Subcategorías dinámicas**

   * El sistema consulta en tiempo real las subcategorías desde el backend al cambiar de categoría principal.

   * Si no hay conexión, se mostrará un mensaje de error genérico.

4. **Integración de ubicación**

   * Se usará Google Places API para autocompletar ubicaciones y validar que la dirección ingresada sea válida y geolocalizable.

5. **Detección de duplicados**

   * Si el mismo comercio intenta publicar una oferta idéntica (nombre \+ ubicación \+ categoría) el mismo día, se mostrará una advertencia y no se permitirá continuar. \- Revisar con desarrollo – Mostrar un error

6. **Accesibilidad**

   * Todos los campos tendrán labels visibles y roles para navegación por teclado.

   * El contraste cumple con WCAG AA para formularios (texto sobre fondos, botones, validaciones).

7. **Modo de vista previa**

   Al hacer clic en “Pre-publicar”, se mostrará un resumen de todos los datos ingresados para revisión final antes de guardar y enviar la publicación. 

**Dudas Generales** 

* Formas de Pago  \- Revisar notas en wireframres arriba  
* Nombre de la Aplicación – Revisar notas

Jueves: 17:00 

