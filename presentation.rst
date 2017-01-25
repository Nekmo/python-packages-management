##############################################
## Gestión de paquetes y entornos en Python ##
##############################################

Se dice que...

Python trae baterías incluidas

----

<imagen>

----

Esto es, que trae módulos para *CASI* todo.

----

CASI

----

Cuando Python no incluye lo que necesitamos, podemos instalarlo a través de Pip.

----

Pip
===
Es el gestor de paquetes de Python que sustituye a ``easy_install`` desde 2008. 

----

Ejemplo: instalar requests
--------------------------

Para instalar el paquete ``requests``, que facilita las consultas http:

.. code-block::

    $ sudo pip install requests

----

¿Y dónde puedo encontrar paquetes?
----------------------------------

* **Proyectos populares en Github**: https://github.com/trending/python
* **Paquetes recomendados para Python**: https://github.com/vinta/awesome-python
* **Los módulos más descargados**: http://pypi-ranking.info/alltime
* Tira de Google.

----

La mayoría de paquetes Python dicen cómo instalarlos usando Pip

<imagen sqlalchemy>

----

¿Dónde se encuentran los paquetes de Pip?
-----------------------------------------
Subidos en **Pypi**. Puedes buscar los paquetes existentes en:

https://pypi.python.org/pypi

Además, puedes subir tus propios paquetes.

----

<imagen pypi python>

----

También puedes echarle un vistazo al próximo portal de *Pypi*:

<imagen pypi.org>

----

Especificar versión
-------------------

Por si hubiese incompatibilidades, es posible restringir la versión:

.. code-block::

    pip install 'Django>=1.7'
    pip install 'Django==1.8.3'
    pip install 'Django~=1.8'  # 1.8.x
    pip install 'Django>=1.8.2,<=1.8.10'

----

Y si no se encuentra en Pypi...
-------------------------------
Puedes instalarlo de infinidad de otras formas:

* Desde una **ruta local**: ``pip install /home/nekmo/myPackage``
* Usando una **url**: ``pip install http://domain/myPackage.zip``
* Con un **VCS** (Git/Hg/Bzr/Svn).

.. code-block::

    pip install git+https://github.com/Nekmo/os3.git@master#egg=os3

----

Otros comandos de ``pip`` de interés
------------------------------------

* **pip download <package>**: sólo descargar el paquete.
* **pip list**: listar los paquetes instalados.
* **pip uninstall <package>**: desinstalar el paquete.
* **pip search <query>**: Buscar en Pypi.
* **pip check**: Comprobar incompatibilidades entre paquetes instalados.
* **pip freeze**: Generar listado de dependencias. Profundizaremos sobre este comando más adelante.

----

Parámetros útiles de ``pip install``
------------------------------------

Editable
^^^^^^^^
Usando ``-e``, se instala usando ``develop``. Esto es, que el paquete puede *editarse* en local y no hace falta reinstalarlo para aplicar los cambios.

.. code-block::

    pip install -e ~/Projects/myProject
    

Upgrade
^^^^^^^
Es posible llevar un paquete a la última versión con:

.. code-block::

    pip install --upgrade my-package
    

----
    
Pre-release
^^^^^^^^^^^
Por defecto, Pypi instala los paquetes estables. Pero es posible instalar los que están en desarrollo:

.. code-block::

    pip install --pre my-package
   

Instalar en tu usuario
^^^^^^^^^^^^^^^^^^^^^^
Pip instala los paquetes a nivel de sistema por defecto (lo cual requiere root). No obstante, es posible instalarlo en tu usuario.

.. code-block::

    pip install --user my-package
    
    
----

Cambiar o añadir repositorio
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Por defecto, ``pip`` usa como repositorio para descargar los paquetes::

    https://pypi.python.org/simple/
    
No obstante, es posible cambiarlo con ``--index-url``. Y añadir repositorios extra por si no estuviese el paquete en el rep. principal con el parámetro ``--extra-index-url``. Por ejemplo, para usar el repositorio de pruebas (para cuando se está aprendiendo a crear paquetes)::

    https://testpypi.python.org/simple/
    
Para saber cómo crear nuestro propio repositorio: https://github.com/pypiserver/pypiserver

----

Instalar Pip
------------
Por si no se encontrase instalado en el sistema, podemos instalarlo con::

    $ sudo apt install python-pip  # Debian/Ubuntu
    $ sudo dnf -y install python-pip  # Fedora
    $ sudo pacman -S python-pip
    
Y si no con::

    $ python get-pip.py
    
    
----

Conflictos entre paquetes
=========================

Ya sabemos cómo instalar paquetes externos. 

¿Pero qué pasa si tenemos conflictos entre ellos?


----

Ejemplo: tenemos 2 proyectos, A y B, con dependencia en diferentes versiones de Django.

Proyecto A: requiere Django >= 1.8, <= 1.10.
Proyecto B: requiere Django <=1.7, >= 1.4.

----

Solución: virtualenvs

----

Virtualenvs
===========
Son entornos de Python independientes al del sistema, con sus propios paquetes instalados.

----

Gracias a los virtualenvs, podemos tener 2 entornos distintos: uno para el proyecto A, 
con Django >= 1.9, y otro con Django <= 1.7 en el proyecto B, además de todas sus dependencias.

----

Cómo crear un virtualenv
------------------------
Tras instalar ``virtualenv``, podemos crear un virtualenv con::
    
    [nekmo@homura /tmp]$ virtualenv venv
    Running virtualenv with interpreter /usr/bin/python2
    New python executable in venv/bin/python2
    Also creating executable in venv/bin/python
    Installing setuptools, pip...done.

----

Cómo entrar en un virtualenv
----------------------------
Debemos ejecutar::
    
    [nekmo@homura /tmp]$ source venv/bin/activate
    (venv)[nekmo@homura /tmp]$ 
    
Véase que ahora, al inicio del *prompt*, tenemos entre paréntesis el nombre del virtualenv::
    
    **(venv)**[nekmo@homura /tmp]$ 
    
Esto significa, que tenemos el virtualenv activado. Podremos movernos con libertad, y seguiremos en el virtualenv mientras aparezca delante ese indicativo.

----

Cómo salir de un virtualenv
---------------------------
Debemos ejecutar ``deactivate``. Tras ejecutarlo, desaparecerá el nombre del virtualenv en el prompt::
    
    (venv)[nekmo@homura /tmp]$ deactivate 
    [nekmo@homura /tmp]$


