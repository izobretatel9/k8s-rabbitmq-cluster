# Описание

`RabbitMQ` — программный брокер сообщений на основе стандарта AMQP — тиражируемое связующее программное обеспечение, ориентированное на обработку сообщений. Создан на основе системы Open Telecom Platform, написан на языке Erlang, в качестве движка базы данных для хранения сообщений использует Mnesia.

## Инструкция по применению: 

1. Изменить под себя;
2. Deploy делать через `Jenkins`;
3. Раскатывать в любой кластер `k8s`;
4. `Credentials` - прописать в Jenkins;
5. `WERF_KUBE_CONTEXT` - поменять;
6. `@Library('jenkins-devops@dev')_` - библиотека функции `Jenkins`.

## Дполнительная информация: 

1. .helm\templates\03-grafana\rabbitmq.yaml - уже готовый `Dashboard` для `Grafana`

    Был взят из источника https://grafana.com/grafana/dashboards/10991

2. Вход в дефолтную админку:
```
login = guest  
password = guest 
```
## P.s.
Разработано под "`Deckhouse Kubernetes platform`"
https://deckhouse.io/en/