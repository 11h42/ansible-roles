akema.uwsgi
===========

config uwsgi.ini files for every uwsgi_config in variables, {{ python_virtualenv_dir }} should exists and have pip installed

Role Variables
--------------

uwsgi_config_dir: /tmp/uwsgi
python_virtualenv_dir: /tmp/.env
uwsgi_configs:
  app:
    - [uwsgi]


Example Playbook
----------------

here an example of how to use the role

    - hosts: servers  
      vars:
        app_name: {{ APP_NAME }}
        app_user: "{{app_name}}"
        app_dir: "/usr/local/{{app_name}}"
        log_dir: "{{app_dir}}/log"
    
        python_virtualenv_dir: "{{app_dir}}/.env"
    
        uwsgi_config_dir: "{{app_dir}}/config"
        
        uwsgi_configs:
          awesome_app:
            - "[uwsgi]"
            - "chdir = {{app_dir}}"
            - "env = {{python_virtualenv_dir}}"
            - "pythonpath = %(chdir)"
            - "processes = 1"
            - "module = run"
            - "callable = {{app_name}}"
            - "uid = {{app_user}}"
            - "gid = {{app_user}}"
            - "socket = /tmp/{{app_name}}.uwsgi.sock"
            - "chmod-socket = 666"
            - "logto = {{log_dir}}/{{app_name}}.uwsgi.log"

            
      roles:
         - uwsgi


License
-------

BSD
