# django-tutorial

- Django 2.1 Official Tutorial on Windows 10
- Virtual machine in VirtualBox running Ubuntu 18.04
- Using MySQL instead of SQLite
## Contents
[Install programs](#install-programs)

[Set up workspace](#set-up-workspace)

[Using Git Bash](#using-git-bash)

[Set Up MySQL](#set-up-mysql)

[Using Atom](#using-atom)

[Do Tutorial: Part 1: Requests and responses](#do-tutorial-part-1-requests-and-responses-httpsdocsdjangoprojectcomen21introtutorial01)

[Do Tutorial: Part 2: Models and the admin site](#do-tutorial-part-2-models-and-the-admin-site-httpsdocsdjangoprojectcomen21introtutorial02)

[Do Tutorial: Part 3: Views and templates](#do-tutorial-part-3-views-and-templates-httpsdocsdjangoprojectcomen21introtutorial03)

[Do Tutorial: Part 4: Forms and generic views](#do-tutorial-part-4-forms-and-generic-views-httpsdocsdjangoprojectcomen21introtutorial04)

## Install programs
1. [Atom](https://atom.io/)
2. [Git](https://git-scm.com/)
    - **Choosing the default editor used by Git**
    - Choose Nano or Atom ( I choose Atom )
    - **How would you like to use Git for the command line?**
    - Use Git and optional Unix Tools from the Windows Command Prompt
3. [VirtualBox](https://www.virtualbox.org/)
4. [Vagrant](https://www.vagrantup.com/)

## Set up workspace
- Create folder `workspace` on C:\Users\Username

## Using Git Bash
**Open the Git Bash prompt**
- Click the Windows or Start icon
- In the Programs list, open the Git folder
- Click the option for Git Bash

**Create folder `django-tutorial`**
- `cd workspace`
- `mkdir django-tutorial`
- `cd django-tutorial`

**Clone this repository into folder `django-tutorial`**
- `git clone https://github.com/eakwichs/django-tutorial.git .`

**Creates and configures guest machines**
- `vagrant up`

**Option, Forces reprovisioning of the vagrant machine**
- `vagrant provision`

**Connects to vagrant machine via SSH**
- `vagrant ssh`
- `cd /vagrant`

**Option, Terminate the virtual machine**
- `vagrant destroy`

**Check python version**
- `python3.7 -V`
    > Python 3.7.2

**Check pip version**
- `pip --version`
    > pip 19.0.2 from /usr/local/lib/python3.7/dist-packages/pip (python 3.7)

**Create folder `src`**
- `mkdir src`

**Create a virtual environment**
- `cd src`
- `virtualenv --always-copy venv`

**To begin using the virtual environment, it needs to be activated**
- `source venv/bin/activate`

**Option, If you are done working in the virtual environment for the moment, you can deactivate it**
- `deactivate`

**Install Django**
- `pip install Django`

**Check Django version**
- `python3.7 -m django --version`
    >2.1.7
## Set Up MySQL
**Install MySQL**

https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/#apt-repo-fresh-install

https://phoenixnap.com/kb/how-to-install-mysql-on-ubuntu-18-04

https://www.tecmint.com/install-mysql-8-in-ubuntu/

1. Go to https://dev.mysql.com/downloads/repo/apt/ for check version-specific-package-name.deb (current is mysql-apt-config_0.8.12-1_all.deb)
2. `cd /tmp && wget -c https://dev.mysql.com/get/mysql-apt-config_0.8.12-1_all.deb`
3. `sudo dpkg -i mysql-apt-config_0.8.12-1_all.deb`
4. `sudo apt-get update`
5. `sudo apt-get install mysql-server`
6. `sudo mysql_secure_installation`

**Starting and Stopping the MySQL Server**
- check the status of the MySQL server with the following command:<br>`sudo service mysql status`
- Stop the MySQL server with the following command:<br>`sudo service mysql stop`
- To restart the MySQL server, use the following command:<br>`sudo service mysql start`

**Check MySQL version**
- `mysql -V`

**Connect to the MySQL Sever**
- `sudo mysql -u root -p`

**Create database `django_tutorial`**
- `CREATE DATABASE django_tutorial CHARACTER SET utf8 COLLATE utf8_general_ci;`

**Create database user `django_tutorial`**
- `CREATE USER 'django_tutorial'@'localhost' IDENTIFIED BY 'PWjg147ttL$';`
- `GRANT ALL PRIVILEGES ON django_tutorial.* TO 'django_tutorial'@'localhost';`
- `GRANT ALL PRIVILEGES ON test_django_tutorial.* TO 'django_tutorial'@'localhost';`

**Lists the databases on the MySQL server host**
- `SHOW DATABASES;`

**Displays the privileges and roles that are assigned to a MySQL user account or role**
- `SHOW GRANTS FOR 'django_tutorial'@'localhost';`

**Disconnecting from the MySQL Server**
- `QUIT`

**Install mysqlclient**
- `cd /vagrant/src`
- `sudo apt-get -y install python3.7-dev default-libmysqlclient-dev gcc libssl-dev`
- `pip install mysqlclient`

## Using Atom
**Open Atom**
- double click Atom icon on desktop

**Add folder `django-tutorial` to Project Folder**
- File > Add Project Folder... > choose C:\Users\Username\workspace\django-tutorial

## Do Tutorial: Part 1: Requests and responses https://docs.djangoproject.com/en/2.1/intro/tutorial01/
**Check Django version**
- `python3.7 -m django --version`
    > 2.1.7

**Creating a project**
- `django-admin startproject mysite .`

**Database setup**
- Open up **src/mysite/settings.py** and replace the current DATABASES lines with the following
```
# Database
# https://docs.djangoproject.com/en/2.1/ref/settings/#databases

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'django_tutorial',
        'USER': 'django_tutorial',
        'PASSWORD': 'PWjg147ttL$',
        'HOST': '',
        'PORT': '',
        'OPTIONS': {
            'init_command': 'SET default_storage_engine=INNODB',
            'sql_mode': 'STRICT_TRANS_TABLES',
        },
    }
}
...
```

- While you’re editing **src/mysite/settings.py**, set TIME_ZONE to your time zone.
```
...
# Internationalization
# https://docs.djangoproject.com/en/2.1/topics/i18n/

LANGUAGE_CODE = 'en-us'

TIME_ZONE = 'Asia/Bangkok'
...
```

- Sync your database

`python3.7 manage.py migrate`

**The development server** Let’s verify your Django project works.
- `python3.7 manage.py runserver 0:8080`
- visit http://127.0.0.1:8080/ with your Web browser. You’ll see a “Congratulations!” page, with a rocket taking off. It worked!

**Creating the Polls app**
- `python3.7 manage.py startapp polls`

**Write your first view**
- Open the file **src/polls/views.py** and put the following Python code in it:
```
from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
```

- In the **src/polls/urls.py** file include the following code:
```
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

- In **src/mysite/urls.py**, add an import for django.urls.include and insert an include() in the urlpatterns list, so you have:
```
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('polls/', include('polls.urls')),
    path('admin/', admin.site.urls),
]
```
- Lets verify it’s working, run the following command:

`python3.7 manage.py runserver 0:8080`

- Go to http://localhost:8080/polls/ in your browser, and you should see the text “Hello, world. You’re at the polls index.”, which you defined in the index view.

**Summary Command**

| From Official | Use this |
| ---- | ---- |
| python -m django --version | python3.7 -m django --version |
| django-admin startproject mysite | django-admin startproject mysite . |
| python manage.py runserver | python3.7 manage.py migrate<br>python3.7 manage.py runserver 0:8080 |
| visit http://127.0.0.1:8000/ with your Web browser | visit http://127.0.0.1:8080/ with your Web browser |
| python manage.py startapp polls | python3.7 manage.py startapp polls |
| visit http://localhost:8000/polls/ with your Web browser | visit http://localhost:8080/polls/ with your Web browser |

## Do Tutorial: Part 2: Models and the admin site https://docs.djangoproject.com/en/2.1/intro/tutorial02/
**Database setup**
- Open the file **src/mysite/settings.py**. If you wish to use another database, install the appropriate database bindings and change the following keys in the DATABASES 'default' item to match your database connection settings.
- If you change your database connection settings, run the following command:

`python3.7 manage.py migrate`

**Creating models**
- Edit the **src/polls/models.py** file so it looks like this:
```
from django.db import models


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```

**Activating models**
- Edit the **src/mysite/settings.py** file and add that dotted path to the **INSTALLED_APPS** setting. It’ll look like this:
```
INSTALLED_APPS = [
    'polls.apps.PollsConfig',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```
- Now Django knows to include the **polls** app. Let’s run another command:

`python3.7 manage.py makemigrations polls`
- Generate command that will run the migrations for you and manage your database schema automatically

`python3.7 manage.py sqlmigrate polls 0001`
- Run **migrate** again to create those model tables in your database:

`python3.7 manage.py migrate`

**Playing with the API**
- To invoke the Python shell, use this command:

`python3.7 manage.py shell`
- Once you’re in the shell, explore the database API:
```
>>> from polls.models import Choice, Question  # Import the model classes we just wrote.

# No questions are in the system yet.
>>> Question.objects.all()
<QuerySet []>

# Create a new Question.
# Support for time zones is enabled in the default settings file, so
# Django expects a datetime with tzinfo for pub_date. Use timezone.now()
# instead of datetime.datetime.now() and it will do the right thing.
>>> from django.utils import timezone
>>> q = Question(question_text="What's new?", pub_date=timezone.now())

# Save the object into the database. You have to call save() explicitly.
>>> q.save()

# Now it has an ID.
>>> q.id
1

# Access model field values via Python attributes.
>>> q.question_text
"What's new?"
>>> q.pub_date
datetime.datetime(2012, 2, 26, 13, 0, 0, 775217, tzinfo=<UTC>)

# Change values by changing the attributes, then calling save().
>>> q.question_text = "What's up?"
>>> q.save()

# objects.all() displays all the questions in the database.
>>> Question.objects.all()
<QuerySet [<Question: Question object (1)>]>
```
- **<Question: Question object (1)>** isn’t a helpful representation of this object. Let’s fix that by editing the **Question** model (in the **src/polls/models.py** file) and adding a **__str__()** method to both **Question** and **Choice**:
```
from django.db import models

class Question(models.Model):
    # ...
    def __str__(self):
        return self.question_text

class Choice(models.Model):
    # ...
    def __str__(self):
        return self.choice_text
```
- Let’s add a custom method, just for demonstration:
```
import datetime

from django.db import models
from django.utils import timezone


class Question(models.Model):
    # ...
    def was_published_recently(self):
        return self.pub_date >= timezone.now() - datetime.timedelta(days=1)
```

- Save these changes and start a new Python interactive shell again:

`exit()`

`python3.7 manage.py shell`
```
>>> from polls.models import Choice, Question

# Make sure our __str__() addition worked.
>>> Question.objects.all()
<QuerySet [<Question: What's up?>]>

# Django provides a rich database lookup API that's entirely driven by
# keyword arguments.
>>> Question.objects.filter(id=1)
<QuerySet [<Question: What's up?>]>
>>> Question.objects.filter(question_text__startswith='What')
<QuerySet [<Question: What's up?>]>

# Get the question that was published this year.
>>> from django.utils import timezone
>>> current_year = timezone.now().year
>>> Question.objects.get(pub_date__year=current_year)
<Question: What's up?>

# Request an ID that doesn't exist, this will raise an exception.
>>> Question.objects.get(id=2)
Traceback (most recent call last):
    ...
DoesNotExist: Question matching query does not exist.

# Lookup by a primary key is the most common case, so Django provides a
# shortcut for primary-key exact lookups.
# The following is identical to Question.objects.get(id=1).
>>> Question.objects.get(pk=1)
<Question: What's up?>

# Make sure our custom method worked.
>>> q = Question.objects.get(pk=1)
>>> q.was_published_recently()
True

# Give the Question a couple of Choices. The create call constructs a new
# Choice object, does the INSERT statement, adds the choice to the set
# of available choices and returns the new Choice object. Django creates
# a set to hold the "other side" of a ForeignKey relation
# (e.g. a question's choice) which can be accessed via the API.
>>> q = Question.objects.get(pk=1)

# Display any choices from the related object set -- none so far.
>>> q.choice_set.all()
<QuerySet []>

# Create three choices.
>>> q.choice_set.create(choice_text='Not much', votes=0)
<Choice: Not much>
>>> q.choice_set.create(choice_text='The sky', votes=0)
<Choice: The sky>
>>> c = q.choice_set.create(choice_text='Just hacking again', votes=0)

# Choice objects have API access to their related Question objects.
>>> c.question
<Question: What's up?>

# And vice versa: Question objects get access to Choice objects.
>>> q.choice_set.all()
<QuerySet [<Choice: Not much>, <Choice: The sky>, <Choice: Just hacking again>]>
>>> q.choice_set.count()
3

# The API automatically follows relationships as far as you need.
# Use double underscores to separate relationships.
# This works as many levels deep as you want; there's no limit.
# Find all Choices for any question whose pub_date is in this year
# (reusing the 'current_year' variable we created above).
>>> Choice.objects.filter(question__pub_date__year=current_year)
<QuerySet [<Choice: Not much>, <Choice: The sky>, <Choice: Just hacking again>]>

# Let's delete one of the choices. Use delete() for that.
>>> c = q.choice_set.filter(choice_text__startswith='Just hacking')
>>> c.delete()
```
- To exit the Python shell, use this command:

`exit()`

### Introducing the Django Admin

**Creating an admin user**
- First we’ll need to create a user who can login to the admin site. Run the following command:

`python3.7 manage.py createsuperuser`
- Enter your desired username and press enter.

`Username: admin`
- You will then be prompted for your desired email address:

`Email address: admin@example.com`
- The final step is to enter your password. You will be asked to enter your password twice, the second time as a confirmation of the first.
```
Password: **********
Password (again): *********
Superuser created successfully.
```

**Start the development server**
- If the server is not running start it like so:

`python3.7 manage.py runserver 0:8080`
- visit http://localhost:8080/admin/ with your Web browser
- Now, try logging in with the superuser account you created in the previous step.


**Make the poll app modifiable in the admin**
- open the **src/polls/admin.py** file, and edit it to look like this:
```
from django.contrib import admin

from .models import Question

admin.site.register(Question)
```
- Now that we’ve registered **Question**, Django knows that it should be displayed on the admin index page
- Click “Questions”. Now you’re at the “change list” page for questions. This page displays all the questions in the database and lets you choose one to change it. There’s the “What’s up?” question we created earlier
- Click the “What’s up?” question to edit it:

## Do Tutorial: Part 3: Views and templates https://docs.djangoproject.com/en/2.1/intro/tutorial03/
**Writing more views**

- Now let’s add a few more views to **src/polls/views.py**. These views are slightly different, because they take an argument:
```
def detail(request, question_id):
    return HttpResponse("You're looking at question %s." % question_id)

def results(request, question_id):
    response = "You're looking at the results of question %s."
    return HttpResponse(response % question_id)

def vote(request, question_id):
    return HttpResponse("You're voting on question %s." % question_id)
```

- Wire these new views into the **polls.urls** module by adding the following **path()** calls:
```
# src/polls/urls.py
from django.urls import path

from . import views

urlpatterns = [
    # ex: /polls/
    path('', views.index, name='index'),
    # ex: /polls/5/
    path('<int:question_id>/', views.detail, name='detail'),
    # ex: /polls/5/results/
    path('<int:question_id>/results/', views.results, name='results'),
    # ex: /polls/5/vote/
    path('<int:question_id>/vote/', views.vote, name='vote'),
]
```

**Write views that actually do something**
- let’s use Django’s own database API, which we covered in **Tutorial 2**. Here’s one stab at a new **index()** view, which displays the latest 5 poll questions in the system, separated by commas, according to publication date:
```
# src/polls/views.py
from django.http import HttpResponse

from .models import Question


def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    output = ', '.join([q.question_text for q in latest_question_list])
    return HttpResponse(output)

# Leave the rest of the views (detail, results, vote) unchanged
```

- Create **src/polls/templates/polls/index.html** and put the following code in that template:
```
# polls/templates/polls/index.html
{% if latest_question_list %}
    <ul>
    {% for question in latest_question_list %}
        <li><a href="/polls/{{ question.id }}/">{{ question.question_text }}</a></li>
    {% endfor %}
    </ul>
{% else %}
    <p>No polls are available.</p>
{% endif %}
```

- Now let’s update our index view in **src/polls/views.py** to use the template:
```
# src/polls/views.py
from django.http import HttpResponse
from django.template import loader

from .models import Question


def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    template = loader.get_template('polls/index.html')
    context = {
        'latest_question_list': latest_question_list,
    }
    return HttpResponse(template.render(context, request))
```

**A shortcut: render()**
```
# src/polls/views.py
from django.shortcuts import render

from .models import Question


def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    context = {'latest_question_list': latest_question_list}
    return render(request, 'polls/index.html', context)
```

**Raising a 404 error**
- Now, let’s tackle the question detail view – the page that displays the question text for a given poll. Here’s the view:
```
# src/polls/views.py
from django.http import Http404
from django.shortcuts import render

from .models import Question
# ...
def detail(request, question_id):
    try:
        question = Question.objects.get(pk=question_id)
    except Question.DoesNotExist:
        raise Http404("Question does not exist")
    return render(request, 'polls/detail.html', {'question': question})
```

- Create **src/polls/templates/polls/detail.html** and put the following code in that template:
```
# src/polls/templates/polls/detail.html
{{ question }}
```

**A shortcut: get_object_or_404()**
```
# src/polls/views.py
from django.shortcuts import get_object_or_404, render

from .models import Question
# ...
def detail(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    return render(request, 'polls/detail.html', {'question': question})
```

**Use the template system**
- Back to the **detail()** view for our poll application. Given the context variable question, here’s what the **src/polls/detail.html** template might look like:
```
# src/polls/templates/polls/detail.html
<h1>{{ question.question_text }}</h1>
<ul>
{% for choice in question.choice_set.all %}
    <li>{{ choice.choice_text }}</li>
{% endfor %}
</ul>
```

**Removing hardcoded URLs in templates**
- you can remove a reliance on specific URL paths defined in your url configurations by using the **{% url %}** template tag:
```
# polls/templates/polls/index.html
<li><a href="{% url 'detail' question.id %}">{{ question.question_text }}</a></li>
```

- If you want to change the URL of the polls detail view to something else, perhaps to something like **polls/specifics/12/** instead of doing it in the template (or templates) you would change it in **src/polls/urls.py**:
```
# src/polls/urls.py
...
# added the word 'specifics'
path('specifics/<int:question_id>/', views.detail, name='detail'),
...
```

**Namespacing URL names**
- The answer is to add namespaces to your URLconf. In the **src/polls/urls.py** file, go ahead and add an app_name to set the application namespace:
```
# src/polls/urls.py
from django.urls import path

from . import views

app_name = 'polls'
urlpatterns = [
    path('', views.index, name='index'),
    path('<int:question_id>/', views.detail, name='detail'),
    path('<int:question_id>/results/', views.results, name='results'),
    path('<int:question_id>/vote/', views.vote, name='vote'),
]
```

- Change your **src/polls/index.html** template and point at the namespaced detail view:
```
# src/polls/index.html
<li><a href="{% url 'polls:detail' question.id %}">{{ question.question_text }}</a></li>
```

## Do Tutorial: Part 4: Forms and generic views https://docs.djangoproject.com/en/2.1/intro/tutorial04/
**Write a simple form**
- Let’s update our poll detail template (“polls/detail.html”) from the last tutorial, so that the template contains an HTML `<form>` element:
```
# src/polls/templates/polls/detail.html
<h1>{{ question.question_text }}</h1>

{% if error_message %}<p><strong>{{ error_message }}</strong></p>{% endif %}

<form action="{% url 'polls:vote' question.id %}" method="post">
{% csrf_token %}
{% for choice in question.choice_set.all %}
    <input type="radio" name="choice" id="choice{{ forloop.counter }}" value="{{ choice.id }}">
    <label for="choice{{ forloop.counter }}">{{ choice.choice_text }}</label><br>
{% endfor %}
<input type="submit" value="Vote">
</form>
```

- Now, let’s create a Django view that handles the submitted data and does something with it. Remember, in **Tutorial 3**, we created a URLconf for the polls application that includes this line:
```
# src/polls/urls.py
path('<int:question_id>/vote/', views.vote, name='vote'),
```

- Add the following to **src/polls/views.py**:
```
# src/polls/views.py
from django.http import HttpResponse, HttpResponseRedirect
from django.shortcuts import get_object_or_404, render
from django.urls import reverse
from django.db.models import F

from .models import Choice, Question
# ...
def vote(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    try:
        selected_choice = question.choice_set.get(pk=request.POST['choice'])
    except (KeyError, Choice.DoesNotExist):
        # Redisplay the question voting form.
        return render(request, 'polls/detail.html', {
            'question': question,
            'error_message': "You didn't select a choice.",
        })
    else:
        # selected_choice.votes += 1
        selected_choice.votes = F('votes') + 1
        selected_choice.save()
        # Always return an HttpResponseRedirect after successfully dealing
        # with POST data. This prevents data from being posted twice if a
        # user hits the Back button.
        return HttpResponseRedirect(reverse('polls:results', args=(question.id,)))
```

- After somebody votes in a question, the **vote()** view redirects to the results page for the question. Let’s write that view:
```
# src/polls/views.py
from django.shortcuts import get_object_or_404, render


def results(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    return render(request, 'polls/results.html', {'question': question})
```

- Now, create a **polls/results.html** template:
```
# src/polls/templates/polls/results.html
<h1>{{ question.question_text }}</h1>

<ul>
{% for choice in question.choice_set.all %}
    <li>{{ choice.choice_text }} -- {{ choice.votes }} vote{{ choice.votes|pluralize }}</li>
{% endfor %}
</ul>

<a href="{% url 'polls:detail' question.id %}">Vote again?</a>
```

**Use generic views: Less code is better**

Let’s convert our poll app to use the generic views system, so we can delete a bunch of our own code. We’ll just have to take a few steps to make the conversion. We will:
1. Convert the URLconf.
2. Delete some of the old, unneeded views.
3. Introduce new views based on Django’s generic views.

**Amend URLconf**
- First, open the **polls/urls.py** URLconf and change it like so:
```
# src/polls/urls.py
from django.urls import path

from . import views

app_name = 'polls'
urlpatterns = [
    path('', views.IndexView.as_view(), name='index'),
    path('<int:pk>/', views.DetailView.as_view(), name='detail'),
    path('<int:pk>/results/', views.ResultsView.as_view(), name='results'),
    path('<int:question_id>/vote/', views.vote, name='vote'),
]
```
**Amend views**
- Next, we’re going to remove our old **index, detail, and results** views and use Django’s generic views instead. To do so, open the **polls/views.py** file and change it like so:
```
# src/polls/views.py
from django.http import HttpResponseRedirect
from django.shortcuts import get_object_or_404, render
from django.urls import reverse
from django.views import generic

from .models import Choice, Question


class IndexView(generic.ListView):
    template_name = 'polls/index.html'
    context_object_name = 'latest_question_list'

    def get_queryset(self):
        """Return the last five published questions."""
        return Question.objects.order_by('-pub_date')[:5]


class DetailView(generic.DetailView):
    model = Question
    template_name = 'polls/detail.html'


class ResultsView(generic.DetailView):
    model = Question
    template_name = 'polls/results.html'


def vote(request, question_id):
    ... # same as above, no changes needed.from django.http import HttpResponseRedirect
from django.shortcuts import get_object_or_404, render
from django.urls import reverse
from django.views import generic

from .models import Choice, Question


class IndexView(generic.ListView):
    template_name = 'polls/index.html'
    context_object_name = 'latest_question_list'

    def get_queryset(self):
        """Return the last five published questions."""
        return Question.objects.order_by('-pub_date')[:5]


class DetailView(generic.DetailView):
    model = Question
    template_name = 'polls/detail.html'


class ResultsView(generic.DetailView):
    model = Question
    template_name = 'polls/results.html'


def vote(request, question_id):
    ... # same as above, no changes needed.
```

## Do Tutorial: Part 5: Testing https://docs.djangoproject.com/en/2.1/intro/tutorial05/
**Writing our first test**
- Confirm the bug by using the **shell** to check the method on a question whose date lies in the future:

`python3.7 manage.py shell`

```
>>> import datetime
>>> from django.utils import timezone
>>> from polls.models import Question
>>> # create a Question instance with pub_date 30 days in the future
>>> future_question = Question(pub_date=timezone.now() + datetime.timedelta(days=30))
>>> # was it published recently?
>>> future_question.was_published_recently()
True
```
- Since things in the future are not ‘recent’, this is clearly wrong.
- To exit the Python shell, use this command:

`exit()`

**Create a test to expose the bug**
- Put the following in the tests.py file in the polls application:
```
# src/polls/tests.py
import datetime

from django.test import TestCase
from django.utils import timezone

from .models import Question


class QuestionModelTests(TestCase):

    def test_was_published_recently_with_future_question(self):
        """
        was_published_recently() returns False for questions whose pub_date
        is in the future.
        """
        time = timezone.now() + datetime.timedelta(days=30)
        future_question = Question(pub_date=time)
        self.assertIs(future_question.was_published_recently(), False)
```

**Running tests**
- we can run our test:

`python3.7 manage.py test polls`
- and you’ll see something like:
```
Creating test database for alias 'default'...
System check identified no issues (0 silenced).
F
======================================================================
FAIL: test_was_published_recently_with_future_question (polls.tests.QuestionModelTests)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "/path/to/mysite/polls/tests.py", line 16, in test_was_published_recently_with_future_question
    self.assertIs(future_question.was_published_recently(), False)
AssertionError: True is not False

----------------------------------------------------------------------
Ran 1 test in 0.001s

FAILED (failures=1)
Destroying test database for alias 'default'...
```
**Fixing the bug**
- We already know what the problem is: **Question.was_published_recently()** should return **False** if its **pub_date** is in the future. Amend the method in **models.py**, so that it will only return **True** if the date is also in the past:
```
# src/polls/models.py
def was_published_recently(self):
    now = timezone.now()
    return now - datetime.timedelta(days=1) <= self.pub_date <= now
```
- and run the test again:
```
Creating test database for alias 'default'...
System check identified no issues (0 silenced).
.
----------------------------------------------------------------------
Ran 1 test in 0.001s

OK
Destroying test database for alias 'default'...
```
**More comprehensive tests**
- Add two more test methods to the same class, to test the behavior of the method more comprehensively:
```
# src/polls/tests.py
def test_was_published_recently_with_old_question(self):
    """
    was_published_recently() returns False for questions whose pub_date
    is older than 1 day.
    """
    time = timezone.now() - datetime.timedelta(days=1, seconds=1)
    old_question = Question(pub_date=time)
    self.assertIs(old_question.was_published_recently(), False)

def test_was_published_recently_with_recent_question(self):
    """
    was_published_recently() returns True for questions whose pub_date
    is within the last day.
    """
    time = timezone.now() - datetime.timedelta(hours=23, minutes=59, seconds=59)
    recent_question = Question(pub_date=time)
    self.assertIs(recent_question.was_published_recently(), True)
```
**The Django test client**
- The first is to set up the test environment in the **shell**:

`python3.7 manage.py shell`

```
>>> from django.test.utils import setup_test_environment
>>> setup_test_environment()
```
- Next we need to import the test client class (later in **tests.py** we will use the **django.test.TestCase** class, which comes with its own client, so this won’t be required):
```
>>> from django.test import Client
>>> # create an instance of the client for our use
>>> client = Client()
```
- With that ready, we can ask the client to do some work for us:
```
>>> # get a response from '/'
>>> response = client.get('/')
Not Found: /
>>> # we should expect a 404 from that address; if you instead see an
>>> # "Invalid HTTP_HOST header" error and a 400 response, you probably
>>> # omitted the setup_test_environment() call described earlier.
>>> response.status_code
404
>>> # on the other hand we should expect to find something at '/polls/'
>>> # we'll use 'reverse()' rather than a hardcoded URL
>>> from django.urls import reverse
>>> response = client.get(reverse('polls:index'))
>>> response.status_code
200
>>> response.content
b'\n    <ul>\n    \n        <li><a href="/polls/1/">What&#39;s up?</a></li>\n    \n    </ul>\n\n'
>>> response.context['latest_question_list']
<QuerySet [<Question: What's up?>]>
```
