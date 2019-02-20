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

[Do Tutorial:  Part 2: Models and the admin site](#do-tutorial-part-2-models-and-the-admin-site-httpsdocsdjangoprojectcomen21introtutorial02)

## Install programs
1. [Atom](https://atom.io/)
2. [Git](https://git-scm.com/)
    - **Choosing the default editor used by Git**
    - Choose Nano or Atom ( I choose Atom )
    - **How would you like to use Git for the command line?**
    - Use Git and optional Unix Tools from the Windows Command Prompt</li>
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

- Sync your database<br>
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
- Lets verify it’s working, run the following command:<br>
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
- If you change your database connection settings, run the following command:<br>
`python3.7 manage.py migrate`

**Creating models**
- Edit the **src/polls/models.py** file so it looks like this:<br>
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
- Now Django knows to include the **polls** app. Let’s run another command:<br>
`python3.7 manage.py makemigrations polls`
- Generate command that will run the migrations for you and manage your database schema automatically<br>
`python3.7 manage.py sqlmigrate polls 0001`
- Run **migrate** again to create those model tables in your database:<br>
`python3.7 manage.py migrate`

**Playing with the API**
- To invoke the Python shell, use this command:<br>
`python3.7 manage.py shell`
- Once you’re in the shell, explore the database API:<br>
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
- **<Question: Question object (1)>** isn’t a helpful representation of this object. Let’s fix that by editing the **Question** model (in the **src/polls/models.py** file) and adding a **__str__()** method to both **Question** and **Choice**:<br>
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
- Let’s add a custom method, just for demonstration:<br>
```
import datetime

from django.db import models
from django.utils import timezone


class Question(models.Model):
    # ...
    def was_published_recently(self):
        return self.pub_date >= timezone.now() - datetime.timedelta(days=1)
```

- Save these changes and start a new Python interactive shell again:<br>
`exit()`<br>
`python3.7 manage.py shell`<br>
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

`exit()`

### Introducing the Django Admin

**Creating an admin user**
- First we’ll need to create a user who can login to the admin site. Run the following command:<br>
`python3.7 manage.py createsuperuser`
- Enter your desired username and press enter.<br>
`Username: admin`
- You will then be prompted for your desired email address:<br>
`Email address: admin@example.com`
- The final step is to enter your password. You will be asked to enter your password twice, the second time as a confirmation of the first.<br>
```
Password: **********
Password (again): *********
Superuser created successfully.
```

**Start the development server**
- If the server is not running start it like so:<br>
`python3.7 manage.py runserver 0:8080`
- visit http://localhost:8080/admin/ with your Web browser
- Now, try logging in with the superuser account you created in the previous step.


**Make the poll app modifiable in the admin**
- open the **src/polls/admin.py** file, and edit it to look like this:<br>
```
from django.contrib import admin

from .models import Question

admin.site.register(Question)
```
- Now that we’ve registered **Question**, Django knows that it should be displayed on the admin index page
- Click “Questions”. Now you’re at the “change list” page for questions. This page displays all the questions in the database and lets you choose one to change it. There’s the “What’s up?” question we created earlier
- Click the “What’s up?” question to edit it:
