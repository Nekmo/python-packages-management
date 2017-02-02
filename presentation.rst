
.. title: Gestión de paquetes y entornos en Python

:data-transition-duration: 500
:css: css/presentation.css
:css: css/monokai.css

----

:id: titulo

########################################
Gestión de paquetes y entornos en Python
########################################

.. note::

    Buenas. Estoy aquí para presentar la gestión de paquetes y entornos en Python. Esta presentación es de iniciación, aunque para no aburrir a los más avanzados incluiré algunos detalles poco conocidos. Por querer contentar a todo el mundo, la presentación ha quedado más extensa que lo planeado, por lo que seguramente no de tiempo a hacer demostraciones, y tendré que ir más rápido de lo que em gustaría. Esta misma presentación está disponible en Github, por si queréis volverla a ver.
    
    Los que habéis empezado a aprender Python, tal vez no hayáis tenido la necesidad de usar más bibliotecas que las incluidas. Esto es gracias a que, como decimos...

----

:id: baterias

Se dice que...

Python trae **baterías incluidas**

.. note::

    Python, trae pilas incluidas.

----

:id: baterias-imagen

.. image:: images/Python_batteries_included.jpg
   :height: 300px
   
----

:id: casi-1

Esto es, que trae módulos para *CASI* todo.

----

:id: casi-2

CASI

----

:id: usar-python

Cuando Python no incluye lo que necesitamos, podemos instalarlo a través de ``Pip``.

.. note::

    Pero en ocasiones, no incluye lo que necesitamos, y para eso tenemos Pip.

----

:id: pip

Pip
===
Es el **gestor de paquetes** de Python que sustituye a ``easy_install`` desde *2008*. 

----

:id: ejemplo-instalar-pip

Ejemplo: instalar requests
--------------------------

Para instalar el paquete ``requests``, que facilita las consultas http:

.. code-block:: bash

    $ sudo pip install requests
    
.. note::

    Requests es una biblioteca que hace más humano el realizar consultas a servidores http.

----

:id: donde-paquetes-1

¿Y dónde puedo encontrar paquetes?
----------------------------------

* **Proyectos populares en Github**: https://github.com/trending/python
* **Paquetes recomendados para Python**: https://github.com/vinta/awesome-python
* **Los módulos más descargados**: http://pypi-ranking.info/alltime
* Tira de Google.

.. note::

    Y para encontrar más bibliotecas geniales para completar Python, aquí tenéis algunos enlaces. El primero es especialmente recomendable. Es un listado por categorías con lo mejor de Python. Sólo lo mejor.

----

:id: donde-paquetes-2

La mayoría de paquetes Python dicen **cómo instalarlos** *usando Pip*

.. image:: images/pip_install_sqlalchemy.png
   :height: 300px
   
.. note::

    Para saber cómo instalarlos mediante Pip, sólo hay que leer la documentación del paquete. En la mayoría dicen cómo. Por ejemplo, aquí la de SQLAlchemy diciendo cómo.

----

:id: pypi-1

¿Dónde se encuentran los paquetes de Pip?
-----------------------------------------
Subidos en **Pypi**. Puedes buscar los paquetes existentes en:

https://pypi.python.org/pypi

Además, puedes subir **tus propios paquetes**.

.. note::

    ¿Pero dónde residen realmente estos paquetes? En los repositorios oficiales de Python.

----

:id: pypi-2

.. image:: images/pypi-python-org.png

.. note::

    Aquí tenéis una captura de cómo es.

----

:id: pypi-3

También puedes echarle un vistazo al **próximo** portal de *Pypi*:

.. image:: images/pypi-org.png

.. note::

    Y éste es el que será el nuevo portal del repositorio.

----

:id: pip-versiones

Especificar versión
-------------------

Por si hubiese incompatibilidades, es posible **restringir la versión**:

.. code-block:: bash

    pip install 'Django>=1.7'
    pip install 'Django==1.8.3'
    pip install 'Django~=1.8'  # 1.8.x
    pip install 'Django>=1.8.2,<=1.8.10'
    
.. note::

    Pero los paquetes tienen también dependencias. Y en ocasiones es necesario restringir la versión.

----

:id: pip-instalar-metodos

Y si no se encuentra en Pypi...
-------------------------------
Puedes instalarlo de infinidad de otras formas:

* Desde una **ruta local**: ``pip install /home/nekmo/myPackage``
* Usando una **url**: ``pip install http://domain/myPackage.zip``
* Con un **VCS** (Git/Hg/Bzr/Svn).

.. code-block:: bash

    $ pip install git+https://github.com/Nekmo/os3.git@master#egg=os3
    
.. note::

    Ya hemos visto el repositorio oficial. Pero en ocasiones no es así, y hace falta instalarlo por otro medio. Por suerte, Python soporta bastantes medios. Por ejemplo, es posible instalarlo de Github usando Git.

----

:id: comandos-pip

Otros comandos de ``pip`` de interés
------------------------------------

* ``pip download <package>``: sólo **descargar** el paquete.
* ``pip list``: **listar** los paquetes instalados.
* ``pip uninstall <package>``: **desinstalar** el paquete.
* ``pip search <query>``: **Buscar** en Pypi.
* ``pip check``: Comprobar **incompatibilidades** entre paquetes instalados.
* ``pip freeze``: Generar **listado de dependencias**. Profundizaremos sobre este comando más adelante.

.. note::

    Aquí una lista de los comandos más útiles de Pip. Aunque parezcan básicos, ``easy_install`` no permitía en su momento ni desinstalar paquetes.

----

:id: comandos-pip-install-title

Parámetros útiles de ``pip install``
------------------------------------

.. note::

    Y aquí parámetros de Pip install, el subcomando más empleado de Pip.

----

:id: comandos-pip-install-1

Editable
^^^^^^^^
Usando ``-e``, se instala usando ``develop``. Esto es, que el paquete puede *editarse* en local y no hace falta reinstalarlo para aplicar los cambios.

.. code-block:: bash

    $ pip install -e ~/Projects/myProject
    

Upgrade
^^^^^^^
Es posible llevar un paquete a la **última versión** con:

.. code-block:: bash

    $ pip install --upgrade my-package

    
.. note::

    Editable permite tener tu proyecto en local, y seguir mejorándolo y usándolo en otros proyectos al mismo tiempo. No hará falta reinstalar por cada mejora. Upgrade es para actualizar, como su nombre dice.
    
----

:id: comandos-pip-install-2
    
Pre-release
^^^^^^^^^^^
Por defecto, Pypi instala los paquetes **estables**. Pero es posible instalar los que están en **desarrollo**:

.. code-block:: bash

    $ pip install --pre my-package
   

Instalar en tu usuario
^^^^^^^^^^^^^^^^^^^^^^
Pip instala los paquetes a nivel de sistema por defecto (lo cual requiere root). No obstante, es posible instalarlo en **tu usuario**.

.. code-block:: bash

    $ pip install --user my-package
    
    
.. note::

    ``--pre`` permite instalar versiones de paquetes que aún no son estables. Con ``--user`` puedes instalar paquetes en tu usuario, por separado de los del sistema.
    
----

:id: comandos-pip-install-3

Cambiar o añadir repositorio
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Por **defecto**, ``pip`` usa como *repositorio* para descargar los paquetes::

    https://pypi.python.org/simple/
    
No obstante, es posible cambiarlo con ``--index-url``. Y añadir **repositorios extra** por si no estuviese el paquete en el *rep. principal* con el parámetro ``--extra-index-url``. Por ejemplo, para usar el *repositorio de pruebas* (para cuando se está aprendiendo a crear paquetes)::

    https://testpypi.python.org/simple/
    
Para saber cómo crear nuestro propio repositorio: https://github.com/pypiserver/pypiserver


