# 環境削除
- `terraform destroy`

## 概要 / 説明

## 前提 / 環境

## 手順 / 解説
### リソース確認

- `$ terraform plan -destroy`

<details><summary>例</summary>

```
Refreshing Terraform state in-memory prior to plan...
The refreshed state will be used to calculate this plan, but will not be
persisted to local or remote state storage.

tls_private_key.ops-manager: Refreshing state... (ID: b906f8b5c6b1f7e158a65522036d87ce41ad63cd)
google_storage_bucket.resources: Refreshing state... (ID: pa-syanagihara-pcf-resources)
google_compute_address.cf_ws: Refreshing state... (ID: pa-syanagihara/asia-northeast1/pcf-cf-ws)
google_service_account.blobstore_service_account: Refreshing state... (ID: projects/pa-syanagihara/serviceAccounts...pa-syanagihara.iam.gserviceaccount.com)
google_compute_address.cf-ssh: Refreshing state... (ID: pa-syanagihara/asia-northeast1/pcf-cf-ssh)
google_compute_address.ops-manager-ip: Refreshing state... (ID: pa-syanagihara/asia-northeast1/pcf-ops-manager-ip)
google_compute_image.ops-manager-image: Refreshing state... (ID: pcf-ops-manager-image)
google_compute_http_health_check.cf_public: Refreshing state... (ID: pcf-cf-public)
google_compute_global_address.cf: Refreshing state... (ID: pcf-cf)
google_dns_managed_zone.default: Refreshing state... (ID: pcf-zone)
google_storage_bucket.droplets: Refreshing state... (ID: pa-syanagihara-pcf-droplets)
google_compute_target_pool.cf-ssh: Refreshing state... (ID: pcf-cf-ssh)
google_service_account.opsman_service_account: Refreshing state... (ID: projects/pa-syanagihara/serviceAccounts...pa-syanagihara.iam.gserviceaccount.com)
google_compute_address.cf-tcp: Refreshing state... (ID: pa-syanagihara/asia-northeast1/pcf-cf-tcp)
google_storage_bucket.packages: Refreshing state... (ID: pa-syanagihara-pcf-packages)
google_compute_http_health_check.cf-tcp: Refreshing state... (ID: pcf-cf-tcp)
google_compute_network.pcf: Refreshing state... (ID: pcf-pcf-network)
google_compute_instance_group.httplb[0]: Refreshing state... (ID: asia-northeast1-a/pcf-httpslb-asia-northeast1-a)
google_compute_instance_group.httplb[1]: Refreshing state... (ID: asia-northeast1-b/pcf-httpslb-asia-northeast1-b)
google_compute_instance_group.httplb[2]: Refreshing state... (ID: asia-northeast1-c/pcf-httpslb-asia-northeast1-c)
google_storage_bucket.buildpacks: Refreshing state... (ID: pa-syanagihara-pcf-buildpacks)
google_compute_ssl_certificate.certificate: Refreshing state... (ID: pcf-pas-lbcert20181130055117169600000001)
google_compute_target_pool.cf_ws: Refreshing state... (ID: pcf-cf-ws)
google_compute_forwarding_rule.cf-ssh: Refreshing state... (ID: pcf-cf-ssh)
google_compute_subnetwork.infrastructure: Refreshing state... (ID: asia-northeast1/pcf-infrastructure-subnet)
google_compute_firewall.pcf-internal: Refreshing state... (ID: pcf-pcf-internal)
google_compute_target_pool.cf-tcp: Refreshing state... (ID: pcf-cf-tcp)
google_compute_forwarding_rule.cf-ws-https: Refreshing state... (ID: pcf-cf-ws-https)
google_compute_forwarding_rule.cf-ws-http: Refreshing state... (ID: pcf-cf-ws-http)
google_compute_firewall.ops-manager-external: Refreshing state... (ID: pcf-ops-manager-external)
google_compute_firewall.cf-ssh: Refreshing state... (ID: pcf-cf-ssh)
google_compute_firewall.cf-tcp: Refreshing state... (ID: pcf-cf-tcp)
google_compute_subnetwork.pas: Refreshing state... (ID: asia-northeast1/pcf-pas-subnet)
google_compute_subnetwork.services: Refreshing state... (ID: asia-northeast1/pcf-services-subnet)
google_compute_firewall.cf-health_check: Refreshing state... (ID: pcf-cf-health-check)
google_compute_firewall.cf_public: Refreshing state... (ID: pcf-cf-public)
google_project_iam_member.blobstore_cloud_storage_admin: Refreshing state... (ID: pa-syanagihara/roles/storage.objectAdmi...pa-syanagihara.iam.gserviceaccount.com)
google_service_account_key.blobstore_service_account_key: Refreshing state... (ID: projects/pa-syanagihara/serviceAccounts...3a7f5222328f365e9e5c186e4e958f3901e94d)
google_project_iam_member.opsman_iam_service_account_actor: Refreshing state... (ID: pa-syanagihara/roles/iam.serviceAccount...pa-syanagihara.iam.gserviceaccount.com)
google_project_iam_member.opsman_compute_network_admin: Refreshing state... (ID: pa-syanagihara/roles/compute.networkAdm...pa-syanagihara.iam.gserviceaccount.com)
google_project_iam_member.opsman_compute_storage_admin: Refreshing state... (ID: pa-syanagihara/roles/compute.storageAdm...pa-syanagihara.iam.gserviceaccount.com)
google_project_iam_member.opsman_storage_admin: Refreshing state... (ID: pa-syanagihara/roles/storage.admin/serv...pa-syanagihara.iam.gserviceaccount.com)
google_project_iam_member.opsman_compute_instance_admin: Refreshing state... (ID: pa-syanagihara/roles/compute.instanceAd...pa-syanagihara.iam.gserviceaccount.com)
google_service_account_key.opsman_service_account_key: Refreshing state... (ID: projects/pa-syanagihara/serviceAccounts...a259ad31ed611322fd7a0d6c373297dc62939c)
google_compute_forwarding_rule.cf-tcp: Refreshing state... (ID: pcf-cf-tcp)
google_compute_backend_service.http_lb_backend_service: Refreshing state... (ID: pcf-httpslb)
google_compute_instance.ops-manager: Refreshing state... (ID: pcf-ops-manager)
google_dns_record_set.ops-manager-dns: Refreshing state... (ID: pcf-zone/pcf.pcf.syanagihara.cf./A)
google_compute_url_map.https_lb_url_map: Refreshing state... (ID: pcf-cf-http)
google_dns_record_set.app-ssh-dns: Refreshing state... (ID: pcf-zone/ssh.sys.pcf.syanagihara.cf./A)
google_dns_record_set.wildcard-sys-dns: Refreshing state... (ID: pcf-zone/*.sys.pcf.syanagihara.cf./A)
google_dns_record_set.wildcard-ws-dns: Refreshing state... (ID: pcf-zone/*.ws.pcf.syanagihara.cf./A)
google_dns_record_set.tcp-dns: Refreshing state... (ID: pcf-zone/tcp.pcf.syanagihara.cf./A)
google_dns_record_set.doppler-sys-dns: Refreshing state... (ID: pcf-zone/doppler.sys.pcf.syanagihara.cf./A)
google_dns_record_set.loggregator-sys-dns: Refreshing state... (ID: pcf-zone/loggregator.sys.pcf.syanagihara.cf./A)
google_dns_record_set.wildcard-apps-dns: Refreshing state... (ID: pcf-zone/*.apps.pcf.syanagihara.cf./A)
google_compute_target_http_proxy.http_lb_proxy: Refreshing state... (ID: pcf-httpproxy)
google_compute_target_https_proxy.https_lb_proxy: Refreshing state... (ID: pcf-httpsproxy)
google_compute_global_forwarding_rule.cf_http: Refreshing state... (ID: pcf-cf-lb-http)
google_compute_global_forwarding_rule.cf_https: Refreshing state... (ID: pcf-cf-lb-https)

------------------------------------------------------------------------

An execution plan has been generated and is shown below.
Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  - module.infra.google_compute_firewall.pcf-internal

  - module.infra.google_compute_network.pcf

  - module.infra.google_compute_subnetwork.infrastructure

  - module.infra.google_dns_managed_zone.default

  - module.infra.google_project_iam_member.blobstore_cloud_storage_admin

  - module.infra.google_service_account.blobstore_service_account

  - module.infra.google_service_account_key.blobstore_service_account_key

  - module.ops_manager.google_compute_address.ops-manager-ip

  - module.ops_manager.google_compute_firewall.ops-manager-external

  - module.ops_manager.google_compute_image.ops-manager-image

  - module.ops_manager.google_compute_instance.ops-manager

  - module.ops_manager.google_dns_record_set.ops-manager-dns

  - module.ops_manager.google_project_iam_member.opsman_compute_instance_admin

  - module.ops_manager.google_project_iam_member.opsman_compute_network_admin

  - module.ops_manager.google_project_iam_member.opsman_compute_storage_admin

  - module.ops_manager.google_project_iam_member.opsman_iam_service_account_actor

  - module.ops_manager.google_project_iam_member.opsman_storage_admin

  - module.ops_manager.google_service_account.opsman_service_account

  - module.ops_manager.google_service_account_key.opsman_service_account_key

  - module.ops_manager.tls_private_key.ops-manager

  - module.pas.google_compute_address.cf-ssh

  - module.pas.google_compute_address.cf-tcp

  - module.pas.google_compute_address.cf_ws

  - module.pas.google_compute_backend_service.http_lb_backend_service

  - module.pas.google_compute_firewall.cf-health_check

  - module.pas.google_compute_firewall.cf-ssh

  - module.pas.google_compute_firewall.cf-tcp

  - module.pas.google_compute_firewall.cf_public

  - module.pas.google_compute_forwarding_rule.cf-ssh

  - module.pas.google_compute_forwarding_rule.cf-tcp

  - module.pas.google_compute_forwarding_rule.cf-ws-http

  - module.pas.google_compute_forwarding_rule.cf-ws-https

  - module.pas.google_compute_global_address.cf

  - module.pas.google_compute_global_forwarding_rule.cf_http

  - module.pas.google_compute_global_forwarding_rule.cf_https

  - module.pas.google_compute_http_health_check.cf-tcp

  - module.pas.google_compute_http_health_check.cf_public

  - module.pas.google_compute_instance_group.httplb[0]

  - module.pas.google_compute_instance_group.httplb[1]

  - module.pas.google_compute_instance_group.httplb[2]

  - module.pas.google_compute_subnetwork.pas

  - module.pas.google_compute_subnetwork.services

  - module.pas.google_compute_target_http_proxy.http_lb_proxy

  - module.pas.google_compute_target_https_proxy.https_lb_proxy

  - module.pas.google_compute_target_pool.cf-ssh

  - module.pas.google_compute_target_pool.cf-tcp

  - module.pas.google_compute_target_pool.cf_ws

  - module.pas.google_compute_url_map.https_lb_url_map

  - module.pas.google_dns_record_set.app-ssh-dns

  - module.pas.google_dns_record_set.doppler-sys-dns

  - module.pas.google_dns_record_set.loggregator-sys-dns

  - module.pas.google_dns_record_set.tcp-dns

  - module.pas.google_dns_record_set.wildcard-apps-dns

  - module.pas.google_dns_record_set.wildcard-sys-dns

  - module.pas.google_dns_record_set.wildcard-ws-dns

  - module.pas.google_storage_bucket.buildpacks

  - module.pas.google_storage_bucket.droplets

  - module.pas.google_storage_bucket.packages

  - module.pas.google_storage_bucket.resources

  - module.pas_certs.google_compute_ssl_certificate.certificate


Plan: 0 to add, 0 to change, 60 to destroy.

------------------------------------------------------------------------

Note: You didn't specify an "-out" parameter to save this plan, so Terraform
can't guarantee that exactly these actions will be performed if
"terraform apply" is subsequently run.

```
</details>

### リソース削除
- `$ terraform destroy`

#### GCP コンソールより削除
1. VM Instance
2. VPC Network - Subnet
3. VPC Network
4. Disks