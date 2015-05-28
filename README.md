# Akema ansible roles

add submodule in roles/ folder

    mkdir deployment
    cd deployment
    git submodule add ssh://git@gitlab.akema.fr:33622/akema/ansible-roles.git roles
    git submodule update --init

copy default-playbook.yml

    cp role/default-playbook.yml ${app_name}.yml
    
modify variables in the playbook to meet your need

    edit ${app_name}.yml

deploy your application (be sure you can ssh to your server and run)

    ansible-playbook --ask-sudo-pass -i '192.168.5.x,' ${app_name}.yml