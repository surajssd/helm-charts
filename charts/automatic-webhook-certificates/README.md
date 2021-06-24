# Automatic Cert Generation

Use this chart to automatically generate certificates for your webhook server or dynamic admission controller. This chart is based on the application [`kube-webhook-certgen`](https://github.com/jet/kube-webhook-certgen).

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

## Usage as sub-chart

You can use this chart as a part of your application. Make the following changes in your helm chart.

### Add dependencies

Include the following snippet in the `Chart.yaml` file of your chart:

```yaml
dependencies:
- name: automatic-webhook-certificates
  version: "0.1.1"
  repository: "https://suraj.io/helm-charts"
```

### Configuration

Include the following snippet in the `values.yaml` file of your chart:

```yaml
automatic-webhook-certificates:
  webhook:
    name: <name of the webhook config>
    service: <name of the service serving the webhook pod>
    secret: <secret you wish to have certificates stored>
    failurePolicy: Fail or Ignore
    validating: true or false
    mutating: true or false
  psp: true or false
```

### Details on the certificates

The secret will be created by the application in this chart. It will be stored in the secret that you mention in `webhook.secret`. The secret keys are `ca`, `cert` and `key`.
