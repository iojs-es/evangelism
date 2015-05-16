# Lanzamiento de io.js 1.4.1

_Nota: la versión **1.4.0** fue etiquetada y construida pero no publicada. Se descubrió un bug en libuv en el proceso por lo que la publicación se abortó. Hemos saltado a 1.4.1 para evitar confusión._

## Cambios notables

* **process** / **promises**: Un evento`'unhandledRejection'` es ahora emitido en `process` cuando una `Promise` fue rechazada y no existe una función que tenga en cuenta un error en la `Promise` durante una vuelta del event loop. Un evento `'rejectionHandled'` es emitido ahora cuando una `Promise` fue rechazada y una función que tenga en cuenta un error fue puesto más tarde que una vuelta al event loop.  [#758](https://github.com/iojs/io.js/pull/758) (Petka Antonov)
* **streams**: ahora pueden usarse streams ordinarios como un socket subyacente para `tls.connect()` [#926](https://github.com/iojs/io.js/pull/926) (Fedor Indutny)
* **http**: Un nuevo evento `'abort'` es emitido cuando se aborta  `http.ClientRequest` por el cliente. [#945](https://github.com/iojs/io.js/pull/945) (Evan Lucas)
* **V8**: Actualización de V8 a 4.1.0.21. Incluye un fix embargado, los detalles deben de estar disponibles una vez se levante el embargo. Un cabmio breaking en ABI se ha mantenido fuera de la actualización, posiblemente será incluido cuando se haga el merge de io.js con V8 4.2. Véase la discursión en  [#952](https://github.com/iojs/io.js/pull/952).
* **npm**: Actualizar npm a 2.6.0. Incluye características que soportan el nuevo registro y prepararse para `npm@3`. Véase [npm CHANGELOG.md](https://github.com/npm/npm/blob/master/CHANGELOG.md#v260-2015-02-12) para los detalles. Resumen:
  * [#5068](https://github.com/npm/npm/issues/5068) Añade nuevo comando logout, y hacer algo útil para los dos clientes autentificados (bearer-based y basic-based).
  * [#6565](https://github.com/npm/npm/issues/6565) Advertir que el comportamiento de `peerDependency` está cambiando y añadir una nota en la documentación.
  * [#7171](https://github.com/npm/npm/issues/7171) Advertir que un `engineStrict` en el `package.json` va a desaparecer en la siguiente versión de npm (¡próximamente!)
* **libuv**: Actualización a 1.4.2. Véase [libuv ChangeLog](https://github.com/libuv/libuv/blob/v1.x/ChangeLog) para los detalles de las correciones.

# ARM ofrece soporte para io.js en ARMv8

ARM contactó Rod Vagg, lider del Build Working Group de io.js, para ofrecer soporte al projecto io.js. ARM y su socios de hardware están en camino para hacer que ARMv8 sea una plataforma de servicio viable y la naturaleza hábil de JavaScript en el lado del servidor hace una combinación perfecta en el nuevo ARM.

Ya que ARMv8 está siendo adoptado por fabricantes de dispositivos móviles, nuevas versiones de V8 ya tienen buen soporte. A causa del rol giratorio de V8 en Anroid, io.js está perfectamente adaptado para ir tras este soporte, e incluso contribuir a que da nuestras nuevas relaciones con el equipo de V8.

Desde el principio del proyecto io.js, Rod ha defendido el papel de ARM para io.js, para la IoT, aficionados, y uso en el servidor. Ya tenemos builds para ARMv6 de cada versión para dispositivos como Raspberry Pi. y builds ARMv7 para muchos dispositivos más populares (incluyendo los Online Labs basadas en la plataforma cloud ARM, que también han ofrecido ayuda a io.js). ARMv8 es la extensión lógica de esto, y también tiene gran potencial para aplicaciones de servidor, particularmente dado el nuevo soporte de 64 bits.

El build team está en el proceso de tener acceso a Linaro ARMv8 Server Cluster para la integración de la plataforma CI de io.js, lo cual debería dar lugar evetualmente a liberaciones regulares de binarios ARMv8.

# Actualizaciones de la comunidad

* [**Propuesta de Reconciliación**](https://github.com/iojs/io.js/issues/978): El proyecto io.js está preparando un plan de reconciliación que pueda ser llevado a la The Node.js Foundation. Las aportaciones de la comunidad son muy importantes en esta etapa temprana, así que por favor dejen sus comentarios.
* **Nueva API C++ de Streams**: Una [nueva API C++ de Streams](https://github.com/iojs/io.js/commit/b9686233fc0be679d7ba1262b611711629ee334e) llegó a io.js esta semana, permitiendo envolver un stream TLS en otro stream TLS.
* **io.js Roadmap**: [El Roadmap](https://github.com/iojs/io.js/blob/v1.x/ROADMAP.md) es el plan para el futuro de io.js. Presenta los planes de política de estabilidad, y lista cuales son las prioridades inmediatas de io.js como un todo.
* **Diapositivas del Roadmap listas y acabadas para su Traducción**: El conjunto de diapositivas introductorias para el Roadmap de io.js [se han terminado, y estan listas para su traducción](https://github.com/iojs/roadmap/issues/18). ¿Crees que puedes presentarlas a un grupo cercano a tí? ¡Coméntanoslo y trabajaremos contigo para prepararte para exponerlas!
* **Tutorial de Microsoft para io.js en los Azure Websites**: Microsoft [publica un tutorial](http://azure.microsoft.com/en-us/documentation/articles/web-sites-nodejs-iojs/) para su plataforma Azure que describe como usar io.js con los Azure Websites.
* **Floobits se mueve a io.js**: El software colaboración en tiempo real Floobits [convirtió su plataforma a io.js](https://news.floobits.com/2015/02/23/on-moving-to-io.js/), en parte por su frustración con los ciclos más lentos de publicación de Node, por incluir más características de ES6 sin necesitar la flag `--harmony`, y porque sentían que los cambios de 0.10.0 a 0.12.0 no eran muy grandes.
* **El artículo de Anand Mani Sankar _Node. contra vs io.js: Why the fork?!?_**: Anand escribió un buen, en la mayor parte objectivo, [artículo acerca de la historia reciente de io.js](http://anandmanisankar.com/posts/nodejs-iojs-why-the-fork/#.VO82hE60PVw.twitter), y lo que esperamos conseguir con el. Una buena lectura para gente que no esta involugrada en la comunidad para estar al día.
* **iojs-jp - Nuevo blog Japones de io.js**: La comunidad iojs-jp creó un [blog localizado de io.js afín](http://blog.iojs.jp/) de diseminar contenido en su lenguaje. Si estas interesado, ¡échale un vistazo!
* **iojs-cn - Nuevo blog Chino de io.js**: De forma similar a la comunidad iojs-jp, la comunidad iojs-cn creó [un blog localizado](http://cn.iojs.org/) para publiar artículos sobre io.js en su lenguage. ¡Asegúrate de visitarlo si estas interesado en la comunidad iojs-cn o en noticias Chinas de io.js!
* **[Revisión de las Diapositivas del Roadmap](https://www.youtube.com/watch?v=etI_UD4wXlo)** - Una revisión de las diapositivas del roadmap antes de que sean publicadas para asegurarse de que cumplican con el mensage que el proyecto defiende.

# Soporte a io.js Añadido
* **[Wallaby.js](http://wallabyjs.com/)**, una libreria de pruebas para JavaScript a tiempo real, llegó a la versión 1.0 y [añadió soporte para io.js](http://dm.gl/2015/02/23/wallaby-version-one/)!
* **[jsdom](https://github.com/tmpvar/jsdom)**, una implementación de los estándares WHATWG DOM y HTML, acaba de llegar a la [versión 4.0.0](https://github.com/tmpvar/jsdom/blob/master/Changelog.md#400), la cual añadió el _requisito_ de io.js.
* El creador de **[give](https://github.com/mmalecki/give)**  [twiteó](https://twitter.com/maciejmalecki/status/569629100215816192) que las versiones más nuevas de give añaden soporte para io.js. Give es un administrador de versiones node.js/io.js basado en git.
* El **Firebase Realtime Client**, cliente oficial para web/node.js de JavaScript de Firebase, [twiteó](https://twitter.com/FirebaseRelease/status/570000737343647744) que añadieron soporte para io.js en la [versión 2.2.1](https://www.firebase.com/docs/web/changelog.html#section-realtime-client)
* **Semaphore**, un servicio *hosted* de integración continua, [twiteó](https://twitter.com/semaphoreapp/status/570987355005431809) acerca de añadir soporte a io.js en su [actualización de Plataforma el 24 de February de 2015](https://semaphoreapp.com/blog/2015/02/17/platform-update-on-february-24th.html?utm_source=twitter&utm_medium=social&utm_content=platform_update_launch&utm_campaign=platformupdate).
