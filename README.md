# High Availability Prometheus and Alertmanager

The following Vagrantfile demonstrates how one COULD configure a HA setup of Prometheus and Alertmanager.  Since the entire cluster is running on one node (in a single Docker Compose file) it is obviously not trully HA in this example.  This project was created to demonstrate the following:

- Not have duplicate alerts trigger when >1 Prometheus instance is registered to the same Alertmanager
- Not have duplicate notifications trigger when >1 Alertmanager instance is registered and all are listenning to the same alerts
- Have multiple Alertmanagers configured in a cluster and share settings (like Silences)
- Alerts still trigger when one of the Prometheus instances is stopped/removed
- Notifications still trigger when one of the Alertmanager instances is stopped/removed