.. Apium documentation master file, created by
   sphinx-quickstart on Mon Nov  8 04:59:28 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

=====
Apium
=====

Python JSON-RPC Framework

Install
=======

.. code-block:: shell-session

    pip install apium-dev

Quick example
=============

Create RPC method
-----------------

Each method must be in path: api/<method_name>/method.py

Create file *api/get_hello_msg/method.py*:

.. code-block:: python

    import apium
    from apium import af


    class GetHelloMsg(apium.Method):
        name = af.Str(required=True)
        age = af.Int(default=18)

        def execute(self):
            return {'msg': f'Hi {self.name}, you are {self.age}'}

Settings web-framework
----------------------

Associate URL to handler.

Django
~~~~~~

Edit *urls.py* in your django project:

.. code-block:: python

    from django.urls import path
    from apium.handlers.django.handler import api_handler

    urlpatterns = [
        # ... your other path, e. g. 'admin/'
        path('api/', api_handler),
    ]

Flask
~~~~~

.. code-block:: python

    #!/usr/bin/env python
    from flask import Flask
    from apium.handlers.flask.handler import api_handler


    app = Flask(__name__)
    app.add_url_rule('/api/', view_func=api_handler, methods=['POST'])
    app.run('localhost', 8080, debug=True)

JSON-RPC request
----------------

First example (without *age*)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

JSON:

.. code-block:: json

    {
        "jsonrpc":"2.0",
        "id": 1,
        "method": "get_hello_msg",
        "params": {
            "name": "John"
        }
    }

Send request:

.. code-block:: shell-session

    curl http://127.0.0.1:8080/api/ \
        -X POST \
        -H 'Content-Type: application/json' \
        -d '{"jsonrpc": "2.0", "id": 1, "method": "get_hello_msg", "params": {"name": "John"}}'

Response:

.. code-block:: json

    {"jsonrpc": "2.0", "id": 1, "result": {"msg": "Hi John, you are 18"}}

Second example (with *age*)
~~~~~~~~~~~~~~~~~~~~~~~~~~~

JSON:

.. code-block:: json

    {
        "jsonrpc":"2.0",
        "id": 1,
        "method": "get_hello_msg",
        "params": {
            "name": "Smith",
            "age": 20
        }
    }

Send request:

.. code-block:: shell-session

    curl http://127.0.0.1:8080/api/ \
        -X POST \
        -H 'Content-Type: application/json' \
        -d '{"jsonrpc": "2.0", "id": 1, "method": "get_hello_msg", "params": {"name": "Smith", "age": 20}}'

Response:

.. code-block:: json

    {"jsonrpc": "2.0", "id": 1, "result": {"msg": "Hi Smith, you are 20"}}

.. toctree::
    :maxdepth: 2
    :caption: Contents:

    fields



.. Contents
.. ========

.. * :ref:`genindex`
.. * :ref:`modindex`
.. * :ref:`search`
