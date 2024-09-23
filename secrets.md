## how to use secrets in EKS or GKS for applications to access them in their environment.
<br>
Applications running in EKS often need access to sensitive data such as database credentials, API keys, or tokens. Secrets can be stored in two primary ways:
<br>
<b>Kubernetes Secrets:</b> A built-in Kubernetes object designed to store and manage sensitive information.<br>
<b>
  AWS Secrets Manager:
</b> A fully managed service to securely store and retrieve secrets, with automatic rotation and fine-grained access control.<br>
<br>
### Using Kubernetes Secrets
Kubernetes Secrets can be created directly from literal values or from files. Here’s how to create a secret for a database password<br>
To access the secret in a container as an environment variable, modify the Pod’s (or Deployment’s) manifest<br>

```
apiVersion: v1
kind: Pod
metadata:
  name: my-app
spec:
  containers:
    - name: app-container
      image: my-app-image
      env:
        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: db-secret  # Name of the secret
              key: DB_PASSWORD  # Key within the secret

```
or Alternatively, the secret can be mounted as a file inside the container:

