# BOSH 操作

## Ops Manager へログイン

```
$ gcloud compute ssh ubuntu@pcf-ops-manager --zone $ZONE
```

## BOSH Director ローカルエイリアス

- `bosh2 alias-env MY-ENV -e DIRECTOR-IP-ADDRESS --ca-cert /var/tempest/workspaces/default/root_ca_certificate`


<details><summary>例</summary>

```
$ bosh alias-env gcp -e 10.0.0.10 --ca-cert

/var/tempest/workspaces/default/root_ca_certificate
Using environment '10.0.0.10' as anonymous user

Name      p-bosh
UUID      15401a41-f686-4713-8540-d93d06c4174c
Version   266.6.0 (00000000)
CPI       google_cpi
Features  compiled_package_cache: disabled
          config_server: enabled
          dns: disabled
          snapshots: disabled
User      (not logged in)

Succeeded
```
</details>

## BOSH Director へログイン
BOSH Director のログインパスワードは Ops Manager の Credentials 画面から確認　
![](images/bosh-pwd.png)


- `bosh2 -e MY-ENV log-in`

<details><summary>例</summary>

```
$ bosh2 -e gcp log-in

Using environment '10.0.0.10'

Email (): director
Password ():

Successfully authenticated with UAA

Succeeded
```
</details>

## BOSH 環境一覧

- `$ bosh2 -e <MY-ENV> environments`

<details><summary>例</summary>

```
$ bosh2 -e gcp environments

URL        Alias
10.0.0.10  gcp

1 environments

Succeeded
```
</details>

## デプロイメント表示

- `$ bosh2 -e <MY-ENV> deployments`

<details><summary>例</summary>

```
$ bosh2 -e gcp deployments

Using environment '10.0.0.10' as user 'director' (bosh.*.read, openid, bosh.*.admin, bosh.read, bosh.admin)

Name                     Release(s)                               Stemcell(s)                                     Team(s)  Cloud Config
cf-e5e5d0d42a09e353221f  backup-and-restore-sdk/1.7.1             bosh-google-kvm-ubuntu-trusty-go_agent/3586.57  -        latest
                         binary-offline-buildpack-lts/1.0.27
                         bosh-dns/1.6.0
                         bosh-dns-aliases/0.0.2
                         bosh-system-metrics-forwarder/0.0.15
                         capi/1.58.8
                         cf-autoscaling/201.9
                         cf-backup-and-restore/0.0.11
                         cf-cli/1.5.0
                         cf-mysql/36.16.0
                         cf-networking/2.3.3
                         cf-smoke-tests/40.0.17
                         cf-syslog-drain/6.6
                         cflinuxfs2/1.249.0
                         consul/195
                         credhub/1.9.3
                         diego/2.8.4
                         dotnet-core-offline-buildpack-lts/2.1.5
                         garden-runc/1.16.1
                         go-offline-buildpack-lts/1.8.28
                         haproxy/8.7.0
                         java-offline-buildpack-lts/4.16.1
                         log-cache/1.4.7
                         loggregator/102.7
                         mysql-monitoring/8.20.0
                         nats/24
                         nfs-volume/1.2.6
                         nodejs-offline-buildpack-lts/1.6.32
                         notifications/46
                         notifications-ui/33
                         php-offline-buildpack-lts/4.3.61
                         pivotal-account/1.9.1
                         push-apps-manager-release/665.0.22
                         push-usage-service-release/666.0.12
                         pxc/0.14.0
                         python-offline-buildpack-lts/1.6.21
                         routing/0.178.4
                         ruby-offline-buildpack-lts/1.7.24
                         silk/2.3.3
                         staticfile-offline-buildpack-lts/1.4.32
                         statsd-injector/1.3.0
                         syslog/11.3.2
                         uaa/60.8

1 deployments

Succeeded
```
</details>

## インスタンス一覧

- `bosh -e MY-ENV -d MY-DEPLOYMENT instances`

<details><summary>例</summary>

```
$ bosh2 -e gcp -d cf-e5e5d0d42a09e353221f instances

Using environment '10.0.0.10' as user 'director' (bosh.*.read, openid, bosh.*.admin, bosh.read, bosh.admin)

Task 291. Done

Deployment 'cf-e5e5d0d42a09e353221f'

Instance                                                            Process State  AZ                 IPs
backup-prepare/c13b1360-cc19-4dfd-8fd2-2b1414a0f941                 running        asia-northeast1-a  10.0.4.15
clock_global/253bcd17-2072-42fe-a995-2b6a0edec618                   running        asia-northeast1-a  10.0.4.24
cloud_controller/b1b47596-2115-4766-be9b-1792b72f70cb               running        asia-northeast1-a  10.0.4.20
cloud_controller_worker/ab8b235b-76fa-4f08-84ec-63f1a986b4af        running        asia-northeast1-a  10.0.4.25
consul_server/c29e3b98-8390-4572-b5ae-42ab3c506fdc                  running        asia-northeast1-a  10.0.4.10
diego_brain/03de574a-47c5-4268-930b-b2e3e8f45eed                    running        asia-northeast1-c  10.0.4.28
diego_brain/1a46f9ef-e782-4d3e-b4f0-bbd72f4c6813                    running        asia-northeast1-b  10.0.4.27
diego_brain/7ba5a505-e252-4258-8c5a-09662d09f14d                    running        asia-northeast1-a  10.0.4.26
diego_cell/7dd300e1-4c88-48e1-98fd-3dcc808e4cd1                     running        asia-northeast1-c  10.0.4.31
diego_cell/ea7ae884-73ec-4cab-832e-40fdbcd308d4                     running        asia-northeast1-a  10.0.4.29
diego_cell/f92368ec-22d9-4338-967a-45f056ef5ef8                     running        asia-northeast1-b  10.0.4.30
diego_database/1f3a0941-c8d5-4051-89f8-4d996ae04aa1                 running        asia-northeast1-b  10.0.4.17
diego_database/54f8621f-3432-48bf-8364-6c771853866b                 running        asia-northeast1-a  10.0.4.16
diego_database/63afb24f-308b-4e9f-95f6-8105db7efdd7                 running        asia-northeast1-c  10.0.4.18
doppler/07d166b3-5a2d-48b0-b439-4115e1156ef8                        running        asia-northeast1-a  10.0.4.35
loggregator_trafficcontroller/d38c9933-3460-4164-9a9a-a1719ab13160  running        asia-northeast1-a  10.0.4.32
mysql/6cb67341-55f0-4d0f-b28a-def0fddf5e31                          running        asia-northeast1-a  10.0.4.14
mysql_monitor/24d57953-a9aa-497e-ba82-918e69fe9dd3                  running        asia-northeast1-a  10.0.4.23
mysql_proxy/b262a4b6-a7e3-4eb1-95c7-badff4232dca                    running        asia-northeast1-a  10.0.4.13
nats/d7ccbef0-f1d9-4fb1-99e3-d5eeee174f67                           running        asia-northeast1-a  10.0.4.11
nfs_server/c78236a9-6159-486e-9623-8d060fdd4ace                     running        asia-northeast1-a  10.0.4.12
router/7f53b94d-0a27-4b85-a750-2ef19a21fc3f                         running        asia-northeast1-a  10.0.4.21
service-discovery-controller/628b0d77-9d9e-4894-be92-e97cf13de969   running        asia-northeast1-a  10.0.4.22
syslog_adapter/0cd4a59a-345f-42da-b1fa-e0d9409cfb73                 running        asia-northeast1-a  10.0.4.33
syslog_scheduler/b05df909-76d4-49c9-ba15-c7f7288772bc               running        asia-northeast1-a  10.0.4.34
uaa/7b7d28d6-1dd8-4fe9-8c8f-48040b5b90ff                            running        asia-northeast1-a  10.0.4.19

26 instances

Succeeded
```
</details>

## PAS 仮想マシンの全停止

- `bosh2 -e MY-ENV -d MY-DEPLOYMENT stop --hard`

<details><summary>例</summary>

```
$ bosh2 -e gcp -d cf-e5e5d0d42a09e353221f stop --hard

```
</details>

## PAS 仮想マシンの個別停止

- `bosh2 -e MY-ENV -d MY-DEPLOYMENT stop VM-NAME --hard`

<details><summary>例</summary>

```
$ bosh2 -e gcp -d cf-e5e5d0d42a09e353221f stop syslog_scheduler/b05df909-76d4-49c9-ba15-c7f7288772bc

Using environment '10.0.0.10' as user 'director' (bosh.*.read, openid, bosh.*.admin, bosh.read, bosh.admin)

Using deployment 'cf-e5e5d0d42a09e353221f'

Continue? [yN]: y

Task 292

Task 292 | 14:24:41 | Preparing deployment: Preparing deployment (00:00:03)
Task 292 | 14:26:54 | Preparing package compilation: Finding packages to compile (00:00:00)
Task 292 | 14:26:56 | Updating instance syslog_scheduler: syslog_scheduler/b05df909-76d4-49c9-ba15-c7f7288772bc (0) (canary) (00:00:11)

Task 292 Started  Sat Dec  1 14:24:41 UTC 2018
Task 292 Finished Sat Dec  1 14:27:07 UTC 2018
Task 292 Duration 00:02:26
Task 292 done

Succeeded
```
</details>

## PAS 仮想マシンの全開始

- `$ find /var/tempest/workspaces/default/deployments -name cf-*.yml`

- `bosh2 -e MY-ENV -d MY-DEPLOYMENT start`

<details><summary>例</summary>

```
$ bosh2 -e gcp -d cf-e5e5d0d42a09e353221f start
```
</details>

## Duplicate ‘bosh-dns-aliases’ error while installing PAS on GCP

```
$ bosh configs
```

```
$ bosh delete-config --name <name of the old ‘bosh-dns-aliases’> --type runtime
```