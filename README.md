# django-tutorial

Django 2.1 Official Tutorial on Windows 10<br>
https://docs.djangoproject.com/en/2.1/


<h1>Guide to preparing for tutorials</h1>

<h3>Install programs</h3>
<ol>
  <li>Atom ( https://atom.io/ )</li>
  <li>Git ( https://git-scm.com/ )
    <ul>
      <li><strong>Choosing the default editor used by Git</strong></li>
      <li>Choose Nano or Atom ( I choose Atom )</li>
      <li><strong>How would you like to use Git for the command line?</strong></li>
      <li>Use Git and optional Unix Tools from the Windows Command Prompt</li>
    </ul>
  </li>
  <li>Vagrant ( https://www.vagrantup.com/ )</li>
  <li>VirtualBox ( https://www.virtualbox.org/ )</li>
</ol>

<h3>Set up workspace</h3>
Create folder <code>workspace</code> on C:\Users\Username


<h1>How to use</h1>

<h3>Open the Git Bash prompt</h3>
<ul>
  <li>Click the Windows or Start icon</li>
  <li>In the Programs list, open the Git folder</li>
  <li>Click the option for Git Bash</li>
</ul>

<h3>Create folder <code>django-tutorial</code></h3>
<ul>
  <li><code>mkdir tutorial</code></li>
  <li><code>cd workspace/django-tutorial</code></li>
</ul>

<h3>Clone this repository into folder <code>django-tutorial</code></h3>
<code>git clone https://github.com/eakwichs/django-tutorial.git .</code>

<h3>Creates and configures guest machines</h3>
<code>vagrant up</code>

<h3>Option, Forces reprovisioning of the vagrant machine</h3>
<code>vagrant provision</code>

<h3>Connects to vagrant machine via SSH</h3>
<ul>
  <li><code>vagrant ssh</code></li>
  <li><code>cd /vagrant</code></li>
</ul>

<h3>Option, Create a virtualenv to isolate our package dependencies locally</h3>
<code>virtualenv --always-copy .venv</code>

<h3>Option, Activate this environment</h3>
<code>source .venv/bin/activate</code>

<h3>Option, Deactivate this environment</h3>
<code>deactivate</code>

<h3>Install Django</h3>
<code>sudo -H pip install Django</code>

<h1>Do Tutorial: Part 1: Requests and responses</h1>
https://docs.djangoproject.com/en/2.1/intro/tutorial01/

<h3>Command</h3>
<table>
  <tr>
    <th>From Official</th>
    <th>Use this</th>
  </tr>
  <tr>
    <td>python -m django --version</td>
    <td>python3 -m django --version</td>
  </tr>
  <tr>
    <td>django-admin startproject mysite</td>
    <td>django-admin startproject mysite</td>
  </tr>
  <tr>
    <td>python manage.py runserver</td>
    <td>sudo python3 manage.py migrate<br>
      sudo python3 manage.py runserver 0:8080
    </td>
  </tr>
  <tr>
    <td>visit http://127.0.0.1:8000/ with your Web browser</td>
    <td>visit http://127.0.0.1:8080/ with your Web browser</td>
  </tr>
  <tr>
    <td>python manage.py startapp polls</td>
    <td>python3 manage.py startapp polls</td>
  </tr>
  <tr>
    <td>visit http://localhost:8000/polls/ with your Web browser</td>
    <td>visit http://localhost:8080/polls/ with your Web browser</td>
  </tr>
</table>
