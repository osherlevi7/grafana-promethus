# grafana-promethus
Monitoring a Linux host with Prometheus, Node Exporter, and Docker Compose




### REQ: 
* A Grafana Cloud account. To create an account, please see Grafana Cloud and click on Start for free.
* A Grafana Cloud API key with the Metrics Publisher role
* A Linux machine
* Docker and Docker Compose installed on your Linux machine

# Compose   
### Start the prometheus and node-exporter containers using the docker-compose command. Instruct Compose to run the containers in the background with the -d flag
    $ docker-compose up -d

</b>
    
    Creating network "root_monitoring" with driver "bridge"
    Creating volume "root_prometheus_data" with default driver
    . . . 
    Creating prometheus    ... done
    Creating node-exporter ... done

</b>

### You can get container status using docker-compose ps

    $ docker-compose ps

</b>

         Name                   Command               State    Ports
    -----------------------------------------------------------------
    node-exporter   /bin/node_exporter --path. ...   Up      9100/tcp
    prometheus      /bin/prometheus --config.f ...   Up      9090/tcp


### Verify the status of prometheus by checking its logs. It should look something like this

    $ docker-compose logs -f prometheus

</b>

     . . .
    prometheus       | level=info ts=2021-08-09T21:33:36.913Z caller=main.go:1012 msg="Completed loading of configuration file" filename=/etc/prometheus/prometheus.yml totalDuration=1.811787ms remote_storage=385.158µs web_handler=479ns query_engine=883ns scrape=885.52µs scrape_sd=40.728µs notify=1.09µs notify_sd=1.44µs rules=1.209µs
    prometheus       | level=info ts=2021-08-09T21:33:36.913Z caller=main.go:796 msg="Server is ready to receive web requests."
    prometheus       | ts=2021-08-09T21:33:44.544Z caller=dedupe.go:112 component=remote level=info remote_name=cd5833 url=https://prometheus-blocks-prod-us-central1.grafana.net/api/prom/push msg="Done replaying WAL" duration=7.632082491s

### Verify the status of node-exporter by checking its logs. It should look something like this:

    $ docker-compose logs -f node-exporter


</b>

     . . .
    node-exporter    | level=info ts=2021-08-09T21:33:36.852Z caller=node_exporter.go:115 collector=vmstat
    node-exporter    | level=info ts=2021-08-09T21:33:36.852Z caller=node_exporter.go:115 collector=xfs
    node-exporter    | level=info ts=2021-08-09T21:33:36.852Z caller=node_exporter.go:115 collector=zfs
    node-exporter    | level=info ts=2021-08-09T21:33:36.852Z caller=node_exporter.go:199 msg="Listening on" address=:9100
    node-exporter    | level=info ts=2021-08-09T21:33:36.852Z caller=tls_config.go:191 msg="TLS is disabled." http2=false

