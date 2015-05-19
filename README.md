# Akema ansible roles

## Roles default variables

### nginx

  * nginx_server_name: localhost
  * nginx_client_max_body_size: 5M
  * uwsgi_socket_path: /tmp/uwsgi.sock
  * application_name: django
  * application_static_folder_location: /var/www

## Inheritance

We want to use roles describe in this repository on another project. In a deployment folder we want :

    deployment/
        roles/
        my_super_project/
            meta/
                main.yml
        hosts
        my_super_project.yml
    

add submodule in roles/ folder

    mkdir deployment
    cd deployment
    git submodule add ssh://git@gitlab.akema.fr:33622/akema/ansible-roles.git roles
    git submodule update --init

create host file

    [ubuntu]
    my_super_project.fr     ansible_ssh_host=192.168.5.130

create yml file

    ---
    - name: my_super_project
      hosts: my_super_project.fr
      remote_user: root
      sudo: yes
    
      roles:
        - my_super_project


add depencies in my_super_project/meta/main.yml file, and overwrite variables for every role

    ---
    dependencies:
      - { role: nginx, application_name: my_super_app }
      


## Deploy application

be sure you can ssh to your server and run

    ansible-playbook -i hosts --ask-sudo-pass my_super_project.yml