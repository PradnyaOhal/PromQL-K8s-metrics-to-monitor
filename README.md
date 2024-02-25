Basic Pod Metrics:

#	Number of pods in a specific namespace:
kube_pod_info{namespace="your-namespace"}

#	Number of pods in a specific state (Running, Pending, etc.):
kube_pod_status_phase{phase="Running"}

#	Resource usage of all pods:
container_cpu_usage_seconds_total{pod!=""}
container_memory_working_set_bytes{pod!=""}

#	Resource requests and limits of all pods:

kube_pod_container_resource_requests{resource="cpu"}
kube_pod_container_resource_limits{resource="memory"}

#Pod Health and Performance:
#	Number of pods in an unhealthy state:
kube_pod_status_phase{phase!="Running" and phase!="Completed"}

#	Pods with restarts:
kube_pod_restart_total{pod!=""}

#	Container crashes:
container_crash_total{pod!=""}

#	Pod scrape failures:
up{job="node-exporter", instance=~".*pod.*"}

#Advanced Monitoring:
#	Pod logs:
http_request_duration_seconds{job="kube-state-metrics", path=~"/v1/namespaces/your-namespace/pods/your-pod-name/log"}

#	Container CPU throttling:
container_cpu_usage_seconds_total{pod!=""} > container_cpu_quota_seconds_total{pod!=""}

#	Network traffic:
sum by (pod) (container_network_transmit_bytes_total{pod!=""} + container_network_receive_bytes_total{pod!=""})

#Remember to replace:
#	your-namespace with the actual namespace you want to monitor.
#	your-pod-name with the specific pod name you're interested in.
