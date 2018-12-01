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

![](images/pas-uploaded.png)

```
$ gcloud compute ssh ubuntu@pcf-ops-manager \
    --zone $ZONE \
    --force-key-file-overwrite \
    --strict-host-key-checking=no \
    --quiet \
    --command "om --target https://localhost -k -u admin -p admin stage-product -p cf -v 2.3.3"
```

![](images/pas-staged.png)

```
$ pivnet products|grep stemcells

| 233 | stemcells-ubuntu-xenial                    | Stemcells for PCF (Ubuntu       |
|  82 | stemcells                                  | Stemcells for PCF               |
| 151 | stemcells-windows-server                   | Stemcells for PCF (Windows)     |
```

```
$ pivnet releases -p stemcells-ubuntu-xenial

+--------+---------+--------------------------------+--------------------------+
|   ID   | VERSION |          DESCRIPTION           |        UPDATED AT        |
+--------+---------+--------------------------------+--------------------------+
| 235787 |   97.34 | Periodic Ubuntu Xenial         | 2018-11-19T23:44:09.164Z |
|        |         | stemcell bump (Nov 19, 2018)   |                          |
| 232696 |   97.33 | Includes updates to address:   | 2018-11-16T01:31:23.520Z |
|        |         |   * USN-3820-2: Linux kernel   |                          |
|        |         | (HWE) vulnerabilities          |                          |
| 226360 |   97.32 | Periodic Ubuntu Xenial         | 2018-11-08T02:31:14.948Z |
|        |         | stemcell bump (Nov 08, 2018)   |                          |
| 225315 |   97.31 | Periodic Ubuntu Xenial         | 2018-11-06T22:54:30.717Z |
|        |         | stemcell bump (Nov 05, 2018)   |                          |
| 214330 |   97.28 | Periodic Ubuntu Xenial         | 2018-10-23T19:56:15.733Z |
|        |         | stemcell bump (Oct 23, 2018)   |                          |
| 199678 |   97.19 | (Oct 02, 2018)                 | 2018-10-03T22:09:45.702Z |
| 194743 |   97.18 | Periodic Ubuntu Xenial         | 2018-09-26T22:41:20.570Z |
|        |         | stemcell bump (Sep 25, 2018)   |                          |
| 189465 |   97.17 | Fixes mounting persistent disk | 2018-09-19T21:35:05.161Z |
|        |         | issue with bosh-agent.         |                          |
| 183842 |   97.16 | Periodic Ubuntu Xenial         | 2018-09-12T18:09:59.841Z |
|        |         | stemcell bump (Sep 11, 2018)   |                          |
| 172283 |   97.15 | Bump Ubuntu Xenial stemcells   | 2018-08-28T22:39:34.575Z |
|        |         | for "USN-3756-1: Intel         |                          |
|        |         | Microcode vulnerabilities"     |                          |
| 162133 |   97.12 | Bump Ubuntu Xenial stemcells   | 2018-08-27T20:48:44.913Z |
|        |         | for "USN-3740-2: Linux kernel  |                          |
|        |         | (HWE) vulnerabilities"         |                          |
+--------+---------+--------------------------------+--------------------------+
```

