# io.js 1.8.1 release
This week we had one io.js release [v1.8.1](https://iojs.org/dist/v1.8.1/), complete changelog can be found [on GitHub](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md).

### Notable changes

* **NOTICE**: Skipped v1.8.0 due to problems with release tooling.
  See [#1436](https://github.com/iojs/io.js/issues/1436) for details.
* **build**: Support for building io.js as a static library (Marat Abdullin) [#1341](https://github.com/iojs/io.js/pull/1341)
* **deps**: Upgrade openssl to 1.0.2a (Shigeki Ohtsu) [#1389](https://github.com/iojs/io.js/pull/1389)
  * Users should see performance improvements when using the crypto API.
  See [here](https://github.com/iojs/io.js/wiki/Crypto-Performance-Notes-for-OpenSSL-1.0.2a-on-iojs-v1.8.0)
  for details.
* **npm**: Upgrade npm to 2.8.3. See the [release notes](https://github.com/npm/npm/releases/tag/v2.8.3) for details. Includes improved git support.
* **src**: Allow multiple arguments to be passed to process.nextTick (Trevor Norris) [#1077](https://github.com/iojs/io.js/pull/1077)
* **module**: The interaction of `require('.')` with `NODE_PATH` has been restored and deprecated. This functionality
will be removed at a later point. (Roman Reiss) [#1363](https://github.com/iojs/io.js/pull/1363)

### Problemas conocidos
Vea https://github.com/iojs/io.js/labels/confirmed-bug para una lista completa y más actual de los problemas conocidos.

* Algunos problemas con timers no referenciados ejecutandose durante `beforeExit` aún se encuentran por resolver. Vea [#1264](https://github.com/iojs/io.js/issues/1264).
* Un par suplente en el REPL puede congelar la terminal [#690](https://github.com/iojs/io.js/issues/690)
* `process.send()` no es una acción síncrona como la documentación sugiere, una regresión introducida en el 1.0.2, vea [#760](https://github.com/iojs/io.js/issues/760) y la solución en el [#774](https://github.com/iojs/io.js/issues/774)
* Llamar a `dns.setServers()` mientras una consulta DNS está en progreso puede ocasionar que el proceso falle en una afirmación fallida [#894](https://github.com/iojs/io.js/issues/894)
* `url.resolve` puede transferir una porción de la autorización de la url mientras se resuelve entre dos hosts, vea [#1435](https://github.com/iojs/io.js/issues/1435).
* readline: los escapes de separación se están procesando incorrectamente, vea [#1403](https://github.com/iojs/io.js/issues/1403)

### Actualizaciones de la comunidad

* Fedor Indutny abrió una discusión acerca de remover los eventos `newSession` y `resumeSession` de TLS. [iojs/io.js#1462](https://github.com/iojs/io.js/issues/1462)
* Propuesta para cambiar el parser HTTP de C a JS [aquí](https://github.com/iojs/io.js/pull/1457)
* El fundador de NPM habla acerca de io.js en [InfoWorld](http://www.infoworld.com/article/2910594/node-js/npm-founder-foresees-merger-node-js-io-js.html)
* Propuesta para agregar a mikeal, mscdex, shigeki como nuevos miembros del TC. [iojs/io.js#1483](https://github.com/iojs/io.js/issues/1483#issuecomment-95128140)

### Próximos eventos

* Los tickets para la [NodeConf](http://nodeconf.com/) están ya a la venta, el evento será del 11 al 14 de junio en Walker Creek Ranch, CA
* Los tickets para [CascadiaJS](http://2015.cascadiajs.com/) están ya a la venta, el evento será del 8 al 10 de julio en el Estado de Washington
* Los tickets para la [BrazilJS Conf](http://braziljs.com.br/) están ya a la venta, el evento será del 21 al 22 de Agosto en el centro comercial BarraShoppingSul
* Los tickets para la [NodeConf EU](http://nodeconf.eu/) están ya a la venta, el evento será del 6 al 9 de Septiembre en Waterford, Irlanda
