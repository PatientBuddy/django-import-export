==============================
Installation and configuration
==============================

django-import-export is available on the Python Package Index (PyPI), so it
can be installed with standard Python tools like ``pip`` or ``easy_install``::

    $ pip install django-import-export

Alternatively, you can install the git repository directly to obtain the
development version::

    $ pip install -e git+https://github.com/django-import-export/django-import-export.git#egg=django-import-export

Now, you're good to go, unless you want to use django-import-export from the
admin as well. In this case, you need to add it to your ``INSTALLED_APPS`` and
let Django collect its static files.

.. code-block:: python

    # settings.py
    INSTALLED_APPS = (
        ...
        'import_export',
    )

.. code-block:: shell

    $ python manage.py collectstatic

All prequisites are set up! See :doc:`getting_started` to learn how to use django-import-export in your project.



Settings
========

You can use the following directives in your settings file:

``IMPORT_EXPORT_USE_TRANSACTIONS``
    Global setting controls if resource importing should use database
    transactions. Default is ``False``.

``IMPORT_EXPORT_SKIP_ADMIN_LOG``
    Global setting controls if creating log entries for
    the admin changelist should be skipped when importing resource.
    The `skip_admin_log` attribute of `ImportMixin` is checked first,
    which defaults to ``None``. If not found, this global option is used.
    This will speed up importing large datasets, but will lose
    changing logs in the admin changelist view.  Default is ``False``.

``IMPORT_EXPORT_TMP_STORAGE_CLASS``
    Global setting for the class to use to handle temporary storage
    of the uploaded file when importing from the admin using an
    `ImportMixin`.  The `tmp_storage_class` attribute of `ImportMixin`
    is checked first, which defaults to ``None``. If not found, this
    global option is used. Default is ``TempFolderStorage``.

``IMPORT_EXPORT_REQUIRE_EXPORT_PERMISSION``
    Global settings to control whether export permission is required.
    If this settings is ``True``, permission will be checked for the current model
    before allowing the user to export data. This setting is ``False`` by default
    for backwards compatibility. To use permissions, add ``export`` to the model's default permission.
    For example::

    class ExampleModel(models.Model)
        class Meta:
            default_permissions = ('add', 'change', 'delete', 'export')


Example app
===========

There's an example application that showcases what django-import-export can do. You can run it via::

    cd tests
    ./manage.py runserver

Username and password for admin are ``admin`` and ``password``.
