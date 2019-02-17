# django-tutorial

- Django 2.1 Official Tutorial on Windows 10
- Virtual machine in VirtualBox running Ubuntu 18.04
- Using MySQL instead of SQLite
## Contents
[Install programs](#install-programs)

[Set up workspace](#set-up-workspace)

[Using Git Bash](#using-git-bash)

[Using Atom](#using-atom)

[Do Tutorial: Part 1: Requests and responses](#do-tutorial-part-1-requests-and-responses-httpsdocsdjangoprojectcomen21introtutorial01)

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
- `sudo apt-get -y install python3.7-dev default-libmysqlclient-dev gcc build-essential libssl-dev`
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
| python -m django --v-ersion | python3.7 -m django --version |
| django-admin startproject mysite | django-admin startproject mysite .|
| python manage.py runserver | python3.7 manage.py migrate<br>python3.7 manage.py runserver 0:8080 |
| visit http://127.0.0.1:8000/ with your Web browser | visit http://127.0.0.1:8080/ with your Web browser |
| python manage.py startapp polls | python3.7 manage.py startapp polls |
| visit http://localhost:8000/polls/ with your Web browser | visit http://localhost:8080/polls/ with your Web browser |

