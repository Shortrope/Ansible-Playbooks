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

## Create a password hash

### Get sha512 password hash:

    ansible localhost -m debug -a "msg={{ 'ansible' | password_hash('sha512') }}"

### Get sha512 password hash w a specific salt:

    ansible localhost -m debug -a "msg={{ 'ansible' | password_hash('sha512', 'thesecretsalt') }}"

### Idempotent method to generate unique hashes per system using a salt that is consistent between runs

    ansible localhost -m debug -a "msg={{ 'ansible' | password_hash('sha512', 65534 | random(seed=inventory_hostname) | string) }}"o
