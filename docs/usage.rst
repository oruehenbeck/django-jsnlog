=====
Usage
=====


AppConfig
---------

To use django-jsnlog in a project, add it to your `INSTALLED_APPS`:

.. code-block:: python

    # settings.py
    INSTALLED_APPS = (
        ...
        'jsnlog',
        ...
    )

or use your own AppConfig like this:

.. code-block:: python

    # settings.py
    INSTALLED_APPS = (
        ...
        'myApp.apps.MyJSNLogConfig',
        ...
    )

    # myApp/apps.py
    from jsnlog.apps import DefaultJSNLogConfig

    class MyJSNLogConfig(DefaultJSNLogConfig):
        ...


URLs and Views
--------------

Add django-jsnlog's URL patterns:

.. code-block:: python

    urlpatterns += [
        path(r'jsnlog.logger', include('jsnlog.urls')),
    ]

or implement your own LogView by inheriting from JSNLogView like this:

.. code-block:: python

    # views.py
    @method_decorator(login_required, name='dispatch')
    class MyJSNLogView(JSNLogView):
        pass

    # urls.py
    urlpatterns += [
        path(r'jsnlog.logger', MyJSNLogView.as_view()),
    ]


Template
--------

Add django-jsnlog's javascript files to your template:

.. code-block:: html

    <script type="text/javascript" src="{% static 'jsnlog/js/jsnlog.min.js' %}"></script>
    <script type="text/javascript" src="{% static 'jsnlog/js/django-jsnlog.js' %}"></script>


Logging
-------

Add django-jsnlog's logger to your project SETTINGS like this:

.. code-block:: python

    LOGGING = {
        ...
        'loggers': {
            ...
            # JSNLog logs (client js errors)
            'jsnlog': {
                'handlers': ['console'],
                'level': 'DEBUG',
                'propagate': True,
            },
            ...
        }
    }
