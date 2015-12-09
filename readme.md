# WAWAS - The WebAbility(r) PHP Web and Application Server v1.0.3

[![Join the chat at https://gitter.im/webability/WAWAS](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/webability/WAWAS?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

[![Average time to resolve an issue](http://isitmaintained.com/badge/resolution/webability/WAWAS.svg)](http://isitmaintained.com/project/webability/WAWAS "Average time to resolve an issue")
[![Percentage of issues still open](http://isitmaintained.com/badge/open/webability/WAWAS.svg)](http://isitmaintained.com/project/webability/WAWAS "Percentage of issues still open")
[![Join the chat at https://gitter.im/webability](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/webability?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)


This is a real multithreaded application server 100% coded in PHP 7.
It uses the pthreads PECL extension, in CLI mode.

---

## Installation:

### Download and compile PHP7 in CLI mode:
In this example it is compiled and installed into an alternative directory.
It may be the default executable PHP in your OS too.

```bash
./configure --prefix=/usr/local/php7 --exec-prefix=/usr/local/php7 \
   --enable-sockets --enable-pcntl --enable-maintainer-zts \
   --enable-shmop --enable-sysvsem --enable-sysvshm
   # you may add anything you need, for example:
   # --with-pgsql=/usr/pgsql-9.2/ --with-mysqli --with-xmlrpc --with-curl

make
make install
ln -s /usr/local/php7/bin/php /usr/local/bin/php7
/usr/local/php7/bin/pecl install pthreads
```

### Download wawas and install it into a local directory

```bash
cd /home/sites
wget http://webability.info/download/wawas/wawas.tar.gz
tar zxvf wawas.tar.gz
cd wawas
```

### Edit configuration files (IPs to listen to, vhosts, etc)

```bash
vi conf/server.conf
vi conf/http11/vhosts.conf
```

### Go to the main installation directory (where runner.php is placed)

```bash
cd /home/sites/wawas
```

### Run the server:

```bash
php7 runner.php
```

I am working on a wawasctl to put in your /etc/init.d or similar.


---

## TO DO at a glance:

### Server:
- Hooks on modules (working on them)
- implement maxs on #threads, #clients, #hits, sizes, headers etc

### Protocol HTTP11:
- Authentication
- Chunks
- SSL/HTTPS
- Hooks
- gzip/compressed
- etags
- portable vhost names (full named host) to detect variants on resolution
- check anything against RFC to be 100% compliant
- Support big files for sending and streaming (and not saturate the memory) (see mod_static, eventually mod_streaming ?)

### Modules:
- mod_static => check mimes types and errors
- mod_file => DO !
- mod_admin => generate the full admin site, hooks, realtile stats/JSON (Comet?) based on Xamboo
- mod_log => log on vhosts and 
- mod_php => use sandbox ? capture output, errors control, namespaces, overload classes ?
- mod_xamboo => integrates SERVER-APP variables (ej. REMOTE_HOST, REMOTE_ADDR, etc)

### New important modules:
- mod_rediect redirect engine
- mod_session manage sessions

### Other interesting modules:
- Implement PSP (PHP Server Pages)
- servlets
- netbeans ?
- Comet module
- WSDL module

### Examples
- a game, twit app, prives polling, realtime graph, edit document, etc
- terminate the chat

### Admin
- Implement admin console fully realtime



---

## Version Changes Control

### Build 3 2015/12/02
- The engine has been totally rewritten for PHP7, namespaces, pthreads v3, and is now really multithreaded.
- The Xamboo has been integrated with the server as a module. This is the application server.
- The server is stable and can server static files and applications, however it is far to be fully implemented (protocols, modules, etc)


### Build 0002 2012/02/01
- wawasctl adjusted to work with wawas.php
- creation of WAWASBase.lib
- HTTP11: Implementation of LWS in headers parser (RFC 2068 p15, headers can be multilines)
- HTTP11: Multiple same keyword headers are now set into an array
- HTTP11: Implementation of anchor into request parser
- ModuleBox: Integration of Box pattern and module

### Build 0001 2012/02/01
This is the first alpha version.
WAWAS is not still fully funcional and is under heavy developement.
This is an alpha version, and may suffer any type of modifications anytime.
This version "works" more or less, and may have lots of bugs.
This is not a stable version or an official release.
Do not use it for production sites.

