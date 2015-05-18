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
  - El REPL puede ser ubicado en uno de los tres modos usando la variable de entorno `NODE_REPL_MODE`: `sloppy`, `strict` o `magic` (predeterminado); el nuevo modo `magic` automáticamente ejecutará las expresiones "strict mode only" en _strict_ mode (Chris Dickinson) [#1513](https://github.com/iojs/io.js/pull/1513)
* **smalloc**: el módulo 'smalloc' ha sido deprecado debido a los cambios que se vienen en V8 4.4 que la volverán inusable.
* **util**: se agrega a Promise, Map y Set soporte de inspección (Christopher Monsanto) [#1471](https://github.com/iojs/io.js/pull/1471)
* **V8**: se actualizó a 4.2.77.18, mira el registro de cambios completo [ChangeLog](https://chromium.googlesource.com/v8/v8/+/refs/heads/4.2.77/ChangeLog) para más detalles. Cambios notables:
  - Las clases se han movido fuera del área de preparación; la palabra reservada `class` ahora es usable en _strict mode_ sin flags
  - Las mejoras de object literals se han movido fuera del área de preparación; la sintáxis de shorthand para métodos y propiedades ahora es usable (`{ method() { }, property }`)
  - Rest parameters (`function(...args) {}`) se han implementado en el área de preparación detrás de la flag `--harmony-rest-parameters`
  - Computed property names (`{['foo'+'bar']:'bam'}`) are implemented in staging behind the `--harmony-computed-property-names` flag
  - Unicode escapes (`'\u{xxxx}'`) are implemented in staging behind the `--harmony_unicode` flag and the `--harmony_unicode_regexps` flag for use in regular expressions
* **Windows**:
  - Random process termination on Windows fixed (Fedor Indutny)  [#1512](https://github.com/iojs/io.js/issues/1512) / [#1563](https://github.com/iojs/io.js/pull/1563)
  - The delay-load hook introduced to fix issues with process naming (iojs.exe / node.exe) has been made opt-out for native add-ons. Native add-ons should include `'win_delay_load_hook': 'false'` in their binding.gyp to disable this feature if they experience problems . (Bert Belder) [#1433](https://github.com/iojs/io.js/pull/1433)
* **Governance**:
  - Rod Vagg (@rvagg) was added to the Technical Committee (TC)
  - Jeremiah Senkpiel (@Fishrock123) was added to the Technical Committee (TC)

### Breaking changes

Full details at https://github.com/iojs/io.js/wiki/Breaking-Changes#200-from-1x

* V8 upgrade to 4.2, minor changes to C++ API
* `os.tmpdir()` is now cross-platform consistent and will no longer returns a path with a trailling slash on any platform
* While not a *breaking change* the 'smalloc' module has been deprecated in anticipation of it becoming unsupportable with a future upgrade to V8 4.4. See [#1451](https://github.com/iojs/io.js/issues/1451)  for further information.

_Note: a new version of the 'url' module was reverted prior to release as it was decided the potential for breakage across the npm ecosystem was too great and that more compatibility work needed to be done before releasing it. See [#1602](https://github.com/iojs/io.js/pull/1602) for further information._

### Known issues
See https://github.com/iojs/io.js/labels/confirmed-bug for complete and current list of known issues.

* Some problems with unreferenced timers running during `beforeExit` are still to be resolved. See [#1264](https://github.com/iojs/io.js/issues/1264).
* Surrogate pair in REPL can freeze terminal [#690](https://github.com/iojs/io.js/issues/690)
* `process.send()` is not synchronous as the docs suggest, a regression introduced in 1.0.2, see [#760](https://github.com/iojs/io.js/issues/760) and fix in [#774](https://github.com/iojs/io.js/issues/774)
* Calling `dns.setServers()` while a DNS query is in progress can cause the process to crash on a failed assertion [#894](https://github.com/iojs/io.js/issues/894)
* `url.resolve` may transfer the auth portion of the url when resolving between two full hosts, see [#1435](https://github.com/iojs/io.js/issues/1435).
* readline: split escapes are processed incorrectly, see [#1403](https://github.com/iojs/io.js/issues/1403)

### Community Updates

* Michael Dawson creates [WG proposal](https://github.com/mhdawson/workgroup-proposals) under the Node Foundation.
* Mikeal Rogers wrote about growing up of io.js [on Medium](https://medium.com/node-js-javascript/growing-up-27d6cc8b7c53).
* CodeSchool [blog post](https://www.codeschool.com/blog/2015/05/08/whats-new-in-io-js-2-0-0/) on what's new in io.js 2.0.
* Node Lead TJ Fontaine [steps back](http://blog.nodejs.org/2015/05/08/next-chapter/) from leader.

# Próximos eventos

* Los tickets para la [NodeConf](http://nodeconf.com/) están ya a la venta, el evento será del 11 al 14 de junio en Walker Creek Ranch, CA
* Los tickets para [CascadiaJS](http://2015.cascadiajs.com/) están ya a la venta, el evento será del 8 al 10 de julio en el Estado de Washington
* Los tickets para la [BrazilJS Conf](http://braziljs.com.br/) están ya a la venta, el evento será del 21 al 22 de Agosto en el centro comercial BarraShoppingSul
* Los tickets para la [NodeConf EU](http://nodeconf.eu/) están ya a la venta, el evento será del 6 al 9 de Septiembre en Waterford, Irlanda
