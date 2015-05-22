# Publicaciones de io.js 2.0.0
Esta semana publicamos dos versiones de io.js, la [v2.0.0](https://iojs.org/dist/v2.0.0/) y [v2.0.1](https://iojs.org/dist/v2.0.1/), el listado de cambios completo está disponible [en GitHub](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md).

### Notable changes

#### 2.0.1
* **async_wrap**: (Trevor Norris) [#1614](https://github.com/iojs/io.js/pull/1614)
  - ahora es posible filtrar por proveedores
  - pequeños flags han sido removidos y reemplazados con llamadas a métodos en el objeto vinculante
  - _ten en cuenta que esta es una API inestable, y las adiciones de fetaures y cambios profundos no cambiarán la versión de semver_
* **libuv**: resuelve numerosos issues de io.js:
  - [#862](https://github.com/iojs/io.js/issues/862) previene la creación de procesos hijos con descriptores de stdio inválidos
  - [#1397](https://github.com/iojs/io.js/issues/1397) corrige el error EPERM con fs.access(W_OK) sobre Windows
  - [#1621](https://github.com/iojs/io.js/issues/1621) construye errores asociados al empaquetado de libuv
  - [#1512](https://github.com/iojs/io.js/issues/1512) debe finalizar apropiadamente errores
* **addons**: la macro `NODE_DEPRECATED` estaba causando problemas al compilar complementos con compiladores antiguos, esto debería haberse resuelto (Ben Noordhuis) [#1626](https://github.com/iojs/io.js/pull/1626)
* **V8**: se actualiza V8 de 4.2.77.18 a 4.2.77.20 con cambios menores, incluido un bug que prevenía compilaciones sobre FreeBSD

#### 2.0.0
* **crypto**: se reduce significativamente el uso de memoria para TLS (Fedor Indutny & Сковорода Никита Андреевич) [#1529](https://github.com/iojs/io.js/pull/1529)
* **net**: `socket.connect()` ahora recibe la opción `'lookup'` para un mecanismo de resolución DNS personalizado, siendo el predeterminado `dns.lookup()` (Evan Lucas) [#1505](https://github.com/iojs/io.js/pull/1505)
* **npm**: Actualizado a npm 2.9.0. Vea las notas de publicación de [v2.8.4](https://github.com/npm/npm/releases/tag/v2.8.4) y [v2.9.0](https://github.com/npm/npm/releases/tag/v2.9.0) para más detalles. Puntos notables:
  - Soporte agregado para el campo de autor predeterminado al hacer `npm init -y` funciona sin interacción de usuario (@othiym23) [npm/npm/d8eee6cf9d](https://github.com/npm/npm/commit/d8eee6cf9d2ff7aca68dfaed2de76824a3e0d9af)
  - Incluye módulos locales en `npm outdated` y `npm update` (@ArnaudRinquin) [npm/npm#7426](https://github.com/npm/npm/issues/7426)
  - El prefijo usado antes del número de versión en `npm version` ahora se puede configurar mediante `tag-version-prefix` (@kkragenbrink) [npm/npm#8014](https://github.com/npm/npm/issues/8014)
* **os**: `os.tmpdir()` ahora es consistente con multi-platforma y no seguirá retornando una ruta con un slash al final en cualquier plataforma (Christian Tellnes) [#747](https://github.com/iojs/io.js/pull/747)
* **process**:
  - El rendimiento de `process.nextTick()` ha mejorado entre 2 y 42% alrededor de la suite de medición, es notable porque es fuertemente utilizado alrededor del núcleo (Brian White) [#1571](https://github.com/iojs/io.js/pull/1571)
  - Los nuevos métodos `process.geteuid()`, `process.seteuid(id)`, `process.getegid()` and `process.setegid(id)` te permiten obtener y establecer de manera efectiva el UID y GID del proceso (Evan Lucas) [#1536](https://github.com/iojs/io.js/pull/1536)
* **repl**:
  - El historial de REPL ahora persiste entre sesiones si la variable de entorno `NODE_REPL_HISTORY_FILE` está establecida a un archivo accesible al usuario, `NODE_REPL_HISTORY_SIZE` permite establecer el tamaño máximo del historial y está predeterminado a `1000` (Chris Dickinson) [#1513](https://github.com/iojs/io.js/pull/1513)
  - El REPL puede ser ubicado en uno de los tres modos usando la variable de entorno `NODE_REPL_MODE`: `sloppy`, `strict` o `magic` (predeterminado); el nuevo modo `magic` ejecutará automáticamente las expresiones "strict mode only" en _strict_ mode (Chris Dickinson) [#1513](https://github.com/iojs/io.js/pull/1513)
* **smalloc**: el módulo 'smalloc' ha sido deprecado debido a los cambios de V8 4.4 que la harán inservible.
* **util**: se agrega a Promise, Map y Set soporte de inspección (Christopher Monsanto) [#1471](https://github.com/iojs/io.js/pull/1471)
* **V8**: se actualizó a 4.2.77.18, mira el registro de cambios completo [ChangeLog](https://chromium.googlesource.com/v8/v8/+/refs/heads/4.2.77/ChangeLog) para más detalles. Cambios notables:
  - Las clases se han movido fuera del área de preparación; la palabra reservada `class` ahora es usable en _strict mode_ sin flags
  - Las mejoras de _object literals_ se han movido fuera del área de preparación; la sintáxis de shorthand para métodos y propiedades ahora es usable (`{ method() { }, property }`)
  - Los _rest parameters_ (`function(...args) {}`) se han implementado en el área de preparación detrás de la flag `--harmony-rest-parameters`
  - Los nombres de propiedad computados (`{['foo'+'bar']:'bam'}`) se han implementado en el área de preparación detrás de la flag `--harmony-computed-property-names`
  - Los escapes de unicode (`'\u{xxxx}'`) se han implementado en el área de preparación detrás de la flag `--harmony_unicode` y la flag `--harmony_unicode_regexps` para su uso en expresiones regulares
* **Windows**:
  - La terminación anómala de procesos se ha corregido (Fedor Indutny)  [#1512](https://github.com/iojs/io.js/issues/1512) / [#1563](https://github.com/iojs/io.js/pull/1563)
  - El evento de carga pendiente introducido para corregir problemas con el nombre de procesos (iojs.exe / node.exe) se hizo opt-out para complementos nativos. Los complementos nativos deben incluir `'win_delay_load_hook': 'false'` en su binding.gyp para deshabilitar esta característica si experimentan problemas. (Bert Belder) [#1433](https://github.com/iojs/io.js/pull/1433)
* **Governance**:
  - Rod Vagg (@rvagg) fue agregado al Technical Committee (TC)
  - Jeremiah Senkpiel (@Fishrock123) fue agregado al Technical Committee (TC)

### Breaking changes

Todos los detalles en https://github.com/iojs/io.js/wiki/Breaking-Changes#200-from-1x

* V8 se actualiza a to 4.2, con cambios menores en la API de C++
* `os.tmpdir()` ahora es consistente con multi-platformas y no seguirá retornando una ruta con un slash al final en cualquier plataforma
* Aunque no es un *breaking change* el módulo 'smalloc' ha sido deprecado en anticipación a la pérdida de soporte en una futura actualización a  V8 4.4. Vea [#1451](https://github.com/iojs/io.js/issues/1451) para mayor información.

_Nota: una nueva versión del módulo 'url' fue revertida antes de la publicación ya que se determina que el potencial de rompimiento alrededor del ecosistema npm era muy grande y que se necesita trabajar más en la compatibilidad antes de liberarlo. Vea [#1602](https://github.com/iojs/io.js/pull/1602) para más información._

### Problemas conocidos
Vea https://github.com/iojs/io.js/labels/confirmed-bug para una lista completa y más actual de los problemas conocidos.

* Algunos problemas con timers no referenciados ejecutandose durante `beforeExit` aún se encuentran por resolver. Vea [#1264](https://github.com/iojs/io.js/issues/1264).
* Un par suplente en el REPL puede congelar la terminal [#690](https://github.com/iojs/io.js/issues/690)
* `process.send()` no es una acción síncrona como la documentación sugiere, una regresión introducida en el 1.0.2, vea [#760](https://github.com/iojs/io.js/issues/760) y la solución en el [#774](https://github.com/iojs/io.js/issues/774)
* Llamar a `dns.setServers()` mientras una consulta DNS está en progreso puede ocasionar que el proceso falle en una afirmación fallida [#894](https://github.com/iojs/io.js/issues/894)
* `url.resolve` puede transferir una porción de la autorización de la url mientras se resuelve entre dos hosts, vea [#1435](https://github.com/iojs/io.js/issues/1435).
* readline: los escapes de separación se están procesando incorrectamente, vea [#1403](https://github.com/iojs/io.js/issues/1403)

### Actualizaciones de la comunidad

* Michael Dawson crea la [WG proposal](https://github.com/mhdawson/workgroup-proposals) bajo la Node Foundation.
* Mikeal Rogers escribe acerca del crecimiento con io.js [en Medium](https://medium.com/node-js-javascript/growing-up-27d6cc8b7c53).
* La [publicación](https://www.codeschool.com/blog/2015/05/08/whats-new-in-io-js-2-0-0/) de CodeSchool sobre lo nuevo en io.js 2.0.0
* El Node Lead, TJ Fontaine [se retira](http://blog.nodejs.org/2015/05/08/next-chapter/) de su puesto.

### Próximos eventos

* Los tickets para la [NodeConf](http://nodeconf.com/) están ya a la venta, el evento será del 11 al 14 de junio en Walker Creek Ranch, CA
* Los tickets para [CascadiaJS](http://2015.cascadiajs.com/) están ya a la venta, el evento será del 8 al 10 de julio en el Estado de Washington
* Los tickets para la [BrazilJS Conf](http://braziljs.com.br/) están ya a la venta, el evento será del 21 al 22 de Agosto en el centro comercial BarraShoppingSul
* Los tickets para la [NodeConf EU](http://nodeconf.eu/) están ya a la venta, el evento será del 6 al 9 de Septiembre en Waterford, Irlanda
