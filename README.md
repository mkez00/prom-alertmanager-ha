# High Availability Prometheus and Alertmanager

![alt text](https://github.com/mkez00/prom-alertmanager-ha/blob/master/resources/PrometheusHA.png)

The following Vagrantfile demonstrates how one could configure a HA setup of Prometheus and Alertmanager.  Two nodes running Docker Compose with mirrored Prometheus and Alertmanager containers (configured in a clustered configuration) helps achieve HA.  This project was created to demonstrate the following:

- Not have duplicate alerts trigger when >1 Prometheus instance is registered to the same Alertmanager
- Not have duplicate notifications trigger when >1 Alertmanager instance is registered and all instances are exposed to receiving the same alerts
- Have multiple Alertmanagers configured in a cluster and share settings (like Silences)
- Alerts still trigger when one of the Prometheus instances is stopped/removed
- Notifications still trigger when one of the Alertmanager instances is stopped/removed