.. note::

    Y con ``--index-url`` y ``--extra-index-url`` se puede cambiar o añadir el repositorio a usar. También podemos crear nuestro propio repositorio.

----

:id: instalar-pip

Instalar Pip
------------
Por si no se encontrase instalado en el sistema, podemos **instalarlo** con:

.. code-block:: bash

    $ sudo apt install python-pip  # Debian/Ubuntu
    $ sudo dnf -y install python-pip  # Fedora
    $ sudo pacman -S python-pip
    
Y si no con:

.. code-block:: bash

    $ wget https://bootstrap.pypa.io/get-pip.py
    $ python get-pip.py
   

.. note::

    Pip se encuentra ya instalado en muchos sistemas GNU/Linux, pero es posible instalarlo por el sistema o con un script.
    
----

:id: conflictos-paquetes-1

Conflictos entre paquetes
=========================

Ya sabemos cómo instalar paquetes externos. 

*¿Pero qué pasa si tenemos conflictos entre ellos?*

.. note::

    Pero a medida que se instalan paquetes, nos encontramos con conflictos entre ellos, sobre todo cuando instalamos paquetes que tienen como dependencia otros paquetes.

----

:id: conflictos-paquetes-2

**Ejemplo:** tenemos *2 proyectos*, ``A`` y ``B``, con dependencia en diferentes versiones de Django.

* **Proyecto A:** requiere ``Django >= 1.8, <= 1.10``.
* **Proyecto B:** requiere ``Django <=1.7, >= 1.4``.

.. note::

    Por ejemplo, tenemos 2 proyectos, uno nuevo usando una de las versiones más nuevas de Django, y otro más antiguo que requiere una versión anterior de Django. ¿Qué podemos hacer?

----

:id: conflictos-paquetes-3

Solución: **virtualenvs**

.. note::

    Virtualenvs.

----

:id: virtualenvs

Virtualenvs
===========
Son *entornos* de Python **independientes al del sistema,** con sus propios paquetes instalados.

*Algunos ejemplos de uso son...*

.. note::

    Los virtualenvs son entornos aislados e independientes, y en cada uno de ellos podemos instalar una versión de Django y Python.

----

:id: virtualenvs-ejemplo-conflictos

soluciona conflictos
--------------------

Gracias a los virtualenvs, podemos tener 2 entornos distintos: uno para el *proyecto A*, 
con ``Django >= 1.9``, y otro con ``Django <= 1.7`` en el *proyecto B*.

.. note::

     Tendremos un virtualenv por proyecto, ejecutándose los proyectos dentro de sus virtualenvs.

----

:id: virtualenvs-ejemplo-pruebas

Para pruebas
------------

Además, podemos usar los virtualenvs **para probar paquetes sin instalarlos** a nivel del sistema,
o para **crear entornos a replicar en otros sistemas**, cosa que veremos más adelante.

.. note::

    También podemos usarlo para probar paquetes sin necesidad de instalarlos en el sistema.

----

:id: virtualenvs-ejemplo-actualizacion

Aislar y evitar sorpresas
-------------------------

Los virtualenvs también nos salvan de *sorpresas* al **actualizar el sistema**: un ``apt upgrade`` podría romper nuestros proyectos sin saberlo.

.. note::

    Y por si fuera poco, nos protege ante sorpresas indeseadas. Por ejemplo, si no usásemos virtualenvs, podríamos cargarnos nuestros proyectos sólo por actualizar el sistema.

----

:id: instalar-virtualenvs

Cómo crear un virtualenv
------------------------
Tras instalar ``virtualenv``, podemos **crear un virtualenv** con:

.. code-block:: bash
    
    [nekmo@homura /tmp]$ virtualenv venv
    Running virtualenv with interpreter /usr/bin/python2
    New python executable in venv/bin/python2
    Also creating executable in venv/bin/python
    Installing setuptools, pip...done.
    
.. note::

    Para crear un virtualenv, sólo debemos usar el comando ``virtualenv``, junto con el nombre del mismo. Se creará un directorio con dicho nombre donde nos encontremos.

