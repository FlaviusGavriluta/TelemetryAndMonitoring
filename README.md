# Telemetry and Monitoring

## Story

On a busy Monday morning you find out that your server has stopped working during the weekend. If you had proper monitoring and alerting set up this stressful situation would have never happened. You remember that guide you read last weekend about how to monitor Linux servers using Prometheus and Grafana, find it in your bookmarks and start setting it up.

## What are you going to learn?

- How to install Grafana, Prometheus and Prometheus Node node_exporter and make them work together.
- How to create alerts for graphs in Grafana.

## Tasks

1. Download and install Prometheus.
Create, start and enable the systemd service.
    - Prometheus is installed in the `/opt` directory. 
    - The systemd service is enabled and started.

2. To install the latest stable OSS Grafana release from apt repo.
    - Grafana is installed.

3. Download and install Prometheus Node Exporter. 
Edit `prometheus.yml` to include the `node_exporter` job and restart the Prometheus service to load the changes.
    - Prometheus Node Exporter is installed and `node_exporter` job is added to Prometheus.

4. Create a new datasource in Grafana with URL http://localhost:9090. Import the dashboard template with id 1860.
    - Datasource and Dashboard are created.

5. [OPTIONAL] Create an alert for a graph of your choice.
    - An alert is created.

## General requirements

None

## Hints

- If you are installing Prometheus and Grafana on your VirtualBox VM you should have your network adapter attached to "Bridged Adapter" using your primary network interface. This way your virtual machine will get an IP address from your router and will be in the same network as your host machine and you will be able to access Grafana and Prometheus UI through your browser.
- When you download and install third party software try to find the best place for them to live in. Leaving them in a home directory of some user that can be deleted is not a good idea. The `/opt` directory is a more suitable place for such kind of software.
- Don't leave any spaces before or after the `=` sign in your systemd service files and make sure you have the correct paths set.
- You are installing Prometheus and Grafana on a server without UI so you won't be able to access localhost:9090 or localhost:3000, but you should be able to access the UI using the IP address of your VM instead of `localhost` from your host machine if you have followed the first hint.
- For each new service that you install don't forget to check if it is enabled with command `systemctl is-enabled <service-name>` and if it is not enable it so it can start automatically after a system reboot.
- To set up an alert for a graph click the title of the graph and select `Edit` from the drop down menu. The `Alert` tab is where you can add an alert but if you have used the node exported dashboard template you may see the following message `Template variables are not supported in alert queries`. This is because the alerts in Grafana do not support templating.
If you take the `CPU Basic` graph for example in the `Query` tab the first query is:
`sum by (instance)(irate(node_cpu_seconds_total{mode="system",instance="$node",job="$job"}[5m])) * 100`
You can add the same query and replace the template values `$node` and `$job` with values such as "localhost:9100" and "node_exporter" and if you don't want it to be visible on the graph you can click on the eye icon. If you go back to the `Alert` tab now you can set up an alert for your new metric.

## Background materials

- <i class="far fa-exclamation"></i> [A Guide to Monitor Linux Server using Prometheus and Grafana](https://geekflare.com/prometheus-grafana-setup-for-linux/)
- <i class="far fa-exclamation"></i> [Grafana: The open observability platform | Grafana Labs](https://grafana.com/)
- <i class="far fa-exclamation"></i> [Prometheus - Monitoring system & time series database](https://prometheus.io/)
- <i class="far fa-exclamation"></i> [prometheus/node_exporter: Exporter for machine metrics](https://github.com/prometheus/node_exporter)
- <i class="far fa-exclamation"></i> [Create alerts](https://grafana.com/docs/grafana/latest/alerting/create-alerts/)
