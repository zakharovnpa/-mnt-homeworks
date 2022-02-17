### Ход выполнения ДЗ "Ansible & Yandex.Cloud"

#### Запуск в Я.Облаке трех ВМ на основе образа, созданного ранее По Packer.

Действия выполняются по уроку ["5.4. Оркестрация группой Docker контейнеров на примере Docker Compose"](https://github.com/zakharovnpa/02-virt-admin-homeworks/blob/main/05-virt-04-docker-compose/Lesson/Log-lesson-docker-compose.md)

1. В ДЗ по Docker-Compose есть файлы Терраформ. Воспльзуемся ими.
Проверяем доступные ресурсы на Я.Облаке
```ps
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# yc resource-manager folder list
+----------------------+---------------+--------+--------+
|          ID          |     NAME      | LABELS | STATUS |
+----------------------+---------------+--------+--------+
| b1ggdhpqn2g4ts7rsvfj | default       |        | ACTIVE |
| b1gd3hm4niaifoa8dahm | netology-alfa |        | ACTIVE |
+----------------------+---------------+--------+--------+

```


Проверка валидности Терраформ
```ps
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform validate
Success! The configuration is valid.
```

```ps
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # yandex_compute_instance.node01 will be created
  + resource "yandex_compute_instance" "node01" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node01.netology.cloud"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node01"
      + network_acceleration_type = "standard"
      + platform_id               = "standard-v1"
      + service_account_id        = (known after apply)
      + status                    = (known after apply)
      + zone                      = "ru-central1-a"

      + boot_disk {
          + auto_delete = true
          + device_name = (known after apply)
          + disk_id     = (known after apply)
          + mode        = (known after apply)

          + initialize_params {
              + description = (known after apply)
              + image_id    = "fd87ftkus6nii1k3epnu"
              + name        = "root-node01"
              + size        = 50
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = (known after apply)
          + ipv4               = true
          + ipv6               = (known after apply)
          + ipv6_address       = (known after apply)
          + mac_address        = (known after apply)
          + nat                = true
          + nat_ip_address     = (known after apply)
          + nat_ip_version     = (known after apply)
          + security_group_ids = (known after apply)
          + subnet_id          = (known after apply)
        }

      + placement_policy {
          + placement_group_id = (known after apply)
        }

      + resources {
          + core_fraction = 100
          + cores         = 8
          + memory        = 8
        }

      + scheduling_policy {
          + preemptible = (known after apply)
        }
    }

  # yandex_vpc_network.default will be created
  + resource "yandex_vpc_network" "default" {
      + created_at                = (known after apply)
      + default_security_group_id = (known after apply)
      + folder_id                 = (known after apply)
      + id                        = (known after apply)
      + labels                    = (known after apply)
      + name                      = "net"
      + subnet_ids                = (known after apply)
    }

  # yandex_vpc_subnet.default will be created
  + resource "yandex_vpc_subnet" "default" {
      + created_at     = (known after apply)
      + folder_id      = (known after apply)
      + id             = (known after apply)
      + labels         = (known after apply)
      + name           = "subnet"
      + network_id     = (known after apply)
      + v4_cidr_blocks = [
          + "192.168.101.0/24",
        ]
      + v6_cidr_blocks = (known after apply)
      + zone           = "ru-central1-a"
    }

Plan: 3 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + external_ip_address_node01_yandex_cloud = (known after apply)
  + internal_ip_address_node01_yandex_cloud = (known after apply)

─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
```


2. Запуск тераформ на создание ВМ. ВМ создавалась долго - 3 минуты, но создалась.

```ps
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform apply -auto-approve

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # yandex_compute_instance.node01 will be created
  + resource "yandex_compute_instance" "node01" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node01.netology.cloud"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node01"
      + network_acceleration_type = "standard"
      + platform_id               = "standard-v1"
      + service_account_id        = (known after apply)
      + status                    = (known after apply)
      + zone                      = "ru-central1-a"

      + boot_disk {
          + auto_delete = true
          + device_name = (known after apply)
          + disk_id     = (known after apply)
          + mode        = (known after apply)

          + initialize_params {
              + description = (known after apply)
              + image_id    = "fd87ftkus6nii1k3epnu"
              + name        = "root-node01"
              + size        = 50
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = (known after apply)
          + ipv4               = true
          + ipv6               = (known after apply)
          + ipv6_address       = (known after apply)
          + mac_address        = (known after apply)
          + nat                = true
          + nat_ip_address     = (known after apply)
          + nat_ip_version     = (known after apply)
          + security_group_ids = (known after apply)
          + subnet_id          = (known after apply)
        }

      + placement_policy {
          + placement_group_id = (known after apply)
        }

      + resources {
          + core_fraction = 100
          + cores         = 8
          + memory        = 8
        }

      + scheduling_policy {
          + preemptible = (known after apply)
        }
    }

  # yandex_vpc_network.default will be created
  + resource "yandex_vpc_network" "default" {
      + created_at                = (known after apply)
      + default_security_group_id = (known after apply)
      + folder_id                 = (known after apply)
      + id                        = (known after apply)
      + labels                    = (known after apply)
      + name                      = "net"
      + subnet_ids                = (known after apply)
    }

  # yandex_vpc_subnet.default will be created
  + resource "yandex_vpc_subnet" "default" {
      + created_at     = (known after apply)
      + folder_id      = (known after apply)
      + id             = (known after apply)
      + labels         = (known after apply)
      + name           = "subnet"
      + network_id     = (known after apply)
      + v4_cidr_blocks = [
          + "192.168.101.0/24",
        ]
      + v6_cidr_blocks = (known after apply)
      + zone           = "ru-central1-a"
    }

Plan: 3 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + external_ip_address_node01_yandex_cloud = (known after apply)
  + internal_ip_address_node01_yandex_cloud = (known after apply)
yandex_vpc_network.default: Creating...
yandex_vpc_network.default: Creation complete after 7s [id=enp4qt9sn4s4hc0mfkrl]
yandex_vpc_subnet.default: Creating...
yandex_vpc_subnet.default: Creation complete after 0s [id=e9bo5c6cno0ffqgskisj]
yandex_compute_instance.node01: Creating...
yandex_compute_instance.node01: Still creating... [10s elapsed]
yandex_compute_instance.node01: Still creating... [20s elapsed]
yandex_compute_instance.node01: Still creating... [30s elapsed]
yandex_compute_instance.node01: Still creating... [40s elapsed]
yandex_compute_instance.node01: Still creating... [50s elapsed]
yandex_compute_instance.node01: Still creating... [1m0s elapsed]
yandex_compute_instance.node01: Still creating... [1m10s elapsed]
yandex_compute_instance.node01: Still creating... [1m20s elapsed]
yandex_compute_instance.node01: Still creating... [1m30s elapsed]
yandex_compute_instance.node01: Still creating... [1m40s elapsed]
yandex_compute_instance.node01: Still creating... [1m50s elapsed]
yandex_compute_instance.node01: Still creating... [2m0s elapsed]
yandex_compute_instance.node01: Still creating... [2m10s elapsed]
yandex_compute_instance.node01: Still creating... [2m20s elapsed]
yandex_compute_instance.node01: Still creating... [2m30s elapsed]
yandex_compute_instance.node01: Still creating... [2m40s elapsed]
yandex_compute_instance.node01: Still creating... [2m50s elapsed]
yandex_compute_instance.node01: Still creating... [3m0s elapsed]
yandex_compute_instance.node01: Still creating... [3m10s elapsed]
yandex_compute_instance.node01: Still creating... [3m20s elapsed]
yandex_compute_instance.node01: Still creating... [3m30s elapsed]
yandex_compute_instance.node01: Still creating... [3m40s elapsed]
yandex_compute_instance.node01: Still creating... [3m50s elapsed]
yandex_compute_instance.node01: Creation complete after 3m52s [id=fhmppk90clccmn989c2i]

Apply complete! Resources: 3 added, 0 changed, 0 destroyed.

Outputs:

external_ip_address_node01_yandex_cloud = "62.84.114.151"
internal_ip_address_node01_yandex_cloud = "192.168.101.18"

```
Подключился к новой ВМ:
```ps
root@PC-Ubuntu:~# ssh centos@62.84.114.151
The authenticity of host '62.84.114.151 (62.84.114.151)' can't be established.
ECDSA key fingerprint is SHA256:Xqj9WB/JgYiE3cpXa03oAYsnXGPtLbA9NPUq6MRHbCw.
Are you sure you want to continue connecting (yes/no/[fingerprint])? y
Please type 'yes', 'no' or the fingerprint: yes
Warning: Permanently added '62.84.114.151' (ECDSA) to the list of known hosts.
[centos@node01 ~]$ 
[centos@node01 ~]$ 
[centos@node01 ~]$ docker ps
-bash: docker: команда не найдена
[centos@node01 ~]$ 
[centos@node01 ~]$ sudo
usage: sudo -h | -K | -k | -V
usage: sudo -v [-AknS] [-g group] [-h host] [-p prompt] [-u user]
usage: sudo -l [-AknS] [-g group] [-h host] [-p prompt] [-U user] [-u user] [command]
usage: sudo [-AbEHknPS] [-r role] [-t type] [-C num] [-g group] [-h host] [-p prompt] [-T timeout] [-u user] [VAR=value] [-i|-s] [<command>]
usage: sudo -e [-AknS] [-r role] [-t type] [-C num] [-g group] [-h host] [-p prompt] [-T timeout] [-u user] file ...
[centos@node01 ~]$ 
[centos@node01 ~]$ df -h
Файловая система Размер Использовано  Дост Использовано% Cмонтировано в
devtmpfs           3,8G            0  3,8G            0% /dev
tmpfs              3,9G            0  3,9G            0% /dev/shm
tmpfs              3,9G         596K  3,9G            1% /run
tmpfs              3,9G            0  3,9G            0% /sys/fs/cgroup
/dev/vda2           50G         1,6G   49G            4% /
tmpfs              783M            0  783M            0% /run/user/1000

```
Остановка и удаление ВМ
```ps
root@PC-Ubuntu:~/netology-project/Docker-Compose/src/terraform# terraform destroy -auto-approve
yandex_vpc_network.default: Refreshing state... [id=enp4qt9sn4s4hc0mfkrl]
yandex_vpc_subnet.default: Refreshing state... [id=e9bo5c6cno0ffqgskisj]
yandex_compute_instance.node01: Refreshing state... [id=fhmppk90clccmn989c2i]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  # yandex_compute_instance.node01 will be destroyed
  - resource "yandex_compute_instance" "node01" {
      - allow_stopping_for_update = true -> null
      - created_at                = "2022-02-17T13:00:39Z" -> null
      - folder_id                 = "b1gd3hm4niaifoa8dahm" -> null
      - fqdn                      = "node01.netology.cloud" -> null
      - hostname                  = "node01" -> null
      - id                        = "fhmppk90clccmn989c2i" -> null
      - labels                    = {} -> null
      - metadata                  = {
          - "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        } -> null
      - name                      = "node01" -> null
      - network_acceleration_type = "standard" -> null
      - platform_id               = "standard-v1" -> null
      - status                    = "running" -> null
      - zone                      = "ru-central1-a" -> null

      - boot_disk {
          - auto_delete = true -> null
          - device_name = "fhm2msemll51fsrt5doo" -> null
          - disk_id     = "fhm2msemll51fsrt5doo" -> null
          - mode        = "READ_WRITE" -> null

          - initialize_params {
              - image_id = "fd87ftkus6nii1k3epnu" -> null
              - name     = "root-node01" -> null
              - size     = 50 -> null
              - type     = "network-ssd" -> null
            }
        }

      - network_interface {
          - index              = 0 -> null
          - ip_address         = "192.168.101.18" -> null
          - ipv4               = true -> null
          - ipv6               = false -> null
          - mac_address        = "d0:0d:19:cd:12:06" -> null
          - nat                = true -> null
          - nat_ip_address     = "62.84.114.151" -> null
          - nat_ip_version     = "IPV4" -> null
          - security_group_ids = [] -> null
          - subnet_id          = "e9bo5c6cno0ffqgskisj" -> null
        }

      - placement_policy {}

      - resources {
          - core_fraction = 100 -> null
          - cores         = 8 -> null
          - gpus          = 0 -> null
          - memory        = 8 -> null
        }

      - scheduling_policy {
          - preemptible = false -> null
        }
    }

  # yandex_vpc_network.default will be destroyed
  - resource "yandex_vpc_network" "default" {
      - created_at = "2022-02-17T13:00:36Z" -> null
      - folder_id  = "b1gd3hm4niaifoa8dahm" -> null
      - id         = "enp4qt9sn4s4hc0mfkrl" -> null
      - labels     = {} -> null
      - name       = "net" -> null
      - subnet_ids = [
          - "e9bo5c6cno0ffqgskisj",
        ] -> null
    }

  # yandex_vpc_subnet.default will be destroyed
  - resource "yandex_vpc_subnet" "default" {
      - created_at     = "2022-02-17T13:00:37Z" -> null
      - folder_id      = "b1gd3hm4niaifoa8dahm" -> null
      - id             = "e9bo5c6cno0ffqgskisj" -> null
      - labels         = {} -> null
      - name           = "subnet" -> null
      - network_id     = "enp4qt9sn4s4hc0mfkrl" -> null
      - v4_cidr_blocks = [
          - "192.168.101.0/24",
        ] -> null
      - v6_cidr_blocks = [] -> null
      - zone           = "ru-central1-a" -> null
    }

Plan: 0 to add, 0 to change, 3 to destroy.

Changes to Outputs:
  - external_ip_address_node01_yandex_cloud = "62.84.114.151" -> null
  - internal_ip_address_node01_yandex_cloud = "192.168.101.18" -> null
yandex_compute_instance.node01: Destroying... [id=fhmppk90clccmn989c2i]
yandex_compute_instance.node01: Still destroying... [id=fhmppk90clccmn989c2i, 10s elapsed]
yandex_compute_instance.node01: Destruction complete after 14s
yandex_vpc_subnet.default: Destroying... [id=e9bo5c6cno0ffqgskisj]
yandex_vpc_subnet.default: Destruction complete after 6s
yandex_vpc_network.default: Destroying... [id=enp4qt9sn4s4hc0mfkrl]
yandex_vpc_network.default: Destruction complete after 1s

Destroy complete! Resources: 3 destroyed.

```
