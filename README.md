# django-tutorial

Django 2.1 Official Tutorial on Windows 10<br>
<a href="https://docs.djangoproject.com/en/2.1/">https://docs.djangoproject.com/en/2.1/</a><br>
<br>
Virtual machine in VirtualBox running Ubuntu 18.04


<h1>Guide to preparing for tutorials</h1>

<h3>Install programs</h3>
<ol>
  <li>Atom ( <a href="https://atom.io/">https://atom.io/</a> )</li>
  <li>Git ( <a href="https://git-scm.com/">https://git-scm.com/</a> )
    <ul>
      <li><strong>Choosing the default editor used by Git</strong></li>
      <li>Choose Nano or Atom ( I choose Atom )</li>
      <li><strong>How would you like to use Git for the command line?</strong></li>
      <li>Use Git and optional Unix Tools from the Windows Command Prompt</li>
    </ul>
  </li>
  <li>VirtualBox ( <a href="https://www.virtualbox.org/">https://www.virtualbox.org/</a> )</li>
  <li>Vagrant ( <a href="https://www.vagrantup.com/">https://www.vagrantup.com/</a> )</li>
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
  <li><code>cd workspace</code></li>
  <li><code>mkdir django-tutorial</code></li>
  <li><code>cd django-tutorial</code></li>
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

<h3>Option, Terminate the virtual machine</h3>
<code>vagrant destroy</code>

<h3>Check python version</h3>
<code>python3.7 -V</code><br>
Python 3.7.2

<h3>Check pip version</h3>
<code>pip --version</code><br>
pip 19.0.2 from /usr/local/lib/python3.7/dist-packages/pip (python 3.7)

<h3>Create folder <code>src</code></h3>
<code>mkdir src</code>

<h3>Create a virtual environment</h3>
<ul>
  <li><code>cd src</code></li>
  <li><code>virtualenv --always-copy venv</code></li>
</ul>

<h3>To begin using the virtual environment, it needs to be activated</h3>
<code>source venv/bin/activate</code>

<h3>Option, If you are done working in the virtual environment for the moment, you can deactivate it</h3>
<code>deactivate</code>

<h3>Install Django</h3>
<code>pip install Django</code>

<h1>Do Tutorial: Part 1: Requests and responses</h1>
<a href="https://docs.djangoproject.com/en/2.1/intro/tutorial01/">https://docs.djangoproject.com/en/2.1/intro/tutorial01/</a>

<h3>Command</h3>
<table>
  <tr>
    <th>From Official</th>
    <th>Use this</th>
  </tr>
  <tr>
    <td>python -m django --version</td>
    <td>python3.7 -m django --version</td>
  </tr>
  <tr>
    <td>django-admin startproject mysite</td>
    <td>django-admin startproject mysite .</td>
  </tr>
  <tr>
    <td>python manage.py runserver</td>
    <td>python3.7 manage.py migrate<br>
      python3.7 manage.py runserver 0:8080
    </td>
  </tr>
  <tr>
    <td>visit <a href="http://127.0.0.1:8000/">http://127.0.0.1:8000/</a> with your Web browser</td>
    <td>visit <a href="http://127.0.0.1:8080/">http://127.0.0.1:8080/</a> with your Web browser</td>
  </tr>
  <tr>
    <td>python manage.py startapp polls</td>
    <td>python3.7 manage.py startapp polls</td>
  </tr>
  <tr>
    <td>visit <a href="http://localhost:8000/polls/" target="_blank">http://localhost:8000/polls/</a> with your Web browser</td>
    <td>visit <a href="http://localhost:8080/polls/" target="_blank">http://localhost:8080/polls/</a> with your Web browser</td>
  </tr>
</table>
