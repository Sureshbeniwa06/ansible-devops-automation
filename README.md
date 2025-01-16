# ansible-k8s-docker-monitoring

This project provides an automated solution for deploying an e-commerce service using **Ansible**, **Docker**, and **Kubernetes**. It includes provisioning Docker containers, deploying applications on Kubernetes, and setting up monitoring with Prometheus and Grafana.


## Prerequisites
- **Ansible** installed on your system.
- **Docker** installed and running on the local system.
- **Kubernetes** cluster setup (e.g., Minikube).
- `kubectl` configured to interact with your cluster.

## Step-by-Step Guide

### Step 1: Clone the Repository
```bash
git clone https://github.com/Sureshbeniwa06/ansible-k8s-docker-monitoring.git
cd ansible-k8s-docker-monitoring
```

### Step 2: Configure Inventory File
Edit the `inventory.ini` file to define your hosts. For local deployment:
```ini
[local]
localhost ansible_connection=local
```

### Step 3: Provision Docker Containers
Run the Docker provisioning playbook:
```bash
ansible-playbook -i inventory.ini playbooks/docker_provision.yml
```
This will ensure Docker is running and the e-commerce service container is provisioned.

### Step 4: Deploy Applications on Kubernetes
Run the Kubernetes deployment playbook:
```bash
ansible-playbook -i inventory.ini playbooks/k8s_deploy.yml
```
This playbook deploys the e-commerce application and sets up Prometheus and Grafana.

### Step 5: Verify Deployment
- **Docker**: Ensure the container is running:
  ```bash
  docker ps
  ```
  Access the e-commerce service at: `http://localhost:8080`

- **Kubernetes**: Check the status of pods and services:
  ```bash
  kubectl get pods
  kubectl get svc
  ```

### Step 6: Access Prometheus and Grafana
#### Prometheus
Port forward the Prometheus service:
```bash
kubectl port-forward svc/prometheus-service 9090:9090
```
Access Prometheus at: `http://localhost:9090`

#### Grafana
Port forward the Grafana service:
```bash
kubectl port-forward svc/grafana-service 3000:3000
```
Access Grafana at: `http://localhost:3000`
Default login credentials:
- **Username**: `admin`
- **Password**: `admin`

### Step 7: Cleanup
To stop and remove all deployments:
```bash
kubectl delete -f monitoring/prometheus.yml
kubectl delete -f monitoring/garfana.yml
```

## Best Practices
- Use a separate namespace in Kubernetes for the e-commerce application and monitoring stack.
- Store sensitive data such as database credentials and API keys in Kubernetes Secrets.
- Set up persistent storage for Prometheus and Grafana to retain data across restarts.

## License
This project is licensed under the MIT License. See the LICENSE file for details.

## Contributing
Contributions are welcome! Feel free to open issues or submit pull requests for improvements.
