template: doc.html
title: News

_TOC_TOP_

.. contents::
    :backlinks: top

_TOC_BOT_

0.11.2 / 2010-10-30
-------------------

* Add SERVER_SOFTWARE to the os.environ
* Add support for django settings environement variable
* Add support for logging configuration in Paster ini-files
* Improve arbiter notification in asynchronous workers
* Display the right error when a worker can't be used
* Fix Django support
* Fix HUP with Paster applications
* Fix readline in wsgi.input

0.11.1 / 2010-09-02
-------------------

* Implement max-requests feature to prevent memory leaks.
* Added 'worker_exit' server hook.
* Reseed the random number generator after fork().
* Improve Eventlet worker.
* Fix Django command `run_gunicorn`.
* Fix the default proc name internal setting.
* Workaround to prevent Gevent worker to segfault on MacOSX.

0.11.0 / 2010-08-12
-------------------

* Improve dramatically performances of Gevent and Eventlet workers
* Optimize HTTP parsing
* Drop Server and Date headers in start_response when provided.
* Fix latency issue in async workers

0.10.1 / 2010-08-06
-------------------

* Improve gevent's workers. Add "egg:gunicorn#gevent_wsgi" worker using 
  `gevent.wsgi <http://www.gevent.org/gevent.wsgi.html>`_ and 
  "egg:gunicorn#gevent_pywsgi" worker using `gevent.pywsgi 
  <http://www.gevent.org/gevent.pywsgi.html>`_ .
  **"egg:gunicorn#gevent"** using our own HTTP parser is still here and
  is **recommended** for normal uses. Use the "gevent.wsgi" parser if you
  need really fast connections and don't need streaming, keepalive or ssl.
* Add pre/post request hooks
* Exit more quietly
* Fix gevent dns issue
  
0.10.0 / 2010-07-08
-------------------

* New HTTP parser.
* New HUP behaviour. Re-reads the configuration and then reloads all
  worker processes without changing the master process id. Helpful for
  code reloading and monitoring applications like supervisord and runit.
* Added a preload configuration parameter. By default, application code
  is now loaded after a worker forks. This couple with the new HUP
  handling can be used for dev servers to do hot code reloading. Using
  the preload flag can help a bit in small memory VM's.
* Allow people to pass command line arguments to WSGI applications. See:
  `examples/alt_spec.py
  <http://github.com/benoitc/gunicorn/raw/master/examples/alt_spec.py>`_
* Added an example gevent reloader configuration:
  `examples/example_gevent_reloader.py
  <http://github.com/benoitc/gunicorn/blob/master/examples/example_gevent_reloader.py>`_.
* New gevent worker "egg:gunicorn#gevent2", working with gevent.wsgi.
* Internal refactoring and various bug fixes.
* New documentation website.

0.9.1 / 2010-05-26
------------------

* Support https via X-Forwarded-Protocol or X-Forwarded-Ssl headers
* Fix configuration
* Remove -d options which was used instead of -D for daemon.
* Fix umask in unix socket

0.9.0 / 2010-05-24
------------------

* Added *when_ready* hook. Called just after the server is started 
* Added *preload* setting. Load application code before the worker processes
  are forked.
* Refactored Config
* Fix pidfile
* Fix QUIT/HUP in async workers
* Fix reexec
* Documentation improvements

0.8.1 / 2010-04-29
------------------

* Fix builtins import in config
* Fix installation with pip
* Fix Tornado WSGI support
* Delay application loading until after processing all configuration

0.8.0 / 2010-04-22
------------------

* Refactored Worker management for better async support. Now use the -k option
  to set the type of request processing to use
* Added support for Tornado_


0.7.2 / 2010-04-15
------------------

* Added --spew option to help debugging (installs a system trace hook)
* Some fixes in async arbiters
* Fix a bug in start_response on error

0.7.1 / 2010-04-01
------------------

* Fix bug when responses have no body.

0.7.0 / 2010-03-26
------------------

* Added support for Eventlet_ and Gevent_ based workers.
* Added Websockets_ support
* Fix Chunked Encoding
* Fix SIGWINCH on OpenBSD_
* Fix `PEP 333`_ compliance for the write callable.

0.6.5 / 2010-03-11
------------------

* Fix pidfile handling
* Fix Exception Error

0.6.4 / 2010-03-08
------------------

* Use cStringIO for performance when possible.
* Fix worker freeze when a remote connection closes unexpectedly.

0.6.3 / 2010-03-07
------------------

* Make HTTP parsing faster.
* Various bug fixes

0.6.2 / 2010-03-01
------------------

* Added support for chunked response.
* Added proc_name option to the config file.
* Improved the HTTP parser. It now uses buffers instead of strings to store
  temporary data.
* Improved performance when sending responses.
* Workers are now murdered by age (the oldest is killed first).


0.6.1 / 2010-02-24
------------------

* Added gunicorn config file support for Django admin command
* Fix gunicorn config file. -c was broken.
* Removed TTIN/TTOU from workers which blocked other signals.

0.6 / 2010-02-22
------------------

* Added setproctitle support
* Change privilege switch behavior. We now work like NGINX, master keeps the
  permissions, new uid/gid permissions are only set for workers.

0.5.1 / 2010-02-22
------------------

* Fix umask
* Added Debian packaging

0.5 / 2010-02-20 
----------------

* Added `configuration file <configuration.html>`_ handler.
* Added support for pre/post fork hooks
* Added support for before_exec hook
* Added support for unix sockets
* Added launch of workers processes under different user/group
* Added umask option
* Added SCRIPT_NAME support
* Better support of some exotic settings for Django projects
* Better support of Paste-compatible applications
* Some refactoring to make the code easier to hack
* Allow multiple keys in request and response headers

.. _Tornado: http://www.tornadoweb.org/
.. _`PEP 333`: http://www.python.org/dev/peps/pep-0333/
.. _Eventlet: http://eventlet.net
.. _Gevent: http://gevent.org
.. _OpenBSD: http://openbsd.org
.. _Websockets: http://dev.w3.org/html5/websockets/
