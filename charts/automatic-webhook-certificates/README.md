# Automatic Cert Generation

Use this chart to automatically generate certificates for your webhook.

## Install

```
helm repo add suraj-helm-charts https://suraj.io/helm-charts
helm install --name automatic-webhook-certificates suraj-helm-charts/automatic-webhook-certificates
```

## Configuration reference

| Parameter             | Description                                                     | Type                                                                 | Optional | Default                        |
|-----------------------|-----------------------------------------------------------------|----------------------------------------------------------------------|----------|--------------------------------|
| application.image     | Container image location.                                       | `string`                                                             | true     | `jettech/kube-webhook-certgen` |
| webhook.name          | Name of the webhook for which to create certificates.           | `string`                                                             | false    | -                              |
| webhook.service       | Service that is serving the webhook.                            | `string`                                                             | false    | -                              |
| webhook.secret        | Name of the secret that will store the certificates.            | `string`                                                             | true     | `webhooksecret`                |
| webhook.failurePolicy | Failure policy to use for the webhook configuration.            | `string` (Fail or Ignore)                                            | true     | `Fail`                         |
| webhook.validating    | Is the webhook validating?                                      | `bool`                                                               | true     | `true`                         |
| webhook.mutating      | Is the webhook mutating?                                        | `bool`                                                               | true     | `false`                        |
| logLevel              | Log level of the job that will patch the webhook configuration. | `string` (panic or fatal or error or warn or info or debug or trace) | true     | `info`                         |
| psp                   | Install PSP configuration?                                      | `bool`                                                               | true     | `true`                         |
