Role Name
=========

Перед разворачиванием кластера:
- В инвентори, каждому серверу присвоить уникальный kafka_node_id (можно натуральное число: 1, 2, 3,...) 
- В инвентори на группу серверов прописать kafka_controller_quorum_voters в формате:
  kafka_controller_quorum_voters=1@0000pcielk31.pcidss.local:9093,2@0000pcielk32.pcidss.local:9093,3@0000pcielk33.pcidss.local:9093
- В инвентори на группу серверов прописать kafka_cluster_uuid - рандомный идентификатор кластера
- Проверить, что сервера кластера доступны по имени хоста (по короткому имени)

Пример записи в инвентори
```yaml
    kafka:
      vars:
        kafka_cluster_uuid: "c848b0c9-ce64-4c59-bc14-824e0554e36a"
        kafka_controller_quorum_voters: "1@192.168.1.12:9093,2@192.168.1.13:9093,3@192.168.1.14:9093"
      hosts:
        s102:
          ansible_host: 192.168.1.12
          kafka_node_id: 1
        s103:
          ansible_host: 192.168.1.13
          kafka_node_id: 2
        s104:
          ansible_host: 192.168.1.14
          kafka_node_id: 3
```


- установка (playbook разворачивает с типовым файлом конфигурации, если требуются специфические настройки готовим файлы конфигурации и выполняем kafka-config.yaml)
> ansible-playbook -i ./inventories/<zone>.yml  kafka-install.yaml  --extra-vars "var_host=<hosts>"
после установки рекомендуется сохнанить файлы конфигурации в репе для возможности их последующего обновления
"{{ playbook_dir }}/files/kafka/{{ zone }}/{{ inventory_hostname }}/server.properties"

- обновление файла конфигурации 
предварительно проверить наличие файлов конфигураций в "{{ playbook_dir }}/files/kafka/{{ zone }}/{{ inventory_hostname }}/server.properties"
> ansible-playbook -i ./inventories/<zone>.yml  kafka-config.yaml  --extra-vars "var_host=<hosts>"