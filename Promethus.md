Open src monitoring solution & time series db

was build by soundcloud
Now standalone open src project
for monitoring on-prem and cloud.
written in GO has integration capability with different cloud platforms.

*Promethus collects metrics from monitored targets by scraping HTTP endpoints.
![How Promethus works](https://github.com/testoranit/Promethus_myrepo/assets/124513439/8130651c-2da1-437b-9724-791d33cbb3c2)


Promethus installation using scripts also from official website
grom scripts
create a vm
clone the git url
u get installation scripts
install promethus..
install grafana
promethus runs on port 9090
and grafana runs on port 3000

check the by default metrics on promethus
connect garfana to data source promethus
and see the same metrics for visualation.

***
promethus config is in config yaml file..u don't need to restart prom to refelct the changes
/etc/prometheus/prometheus.yml
check
promurl:9090/targets
promurl:9090/metrics

Install node exporter
2-node-exporter.sh
script gives output to add :- Add the following lines to /etc/prometheus/prometheus.yml:

  - job_name: 'node_exporter'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9100']

on prom server do:- curl http://localhost:9100/metrics
for node exporter metrics above command.
restart prometheus
 u see node exporter also added under tareget
 ![Node exporter](https://github.com/testoranit/Promethus_myrepo/assets/124513439/3d90b64b-0411-43e0-b1b6-444023371c7e)

U can launch an Windows VM
WMI exporter for windows:-
This is similar to AMA agents in Azure monitor

download wmi expoter
Install
u can then mention the config as u did above in proemthus.yaml for wmi exporter
 - job_name: 'node_exporter'
    scrape_interval: 5s
    static_configs:
      - targets: ['ipofwindows machine:9100']
  This now scrapes metrics of windows server and sends to promsetheus server(our server)

 

Node exporter;_ for linux machines to scrape metrics
WMI exporter:- for windows machines to scrape metrics

*********
Client libraries
befor u monitor ur code..u should instrument ur code.
u can also implement using ur own exposition format
exposition formats
1)Simple text based format
2)Protocol buffer format
4 types of metrics
1)Counter:-A alue that only goes up(eg:- website  up )

2)Gauge:-A numerc value that goes up and down(CPU load)

3)histogram:-Sample observations(eg:- request durations or response sizes) and observations get counted into buckes
Include count or sum

4)Summary:-also does histogram and summary gives more details
u have 2 counters like no of requesta nd avg latency

u need install client libraries for uf application

**********
pushing metrics
Prometheus b deafult has pull based metrics
sometimes a job runs for small time(or server NA,or due to FIREWALL) and it many not be possible for promeths to pull metrics
hence that job(app)

job---->push metrics-->PUSSH GATEWAY<-----> PROmethus Pulls metrics
U can delete the metrics using API it doesn't do it on it's own.

****
PROMQL
it is read only u can't insert data

hhtp request toal in pro gui


**Service discovery**
add secret key and access key in config file yaml
Check service discovery doc for promethus online


**Exporters**
(system statstiscs)

***Aleting**
After configuring alerts on Promethus server it will send push alerts to Alert manager
in config file
- alert : cpuUsage

by default alert manager is not installed u need to install it.
COncepts
grouping:- multiple alerts ino 1 config.
inhibition:- silence other alerts if one specific alert is already fired.
Silences:- silence the alert for maintainence window.

Alert states(Inactive,pending,firing)
Alert manager runs on port 9093


lab:-
go to scripts dir on ur server
install alerbanager script run it
add the output to alertmanager.yaml
install mail server script
restart alertmanager restrat

setup alert rules


**Prometheus storage**
**Prometheus Security**
you can still enable security via authentication and TLS,using a reverse proxy.

Demo:-
go to Prom server

reverse proxy.sh


**Monitoring a Python Flask Web Application** backend **mySQL**

![MOnitoring Python web app](https://github.com/testoranit/Promethus_myrepo/assets/124513439/9f4431d1-7d31-465d-9f83-ac20bdef1ff4)

Lab:-
go to promethus server
install docker
/flask dir
docker-compose up -d 
curl localhost:5000
curl localhost:5000/query
curl localhost:5000/sleep
curl localhost:8000
curl localhost:5000/sleep

go to scrips dir
cadd add-flashk-app
execute this script
and restart prometheus
go to prom server ui and search mysql_query_latency_seconds_sum
