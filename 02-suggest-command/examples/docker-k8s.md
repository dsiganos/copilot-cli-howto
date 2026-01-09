# Docker & Kubernetes Examples

Container and orchestration operations using `gh copilot suggest`.

## Docker Basics

### Container Management

```bash
# List containers
gh copilot suggest "show all running containers"
# → docker ps

# List all containers (including stopped)
gh copilot suggest "show all containers including stopped ones"
# → docker ps -a

# Start container
gh copilot suggest "start stopped container"
# → docker start container-name

# Stop container
gh copilot suggest "stop running container"
# → docker stop container-name

# Restart container
gh copilot suggest "restart container"
# → docker restart container-name
```

### Running Containers

```bash
# Run container
gh copilot suggest "run nginx container on port 8080"
# → docker run -d -p 8080:80 nginx

# Run with volume
gh copilot suggest "run container with mounted volume"
# → docker run -v /host/path:/container/path image-name

# Run interactively
gh copilot suggest "run ubuntu container with interactive shell"
# → docker run -it ubuntu /bin/bash

# Run with environment variables
gh copilot suggest "run container with environment variables"
# → docker run -e KEY=value image-name

# Run with name
gh copilot suggest "run container with specific name"
# → docker run --name my-container image-name
```

### Container Information

```bash
# Inspect container
gh copilot suggest "show detailed container information"
# → docker inspect container-name

# Container logs
gh copilot suggest "show container logs"
# → docker logs container-name

# Follow logs
gh copilot suggest "stream container logs in real-time"
# → docker logs -f container-name

# Last N lines
gh copilot suggest "show last 100 lines of container logs"
# → docker logs --tail 100 container-name

# Resource usage
gh copilot suggest "show container resource usage"
# → docker stats container-name
```

### Executing in Containers

```bash
# Execute command
gh copilot suggest "run command in running container"
# → docker exec container-name command

# Interactive shell
gh copilot suggest "open bash shell in running container"
# → docker exec -it container-name /bin/bash

# Run as specific user
gh copilot suggest "execute command as root in container"
# → docker exec -u root container-name command
```

## Docker Images

### Image Management

```bash
# List images
gh copilot suggest "show all docker images"
# → docker images

# Pull image
gh copilot suggest "download ubuntu image from docker hub"
# → docker pull ubuntu

# Remove image
gh copilot suggest "delete docker image"
# → docker rmi image-name

# Remove unused images
gh copilot suggest "remove dangling docker images"
# → docker image prune
```

### Building Images

```bash
# Build image
gh copilot suggest "build docker image from Dockerfile"
# → docker build -t my-image:tag .

# Build with no cache
gh copilot suggest "build docker image without using cache"
# → docker build --no-cache -t my-image:tag .

# Build with different Dockerfile
gh copilot suggest "build using specific Dockerfile"
# → docker build -f Dockerfile.prod -t my-image .
```

### Image Information

```bash
# Image history
gh copilot suggest "show docker image build history"
# → docker history image-name

# Image size
gh copilot suggest "show docker image sizes"
# → docker images --format "{{.Repository}}:{{.Tag}}\t{{.Size}}"

# Inspect image
gh copilot suggest "show detailed image information"
# → docker inspect image-name
```

## Docker Cleanup

### Container Cleanup

```bash
# Remove container
gh copilot suggest "remove stopped container"
# → docker rm container-name

# Force remove running container
gh copilot suggest "force remove running container"
# → docker rm -f container-name

# Remove all stopped containers
gh copilot suggest "remove all stopped containers"
# → docker container prune

# Stop and remove all containers
gh copilot suggest "stop all running containers and remove them"
# → docker stop $(docker ps -q) && docker rm $(docker ps -aq)
```

### System Cleanup

```bash
# Clean up everything
gh copilot suggest "remove all unused docker resources"
# → docker system prune -a

# Remove unused volumes
gh copilot suggest "remove unused docker volumes"
# → docker volume prune

# Remove unused networks
gh copilot suggest "remove unused docker networks"
# → docker network prune

# Show disk usage
gh copilot suggest "show docker disk usage"
# → docker system df
```

## Docker Compose

### Basic Operations

```bash
# Start services
gh copilot suggest "start docker compose services"
# → docker-compose up -d

# Stop services
gh copilot suggest "stop docker compose services"
# → docker-compose down

# View logs
gh copilot suggest "show logs for all compose services"
# → docker-compose logs

# Restart service
gh copilot suggest "restart specific compose service"
# → docker-compose restart service-name
```

