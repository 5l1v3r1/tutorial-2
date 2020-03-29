# Django URLs

Готови сме да създадем нашата първа уеб страница: начална страница на твоя блог! Но първо нека научим малко повече за Django URLs.

## Какво е URL?

URL е уеб адрес. Може да видиш URL всеки път когато посещаваш уебсайт – видимо е в полето за адрес на твоята търсачка. (Да! `127.0.0.1:8000` е URL! И `https://djangogirls.org` също е URL.)

![URL](images/url.png)

Всяка страница в Internet има нужда от собствен URL. По този начин твоето приложение знае какво трябва да покаже на потребителя, който отваря този URL. В Django използваме нещо наречено `URLconf` (URL конфигурация). URLconf е пакет от примери, които Django се опитва да съпостави със запитания URL за да намери правилния изглед.

## Как работят URL в Django?

Нека отворим файла `mysite/urls.py` в редактора си и видим как изглежда:

{% filename %}mysite/urls.py{% endfilename %}

```python
"""mysite URL Configuration

[...]
"""
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
]
```

Както може да видите, Django вече е сложил нещо за нас тук.

Редовете между трите кавички (`'''` or `"""`) се наричат docstrings – може да ги изписвате в началото на файла, класове или методи за да обясните какво прави кода - като коментар. Те няма да се изпълнят от Python.

Администртивния URL, който посетихте в предната глава е вече тук:

{% filename %}mysite/urls.py{% endfilename %}

```python
    path('admin/', admin.site.urls),
```

Този ред означава, че за всеки URL, който започва с `admin/`, Django ще намери съответстващ изглед *view*. В този случай въвеждаме много администраторски URL, така че да не е претъпкано в този малък файл – по-четимо и по-чисто.

## Твоя първи Django URL!

Време е да създадете вашия първи URL! Искаме 'http://127.0.0.1:8000/' да бъде началната страница на нашия блог и да показва лист от публикации.

Също така искаме да задържим файла `mysite/urls.py` чист, така че да въведем URL от нашата `blog` апликация към главният файл `mysite/urls.py`.

Давайте напред, акто добавите ред с който ще въведете `blog.urls`. You will also need to change the `from django.urls…` line because we are using the `include` function here, so you will need to add that import to the line.

Your `mysite/urls.py` file should now look like this:

{% filename %}mysite/urls.py{% endfilename %}

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('blog.urls')),
]
```

Django will now redirect everything that comes into 'http://127.0.0.1:8000/' to `blog.urls` and looks for further instructions there.

## blog.urls

Create a new empty file named `urls.py` in the `blog` directory, and open it in the code editor. All right! Add these first two lines:

{% filename %}blog/urls.py{% endfilename %}

```python
from django.urls import path
from . import views
```

Here we're importing Django's function `path` and all of our `views` from the `blog` application. (We don't have any yet, but we will get to that in a minute!)

After that, we can add our first URL pattern:

{% filename %}blog/urls.py{% endfilename %}

```python
urlpatterns = [
    path('', views.post_list, name='post_list'),
]
```

As you can see, we're now assigning a `view` called `post_list` to the root URL. This URL pattern will match an empty string and the Django URL resolver will ignore the domain name (i.e., http://127.0.0.1:8000/) that prefixes the full URL path. This pattern will tell Django that `views.post_list` is the right place to go if someone enters your website at the 'http://127.0.0.1:8000/' address.

The last part, `name='post_list'`, is the name of the URL that will be used to identify the view. This can be the same as the name of the view but it can also be something completely different. We will be using the named URLs later in the project, so it is important to name each URL in the app. We should also try to keep the names of URLs unique and easy to remember.

If you try to visit http://127.0.0.1:8000/ now, then you'll find some sort of 'web page not available' message. This is because the server (remember typing `runserver`?) is no longer running. Take a look at your server console window to find out why.

![Error](images/error1.png)

Your console is showing an error, but don't worry – it's actually pretty useful: It's telling you that there is **no attribute 'post_list'**. That's the name of the *view* that Django is trying to find and use, but we haven't created it yet. At this stage, your `/admin/` will also not work. No worries – we will get there. If you see a different error message, try restarting your web server. To do that, in the console window that is running the web server, stop it by pressing Ctrl+C (the Control and C keys together). On Windows, you might have to press Ctrl+Break. Then you need to restart the web server by running a `python manage.py runserver` command.

> If you want to know more about Django URLconfs, look at the official documentation: https://docs.djangoproject.com/en/2.2/topics/http/urls/