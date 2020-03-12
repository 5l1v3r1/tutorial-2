# Внедряване!

> **Забележка** Следващата глава понякога може да бъде малко трудна за преминаване. Продължете и я завършете; внедряването е важна част от процеса на разработване на уебсайтове. Тази глава е поставена в средата на урока, така че вашият ментор да ви помогне с малко по-сложния процес на вдигане на уебсайта ви онлайн. Това означава, че все още можете да завършите урока самостоятелно, ако ви липсва време.

Досега вашият уебсайт беше достъпен само на вашия компютър. Сега ще научите как да го разгърнете! Разгръщането е процесът на публикуване на приложението ви в Интернет, така че хората най-накрая да могат да отидат и да видят приложението ви. :)

Както научихте, уебсайт трябва да бъде разположен на сървър. В интернет има много доставчици на сървъри, ще използваме [PythonAnywhere](https://www.pythonanywhere.com/). PythonAnywhere е безплатен за малки приложения, които нямат твърде много посетители, така че определено сега ще ви бъде достатъчно.

Другата външна услуга, която ще използваме е [GitHub](https://www.github.com), която е услуга за хостинг на код. Има и други, но почти всички програмисти имат GitHub акаунт в наши дни, а сега и вие!

Тези три места ще бъдат важни за вас. Вашият локален компютър ще бъде мястото, където правите разработка и тестване. Когато сте доволни от промените, ще поставите копие на програмата си в GitHub. Вашият уебсайт ще бъде на PythonAnywhere и ще го актуализирате, като получите ново копие на вашия код от GitHub.

# Git

> **Забележка** Ако вече сте направили стъпките за инсталиране, няма нужда да правите това отново - можете да преминете към следващия раздел и да започнете да създавате вашето Git хранилище.

{% include "/deploy/install_git.md" %}

## Стартираме нашето Git хранилище

Git проследява промените в определен набор от файлове в т.нар. репозиторий (или за кратко "репо"). Нека започнем еднo за нашия проект. Отворете конзолата и стартирайте тези команди в директорията `djangogirls`:

> **Забележка** Проверете текущата си работна директория с команда `pwd` (Mac OS X / Linux) или `cd` (Windows), преди да инициализирате хранилището. Трябва да сте в папката `djangogirls`.

{% filename %}command-line{% endfilename %}

    $ git init
    Initialized empty Git repository in ~/djangogirls/.git/
    $ git config --global user.name "Your Name"
    $ git config --global user.email you@example.com
    

Инициализирането на git хранилището е нещо, което трябва да направим само веднъж за всеки проект (и няма да се налага да въвеждате отново потребителското име и имейла отново).

Git ще проследи промените във всички файлове и папки в тази директория, но има някои файлове, които искаме да игнорира. Правим това чрез създаване на файл, наречен `.gitignore` в основната директория. Отворете редактора си и създайте нов файл със следното съдържание:

{% filename %}.gitignore{% endfilename %}

    *.pyc
    *~
    /.vscode
    __pycache__
    myvenv
    db.sqlite3
    /static
    .DS_Store
    

И го запишете като `.gitignore` в папката "djangogirls".

> **Забележка** Точката в началото на името на файла е важна! Ако имате проблеми с създаването му (Macs не харесва да създавате файлове, които започват с точка чрез Finder, например), след това използвайте функцията "Save As" в редактора си; това е бронеустойчиво. И не забравяйте да добавите `.txt`, `.py` или друго разширение към името на файла - той ще бъде разпознат от Git само ако името е просто `.gitignore`.
> 
> **Забележка** Един от файловете, които сте посочили във вашия `.gitignore` файл е `db.sqlite3`. Този файл е вашата локална база данни, където се съхраняват всички ваши потребители и публикации. Ще следваме стандартната практика за уеб програмиране, което означава, че ще използваме отделни бази данни за вашия локален тестващ сайт и вашия уеб сайт на живо в PythonAnywhere. Базата данни на PythonAnywhere може да бъде SQLite, като вашата разработваща машина, но обикновено ще използвате такава, наречена MySQL, която може да се справи с много повече посетители на сайта, отколкото SQLite. Така или иначе, като игнорирате вашата SQLite база данни за копието на GitHub, това означава, че всички публикувани досега публикации и superuser ще бъдат достъпни само локално и ще трябва да създавате нови в производството. Трябва да мислите за вашата локална база данни като за добра площадка, където можете да тествате различни неща и да не се страхувате, че ще изтриете истинските си публикации от блога си.

Добра идея е да използвате команда `git status` преди `git add` или винаги, когато се окажете несигурни какво се е променило. Това ще ви помогне да предотвратите появата на изненади, като например добавяне или поемане на грешни файлове. Командата `git status` връща информация за всички непроследени/модифицирани/поетапни файлове, състоянието на клона и много други. Изходът трябва да бъде подобен на следното:

{% filename %}command-line{% endfilename %}

    $ git status
    On branch master
    
    No commits yet
    
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
    
            .gitignore
            blog/
            manage.py
            mysite/
            requirements.txt
    
    nothing added to commit but untracked files present (use "git add" to track)
    

И накрая спестяваме промените си. Отидете на конзолата си и изпълнете следните команди:

{% filename %}command-line{% endfilename %}

    $ git add --all .
    $ git commit -m "My Django Girls app, first commit"
     [...]
     13 files changed, 200 insertions(+)
     create mode 100644 .gitignore
     [...]
     create mode 100644 mysite/wsgi.py
    

## Избутване на кода ви към GitHub

Отидете на [GitHub.com](https://www.github.com) и се регистрирайте за нов безплатен потребителски акаунт. (Ако вече сте го направили в подготвителната работилница, това е чудесно!) Не забравяйте да запомните паролата си (добавете я към вашия мениджър на пароли, ако използвате такъв).

След това създайте ново хранилище, като му дадете името "my-first-blog". Оставете квадратчето за „инициализация с README“ отместено, оставете опцията .gitignore празна (направихме това ръчно) и оставете лиценза като None.

![](images/new_github_repo.png)

> **Забележка** Името `my-first-blog` е важно - бихте могли да изберете нещо друго, но това ще се случва много пъти в инструкциите по-долу и ще трябва да го замествате всеки път. Вероятно е по-лесно да се придържаме към името `my-first-blog`.

На следващия екран ще се покаже URL за клониране на вашия репозиторий, което ще използвате в някои от следващите команди:

![](images/github_get_repo_url_screenshot.png)

Сега трябва да свържем Git хранилището на вашия компютър към това в GitHub.

Въведете следното в конзолата си (заменете `<your-github-username>` с потребителското име, което сте въвели, когато сте създали акаунта си в GitHub, но без скобите на ъглите - URL адресът трябва да съответства на клониращия URL адрес, който току-що видяхте):

{% filename %}command-line{% endfilename %}

    $ git remote add origin https://github.com/<your-github-username>/my-first-blog.git
    $ git push -u origin master
    

Когато натиснете към GitHub, ще бъдете попитани за вашето потребителско име и парола за GitHub (било то в прозореца на командния ред или в изскачащ прозорец), а след въвеждане на идентификационни данни трябва да видите нещо подобно:

{% filename %}command-line{% endfilename %}

    Counting objects: 6, done.
    Writing objects: 100% (6/6), 200 bytes | 0 bytes/s, done.
    Total 3 (delta 0), reused 0 (delta 0)
    To https://github.com/ola/my-first-blog.git
    
     * [new branch]      master -> master
    Branch master set up to track remote branch master from origin.
    

<!--TODO: maybe do ssh keys installs in install party, and point ppl who dont have it to an extension -->

Кодът ви вече е на GitHub. Отидете и го вижте! Ще откриете, че е в добра компания - [Django](https://github.com/django/django), [Django Girls Tutorial](https://github.com/DjangoGirls/tutorial) и много други страхотни софтуерни проекти с отворен код също са домакини на кода си в GitHub. :)

# Настройване на нашия блог на PythonAnywhere

## Регистрирайте се за акаунт в PythonAnywhere

> **Забележка** Може би вече сте създали акаунт в PythonAnywhere по-рано по време на стъпките за инсталиране - ако е така, няма нужда да го правите отново.

{% include "/deploy/signup_pythonanywhere.md" %}

## Конфигуриране на нашия сайт на PythonAnywhere

Върнете се към главното [PythonAnywhere Dashboard](https://www.pythonanywhere.com/), като кликнете върху логото и изберете опцията за стартиране на конзола "Bash" - това е версията на командния ред PythonAnywhere, точно като тази на вашия компютър.

![The 'New Console' section on the PythonAnywhere web interface, with a button for 'bash'](images/pythonanywhere_bash_console.png)

> **Забележка** PythonAnywhere е базиран на Linux, така че ако сте на Windows, конзолата ще изглежда малко по-различна от тази на вашия компютър.

Внедряването на уеб приложение в PythonAnywhere включва сваляне на кода от GitHub и конфигуриране на PythonAnywhere да го разпознае и да започне да го обслужва като уеб приложение. Има ръчни начини за това, но PythonAnywhere предоставя помощен инструмент, който ще свърши всичко за вас. Нека го инсталираме първо:

{% filename %}PythonAnywhere command-line{% endfilename %}

    $ pip3.6 install --user pythonanywhere
    

Това трябва да отпечата някои неща като `Collecting pythonanywhere` и в крайна сметка да завърши с ред, който казва `Successfully installed (...) pythonanywhere- (...)`.

Сега стартираме помощника за автоматично конфигуриране на приложението ви от GitHub. Въведете следното в конзолата на PythonAnywhere (не забравяйте да използвате потребителското си име на GitHub вместо `<your-github-username>`, така че URL адресът да съответства на клонираният URL от GitHub):

{% filename %}PythonAnywhere command-line{% endfilename %}

    $ pa_autoconfigure_django.py --python=3.6 https://github.com/<your-github-username>/my-first-blog.git
    

Докато гледате това да работи, ще можете да видите какво прави:

- Изтегляне на вашия код от GitHub
- Създаване на virtualenv на PythonAnywhere, точно като този на вашия собствен компютър
- Актуализиране на вашия файл с настройки с някои настройки за внедряване
- Настройка на база данни на PythonAnywhere с помощта на командата `manage.py migrate`
- Настройка на статичните ви файлове (за тях ще научим по-късно)
- И конфигуриране на PythonAnywhere да обслужва вашето уеб приложение чрез неговия API

На PythonAnywhere всички тези стъпки са автоматизирани, но те са същите стъпки, които би трябвало да преминете с всеки друг доставчик на сървъри.

Основното, което трябва да забележите в момента, е, че вашата база данни в PythonAnywhere всъщност е напълно отделена от вашата база данни на вашия собствен компютър, така че може да има различни публикации и администраторски акаунти. В резултат на това, точно както направихме на вашия собствен компютър, трябва да инициализираме администраторския акаунт с `createsuperuser`. PythonAnywhere автоматично активира вашия virtualenv за вас, така че всичко, което трябва да направите, е да стартирате:

{% filename %}PythonAnywhere command-line{% endfilename %}

    (ola.pythonanywhere.com) $ python manage.py createsuperuser
    

Въведете данните за вашия администратор потребител. Най-добре е да използвате същите, които използвате на собствения си компютър, за да избегнете объркване, освен ако не искате да направите паролата на PythonAnywhere по-сигурна.

Сега, ако желаете, можете също да разгледате кода си на PythonAnywhere, като използвате `ls`:

{% filename %}PythonAnywhere command-line{% endfilename %}

    (ola.pythonanywhere.com) $ ls
    blog  db.sqlite3  manage.py  mysite requirements.txt static
    (ola.pythonanywhere.com) $ ls blog/
    __init__.py  __pycache__  admin.py  apps.py  migrations  models.py
    tests.py  views.py
    

Можете също да отидете на страницата „Файлове“ и да се придвижвате наоколо, използвайки вградения файлов браузър на PythonAnywhere. (От страницата на конзолата можете да стигнете до други страници на PythonAnywhere от бутона на менюто в горния десен ъгъл. След като сте на една от страниците, има връзки към другите в горната част.)

## Вече сте на живо!

Сега вашият сайт трябва да бъде на живо в публичния Интернет! Кликнете върху страницата „Уеб“ на PythonAnywhere, за да получите линк към нея. Можете да споделите това с всеки, който искате :)

> **Забележка** Това е урок за начинаещи и при разгръщането на този сайт взехме няколко преки пътища, които не са идеални от гледна точка на сигурността. Ако и когато решите да надградите този проект или да започнете нов проект, трябва да прегледате [контролния списък за разгръщане на Django](https://docs.djangoproject.com/en/2.2/howto/deployment/checklist/) за някои съвети относно осигуряването на вашия сайт.

## Съвети за отстраняване на грешки

If you see an error while running the `pa_autoconfigure_django.py` script, here are a few common causes:

- Forgetting to create your PythonAnywhere API token.
- Making a mistake in your GitHub URL
- If you see an error saying *"Could not find your settings.py"*, it's probably because you didn't manage to add all your files to Git, and/or you didn't push them up to GitHub successfully. Have another look at the Git section above
- If you previously signed up for a PythonAnywhere account and had an error with collectstatic, you probably have an older version of SQLite (eg 3.8.2) for your account. In that case, sign up for a new account and try the commands in the PythonAnywhere section above.

If you see an error when you try to visit your site, the first place to look for some debugging info is in your **error log**. You'll find a link to this on the PythonAnywhere ["Web" page](https://www.pythonanywhere.com/web_app_setup/). See if there are any error messages in there; the most recent ones are at the bottom.

There are also some [general debugging tips on the PythonAnywhere help site](http://help.pythonanywhere.com/pages/DebuggingImportError).

And remember, your coach is here to help!

# Check out your site!

The default page for your site should say "It worked!", just like it does on your local computer. Try adding `/admin/` to the end of the URL, and you'll be taken to the admin site. Log in with the username and password, and you'll see you can add new Posts on the server -- remember, the posts from your local test database were not sent to your live blog.

Once you have a few posts created, you can go back to your local setup (not PythonAnywhere). From here you should work on your local setup to make changes. This is a common workflow in web development – make changes locally, push those changes to GitHub, and pull your changes down to your live Web server. This allows you to work and experiment without breaking your live Web site. Pretty cool, huh?

Give yourself a *HUGE* pat on the back! Server deployments are one of the trickiest parts of web development and it often takes people several days before they get them working. But you've got your site live, on the real Internet!