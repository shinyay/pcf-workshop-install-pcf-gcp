# Pivotal Cloud Foundry インストレーション

## 概要 / 説明

## 前提 / 環境

## 手順 / 解説
### Terraform
#### terraform.tfvars
```
env_name         = "YOUR-ENVIRONMENT-NAME"
opsman_image_url = "YOUR-OPS-MAN-IMAGE-URL"
region           = "YOUR-GCP-REGION"
zones            = ["YOUR-AZ-1", "YOUR-AZ-2", "YOUR-AZ-3"]
project          = "YOUR-GCP-PROJECT"
dns_suffix       = "YOUR-DNS-SUFFIX"

ssl_cert = <<SSL_CERT
-----BEGIN CERTIFICATE-----
YOUR-CERTIFICATE
-----END CERTIFICATE-----
SSL_CERT

ssl_private_key = <<SSL_KEY
-----BEGIN EXAMPLE RSA PRIVATE KEY-----
YOUR-PRIVATE-KEY
-----END EXAMPLE RSA PRIVATE KEY-----
SSL_KEY

service_account_key = <<SERVICE_ACCOUNT_KEY
YOUR-KEY-JSON
SERVICE_ACCOUNT_KEY
```

#### Terraform 実行
```
```

### OpsManager
#### OpsManager アクセス
- `$ terraform output|grep ops_manager_dns`

```
ops_manager_dns = pcf.pcf.syanagihara.cf
```

![](images/opsman-initial.png)
![](images/opsman-login.png)
![](images/opsman-bosh-before.png)

- `$ terraform output|grep project`

![](images/bosh-google-config.png)

![](images/bosh-director-config1.png)
![](images/bosh-director-config2.png)
![](images/bosh-director-config3.png)
![](images/bosh-director-config4.png)
![](images/bosh-director-config5.png)
![](images/bosh-director-config6.png)

- `$ cat ./terraform.tfstate | jq -r '.modules[0].outputs.azs.value'`

![](images/bosh-az.png)

- `$ cat ./terraform.tfstate | jq -r '.modules[0].outputs.network_name.value'`

- `$ cat ./terraform.tfstate | jq -r '.modules[0].outputs.management_subnet_name.value'`

- `$ cat ./terraform.tfstate | jq -r '.modules[0].outputs.region.value'`

- `$ cat ./terraform.tfstate | jq -r '.modules[0].outputs.management_subnet_cidrs.value'`

- `$ cat ./terraform.tfstate | jq -r '.modules[0].outputs.management_subnet_gateway.value'`

- `$ cat ./terraform.tfstate | jq -r '.modules[0].outputs.pas_subnet_name.value'`

- `$ cat ./terraform.tfstate | jq -r '.modules[0].outputs.pas_subnet_cidrs.value'`

- `$ cat ./terraform.tfstate | jq -r '.modules[0].outputs.pas_subnet_gateway.value'`

- `$ cat ./terraform.tfstate | jq -r '.modules[0].outputs.services_subnet_name.value'`

- `$ cat ./terraform.tfstate | jq -r '.modules[0].outputs.services_subnet_cidrs.value'`

- `$ cat ./terraform.tfstate | jq -r '.modules[0].outputs.services_subnet_gateway.value'`

![](images/bosh-network1.png)
![](images/bosh-network2.png)
![](images/bosh-network3.png)

![](images/bosh-az-nw.png)

![](images/bosh-security.png)

![](images/bosh-syslog.png)

![](images/bosh-resource.png)

![](images/bosh-apply.png)

## まとめ / 振り返り