### Advanced Compose

```bash
# Build and start
gh copilot suggest "rebuild and start compose services"
# → docker-compose up -d --build

# Scale service
gh copilot suggest "scale compose service to 3 instances"
# → docker-compose up -d --scale service-name=3

# View running services
gh copilot suggest "list running compose services"
# → docker-compose ps

# Execute in service
gh copilot suggest "run command in compose service"
# → docker-compose exec service-name command
```

## Kubernetes Basics

### Cluster Information

```bash
# Cluster info
gh copilot suggest "show kubernetes cluster information"
# → kubectl cluster-info

# Node information
gh copilot suggest "list all kubernetes nodes"
# → kubectl get nodes

# Node details
gh copilot suggest "show detailed node information"
# → kubectl describe node node-name

# Namespaces
gh copilot suggest "list all namespaces"
# → kubectl get namespaces
```

### Pod Management

```bash
# List pods
gh copilot suggest "show all pods"
# → kubectl get pods

# Pods in all namespaces
gh copilot suggest "show pods across all namespaces"
# → kubectl get pods --all-namespaces

# Pod details
gh copilot suggest "show detailed pod information"
# → kubectl describe pod pod-name

# Pod logs
gh copilot suggest "show logs from pod"
# → kubectl logs pod-name

# Follow logs
gh copilot suggest "stream pod logs in real-time"
# → kubectl logs -f pod-name
```

### Pod Operations

```bash
# Execute in pod
gh copilot suggest "run command in kubernetes pod"
# → kubectl exec -it pod-name -- command

# Shell into pod
gh copilot suggest "open shell in pod"
# → kubectl exec -it pod-name -- /bin/bash

# Delete pod
gh copilot suggest "delete kubernetes pod"
# → kubectl delete pod pod-name

# Port forward
gh copilot suggest "forward local port to pod port"
# → kubectl port-forward pod-name 8080:80
```

### Deployments

```bash
# List deployments
gh copilot suggest "show all deployments"
# → kubectl get deployments

# Deployment details
gh copilot suggest "show detailed deployment information"
# → kubectl describe deployment deployment-name

# Scale deployment
gh copilot suggest "scale deployment to 5 replicas"
# → kubectl scale deployment deployment-name --replicas=5

# Update image
gh copilot suggest "update deployment with new image"
# → kubectl set image deployment/deployment-name container=image:tag

# Rollout status
gh copilot suggest "check deployment rollout status"
# → kubectl rollout status deployment/deployment-name
```

### Rollout Management

```bash
# Rollout history
gh copilot suggest "show deployment rollout history"
# → kubectl rollout history deployment/deployment-name

# Rollback
gh copilot suggest "rollback deployment to previous version"
# → kubectl rollout undo deployment/deployment-name

# Restart deployment
gh copilot suggest "restart deployment"
# → kubectl rollout restart deployment/deployment-name

# Pause rollout
gh copilot suggest "pause deployment rollout"
# → kubectl rollout pause deployment/deployment-name
```

## Kubernetes Services

```bash
# List services
gh copilot suggest "show all kubernetes services"
# → kubectl get services

# Service details
gh copilot suggest "show detailed service information"
# → kubectl describe service service-name

# Expose deployment
gh copilot suggest "expose deployment as service"
# → kubectl expose deployment deployment-name --port=80 --type=LoadBalancer

# Delete service
gh copilot suggest "delete kubernetes service"
# → kubectl delete service service-name
```

## ConfigMaps and Secrets

```bash
# List configmaps
gh copilot suggest "show all configmaps"
# → kubectl get configmaps

# Create configmap
gh copilot suggest "create configmap from file"
# → kubectl create configmap config-name --from-file=config.yaml

# List secrets
gh copilot suggest "show all secrets"
# → kubectl get secrets

# Create secret
gh copilot suggest "create secret from literal values"
# → kubectl create secret generic secret-name --from-literal=key=value

# View secret
gh copilot suggest "decode and view secret data"
# → kubectl get secret secret-name -o jsonpath='{.data}' | base64 -d
```

## Kubernetes Debugging

### Troubleshooting Pods