----

:id: entrar-virtualenv

Cómo entrar en un virtualenv
----------------------------
Debemos ejecutar:

.. code-block:: bash
    
    [nekmo@homura /tmp]$ source venv/bin/activate
    (venv)[nekmo@homura /tmp]$ 
    
Véase que ahora, al inicio del *prompt*, tenemos *entre paréntesis* el nombre del virtualenv:

.. code-block:: bash
    
    (venv)[nekmo@homura /tmp]$ 
    
Esto significa, que tenemos el virtualenv **activado**. Podremos movernos con libertad, y seguiremos en el virtualenv mientras aparezca delante ese indicativo.

.. note::

    Para iniciar el virtualenv, cargamos el script ``activate`` al shell. Sabremos que está activado por el nombre del virtualenv al inicio de la línea de comandos.

----

:id: salir-virtualenv

Cómo salir de un virtualenv
---------------------------
Debemos ejecutar ``deactivate``. Tras ejecutarlo, desaparecerá el nombre del virtualenv en el prompt:

.. code-block:: bash
    
    (venv)[nekmo@homura /tmp]$ deactivate 
    [nekmo@homura /tmp]$

Tras salir del virtualenv, podremos crear otro donde podremos instalar otros paquetes, manteniéndose aislados.

.. note::

    Para poder salir del virtualenv, usamos ``deactivate``. Tras hacerlo desaparecerá el nombre del virtualenv al inicio de la línea.

----

:id: instalar-virtualenv

Instalar virtualenv
-------------------
Podemos instalarlo bien **por el sistema**, o haciendo uso de **pip**, como cualquier otro paquete:

.. code-block:: bash

    $ sudo pip install virtualenv
    
.. note::

    Para instalarlo, podemos instalarlo por el sistema, o por ``pip``, que para eso está.
    
----

:id: como-funcionan-virtualenvs-1

Cómo funciona
-------------
El archivo ``./bin/activate`` del ``venv`` es un fichero en bash, que si lo leemos, encontramos:

.. code-block:: bash

    PATH="$VIRTUAL_ENV/bin:$PATH"
    export PATH

Con esto lo que hacemos es añadir el directorio ``./bin/`` al ``$PATH``.

.. note::

    Aunque todo esto parezca magia, en realidad no lo es. Si miramos el archivo ``activate``, vemos que modifica la variable ``$PATH`` para poner el directorio ``./bin`` del virtualenv como prioritario.

----

:id: como-funcionan-virtualenvs-2

Si miramos este directorio, encontramos:

.. code-block:: bash

    (test)[nekmo@homura /tmp/env]$ ls -1
    activate
    ...
    easy_install
    pip
    **python**
    ...


.. note::

    Esto es porque si miramos dicho directorio, encontramos otro intérprete de ``python``, el del virtualenv.

----

:id: como-funcionan-virtualenvs-3

Esto *sustituye* el binario de ``python`` del sistema por el del virtualenv.

Para determinar el directorio de las bibliotecas, lo que hace es buscarse el directorio que **contiene** ``./lib/pythonX.Y/os.py`` desde el directorio del ejecutable de Python. Si no se encuentra, se van **bajando niveles** hasta encontrarlo:


.. code-block:: bash

    ./venv/bin/lib/python2.7/os.py << No existe, sigo bajando...
    ./venv/lib/python2.7/os.py << ¡Existe! ¡Usaré este directorio!
    
.. note::

    Así pues, usará éste en lugar del del sistema. El intérprete de Python usará a su vez la carpeta de bibliotecas que se encuentra junto con intérprete. Para ser exactos, buscará el archivo ``os.py`` como aquí se muestra, e irá bajando niveles hasta entontrarlo, en el caso de los virtualenvs, en el segundo nivel.
    
----

:id: gestionar-virtualenvs

Pero ahora tengo muchos virtualenvs...

**¿cómo los gestiono?**

