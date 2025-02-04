# ansible roles

проверить наличие файла для пользователя, под которым выполняется playbook и у пользователя должны быть права на целевых хостах
- ansible_ssh_user: ansible
- ansible_ssh_private_key_file: ~/.ssh/id_ansible

# Установка java
> ansible-playbook -i ./inventories/home.yml  java-install.yml  --extra-vars "var_hosts=s101"

# Установка kafka
Установка kafka кластера (выполняем для каждого сервера кластера, в зависимости от настроек инвентори). См. также Readme в роли
> ansible-playbook -i ./inventories/home.yml  kafka-install.yml  --extra-vars "var_hosts=s102"