---
layout: default
title: Interfaz de línea de comandos para WordPress
---

[WP-CLI](https://wp-cli.org/) es la interfaz de línea de comandos para [WordPress](https://wordpress.org/). Puedes actualizar plugins, configurar instalaciones multisitio y mucho más, sin usar un navegador web.

El mantenimiento continuo es <a href="https://make.wordpress.org/cli/2017/04/03/new-co-maintainer-alain-thanks-2017-sponsors/#sponsors">posible gracias a</a>:

<a href="https://automattic.com/"><img src="https://make.wordpress.org/cli/files/2017/04/automattic-1.png" style="width:19%;height:auto;display:inline-block;vertical-align:middle;" alt="" width="160" height="35" class="aligncenter size-full wp-image-347" /></a> <a href="https://www.bluehost.com/"><img class="aligncenter size-full wp-image-335" style="width:19%;height:auto;display:inline-block;vertical-align:middle;" src="https://make.wordpress.org/cli/files/2017/04/bluehost.png" alt="" width="160" height="26" /></a> <a href="https://www.dreamhost.com/"><img class="aligncenter size-full wp-image-324" style="width:19%;height:auto;display:inline-block;vertical-align:middle;" src="https://make.wordpress.org/cli/files/2017/04/dreamhost.png" alt="" width="160" height="30" /></a> <a href="https://www.siteground.com/"><img class="aligncenter size-full wp-image-332" style="width:19%;height:auto;display:inline-block;vertical-align:middle;" src="https://make.wordpress.org/cli/files/2017/04/siteground.png" alt="" width="160" height="33" /></a> <a href="https://wpengine.com/"><img class="aligncenter size-full wp-image-333" style="width:19%;height:auto;display:inline-block;vertical-align:middle;" src="https://make.wordpress.org/cli/files/2017/04/wpengine.png" alt="" width="160" height="30" /></a>

La versión estable actual es la [1.5.1](https://make.wordpress.org/cli/2018/04/21/version-1-5-1-released/). Para estar al día, sigue [@wpcli en Twitter](https://twitter.com/wpcli) o [regístrate para recibir actualizaciones por correo electrónico](https://make.wordpress.org/cli/subscribe/). [Consulta la hoja de ruta](https://make.wordpress.org/cli/handbook/roadmap/) para una visión general de lo que está planeado para las próximas versiones.

[![Build Status](https://travis-ci.org/wp-cli/wp-cli.svg?branch=master)](https://travis-ci.org/wp-cli/wp-cli) [![Average time to resolve an issue](https://isitmaintained.com/badge/resolution/wp-cli/wp-cli.svg)](https://isitmaintained.com/project/wp-cli/wp-cli "Average time to resolve an issue") [![Percentage of issues still open](https://isitmaintained.com/badge/open/wp-cli/wp-cli.svg)](https://isitmaintained.com/project/wp-cli/wp-cli "Percentage of issues still open")

Enlaces rápidos: [Uso](#uso) &#124; [Instalación](#instalación) &#124; [Soporte](#soporte) &#124; [Extendiendo](#extendiendo) &#124; [Contribuyendo](#contribuyendo) &#124; [Créditos](#créditos)

## Uso

WP-CLI proporciona una interfaz de línea de comandos para muchas acciones que puedes realizar en el administrador de WordPress. Por ejemplo, `wp plugin install --activate` ([doc](https://developer.wordpress.org/cli/commands/plugin/install/)) te permite instalar y activar un plugin de WordPress:

```bash
$ wp plugin install user-switching --activate
Installing User Switching (1.0.9)
Downloading install package from https://downloads.wordpress.org/plugin/user-switching.1.0.9.zip...
Unpacking the package...
Installing the plugin...
Plugin installed successfully.
Activating 'user-switching'...
Plugin 'user-switching' activated.
Success: Installed 1 of 1 plugins.
```

WP-CLI también incluye comandos para muchas cosas que no puedes hacer en el administrador de WordPress. Por ejemplo, `wp transient delete --all` ([doc](https://developer.wordpress.org/cli/commands/transient/delete/)) te permite eliminar uno o todos los datos transitorios:

```bash
$ wp transient delete --all
Success: 34 transients deleted from the database.
```

Para una introducción más completa al usar WP-CLI, lee la [guía de inicio rápido](https://make.wordpress.org/cli/handbook/quick-start/). O bien, ponte al día con [shell friends](https://make.wordpress.org/cli/handbook/shell-friends/) para aprender acerca de las utilidades de línea de comandos.

¿Ya te sientes cómodo con lo básico? Ve a la [lista completa de comandos](https://developer.wordpress.org/cli/commands/) para obtener información detallada sobre la gestión de temas y plugins, importación y exportación de datos, realización de operaciones de búsqueda y reemplazo de bases de datos y más.

## Instalación

La descarga del archivo Phar es nuestro método de instalación recomendado para la mayoría de usuarios. Si lo necesitas, consulta también nuestra documentación acerca de [métodos de instalación alternativos](https://wp-cli.org/docs/installing/).

Antes de instalar WP-CLI, asegúrate de que tu entorno cumple con los requisitos mínimos:

- Entorno de tipo UNIX (OS X, Linux, FreeBSD, Cygwin); soporte limitado en el entorno de Windows
- PHP 5.3.29 o posterior
- WordPress 3.7 o posterior. Las versiones anteriores a la última versión de WordPress pueden tener funcionalidad degradada

Una vez que hayas verificado los requisitos, descarga el archivo [wp-cli.phar](https://raw.github.com/wp-cli/builds/gh-pages/phar/wp-cli.phar) usando `wget` o `curl` :

```bash
curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
```

A continuación, comprueba el archivo Phar para verificar que está funcionando:

```bash
php wp-cli.phar --info
```

Para usar WP-CLI desde la línea de comandos tecleando `wp`, haz que el archivo sea ejecutable y muévelo a algún lugar de tu `PATH`. Por ejemplo:

```bash
chmod +x wp-cli.phar
sudo mv wp-cli.phar /usr/local/bin/wp
```

Si WP-CLI se instaló correctamente, deberías ver algo como esto cuando ejecutas `wp --info`:

```bash
$ wp --info
OS:	Darwin 16.7.0 Darwin Kernel Version 16.7.0: Thu Jan 11 22:59:40 PST 2018; root:xnu-3789.73.8~1/RELEASE_X86_64 x86_64
Shell:	/bin/zsh
PHP binary:    /usr/local/bin/php
PHP version:    7.0.22
php.ini used:   /etc/local/etc/php/7.0/php.ini
WP-CLI root dir:        /home/wp-cli/.wp-cli
WP-CLI vendor dir:	    /home/wp-cli/.wp-cli/vendor
WP-CLI packages dir:    /home/wp-cli/.wp-cli/packages/
WP-CLI global config:   /home/wp-cli/.wp-cli/config.yml
WP-CLI project config:
WP-CLI version: 1.5.1
```

### Actualización

Puedes actualizar WP-CLI con `wp cli update` ([doc](https://wp-cli.org/commands/cli/update/)), o repitiendo los pasos de instalación.

Si WP-CLI es propiedad de root u otro usuario del sistema, necesitarás ejecutar `sudo wp cli update`.

¿Quieres vivir la vida al límite? Ejecuta `wp cli update --nightly` para usar la última nightly build de WP-CLI. Una nightly build es más o menos lo suficientemente estable como para que puedas utilizarla en tu entorno de desarrollo, y siempre incluye las últimas y mejores características de WP-CLI.

### Autocompletar con el tabulador

WP-CLI también viene con un scripts para autocompletar con el tabulador para Bash y ZSH. Tan sólo descarga [wp-completion.bash](https://raw.githubusercontent.com/wp-cli/wp-cli/master/utils/wp-completion.bash) y usa el comando `source` desde `~/.bash_profile`:

```bash
source /FULL/PATH/TO/wp-completion.bash
```

No te olvides de ejecutar `source ~ / .bash_profile` después.

Si usa la shell zsh, es posible que debas cargar e iniciar `bashcompinit` antes de usar el comando `source`. Pon lo siguiente en tu `.zshrc`:

```bash
autoload bashcompinit
bashcompinit
source /FULL/PATH/TO/wp-completion.bash
```

## Soporte

Tanto los que mantienen WP-CLI como sus colaboradores tienen disponibilidad limitada para responder preguntas generales de soporte. La [versión actual de WP-CLI](https://make.wordpress.org/cli/handbook/roadmap/) es la única versión oficialmente admitida.

Cuando busques ayuda, primero busca tu pregunta en estos lugares:

* [Problemas comunes y sus soluciones](https://make.wordpress.org/cli/handbook/common-issues/)
* [WP-CLI handbook](https://make.wordpress.org/cli/handbook/)
* [Issues abiertos o cerrados en la organización de WP-CLI GitHub](https://github.com/issues?utf8=%E2%9C%93&q=sort%3Aupdated-desc+org%3Awp-cli+is%3Aissue)
* [Hilos etiquetados con 'WP-CLI' en el foro de soporte de WordPress.org](https://wordpress.org/support/topic-tag/wp-cli/)
* [Preguntas etiquetadas con 'WP-CLI' en el WordPress StackExchange](https://wordpress.stackexchange.com/questions/tagged/wp-cli)

Si no encontraste una respuesta en uno de los lugares anteriores, puedes:

* Únete al canal `#cli` en el [Slack de WordPress.org](https://make.wordpress.org/chat/) para chatear con quien esté disponible en ese momento. Esta opción es la mejor para preguntas rápidas.
* [Publicar un nuevo hilo](https://wordpress.org/support/forum/wp-advanced/#new-post) en el foro de soporte de WordPress.org y etiquetarlo como 'WP-CLI' para que lo vea la comunidad.

Los issues de GitHub están destinados al seguimiento de mejoras y errores de los comandos existentes, no para soporte general. Antes de enviar un informe de errores, por favor [revise nuestras mejores prácticas](https://make.wordpress.org/cli/handbook/bug-reports/) para ayudar a garantizar que tu issue se resuelve de manera oportuna.

Por favor, no hagas preguntas de soporte en Twitter. Twitter no es un lugar aceptable para el soporte porque: Twitter no es un sitio conveniente para hacer soporte: 1) es difícil mantener conversaciones con menos de 140 caracteres, y 2) Twitter no es un lugar donde alguien con tu misma pregunta pueda buscar una respuesta en una conversación previa.

Recuerda, libre != gratis; la licencia open source te da la libertad de usar y modificar, pero no a expensas del tiempo de otras personas. Por favor, se respetuoso y establece tus expectativas en consecuencia.

## Extendiendo

Un **comando** es la unidad atómica de la funcionalidad de WP-CLI. `wp plugin install` ([doc](https://developer.wordpress.org/cli/commands/plugin/install/)) es un comando. `wp plugin activate` ([doc](https://developer.wordpress.org/cli/commands/plugin/activate/)) es otro.

WP-CLI permite registrar cualquier clase, función o closure invocable como un comando. Lee los detalles de uso del PHPdoc de la devolución de llamada. `WP_CLI::add_command()` ([doc](https://make.wordpress.org/cli/handbook/internal-api/wp-cli-add-command/)) se utiliza tanto para el registro de comandos internos y de terceros.

```php
/**
 * Delete an option from the database.
 *
 * Returns an error if the option didn't exist.
 *
 * ## OPTIONS
 *
 * <key>
 * : Key for the option.
 *
 * ## EXAMPLES
 *
 *     $ wp option delete my_option
 *     Success: Deleted 'my_option' option.
 */
$delete_option_cmd = function( $args ) {
	list( $key ) = $args;

	if ( ! delete_option( $key ) ) {
		WP_CLI::error( "Could not delete '$key' option. Does it exist?" );
	} else {
		WP_CLI::success( "Deleted '$key' option." );
	}
};
WP_CLI::add_command( 'option delete', $delete_option_cmd );
```

WP-CLI viene con docenas de comandos. Es más fácil de lo que parece crear un comando WP-CLI personalizado. Lee el [commands cookbook](https://make.wordpress.org/cli/handbook/commands-cookbook/) para obtener más información. Explore los [documentos del API interno](https://make.wordpress.org/cli/handbook/internal-api/) para descubrir una variedad de funciones útiles que puedes usar en su comando WP-CLI personalizado.

## Contribuyendo

Apreciamos que tomes la iniciativa de contribuir con WP-CLI. Es gracias a ti y la comunidad que lo rodea, que WP-CLI es un gran proyecto.

**Contribuir no se limita únicamente al código.** Te animamos a contribuir de la forma que mejor se adapte a tus habilidades, escribiendo tutoriales, haciendo una demostraciones en tu meetup local, ayudando a los demás con sus preguntas de soporte, o revisando nuestra documentación.

Lee atentamente nuestras [pautas de colaboración en el handbook](https://make.wordpress.org/cli/handbook/contributing/) para una introducción completa sobre cómo puedes involucrarte. Seguir estas pautas ayuda a comunicar que respetas el tiempo de otros colaboradores en el proyecto. A su vez, harán todo lo posible para corresponder a ese respeto cuando trabajen contigo, en zonas horarias y en todo el mundo.

## Liderazgo

WP-CLI tiene un encargado del mantenimiento del proyecto: [schlessera](http://github.com/schlessera).

En ocasiones, [concedemos permisos de escritura a los colaboradores](https://make.wordpress.org/cli/handbook/committers-credo/) que han demostrado, durante un período de tiempo, que son capaces e invirtieron en avanzar el proyecto.

Lee el [documento de gobierno en el handbook](https://make.wordpress.org/cli/handbook/governance/) para obtener más detalles operativos acerca del proyecto.

## Créditos

Además de las bibliotecas definidas en [composer.json](composer.json), hemos utilizado código o ideas de los siguientes proyectos:

* [Drush](https://github.com/drush-ops/drush) para... un montón de cosas
* [wpshell](https://code.trac.wordpress.org/browser/wpshell) para `wp shell`
* [Regenerate Thumbnails](https://wordpress.org/plugins/regenerate-thumbnails/) para `wp media regenerate`
* [Search-Replace-DB](https://github.com/interconnectit/Search-Replace-DB) para `wp search-replace`
* [WordPress-CLI-Exporter](https://github.com/Automattic/WordPress-CLI-Exporter) para `wp export`
* [WordPress-CLI-Importer](https://github.com/Automattic/WordPress-CLI-Importer) para `wp import`
* [wordpress-plugin-tests](https://github.com/benbalter/wordpress-plugin-tests/) para `wp scaffold plugin-tests`