Django Missing
==============

Whatever I think is missing in Django core.


Features
--------

* `LanguageField` -- Stores language codes as defined by ISO 639-1
* `CountryField` -- Stores language codes as defined by ISO 3166-1-alpha-2


Installation
------------

Place *djangomissing* app on your PYTHONPATH or add it to your django project.


Usage
-----

Just import new fields as:

```python
from djangomissing.fields import *
```

Then you can use'em in your models like:

```python
class Foo(models.Model):
    name = models.CharField(max_length=100)
    language = LanguageField()
    country = CountryField(blank=True)

    class Meta:
        unique_together = ('name', 'language', 'country')

    def __unicode__(self):
        len_max = 50
        return '%(name)s (%(locale_name)s)' % {
            'name': '%s%s' % (
                self.name[:len_max],
                '...' if len(self.name) > len_max else '',
            ),
            'locale_name': self.locale_name
        }

    @property
    def locale_name(self):
        return '%(ll)s%(_CC)s' % {
            'll': self.language,
            '_CC': ('_' + self.country.upper()) if self.country else ''
        }
```


Notes
-----

`LanguageField` and `CountryField` fields are ready for South and
internationalization, so you can already do things such as:

```bash
./manage.py schemamigration <foo> --auto
```

or

```bash
django-admin.py makemessages -l <ll>_<CC>
```

No worries if you either don't use South [http://south.aeracode.org/] or
don't know what that is, in that case feature won't be get on your way.
