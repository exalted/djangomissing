Trango Missing
==============

This Django application holds whatever we found that is missing in Django core.

Features
--------

* `LanguageField` -- Stores language codes as defined by ISO 639-1
* `CountryField` -- Stores language codes as defined by ISO 3166-1-alpha-2

Installation
------------

Download and copy trango-missing files into a new directory called
*trango_missing* to your django project or place it on your PYTHONPATH.

Usage
-----

Just import new fields as:

    from trango_missing.fields import *

Then you can use'em in your models like:

    class Foo(models.Model):
        language = LanguageField()
        country = CountryField(blank=True)

Notes
-----

`LanguageField` and `CountryField` fields are ready for South and
internationalization, so you can already do things such as:

    ./manage.py schemamigration <foo> --auto

or

    django-admin.py makemessages -l <ll>_<CC>

No worries if you either don't use South or don't know what that is, our code
will gracefully handle those cases and won't enable this feature.
