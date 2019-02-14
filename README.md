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
</ol>
<div>
  <h3>h3</h3>
  <p>p</p>
</div>
cd workspace/django-tutorial<br>
<br>
$ git clone https://github.com/eakwichs/django-tutorial.git .<br>
<br>
vagrant up<br>
<br>
vagrant ssh<br>
<br>
cd /vagrant<br>
<br>
virtualenv --always-copy .venv<br>
<br>
source .venv/bin/activate<br>
