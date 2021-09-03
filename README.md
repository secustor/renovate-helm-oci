# helm-values-issue

`$ helm upgrade --install umbrella umbrella --debug --dry-run`

Output: App chart values take precedence and ports are set correctly -

```
MANIFEST:
---
# Source: umbrella/charts/app1/templates/service.yaml
apiVersion: v1
kind: Service
metadata:
  name: umbrella-app1
  labels:
    helm.sh/chart: app1-0.1.0
    app.kubernetes.io/name: app1
    app.kubernetes.io/instance: umbrella
    app.kubernetes.io/version: "1.16.0"
    app.kubernetes.io/managed-by: Helm
spec:
  type: ClusterIP
  ports:
    - port: 1234
      targetPort: http
      protocol: TCP
      name: http
  selector:
    app.kubernetes.io/name: app1
    app.kubernetes.io/instance: umbrella
---
# Source: umbrella/charts/app2/templates/service.yaml
apiVersion: v1
kind: Service
metadata:
  name: umbrella-app2
  labels:
    helm.sh/chart: app2-0.1.0
    app.kubernetes.io/name: app2
    app.kubernetes.io/instance: umbrella
    app.kubernetes.io/version: "1.16.0"
    app.kubernetes.io/managed-by: Helm
spec:
  type: ClusterIP
  ports:
    - port: 8080
      targetPort: http
      protocol: TCP
      name: http
  selector:
    app.kubernetes.io/name: app2
    app.kubernetes.io/instance: umbrella
```
    
    
`$ helm upgrade --install umbrella umbrella --debug --dry-run --values umbrella/values.yaml`

Output: Library chart values take precedence and port is set to library default 9090 (which seems like a bug to me)

```
MANIFEST:
---
# Source: umbrella/charts/app1/templates/service.yaml
apiVersion: v1
kind: Service
metadata:
  name: umbrella-app1
  labels:
    helm.sh/chart: app1-0.1.0
    app.kubernetes.io/name: app1
    app.kubernetes.io/instance: umbrella
    app.kubernetes.io/version: "1.16.0"
    app.kubernetes.io/managed-by: Helm
spec:
  type: ClusterIP
  ports:
    - port: 9090
      targetPort: http
      protocol: TCP
      name: http
  selector:
    app.kubernetes.io/name: app1
    app.kubernetes.io/instance: umbrella
---
# Source: umbrella/charts/app2/templates/service.yaml
apiVersion: v1
kind: Service
metadata:
  name: umbrella-app2
  labels:
    helm.sh/chart: app2-0.1.0
    app.kubernetes.io/name: app2
    app.kubernetes.io/instance: umbrella
    app.kubernetes.io/version: "1.16.0"
    app.kubernetes.io/managed-by: Helm
spec:
  type: ClusterIP
  ports:
    - port: 9090
      targetPort: http
      protocol: TCP
      name: http
  selector:
    app.kubernetes.io/name: app2
    app.kubernetes.io/instance: umbrella
```
