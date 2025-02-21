# Basic Configuration & Deployment

# Apply configurations
- kubectl apply -f <file.yaml>          # Deploy a resource
- kubectl apply -f <dir/>         # Deploy all YAMLs in a directory

# Create resources imperatively
- kubectl create deployment <name> --image=<image>
- kubectl expose deployment <name> --port=<port> --type=LoadBalancer

# Cluster & Context Management
- kubectl config get-clusters           # List clusters
- kubectl config get-contexts            # List contexts
- kubectl config use-context <context>   # Switch context
- kubectl config set-context --current --namespace=<ns> # Set default namespace

# Namespace Operations
- kubectl create namespace <ns-name>
- kubectl get namespaces                 # List all namespaces
- kubectl get pods -n <ns-name>          # Get pods in a specific namespace
- kubectl get all -n <ns-name>           # Get all resources in a namespace

# Resource Inspection
Get commands
- kubectl get pods [-o wide|yaml|json]   # List pods (with extended info)
- kubectl get deployments               # List deployments
- kubectl get services                  # List services
- kubectl get statefulsets              # List statefulsets
- kubectl get daemonsets                # List daemonsets
- kubectl get ingress                   # List ingress resources
- kubectl get pv                        # List persistent volumes
- kubectl get pvc                       # List persistent volume claims
- kubectl get secrets                   # List secrets
- kubectl get configmaps                # List configmaps
- kubectl get endpoints                 # List endpoints

# Watch resources
- kubectl get pods --watch              # Real-time updates
- kubectl get pods -w -l app=<label>    # Watch specific labeled pods

# Detailed view
- kubectl describe pod <pod-name>       # Show pod details (events, config)
- kubectl describe svc <service-name>   # Describe service configuration

# Scaling & Updates
- kubectl scale deployment/<name> --replicas=<number>  # Scale deployment
- kubectl rollout restart deployment/<name>           # Rolling restart
- kubectl rollout status deployment/<name>           # Check rollout progress
- kubectl rollout history deployment/<name>          # View revision history
- kubectl rollout undo deployment/<name> --to-revision=<number>  # Rollback
- kubectl edit deployment/<name>                    # Edit live configuration

# Debugging & Logs
- kubectl logs <pod-name>               # View logs
- kubectl logs -f <pod-name>            # Follow logs in real-time
- kubectl logs --previous <pod-name>    # Logs from crashed/previous instance
- kubectl exec -it <pod-name> -- sh     # Start shell in pod
- kubectl top pod <pod-name>            # Resource usage (CPU/memory)
- kubectl top node                       # Node resource usage
- kubectl get events --sort-by=.metadata.creationTimestamp  # Recent events

# Networking & Connectivity
- kubectl port-forward <pod-name> <local-port>:<pod-port>  # Forward ports
- kubectl port-forward svc/<service> <local-port>:<service-port> # Forward service
- kubectl proxy                        # Create proxy to API server

Deletion & Cleanup
- kubectl delete pod <pod-name>         # Delete pod
- kubectl delete deployment <name>      # Delete deployment
- kubectl delete -f <file.yaml>         # Delete resources from YAML
- kubectl delete all --all             # Delete all resources in namespace
- kubectl delete pods --all            # Delete all pods
- kubectl delete pvc --all             # Delete all persistent volume claims

# Advanced Commands
- kubectl explain <resource>           # Documentation for a resource (e.g., `kubectl explain pod.spec`)
- kubectl auth can-i <verb> <resource> # Check permissions (e.g., `kubectl auth can-i delete pods`)
- kubectl diff -f <file.yaml>          # Show changes before applying
- kubectl get --raw /metrics           # View raw cluster metrics
- kubectl api-resources               # List all API resources

# YAML/Manifest Management
- kubectl get <resource> <name> -o yaml > file.yaml  # Export config
- kubectl apply --dry-run=client -f file.yaml        # Test without applying
- kubectl create <resource> <name> --dry-run=client -o yaml > file.yaml # Generate YAML

Troubleshooting Tips
--Use kubectl get events --field-selector type=Warning to filter errors

- Add -v=6 to any command to see API requests (e.g., kubectl get pods -v=6)

For stuck terminating pods: kubectl delete pod <name> --grace-period=0 --force

# Shortcuts & Aliases
alias k=kubectl
alias kgp='kubectl get pods'
alias kgs='kubectl get services'
alias kdp='kubectl describe pod'
Useful Flags for Most Commands
-A/--all-namespaces: All namespaces

-l app=<label>: Filter by label

--selector key=value: Advanced selector queries

-o wide|yaml|json|name: Output formats
