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
Click the Windows or Start icon.<br>
In the Programs list, open the Git folder.<br>
Click the option for Git Bash.

<h3>Create folder <code>django-tutorial</code></h3>
<code>mkdir tutorial</code><br>
<code>cd workspace/django-tutorial</code>

<h3>Clone this repository into folder <code>django-tutorial</code></h3>
<code>git clone https://github.com/eakwichs/django-tutorial.git .</code>

<h3>Creates and configures guest machines</h3>
<code>vagrant up</code>

<h3>Option, Forces reprovisioning of the vagrant machine</h3>
<code>vagrant provision</code>

<h3>connects to vagrant machine via SSH</h3>
<code>vagrant ssh</code><br>
<code>cd /vagrant</code>

<h3>Option, Create a virtualenv to isolate our package dependencies locally</h3>
<code>virtualenv --always-copy .venv</code>

<h3>Option, Activate this environment</h3>
<code>source .venv/bin/activate</code>

<h3>Option, Deactivate this environment</h3>
<code>deactivate</code>