```bash
# Failing pods
gh copilot suggest "show pods that are not running"
# → kubectl get pods --field-selector=status.phase!=Running

# Events
gh copilot suggest "show recent cluster events"
# → kubectl get events --sort-by='.lastTimestamp'

# Pod events
gh copilot suggest "show events for specific pod"
# → kubectl get events --field-selector involvedObject.name=pod-name

# Previous logs (crashed container)
gh copilot suggest "show logs from crashed container"
# → kubectl logs pod-name --previous
```

### Resource Usage

```bash
# Node resources
gh copilot suggest "show node resource usage"
# → kubectl top nodes

# Pod resources
gh copilot suggest "show pod CPU and memory usage"
# → kubectl top pods

# Specific namespace
gh copilot suggest "show resource usage for namespace"
# → kubectl top pods -n namespace-name

# Sort by CPU
gh copilot suggest "show pods sorted by CPU usage"
# → kubectl top pods --sort-by=cpu
```

## Kubernetes Apply and Delete

```bash
# Apply configuration
gh copilot suggest "apply kubernetes configuration from file"
# → kubectl apply -f config.yaml

# Apply directory
gh copilot suggest "apply all configs in directory"
# → kubectl apply -f ./configs/

# Delete from file
gh copilot suggest "delete resources defined in file"
# → kubectl delete -f config.yaml

# Delete all resources
gh copilot suggest "delete all resources of a type"
# → kubectl delete deployment --all
```

## Contexts and Namespaces

```bash
# Current context
gh copilot suggest "show current kubernetes context"
# → kubectl config current-context

# List contexts
gh copilot suggest "list all kubernetes contexts"
# → kubectl config get-contexts

# Switch context
gh copilot suggest "switch to different kubernetes context"
# → kubectl config use-context context-name

# Set namespace
gh copilot suggest "set default namespace for context"
# → kubectl config set-context --current --namespace=namespace-name
```

## Helm Operations

```bash
# List releases
gh copilot suggest "show all helm releases"
# → helm list

# Install chart
gh copilot suggest "install helm chart"
# → helm install release-name chart-name

# Upgrade release
gh copilot suggest "upgrade helm release"
# → helm upgrade release-name chart-name

# Rollback release
gh copilot suggest "rollback helm release"
# → helm rollback release-name revision

# Uninstall release
gh copilot suggest "uninstall helm release"
# → helm uninstall release-name

# Search charts
gh copilot suggest "search for helm charts"
# → helm search repo chart-name
```

## Practical Scenarios

### Debug Failing Pod

```bash
# 1. Check pod status
gh copilot suggest "show pod status and events"

# 2. View logs
gh copilot suggest "show pod logs with timestamps"

# 3. Describe pod
gh copilot suggest "show detailed pod information and events"

# 4. Check previous container
gh copilot suggest "show logs from previous crashed container"

# 5. Execute in pod
gh copilot suggest "open shell in pod for debugging"
```

### Clean Up Docker System

```bash
# 1. Stop all containers
gh copilot suggest "stop all running containers"

# 2. Remove containers
gh copilot suggest "remove all stopped containers"

# 3. Remove images
gh copilot suggest "remove unused docker images"

# 4. Clean volumes
gh copilot suggest "remove unused volumes"

# 5. System prune
gh copilot suggest "clean up all unused docker resources"
```

### Update Kubernetes Deployment

```bash
# 1. Check current status
gh copilot suggest "show deployment status and replicas"

# 2. Update image
gh copilot suggest "update deployment with new image version"

# 3. Watch rollout
gh copilot suggest "watch deployment rollout progress"

# 4. Verify pods
gh copilot suggest "check if new pods are running"

# 5. Rollback if needed
gh copilot suggest "rollback deployment if update failed"
```

## Tips

1. **Use labels**: Tag resources for easier management
2. **Check logs first**: Most issues visible in logs
3. **Use dry-run**: Test kubectl apply with --dry-run
4. **Namespace awareness**: Always specify namespace in production
5. **Resource limits**: Set memory and CPU limits
6. **Health checks**: Configure liveness and readiness probes

## Common Gotchas

- **Image pull errors**: Check image name and registry access
- **Port conflicts**: Ensure ports aren't already in use
- **Resource limits**: Pods may fail if insufficient resources
- **Network policies**: May block communication between pods
- **Persistent volumes**: Check PVC binding status

---

**Related**: [file-operations.md](./file-operations.md) | [system-admin.md](./system-admin.md)
