# Lanzamiento de io.js 1.5.0

El viernes, 6 de Marzo, [@rvagg](https://github.com/rvagg) publicó io.js [**v1.5.0**](https://iojs.org/dist/latest/). El log de cambios completo puede encontrarse [en GitHub](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md).

### Cambios notables

* **buffer**: Nuevo método `Buffer#indexOf()`, modelado a partir de [`Array#indexOf()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf). Acepta String, Buffer o un Number. Strings se interpretan como UTF8. (Trevor Norris) [#561](https://github.com/iojs/io.js/pull/561)
* **fs**: el objeto de propiedades `options` en los métodos de `'fs'` no llevarán más a cabo la comprobación `hasOwnProperty()`, permitiendo así que los objetos de opciones con propiedades en el prototype. (Jonathan Ong) [#635](https://github.com/iojs/io.js/pull/635)
* **tls**: Un probable memory leak en TLS fue informado por PayPal. Algunos de los cambios recientes en **stream_wrap** paracen tener la culpa. La solución inicial está en [#1078](https://github.com/iojs/io.js/pull/1078), puedes seguir cómo se progresa en la solución del leak en [#1075](https://github.com/iojs/io.js/issues/1075) (Fedor Indutny).
* **npm**: Actualización a npm 2.7.0. Véase [npm CHANGELOG.md](https://github.com/npm/npm/blob/master/CHANGELOG.md#v270-2015-02-26) para los detalles incluyendo porqué es un semver-minor cuando podría haber sido semver-major.
* **TC**: Colin Ihrig (@cjihrig) resignó del TC debido a su deseo de programar más e ir a menos reuninones.

### Problemas conocidos

* Memory leak relacionado posiblemente con TLS, detalles en [#1075](https://github.com/iojs/io.js/issues/1075).
* Windows aún informa sobre algunos fallos en pruebas y seguimos en dirección de ocuparnos de todos ellos como una prioridad. Véase [#1005](https://github.com/iojs/io.js/issues/1005).
* Pares Suplentes en REPL pueden congelar el terminal [#690](https://github.com/iojs/io.js/issues/690)
* No es posible construir io.js como una librería estática [#686](https://github.com/iojs/io.js/issues/686)
* `process.send()` no es tal y como sugiere la documentación, una regresión introducida en 1.0.2, véase [#760](https://github.com/iojs/io.js/issues/760) y fix en [#774](https://github.com/iojs/io.js/issues/774)

# Actualizaciones de la Comunidad

* Puedes relajarte sabiendo que io.js y el último node.js [**no están afetados**](https://strongloop.com/strongblog/are-node-and-io-js-affected-by-the-freak-attack-openssl-vulnerability/) por el [FREAK Attack](https://freakattack.com/). ¿Estás utilizando la última versión de io.js o la última versíon de node.js, verdad?

* Walmart patrocina ahora una máquina build para el sistema CI de io.js de Jenkins.  El equipo @iojs/build está trabajando en crear binarios de io.js para SunOS (como los que puedes obtener de nodejs.org). Un fix en V8 ([iojs/io.js#1079](https://github.com/iojs/io.js/pull/1079)) necesita de llegar antes de que más progreso pueda hacerse.
* También nos gustaría dar las gracias a las siguientes compañías por contribuir con hardware y tecnologías/soporte/ingeniería para builds de io.js:
  * **Digital Ocean** (Linux principalmente)
  * **Rackspace** (Windows principalmente)
  * **Voxer** (OS X y FreeBSD)
  * **NodeSource** (ARMv6 & ARMv7)
  * **Linaro** (ARMv8)
  * **Walmart** (SmartOS / Solaris)
* La comunidad de io.js ha estado trabajando duro en internacionalización de todo el contenido. Hay ya más de 20 lenguajes activos publicados en [iojs.org](http://iojs.org) e i18n sitios de comunidad. Además, links i18n ([iojs/website#258](https://github.com/iojs/website/pull/258)) se han añadido al pie de página para un fácil acceso. ¿Nos falta tu idioma?  [¡Ayudanos!](https://github.com/iojs/website/blob/master/TRANSLATION.md)
* Hablando de traducciones, la [presentación del roadmap de io.js](http://roadmap.iojs.org/) se ha actualizado con el link a versiones en otros idiomas.

* Parece que **PayPal** está haciendo un experimento para comparar [Kappa](https://www.npmjs.com/package/kappa) en io.js vs node.js 0.12 vs node.js v0.10. El equipo de PayPal indentificó un posible memory leak en TLS. El fix inicial está en  [#1078](https://github.com/iojs/io.js/pull/1078) y su progreso hacia ser cerrado está en [#1075](https://github.com/iojs/io.js/issues/1075)

* [**NodeSource**](http://nodesource.com) está ahora proveyendo a io.js de paquetes [binarios Linux](https://nodesource.com/blog/nodejs-v012-iojs-and-the-nodesource-linux-repositories) tanto para distributions Ubuntu/Debian como RHEL/Fedora.
* El io.js [Docker build](https://registry.hub.docker.com/u/library/iojs/) es uno de los trece nuevos [repositorios oficiales de Docker](http://blog.docker.com/2015/03/thirteen-new-official-repositories-added-in-january-and-february/) añadidos en Enero y Febrero.

* Gente de NodeBots y IoT debería de estar feliz por escuchar que el recién anunciado [**Tessel2**](http://blog.technical.io/post/112787427217/tessel-2-new-hardware-for-the-tessel-ecosystem) usa [io.js de forma nativa](http://blog.technical.io/post/112888410737/moving-faster-with-io-js).
* [**@maxbeatty**](https://twitter.com/maxbeatty) está trabajando en una nueva versión del backend de [jsperf.com](http://jsperf.com/), usando io.js y está enteramente en [código abierto](https://github.com/jsperf/jsperf.com).  ¡Contribuciones bienvenidas!

* [@eranhammer](https://twitter.com/eranhammer) escribió un articulo llamado [The Node Version Dilemma](http://hueniverse.com/2015/03/02/the-node-version-dilemma/) en el que se discute sobre varias versiones node.js / io.js y propone cuales usar y cuando usarlas.

# Soporte io.js Añadido

* **[scrypt](https://npmjs.com/scrypt)** ahora soporta io.js. Aprende más acerca de esto en el su [GitHub issue](https://github.com/barrysteyn/node-scrypt/issues/39)
* **[proxyquire](https://github.com/thlorenz/proxyquire)** v1.3.2 publicado con soporte para iojs.
