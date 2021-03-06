## Provider

Provider configuration currently carries kapp kubeconfig.

### Input Attributes

- `kapp` (optional) Required if kapp resource is used
  - `kubeconfig` (optional) Required if kapp resource is used
    - `from_env` (bool; optional; default=false) Use kubeconfig from the environment (e.g. `~/.kube/config` or `KUBECONFIG`, etc.)
    - `context` (string; optional) Context name. Only applies to `env` configuration.
    - `server` (string; optional) Required if `from_env` is not used. Specifies API server URL.
    - `username` (string; optional) Username
    - `password` (string; optional) Password
    - `ca_cert` (string; optional) CA certificate in PEM format (multiline strings are indent-trimmed)
    - `client_cert` (string; optional) Client certificate in PEM format (multiline strings are indent-trimmed)
    - `client_key` (string; optional) Client key in PEM format (multiline strings are indent-trimmed)
    - `token` (string; optional) Authentication token
  - `kubeconfig_yaml` (optional) Kubeconfig as YAML (multiline strings are indent-trimmed)

### Example

```yaml
provider "k14s" {}
```

Use configuration used by kubectl:

```yaml
provider "k14s" {
  kapp {
    kubeconfig {
      from_env = true
    }
  }
}
```

Use specific context with environment config:

```yaml
provider "k14s" {
  kapp {
    kubeconfig {
      from_env = true
      context = "prod-ctx"
    }
  }
}
```

Authenticate with username and password:

```yaml
provider "k14s" {
  kapp {
    kubeconfig {
      server = "https://..."
      ca_cert = <<EOF
        -----BEGIN CERTIFICATE-----
        MIIDCzCCAfOgAwIBAgIQAkwp/felW4+kYeaI0LwmezANBgkqhkiG9w0BAQsFADAv
        ...
        NPB7dNDuLFmCvKX9Anhr
        -----END CERTIFICATE-----
      EOF
      username = "admin"
      password = "supersecret..."
    }
  }
}
```

Authenticate with client certificate:

```yaml
provider "k14s" {
  kapp {
    kubeconfig {
      server = "https://..."
      ca_cert = <<EOF
        -----BEGIN CERTIFICATE-----
        MIIDCzCCAfOgAwIBAgIQAkwp/felW4+kYeaI0LwmezANBgkqhkiG9w0BAQsFADAv
        ...
        NPB7dNDuLFmCvKX9Anhr
        -----END CERTIFICATE-----
      EOF
      client_cert = "-----BEGIN CERTIFICATE-----\n..."
      client_key = "-----BEGIN PRIVATE KEY-----\n..."
    }
  }
}
```

Authenticate with token:

```yaml
provider "k14s" {
  kapp {
    kubeconfig {
      server = "https://..."
      ca_cert = <<EOF
        -----BEGIN CERTIFICATE-----
        MIIDCzCCAfOgAwIBAgIQAkwp/felW4+kYeaI0LwmezANBgkqhkiG9w0BAQsFADAv
        ...
        NPB7dNDuLFmCvKX9Anhr
        -----END CERTIFICATE-----
      EOF
      token = "IBAgIQAkwp..."
    }
  }
}
```
