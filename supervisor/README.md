akema.supervisor
================

copy in {{ supervisor_conf_dir }} confif files for every process in {{ supervisor_process }}

Role Variables
--------------

supervisor_conf_dir: /etc/supervisor (default)
supervisor_process is mandatory ! example of a supervisor process with variable app_name defined

    supervisor_process:
      app:
        - [program:app]
        - command=/usr/local/{{app_name}}/.env/bin/uwsgi --ini /usr/local/{{app_name}}/config/uwsgi.ini
        - numprocs=1
        - process_name={{app_name}}
        - stdout_logfile=/var/log/supervisor/{{app_name}}.supervisor.log
        - loglevel=debug
        - redirect_stderr=true
        - autostart=true
        - autorestart=true
        - user={{app_user}}


Example Playbook
----------------

here an example of how to use the role

    - hosts: servers  
      vars:
        app_name: awesome_app
        app_user: {{app_name}}

        supervisor_process:
          awesome_app:
            - "[program:awesome_app]"
            - "command={{python_virtualenv_dir}}/bin/uwsgi --ini {{app_dir}}/config/uwsgi.ini"
            - "numprocs=1"
            - "process_name={{app_name}}"
            - "stdout_logfile={{log_dir}}/{{app_name}}.supervisor.log"
            - "loglevel=debug"
            - "redirect_stderr=true"
            - "autostart=true"
            - "autorestart=true"
            - "user={{app_user}}"
            
      roles:
         - supervisor

will create a awesome_app.conf file in {{supervisor_conf_dir}}

License
-------

BSD