.. note::

    Los virtualenvs son muy útiles, pero llega un momento en que tienes muchos. ¿Cómo gestionarlos?

----

:id: virtualenvwrapper

Virtualenvwrapper
=================
Permite gestionar los virtualenvs *identificándolos por un nombre*, y organizados en un directorio común. Para instalarlo, usamos de nuevo ``pip``:

.. code-block:: bash

    $ sudo pip install virtualenv
    
.. note::

    Virtualenvwrapper administra los virtualenvs por su nombre, y los guarda en un directorio propio centralizado. Para instalarlo, usamos de nuevo ``pip`` o el gestor de paquetes del sistema.
    
----

:id: configurar-virtualenvwrapper

Configuración
-------------
En el ``.bashrc``, añadimos lo siguiente:

.. code-block:: bash

    export WORKON_HOME=$HOME/.virtualenvs
    export PROJECT_HOME=$HOME/Projects
    source `which virtualenvwrapper.sh`

La primera línea es donde se guardarán los *virtualenvs*. La segunda, donde creamos nuestros *proyectos y trabajos*. Veremos más sobre esto más adelante.

.. note::

    Para configurarlo, debemos añadir al ``.bashrc`` el directorio donde se guardarán los virtualenvs. Adicionalmente, un directorio para nuestros proyectos.

----

:id: crear-virtualenvwrapper

Crear un virtualenv con virtualenvwrapper
-----------------------------------------
Usamos el comando ``mkvirtualenv <name>``. Si ponemos el argumento ``-p <binario python>``, podremos cambiar el ejecutable de Python a usar:

.. code-block:: bash

    $ mkvirtualenv -p /usr/bin/python3 my-venv
    
Al crear un proyecto, *entraremos automáticamente en el*.

.. note::

    Con ``mkvirtualenv`` podemos crear un virtualenv. Además, con ``-p`` podemos definir el binario de Python a usar, lo cual permite diferenciar entre versiones de Python.

----

:id: salir-entrar-virtualenvwrapper

Salir y entrar en el virtualenv
-------------------------------
Para **salir** del virtualenv, el comando es igual que con los virtualenv de serie:

.. code-block:: bash

    $ deactivate
    
Y para volver a **entrar**, usamos ``workon``:

.. code-block:: bash

    $ workon my-venv
    
.. note::

    Para salir es igual que con los ``virtualenvs``, y con ``workon`` entramos de nuevo.
    
----

:id: proyectos-virtualenvwrapper

Proyectos
---------
Cuando se crea un virtualenv con ``mkproject <project name>``, se crea un virtualenv y adicionalmente un directorio en ``$PROJECT_HOME``, que es nuestro *directorio de proyectos*. Cada vez que se entre en el virtualenv, se activará el virtualenv y además, se accederá el **directorio del proyecto**:

.. code-block:: bash

    mkproject my-project

El resto de funciones son exactamente iguales a las de cualquier otro virtualenv.
    
.. note::

    Con ``mkproject`` podemos crear un directorio para uno de nuestros proyectos, junto con un virtualenv a utilizar. Es igual que ``mkvirtualenv``, pero crea adicionalmente un directorio de proyecto, y además cuando entremos en el virtualenv, entraremos también en el directorio del proyecto.
    
----

:id: comandos-fuera-virtualenvwrapper

Comandos fuera del virtualenv
-----------------------------

* ``workon <venv>``: **Entrar** en un virtualenv.
* ``mkvirtualenv <venv>``: **Crear** un virtualenv.
* ``mkproject <proj>``: **Crea** un directorio de **proyecto** con su correspondiente virtualenv.
* ``mktmpenv``: **Crea** un virtualenv sin nombre y **temporal**, que al hacer deactivate se autodestruye.
* ``rmvirtualenv <venv>``: **Borrar** un virtualenv. En el caso de proyectos, no borra el dir. de proyecto.
* ``allvirtualenv <command>``: **Ejecutar** un comando en **todos los venv**. Útil para actualizar pip.

