# Configuration_projet_django


# Tuto : Comment configurer un projet Django

## Installation

- Creer un dossier <<projet>> et l ouvrir avec VS code
- Dans le terminal de visual studio code creer l environnement virtuel et installer Django
    - Sur iMAC
        python3 -m venv venv
        activer l environnement virtuel : source venv/bin/activate
        installer Django : pip3 install django

    - Sur Windows
        python -m venv venv 
        activer l environnement virtuel : source venv/Script/activate
        installer Django : pip install django

## Creation dossiers
Creer un dossier <<projet_tuto>> dans le dossier <<projet>>

Ensuite creer deux dossier dans le dossier <<projet_tuto>> media_cdn et static_cdn

Puis dans ce dossier <<projet_tuto>> creer le projet et l application avec ses commandes:
    - Sur iMAC et Windows
        django-admin startproject myproject
        python manage.py startapp myapp

## Le dossier myproject aura plusieurs fichiers a l interieur ouvrez le fichier settings.py et configurer ainsi:

    Dans INSTALLED_APPS mettez le nom de votre application

```python
    INSTALLED_APPS = [
    'myapp.apps.MyappConfig',

]
```

##    Dans TEMPLATES ajouter le nom du dossier qui contiendra les TEMPLATES

```python
    TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': ['templates'],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

## A la fin du settings.py ajouter ces routes

```python
    STATIC_URL = '/static/'
    STATICFILES_DIRS = [
        os.path.join(BASE_DIR, 'static')
    ]
    MEDIA_URL = '/media/'
    MEDIA_ROOT = os.path.join(BASE_DIR, '../media_cdn')
    STATIC_ROOT = os.path.join(BASE_DIR, '../static_cdn')
```

## Dans le dossier myproject et dans le fichier urls.py completer avec ce code:

```python
    from django.contrib import admin
    from django.urls import path,include
    from django.conf import settings
    from django.conf.urls.static import static

    urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('myapp.urls')),

    ]

    if settings.DEBUG:
        urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
        urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```

## Et creer le fichier urls.py dans le dossier myapp et ajouter ce code:


```python
    from django.contrib import admin
    from django.urls import path,include
    from . import views

    app_name = 'myapp'
    urlpatterns = [
        path('', views.home, name='home'),
    
    ]
```

## Dans le fichier views.py de myapp :

```python
    def home(request):

        data={}
        return render(request, 'home.html',data)
```    

## Creer le dossier templates au meme niveau que les dossiers myapp et myproject et ajouter fichier html avec votre code html

## Enfin lancer le serveur avec cette commande et ouvrez le lien qui s'affiche dans le votre navigateur

    - commande pour lancer le serveur sur iMAC et Windows : 
        python manage.py runserver


## how to do search field in django
```python
            from django.shortcuts import render
            from django.db.models import Q
            from posts.models import Post

            def searchposts(request):
                if request.method == 'GET':
                    query= request.GET.get('q')

                    submitbutton= request.GET.get('submit')

                    if query is not None:
                        lookups= Q(title__icontains=query) | Q(content__icontains=query)

                        results= Post.objects.filter(lookups).distinct()

                        context={'results': results,
                                 'submitbutton': submitbutton}

                        return render(request, 'search/search.html', context)

                    else:
                        return render(request, 'search/search.html')

                else:
                    return render(request, 'search/search.html')
```
# liens utiles
## learn VueJS
https://wwww.techiediaries.com/vue-axios-tutorial/

https://blog.vuejoy.com/4-axios/

https://vuejsdeveloppers.com/2017/03/24/vue-js-component-templates/

https://wwww.vuemastery.com/courses/intro-vue-js/components/

https://wwww.google.com/amp/s/serversideup.net/uploading-files-vuejs-axios/amp

https://lostinbritattany.github.io/vue-beer/step-09/

https://medium.com/@thibault60000/vue-js-pour-les-d%C3%A9butants-37a83aaea9c4

https://morioh.com/p/b8679ac09d52

## GraphQL et DRF

https://www.howtographql.com/graphql-python/0-introduction/

https://docs.graphene-python.org/projects/django/en/latest/

https://www.django-rest-framework.org/community/tutorials-and-resources/

https://www.django-rest-framework.org/tutorial/quickstart/

https://www.django-rest-framework.org/

## lien Modeles et queryset
```
    https://djangobook.com/mdj2-models/

    https://djangobook.com/mdj2-advanced-models/
```
