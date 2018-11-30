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
- `$ cat ./terraform.tfstate | jq -r '.modules[0].outputs.ops_manager_dns.value'`

  - http://`pcf.pcf.syanagihara.cf`

![](images/opsman-initial.png)
![](images/opsman-login.png)
![](images/opsman-bosh-before.png)

- `$ cat ./terraform.tfstate | jq -r '.modules[0].outputs.project.value'`

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

### Pivotal Application Service ダウンロード

#### Pivnet ID 特定
```
$ pivnet products |grep elastic-runtime

|  60 | elastic-runtime                            | Pivotal Application Service     |
``` 

```
$ pivnet releases -p elastic-runtime |grep 2.3

| 220833 | 2.3.3           | Please refer to the release    | 2018-11-28T05:35:33.257Z |
| 209723 | 2.3.2           | Please refer to the release    | 2018-11-28T05:35:32.999Z |
| 196729 | 2.3.1           | Please refer to the release    | 2018-11-28T05:35:32.806Z |
| 188503 | 2.3.0           | Please refer to the release    | 2018-11-28T05:35:32.767Z |
```

```
$ pivnet product-files -p elastic-runtime -r 2.3.3

+--------+--------------------------------+----------------+---------------------+------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
|   ID   |              NAME              |  FILE VERSION  |      FILE TYPE      |                              SHA256                              |                                       AWS OBJECT KEY                                        |
+--------+--------------------------------+----------------+---------------------+------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
| 258595 | AWS Terraform Templates 0.22.0 | 0.22.0         | Software            | b0f02d61697b3a611c389d8df2e2d68a346cddedd7768c5fcb6ba186442776e7 | product-files/elastic-runtime/terraforming-aws-0.22.0.zip                                   |
| 258621 | GCP Terraform Templates 0.35.0 | 0.35.0         | Software            | dd3fc39dd973bf0c3a3a0ed687165e5530a1b556f27e230aad8467c2a29602e2 | product-files/elastic-runtime/terraforming-gcp-0.35.0.zip                                   |
| 254227 | CF CLI 6.40.1                  | 6.40.1         | Software            | 712512381615cc2280b7163383785a6fffff45101abca79150bbc7325a942fd8 | product-files/elastic-runtime/cf-cli-6.40.1.zip                                             |
| 249929 | Azure Terraform Templates      | 0.15.1         | Software            | 7719b71f611cc795531a491513efa440d43ac6084ed0d70f61cb6f1e2ee7a446 | product-files/elastic-runtime/terraforming-azure-0.15.1.zip                                 |
|        | 0.15.1                         |                |                     |                                                                  |                                                                                             |
| 223838 | PCF Pivotal Application        |            2.3 | Open Source License |                                                                  | product-files/elastic-runtime/open_source_license_cf-2.3.0-build.264-719b0ec-1537805535.txt |
|        | Service v2.3 OSL               |                |                     |                                                                  |                                                                                             |
| 254473 | Small Footprint PAS            | 2.3.3-build.10 | Software            | 1ab242bff8f95598193b0c742b7d6a520628ebeb682fd949d18da5ef6c8e5c7a | product-files/elastic-runtime/srt-2.3.3-build.10.pivotal                                    |
| 254457 | Pivotal Application Service    | 2.3.3-build.10 | Software            | 5540900a3626b092bffdb01b530791a116cf5f1022fd1b048edaeea4424318fd | product-files/elastic-runtime/cf-2.3.3-build.10.pivotal                                     |
+--------+--------------------------------+----------------+---------------------+------------------------------------------------------------------+---------------------------------------------------------------------------------------------+
```

```
$ set -x ZONE asia-northeast1-b
```

```
$ gcloud compute ssh ubuntu@pcf-ops-manager \
    --zone $ZONE \
    --force-key-file-overwrite \
    --strict-host-key-checking=no \
    --quiet \
    --command "wget -O pivnet https://github.com/pivotal-cf/pivnet-cli/releases/download/v0.0.55/pivnet-linux-amd64-0.0.55 && chmod +x pivnet && sudo mv pivnet /usr/local/bin/"
```

```
$ gcloud compute ssh ubuntu@pcf-ops-manager \
    --zone $ZONE \
    --force-key-file-overwrite \
    --strict-host-key-checking=no \
    --quiet \
    --command "pivnet login --api-token=$REFRESH_TOKEN && pivnet accept-eula -p elastic-runtime -r 2.3.3 && pivnet download-product-files -p elastic-runtime -r 2.3.3 -i 254457"
```

```
$ gcloud compute ssh ubuntu@pcf-ops-manager \
    --zone $ZONE \
    --force-key-file-overwrite \
    --strict-host-key-checking=no \
    --quiet \
    --command "wget -O om https://github.com/pivotal-cf/om/releases/download/0.46.0/om-linux && chmod +x om && sudo mv om /usr/local/bin/"
```

```
$ gcloud compute ssh ubuntu@pcf-ops-manager \
    --zone $ZONE \
    --force-key-file-overwrite \
    --strict-host-key-checking=no \
    --quiet \
    --command "om --target https://localhost -k -u admin -p admin --request-timeout 3600 upload-product -p ~/cf-2.3.3-build.10.pivotal"
```

```
$ gcloud compute ssh ubuntu@$PKS_ENV_PREFIX-ops-manager \
    --zone $ZONE \
    --force-key-file-overwrite \
    --strict-host-key-checking=no \
    --quiet \
    --command "om --target https://localhost -k -u admin -p admin stage-product -p cf -v 2.3.3"
```
## まとめ / 振り返り
