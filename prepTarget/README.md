# Prep new host

The hosts file will contain the variables `ansible_host` and `ansible_user`  
The alias can be referred to with the variable `inventory_hostname`  
The docs say the variables should be defined in separate file but will do this for now

    [newapt]
    deb1 ansible_host=10.1.1.30 ansible_user=root
    ubu1 ansible_host=10.1.1.31 ansible_user=root
    ubuk1 ansible_host=10.1.1.32 ansible_user=ubuntu

## Run the playbook

    ansible-playbook prepApt.yml -k -K
    or
    ansible-playbook prepApt.yml --ask-pass --ask-sudo-pass