```
$ pivnet product-files -p stemcells-ubuntu-xenial -r 97.34

+--------+--------------------------------+--------------+---------------------+------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+
|   ID   |              NAME              | FILE VERSION |      FILE TYPE      |                              SHA256                              |                                                 AWS OBJECT KEY                                                 |
+--------+--------------------------------+--------------+---------------------+------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+
| 266870 | Ubuntu Xenial Stemcell for     |        97.34 | Software            | e32f52084c3aea624bfd18959954529cab3505e4d30d1312d6055a13544851c9 | product-files/stemcells-ubuntu-xenial/bosh-stemcell-97.34-vsphere-esxi-ubuntu-xenial-go_agent.tgz              |
|        | vSphere 97.34                  |              |                     |                                                                  |                                                                                                                |
| 266869 | Ubuntu Xenial Stemcell for     |        97.34 | Software            | 3f503e044d92c115515ca51f106572cba4ee0e843600e410971820ad75d7954b | product-files/stemcells-ubuntu-xenial/bosh-stemcell-97.34-vcloud-esxi-ubuntu-xenial-go_agent.tgz               |
|        | vCloud 97.34                   |              |                     |                                                                  |                                                                                                                |
| 202813 | Ubuntu Xenial Stemcell 97.10   |        97.10 | Open Source License | f80d689702f0e7eb360dbe94c4bb7b0bcf1c6e80e15aa7b2fee0d2ce365cda6a | product-files/stemcells-ubuntu-xenial/open_source_license_stemcells-ubuntu-xenial-97.10-e68fd75-1535122432.txt |
|        | OSL                            |              |                     |                                                                  |                                                                                                                |
| 266868 | Ubuntu Xenial Stemcell for     |        97.34 | Software            | 60a3a17f2daf294cbe0b1f5bf71e378e4db5279aac0a96f5e5ee1c7e48e5ceae | product-files/stemcells-ubuntu-xenial/bosh-stemcell-97.34-openstack-kvm-ubuntu-xenial-go_agent-raw.tgz         |
|        | Openstack 97.34                |              |                     |                                                                  |                                                                                                                |
| 266866 | Ubuntu Xenial Stemcell for     |        97.34 | Software            | e0c754ef7ea9de659b041f572b9a2bdc618a94affcf96d4d07713df7b948c991 | product-files/stemcells-ubuntu-xenial/light-bosh-stemcell-97.34-google-kvm-ubuntu-xenial-go_agent.tgz          |
|        | Google Cloud Platform 97.34    |              |                     |                                                                  |                                                                                                                |
| 266865 | Ubuntu Xenial Stemcell for     |        97.34 | Software            | ec73def9841147158e4f02ca3e950a9782428c8f2dd7bba364138450b3504db5 | product-files/stemcells-ubuntu-xenial/bosh-stemcell-97.34-azure-hyperv-ubuntu-xenial-go_agent.tgz              |
|        | Azure 97.34                    |              |                     |                                                                  |                                                                                                                |
| 266863 | Ubuntu Xenial Stemcell for AWS |        97.34 | Software            | 9ed65b6e81baa80ecf0d7cea1ed75241702c01f8bdf350128106352714f90f29 | product-files/stemcells-ubuntu-xenial/light-bosh-stemcell-97.34-aws-xen-hvm-ubuntu-xenial-go_agent.tgz         |
|        |                          97.34 |              |                     |                                                                  |                                                                                                                |
+--------+--------------------------------+--------------+---------------------+------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+
```

```
$ gcloud compute ssh ubuntu@pcf-ops-manager \
    --zone $ZONE \
    --force-key-file-overwrite \
    --strict-host-key-checking=no \
    --quiet \
    --command "pivnet login --api-token=$REFRESH_TOKEN && pivnet accept-eula -p stemcells-ubuntu-xenial -r 97.34 && pivnet download-product-files -p stemcells-ubuntu-xenial -r 97.34 -i 266866"
```

```
$ gcloud compute ssh ubuntu@pcf-ops-manager \
    --zone $ZONE \
    --force-key-file-overwrite \
    --strict-host-key-checking=no \
    --quiet \
    --command "ls -l"

total 13553488
-rw-rw-r-- 1 ubuntu ubuntu 13878740011 Nov 30 13:02 cf-2.3.3-build.10.pivotal
-rw-rw-r-- 1 ubuntu ubuntu       20349 Dec  1 00:48 light-bosh-stemcell-97.34-google-kvm-ubuntu-xenial-go_agent.tgz
```

```
$ gcloud compute ssh ubuntu@pcf-ops-manager \
    --zone $ZONE \
    --force-key-file-overwrite \
    --strict-host-key-checking=no \
    --quiet \
    --command "om --target https://localhost -k -u admin -p admin --request-timeout 3600 upload-stemcell -s ~/light-bosh-stemcell-97.34-google-kvm-ubuntu-xenial-go_agent.tgz"
```

![](images/pas-stemcell.png)

### Pivotal Application Service 設定

![](images/pas-az-nw.png)

![](images/pas-domain.png)

![](images/pas-cert-gen.png)

![](images/pas-nw1.png)
![](images/pas-nw2.png)
![](images/pas-nw3.png)
![](images/pas-nw4.png)
![](images/pas-nw5.png)
![](images/pas-nw6.png)
![](images/pas-nw7.png)
![](images/pas-nw8.png)


## まとめ / 振り返り
