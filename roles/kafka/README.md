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
    elk-kafka:
      vars:
        kafka_cluster_uuid: "c848b0c9-ce64-4c59-bc14-824e0554e36a"
        kafka_controller_quorum_voters: "1@ft-kafka-d02p:9093,2@ft-kafka-d04p:9093,3@ft-kafka-d05p:9093"
      hosts:
        ft-kafka-d02p:
          ansible_host: 11.211.240.31
          kafka_node_id: 1
        ft-kafka-d04p:
          ansible_host: 11.211.240.32
          kafka_node_id: 2
        ft-kafka-d05p:
          ansible_host: 11.211.240.33
          kafka_node_id: 3
```