.. note::

    Y aquí algunos de los comandos más usados sin necesidad de estar dentro del virtualenv.

----

:id: comandos-dentro-virtualenvwrapper

Comandos dentro del virtualenv
------------------------------

* ``deactivate``: **Salir** del virtualenv actual.
* ``cdvirtualenv``: Ir al directorio *~/.virtualenvs/<venv>*.
* ``cdsitepackages``: Ir al directorio *~/.virtualenvs/<venv>/lib/PythonX.Y/site-packages*.
* ``cdproject``: En el caso de proyectos, *volver al directorio del proyecto*.
* ``wipeenv``: **Borrar** todos los **paquetes** del venv.
* ``add2virtualenv <dir 1>[ <dir 2>]``: Permite añadir directorios al site-packages del virtualenv sin instalarlos
* ``toggleglobalsitepackages``: Habilita o deshabilita que se puedan usar a **paquetes del sistema** en el virtualenv.

.. note::

    Y estos otros son los que pueden usarse dentro del virtualenv.

----

:id: hooks-virtualenvwrapper

Scripts personalizables (hooks)
-------------------------------
*Virtualenvwrapper* permite personalizar las acciones cuando se interactúa con los virtualenvs. Por ejemplo, ``postactivate`` permite ejecutar cuandos al activar el virtualenv, o ``postmkvirtualenv`` **ejecutar comandos** al crear un nuevo virtualenv. Esto puede usarse para *iniciar servicios* o *instalar paquetes*.

Un listado completo de los scripts se encuentra en: http://virtualenvwrapper.readthedocs.io/en/latest/scripts.html

Es posible crear scripts *por cada virtualenv* o *de forma global*.

.. note::

    Los hooks son scripts bash que se ejecutarán con ciertas acciones de virtualenvwrapper. Por ejemplo, ``postmkvirtualenv`` nos permitirá instalar paquetes automáticamente tras crear un virtualenv.

----
    
Templates
---------
El parámetro ``-t`` definir un template a utilizar en la creación de un proyecto o virtualenv. Por ejemplo, para la estrictura de Django:

.. code-block:: bash

    $ mkproject -t django myproject
    
.. note::

    Virtualenvwrapper permite usar un template al crear un proyecto o virtualenv. Por ejemplo, puede usarse el de Django para crear la estructura básica al crear un nuevo proyecto.
    
----

:id: requirements

Requirements
============
Tras instalar los paquetes que necesitamos, podemos querer **replicar la misma instalación** que ya funciona en otro equipo, como por ejemplo pasarlo a **producción**. Esto podemos lograrlo gracias al archivo ``requirements.txt``.

En este archivo apuntamos las dependencias necesarias para que un proyecto funcione. Por ejemplo:

.. code-block:: bash

    requirements.txt
    ----------------
    Django>=1.9.1
    six==1.10.0
    appdirs==1.4.0
    
.. note::

    Ahora que usamos virtualenvs, es posible que queramos compartir nuestras instalaciones, y establecer los requisitos para que nuestros proyectos funcionen en otras máquinas. Para ello, se usa un archivo en texto plano con el listado de los paquetes necesarios, y optativamente con su versión. Este archivo se llama ``requirements``.
    
----

:id: instalar-requirements

Luego podemos **instalar las dependencias** mediante:

.. code-block:: bash

    pip install -r requirements.txt
    
Con esto podemos **replicar la instalación** de la *máquina original* en *otras máquinas*.

.. note::
    
    Para instalar los paquetes que se encuentran en un ``requirements``, usamos el parámetro ``-r`` de ``pip install``

----

:id: pip-freeze

pip freeze
----------
El comando ``pip freeze`` nos permite generar un **listado de las dependencias instaladas** con la versión con el formato ``paquete==versión`` por cada línea. Podemos usar este comando para generar el archivo ``requirements.txt`` con las **dependencias exactas** que hay en el virtualenv actual:

