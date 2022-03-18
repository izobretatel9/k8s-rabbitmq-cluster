# Description

`RabbitMQ` — AMQP-based messaging software broker is a replicable message-oriented middleware. Created on the basis of the Open Telecom Platform system, written in the Erlang language, it uses Mnesia as a database engine for storing messages.

## Instructions for use: 

1. Change for yourself;
2. Deploy do through `Jenkins`;
3. `Credentials` - prescribe in Jenkins;
4. `WERF_KUBE_CONTEXT` - change;
5. `@Library('jenkins-devops@dev')_` - function library `Jenkins`.

## Additional Information: 

1. .helm\templates\03-grafana\rabbitmq.yaml - ready `Dashboard` in `Grafana`

    Was taken from the source https://grafana.com/grafana/dashboards/10991

2. Default admin login:
```
login = guest  
password = guest 
```
## P.s.
Designed for "`Deckhouse Kubernetes platform`"
https://deckhouse.io/en/
