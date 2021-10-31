# Register-all-Models-in-Django-Admin

##By this code we can reduce a lot of works to register in djagno admin panel.
Just paste this code below of all other codes in ``` admin.py``` file( in any apps level admin.py file)

```

from django.apps import apps
from django.contrib import admin


class ListAdminMixin(object):
    def __init__(self, model, admin_site):
        self.list_display = [field.name for field in model._meta.fields]
        super(ListAdminMixin, self).__init__(model, admin_site)


models = apps.get_models()
for model in models:
    admin_class = type('AdminClass', (ListAdminMixin, admin.ModelAdmin), {})
    try:
        admin.site.register(model, admin_class)
    except admin.sites.AlreadyRegistered:
        pass

```
