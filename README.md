# ansible roles

# Установка java
ansible-playbook -i ./inventories/home.yml  java-install.yml  --extra-vars "var_hosts=s101"

# Установка kafka
## Установка kafka кластера (выполняем для каждого сервера кластера, в зависимости от настроек инвентори). См. также Readme в роли
ansible-playbook -i ./inventories/home.yml  kafka-install.yml  --extra-vars "var_hosts=s102"