.. code-block:: bash

    $ pip freeze > requirements.txt
    
.. note::

    No obstante, ``Pip`` ofrece una utilidad para generar un archivo de este tipo. Es posible generar un listado con las dependencias y versiones exactas instaladas en nuestro virtualenv, por lo que la instalación debería ser la misma en cualquier máquina que lo utilice. Esto se logra con ``pip freeze``.
    
----

:id: constraints-1

Constraints
-----------
En ocasiones, podemos no desear instalar *ciertos paquetes* en la máquina de producción, como *los de desarrollo*, o los instalados *por pruebas*; pero también queremos asegurar que se instalan las **versiones correctas** de los paquetes y sus dependencias, para evitar problemas. Para ello podemos usar **constraints**:

.. code-block:: bash

    $ pip freeze > constraints.txt
  
.. note::

    En ocasiones, podemos no querer recomendar instalar todas las dependencias que tenemos, sino sólo algunas. No obstante, podemos sí querer especificar qué versiones se usarán. Para ello, haremos un archivo ``constraints``, que será igual al ``requirements`` que hicimos antes...
  
----

:id: constraints-2
  
Luego, en *el requirements* especificamos lo que nosotros quisimos **instalar explícitamente**, y *el constraints* se asegurará de instalar las **versiones correctas** de los paquetes y sus dependencias, pero no se instalarán los paquetes del *constraints* que no estén especificados en el *requirements*:

.. code-block:: bash

    requirements.txt
    ----------------
    -c constraints.txt
    pandas
    
.. note::

    Pero en el ``requirements`` ponemos las dependencias a mano, y definimos el archivo de ``constraints`` con ``-c``. Esto no instalará las dependencias de dicho archivo, pero sí que forzará que toda dependencia instalada en el requirements, cumpla las versiones del ``constraints``.
  
----

:id: constraints-3
  
Y el ``constraints.txt`` **generado automáticamente** usando ``pip freeze > constraints.txt``:

.. code-block:: bash

    constraints.txt
    ---------------
    appdirs==1.4.0
    numpy==1.12.0
    packaging==16.8
    pandas==0.19.2
    pyparsing==2.1.10
    python-dateutil==2.6.0
    pytz==2016.10
    six==1.10.0
    
.. note::

    Mientras que el ``requirements`` tiene las dependencias escritas a mano, el ``constraints`` se ha generado solo, como vemos aquí.

----

:id: utilidades

Otras utilidades
================

* ``pipdeptree``: Representa las *dependencias* instaladas en *forma de árbol*. Ayuda a comprender **qué paquete instaló cual**.
* ``Pipfile``: Otra forma de trabajar con los archivos de requirements, que facilita *distinguir entre entornos* y *qué paquetes se instalaron explícitamente*.
* ``pipenv``: Aúna en uno ``virtualenv``, ``Pipfile`` y ``Pip``. *Crea virtualenvs automáticamente* en tu proyecto.
* ``pip-tools``: Ayuda a **mantener los paquetes actualizados**. Usando archivos de dependencias propios, se compilan los archivos de requirements.
* ``compare-requirements``: Compara archivos de ``requirements.txt`` y permite *compararlos* con los requirements del venv.
* ``curd``: Alternativa compatible con ``pip``, que le ofrece **mayor velocidad** en la instalación de paquetes.

.. note::

    Aquí un listado de utilidades...
    
----

:id: acerca-de
    
Sobre esta presentación...
==========================

* **Código fuente presentación:** https://github.com/Nekmo/python-packages-management
    
.. note::
    si te ha gustado la presentación, puedes verla en mi Github, y no olvidéis darle a like :)

----
    
:id: end

¡Muchas gracias a todos!
========================

* **Sitio web:** http://nekmo.com
* **Email:** contacto@nekmo.com
* **Telegram:** @nekmo
* **Twitter:** @nekmocom

.. note::
    Muchas gracias. Por si queréis hablar conmigo, podéis hacerlo por estos medios, o luego al final.
