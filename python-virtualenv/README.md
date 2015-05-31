akema.python
============

Install virtualenv with python interpreter 2.7 or 3.4. Work on Freebsd and Debian

Role Variables
--------------

    python_virtualenv_dir: /tmp/.env
    python3_enabled: true
    python_remove_virtualenv: false

Example Playbook
----------------

here an example of how to use the role

    - hosts: servers
      roles:
         - { role: akema.python, python_virtualenv_dir: /tmp/.env, python3_enabled: true }

FreeBSD
-------

on FREEBSD set ansible_python_interpreter variable to /usr/local/bin/python

    ansible_python_interpreter: /usr/local/bin/python

License
-------

BSD
