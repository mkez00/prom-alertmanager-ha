# High Availability Prometheus and Alertmanager

![alt text](https://github.com/mkez00/prom-alertmanager-ha/blob/master/resources/PrometheusHA.png)

The following Vagrantfile demonstrates how one could configure a HA setup of Prometheus and Alertmanager.  Two nodes running Docker Compose with mirrored Prometheus and Alertmanager containers (configured in a clustered configuration) helps achieve HA.  This project was created to demonstrate the following:

- Not have duplicate alerts trigger when >1 Prometheus instance is registered to the same Alertmanager
- Not have duplicate notifications trigger when >1 Alertmanager instance is registered and all instances are exposed to receiving the same alerts
- Have multiple Alertmanagers configured in a cluster and share settings (like Silences)
- Alerts still trigger when one of the Prometheus instances is stopped/removed
- Notifications still trigger when one of the Alertmanager instances is stopped/removed

## Setup and Testing

1. Clone/download project source code
2. Run `vagrant up` from project root
3. Update alert Receiver's (this project has a sample AWS SES setup) by updating `/etc/alertmanager/alertmanager.yml` in both Docker nodes.  Access Docker nodes using `vagrant ssh docker-node-1` and `vagrant ssh docker-node-2`
4. Restart Alertmanager Docker container on both Docker nodes (`docker ps` to get list of Docker containers.  Copy ID of Alertmanager.  Restart using `docker restart <CONTAINER_ID>`)
5. Poweroff worker node to trigger alert