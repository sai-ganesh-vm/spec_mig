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

```
apiVersion: v1
kind: Pod
metadata:
  name: my-app
spec:
  containers:
    - name: app-container
      image: my-app-image
      volumeMounts:
        - name: secret-volume
          mountPath: "/etc/secrets"
          readOnly: true
    volumes:
      - name: secret-volume
        secret:
          secretName: db-secret

```
<br>

### aws secret Manager
For enhanced security, you can store secrets in AWS Secrets Manager and access them inside your Kubernetes Pods. This requires the setup of IAM Roles for Service Accounts (IRSA), allowing your pods to authenticate with AWS and fetch secrets.<br>

you can store secrets in AWS Secrets Manager via the AWS Console<br>
To allow your Kubernetes Pods to access AWS Secrets Manager, you need to create an IAM role and associate it with a Kubernetes Service Account.<br>
Step 1: Create IAM Policy<br>
Create a policy that allows access to your secret in AWS Secrets Manager:<br>
You can access AWS Secrets Manager directly in your application using AWS SDKs, or you can inject the secret as an environment variable by fetching it using an init container or sidecar container.<br>
```
import boto3

def get_secret():
    client = boto3.client('secretsmanager')
    secret_name = "my-db-secret"
    
    response = client.get_secret_value(SecretId=secret_name)
    
    return response['SecretString']

```
