# ArgeepCD

## Sealed Secrets

Sealed Secrets is a tool for encrypting Kubernetes secrets into a format that can be safely stored in Git repositories. It allows you to manage sensitive information, such as passwords and API keys, without exposing them in your source code. Sealed Secrets uses a public/private key pair to encrypt and decrypt secrets, ensuring that only authorized users can access the sensitive data.

### Usage

To use Sealed Secrets, you need to install the `kubeseal` CLI tool and have the correct kubernetes cluster configured. The basic workflow involves creating a Kubernetes Secret, sealing it with `kubeseal`, and then applying the sealed secret to your cluster.

1. Install `kubeseal` CLI tool: [Documentation](https://github.com/bitnami-labs/sealed-secrets?tab=readme-ov-file#kubeseal)
2. Create a Kubernetes Secret manifest file (e.g., `my-secret.yaml`):
    ```yaml
    apiVersion: v1
    kind: Secret
    metadata:
      name: my-secret
      namespace: my-namespace
    type: Opaque
    data:
      username: <base64-encoded-username>
      password: <base64-encoded-password>
    ```
3. Seal the secret using `kubeseal`:
    ```bash
    kubeseal --controller-name=sealed-secrets-controller --controller-namespace=kube-system --format yaml < my-secret.yaml > my-sealed-secret.yaml
    ```
4. Update the sealed secret manifest file in `sealed-secrets/<environment>/` directory. **Attention**: Be carful to update the correct namespace.