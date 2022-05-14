### Тестирование возможности установки своих ВМ 

* Рабочая директория:
```
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Gamma#
```

* На соснове конфигурации Terraform из урока Docker-Swarm по созданию шести инстансов
* План: изменить так конфигурацию Teraform, чтобы в результате могли создаваться 3 инстанса с именами `el-instance`, `k-instance`, `application-instance`

####  Для начала 
* в каталог `~/ansible-learning/yandex-cloud/Gamma/terraform` переносим файлы конфиги Terraform из каталога `~/netology-project/Docker-Compose-Swarm/src/terraform`
```ps
root@PC-Ubuntu:~/netology-project/Docker-Compose-Swarm/src/terraform# ll
итого 108
drwxr-xr-x 3 root root  4096 дек 14 07:19 ./
drwxr-xr-x 5 root root  4096 дек 11 09:03 ../
-rw-r--r-- 1 root root   125 дек 11 09:03 ansible.cfg
-rw-r--r-- 1 root root   856 дек 11 09:03 ansible.tf
-rw-r--r-- 1 root root  1204 дек 11 09:03 inventory.tf
-rw------- 1 root root  2402 дек 10 18:10 key.json
-rw-r--r-- 1 root root   260 дек 11 09:03 network.tf
-rw-r--r-- 1 root root   661 дек 11 09:03 node01.tf
-rw-r--r-- 1 root root   661 дек 11 09:03 node02.tf
-rw-r--r-- 1 root root   661 дек 11 09:03 node03.tf
-rw-r--r-- 1 root root   661 дек 11 09:03 node04.tf
-rw-r--r-- 1 root root   661 дек 11 09:03 node05.tf
-rw-r--r-- 1 root root   661 дек 11 09:03 node06.tf
-rw-r--r-- 1 root root  1439 дек 11 09:03 output.tf
-rw-r--r-- 1 root root   252 дек 11 09:03 provider.tf
-rw-r--r-- 1 root root   560 дек 10 20:52 variables.tf

```
#### Затем проверяем возможность создания инстансов на основе этой конфигурации.
* Для запуска пришлось в файле переменных выставить свои значения ID облака, папки и сетив Я.Облаке
* Затем выпоняем:
```ps
terraform init
```
```ps
terraform validate
```
```ps
terraform plan
```
```ps
terraform apply -auto-aprove
```
####  В результате были созданы 6 инстансов
```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Gamma/terraform# terraform apply -auto-approve

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # local_file.inventory will be created
  + resource "local_file" "inventory" {
      + content              = (known after apply)
      + directory_permission = "0777"
      + file_permission      = "0777"
      + filename             = "../ansible/inventory"
      + id                   = (known after apply)
    }

  # yandex_compute_instance.node01 will be created
  + resource "yandex_compute_instance" "node01" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node01.netology.yc"
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
              + block_size  = (known after apply)
              + description = (known after apply)
              + image_id    = "fd87ftkus6nii1k3epnu"
              + name        = "root-node01"
              + size        = 10
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.11"
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
          + cores         = 4
          + memory        = 8
        }

      + scheduling_policy {
          + preemptible = (known after apply)
        }
    }

  # yandex_compute_instance.node02 will be created
  + resource "yandex_compute_instance" "node02" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node02.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node02"
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
              + block_size  = (known after apply)
              + description = (known after apply)
              + image_id    = "fd87ftkus6nii1k3epnu"
              + name        = "root-node02"
              + size        = 10
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.12"
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
          + cores         = 4
          + memory        = 8
        }

      + scheduling_policy {
          + preemptible = (known after apply)
        }
    }

  # yandex_compute_instance.node03 will be created
  + resource "yandex_compute_instance" "node03" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node03.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node03"
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
              + block_size  = (known after apply)
              + description = (known after apply)
              + image_id    = "fd87ftkus6nii1k3epnu"
              + name        = "root-node03"
              + size        = 10
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.13"
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
          + cores         = 4
          + memory        = 8
        }

      + scheduling_policy {
          + preemptible = (known after apply)
        }
    }

  # yandex_compute_instance.node04 will be created
  + resource "yandex_compute_instance" "node04" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node04.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node04"
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
              + block_size  = (known after apply)
              + description = (known after apply)
              + image_id    = "fd87ftkus6nii1k3epnu"
              + name        = "root-node04"
              + size        = 40
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.14"
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
          + cores         = 4
          + memory        = 8
        }

      + scheduling_policy {
          + preemptible = (known after apply)
        }
    }

  # yandex_compute_instance.node05 will be created
  + resource "yandex_compute_instance" "node05" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node05.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node05"
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
              + block_size  = (known after apply)
              + description = (known after apply)
              + image_id    = "fd87ftkus6nii1k3epnu"
              + name        = "root-node05"
              + size        = 40
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.15"
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
          + cores         = 4
          + memory        = 8
        }

      + scheduling_policy {
          + preemptible = (known after apply)
        }
    }

  # yandex_compute_instance.node06 will be created
  + resource "yandex_compute_instance" "node06" {
      + allow_stopping_for_update = true
      + created_at                = (known after apply)
      + folder_id                 = (known after apply)
      + fqdn                      = (known after apply)
      + hostname                  = "node06.netology.yc"
      + id                        = (known after apply)
      + metadata                  = {
          + "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        }
      + name                      = "node06"
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
              + block_size  = (known after apply)
              + description = (known after apply)
              + image_id    = "fd87ftkus6nii1k3epnu"
              + name        = "root-node06"
              + size        = 40
              + snapshot_id = (known after apply)
              + type        = "network-nvme"
            }
        }

      + network_interface {
          + index              = (known after apply)
          + ip_address         = "192.168.101.16"
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
          + cores         = 4
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

Plan: 9 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + external_ip_address_node01 = (known after apply)
  + external_ip_address_node02 = (known after apply)
  + external_ip_address_node03 = (known after apply)
  + external_ip_address_node04 = (known after apply)
  + external_ip_address_node05 = (known after apply)
  + external_ip_address_node06 = (known after apply)
  + internal_ip_address_node04 = "192.168.101.14"
  + internal_ip_address_node05 = "192.168.101.15"
  + internal_ip_address_node06 = "192.168.101.16"
yandex_vpc_network.default: Creating...
yandex_vpc_network.default: Creation complete after 1s [id=enpu3e8fj4cco6abg7o8]
yandex_vpc_subnet.default: Creating...
yandex_vpc_subnet.default: Creation complete after 0s [id=e9bupc4vro745c18rpv5]
yandex_compute_instance.node06: Creating...
yandex_compute_instance.node05: Creating...
yandex_compute_instance.node02: Creating...
yandex_compute_instance.node01: Creating...
yandex_compute_instance.node04: Creating...
yandex_compute_instance.node03: Creating...
yandex_compute_instance.node05: Still creating... [10s elapsed]
yandex_compute_instance.node06: Still creating... [10s elapsed]
yandex_compute_instance.node02: Still creating... [10s elapsed]
yandex_compute_instance.node04: Still creating... [10s elapsed]
yandex_compute_instance.node03: Still creating... [10s elapsed]
yandex_compute_instance.node01: Still creating... [10s elapsed]
yandex_compute_instance.node06: Still creating... [20s elapsed]
yandex_compute_instance.node05: Still creating... [20s elapsed]
yandex_compute_instance.node02: Still creating... [20s elapsed]
yandex_compute_instance.node03: Still creating... [20s elapsed]
yandex_compute_instance.node04: Still creating... [20s elapsed]
yandex_compute_instance.node01: Still creating... [20s elapsed]
yandex_compute_instance.node06: Still creating... [30s elapsed]
yandex_compute_instance.node05: Still creating... [30s elapsed]
yandex_compute_instance.node02: Still creating... [30s elapsed]
yandex_compute_instance.node01: Still creating... [30s elapsed]
yandex_compute_instance.node03: Still creating... [30s elapsed]
yandex_compute_instance.node04: Still creating... [30s elapsed]
yandex_compute_instance.node06: Still creating... [40s elapsed]
yandex_compute_instance.node05: Still creating... [40s elapsed]
yandex_compute_instance.node02: Still creating... [40s elapsed]
yandex_compute_instance.node04: Still creating... [40s elapsed]
yandex_compute_instance.node03: Still creating... [40s elapsed]
yandex_compute_instance.node01: Still creating... [40s elapsed]
yandex_compute_instance.node06: Creation complete after 43s [id=fhm1ehru75ok277nveh7]
yandex_compute_instance.node01: Creation complete after 43s [id=fhmgnj3ff59ndbov8jl4]
yandex_compute_instance.node05: Creation complete after 44s [id=fhm6s5fqek8iatm0u434]
yandex_compute_instance.node02: Still creating... [50s elapsed]
yandex_compute_instance.node03: Still creating... [50s elapsed]
yandex_compute_instance.node04: Still creating... [50s elapsed]
yandex_compute_instance.node02: Creation complete after 55s [id=fhmsv7079ef9kd9q6gv1]
yandex_compute_instance.node04: Creation complete after 1m0s [id=fhm9aggjbst462eioh76]
yandex_compute_instance.node03: Creation complete after 1m0s [id=fhml856pv1qm486p5bek]
local_file.inventory: Creating...
local_file.inventory: Creation complete after 0s [id=72bd628647f2fd67dc7675f3cf29f9d1d286d501]

Apply complete! Resources: 9 added, 0 changed, 0 destroyed.

Outputs:

external_ip_address_node01 = "51.250.7.171"
external_ip_address_node02 = "51.250.15.231"
external_ip_address_node03 = "62.84.115.182"
external_ip_address_node04 = "62.84.113.181"
external_ip_address_node05 = "62.84.115.248"
external_ip_address_node06 = "51.250.5.234"
internal_ip_address_node01 = "192.168.101.11"
internal_ip_address_node02 = "192.168.101.12"
internal_ip_address_node03 = "192.168.101.13"
internal_ip_address_node04 = "192.168.101.14"
internal_ip_address_node05 = "192.168.101.15"
internal_ip_address_node06 = "192.168.101.16"

```
#### Заходим на инстанс и проверяем доступность в лоакльной сети облака других инстансов
```ps
root@PC-Ubuntu:~# ssh centos@51.250.7.171
The authenticity of host '51.250.7.171 (51.250.7.171)' can't be established.
ECDSA key fingerprint is SHA256:gnFXrTlEUNP/EFmK4D9WYvLNCFmAOQC4CnfzpkKSpFU.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '51.250.7.171' (ECDSA) to the list of known hosts.
[centos@node01 ~]$ 
[centos@node01 ~]$ 
[centos@node01 ~]$ sudo -i
[root@node01 ~]# 
[root@node01 ~]# 
[root@node01 ~]# 
```
```ps
[root@node01 ~]# ping 192.168.101.11
PING 192.168.101.11 (192.168.101.11) 56(84) bytes of data.
64 bytes from 192.168.101.11: icmp_seq=1 ttl=64 time=0.018 ms
64 bytes from 192.168.101.11: icmp_seq=2 ttl=64 time=0.033 ms
^C
--- 192.168.101.11 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 999ms
rtt min/avg/max/mdev = 0.018/0.025/0.033/0.009 ms
```
```ps
[root@node01 ~]# ping 192.168.101.12
PING 192.168.101.12 (192.168.101.12) 56(84) bytes of data.
64 bytes from 192.168.101.12: icmp_seq=1 ttl=63 time=1.39 ms
64 bytes from 192.168.101.12: icmp_seq=2 ttl=63 time=0.614 ms
^C
--- 192.168.101.12 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 0.614/1.006/1.399/0.393 ms
```
```ps
[root@node01 ~]# ping 192.168.101.13
PING 192.168.101.13 (192.168.101.13) 56(84) bytes of data.
64 bytes from 192.168.101.13: icmp_seq=1 ttl=63 time=1.33 ms
64 bytes from 192.168.101.13: icmp_seq=2 ttl=63 time=0.645 ms
^C
--- 192.168.101.13 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 0.645/0.990/1.335/0.345 ms
```
```ps
[root@node01 ~]# ping 192.168.101.15
PING 192.168.101.15 (192.168.101.15) 56(84) bytes of data.
64 bytes from 192.168.101.15: icmp_seq=1 ttl=63 time=1.33 ms
64 bytes from 192.168.101.15: icmp_seq=2 ttl=63 time=0.719 ms
^C
--- 192.168.101.15 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 0.719/1.025/1.332/0.308 ms
```
```ps
[root@node01 ~]# ping 192.168.101.16
PING 192.168.101.16 (192.168.101.16) 56(84) bytes of data.
64 bytes from 192.168.101.16: icmp_seq=1 ttl=63 time=1.44 ms
64 bytes from 192.168.101.16: icmp_seq=2 ttl=63 time=0.517 ms
^C
--- 192.168.101.16 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 0.517/0.980/1.443/0.463 ms
```
```ps
[root@node01 ~]# ping 192.168.101.17
PING 192.168.101.17 (192.168.101.17) 56(84) bytes of data.
^C
--- 192.168.101.17 ping statistics ---
4 packets transmitted, 0 received, 100% packet loss, time 2999ms
```
```ps
[root@node01 ~]# ping 192.168.101.18
PING 192.168.101.18 (192.168.101.18) 56(84) bytes of data.
^C
--- 192.168.101.18 ping statistics ---
2 packets transmitted, 0 received, 100% packet loss, time 1000ms

[root@node01 ~]# 
[root@node01 ~]# 

```
#### Удаляем инстансы
```ps
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Gamma/terraform# terraform destroy -auto-approve
yandex_vpc_network.default: Refreshing state... [id=enpu3e8fj4cco6abg7o8]
yandex_vpc_subnet.default: Refreshing state... [id=e9bupc4vro745c18rpv5]
yandex_compute_instance.node06: Refreshing state... [id=fhm1ehru75ok277nveh7]
yandex_compute_instance.node01: Refreshing state... [id=fhmgnj3ff59ndbov8jl4]
yandex_compute_instance.node02: Refreshing state... [id=fhmsv7079ef9kd9q6gv1]
yandex_compute_instance.node04: Refreshing state... [id=fhm9aggjbst462eioh76]
yandex_compute_instance.node05: Refreshing state... [id=fhm6s5fqek8iatm0u434]
yandex_compute_instance.node03: Refreshing state... [id=fhml856pv1qm486p5bek]
local_file.inventory: Refreshing state... [id=72bd628647f2fd67dc7675f3cf29f9d1d286d501]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  # local_file.inventory will be destroyed
  - resource "local_file" "inventory" {
      - content              = <<-EOT
            # Ansible inventory containing variable values from Terraform.
            # Generated by Terraform.
            
            [nodes:children]
            managers
            workers
            
            [managers:children]
            active
            standby
            
            [active]
            node01.netology.yc ansible_host=51.250.7.171
            
            [standby]
            node02.netology.yc ansible_host=51.250.15.231
            node03.netology.yc ansible_host=62.84.115.182
            
            [workers]
            node04.netology.yc ansible_host=62.84.113.181
            node05.netology.yc ansible_host=62.84.115.248
            node06.netology.yc ansible_host=51.250.5.234
        EOT -> null
      - directory_permission = "0777" -> null
      - file_permission      = "0777" -> null
      - filename             = "../ansible/inventory" -> null
      - id                   = "72bd628647f2fd67dc7675f3cf29f9d1d286d501" -> null
    }

  # yandex_compute_instance.node01 will be destroyed
  - resource "yandex_compute_instance" "node01" {
      - allow_stopping_for_update = true -> null
      - created_at                = "2022-02-19T03:10:29Z" -> null
      - folder_id                 = "b1gd3hm4niaifoa8dahm" -> null
      - fqdn                      = "node01.netology.yc" -> null
      - hostname                  = "node01" -> null
      - id                        = "fhmgnj3ff59ndbov8jl4" -> null
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
          - device_name = "fhmpaifa5uuhg009nbqn" -> null
          - disk_id     = "fhmpaifa5uuhg009nbqn" -> null
          - mode        = "READ_WRITE" -> null

          - initialize_params {
              - block_size = 4096 -> null
              - image_id   = "fd87ftkus6nii1k3epnu" -> null
              - name       = "root-node01" -> null
              - size       = 10 -> null
              - type       = "network-ssd" -> null
            }
        }

      - network_interface {
          - index              = 0 -> null
          - ip_address         = "192.168.101.11" -> null
          - ipv4               = true -> null
          - ipv6               = false -> null
          - mac_address        = "d0:0d:10:bc:c6:f7" -> null
          - nat                = true -> null
          - nat_ip_address     = "51.250.7.171" -> null
          - nat_ip_version     = "IPV4" -> null
          - security_group_ids = [] -> null
          - subnet_id          = "e9bupc4vro745c18rpv5" -> null
        }

      - placement_policy {}

      - resources {
          - core_fraction = 100 -> null
          - cores         = 4 -> null
          - gpus          = 0 -> null
          - memory        = 8 -> null
        }

      - scheduling_policy {
          - preemptible = false -> null
        }
    }

  # yandex_compute_instance.node02 will be destroyed
  - resource "yandex_compute_instance" "node02" {
      - allow_stopping_for_update = true -> null
      - created_at                = "2022-02-19T03:10:29Z" -> null
      - folder_id                 = "b1gd3hm4niaifoa8dahm" -> null
      - fqdn                      = "node02.netology.yc" -> null
      - hostname                  = "node02" -> null
      - id                        = "fhmsv7079ef9kd9q6gv1" -> null
      - labels                    = {} -> null
      - metadata                  = {
          - "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        } -> null
      - name                      = "node02" -> null
      - network_acceleration_type = "standard" -> null
      - platform_id               = "standard-v1" -> null
      - status                    = "running" -> null
      - zone                      = "ru-central1-a" -> null

      - boot_disk {
          - auto_delete = true -> null
          - device_name = "fhmkt3hgpa431rribohq" -> null
          - disk_id     = "fhmkt3hgpa431rribohq" -> null
          - mode        = "READ_WRITE" -> null

          - initialize_params {
              - block_size = 4096 -> null
              - image_id   = "fd87ftkus6nii1k3epnu" -> null
              - name       = "root-node02" -> null
              - size       = 10 -> null
              - type       = "network-ssd" -> null
            }
        }

      - network_interface {
          - index              = 0 -> null
          - ip_address         = "192.168.101.12" -> null
          - ipv4               = true -> null
          - ipv6               = false -> null
          - mac_address        = "d0:0d:1c:f9:c0:74" -> null
          - nat                = true -> null
          - nat_ip_address     = "51.250.15.231" -> null
          - nat_ip_version     = "IPV4" -> null
          - security_group_ids = [] -> null
          - subnet_id          = "e9bupc4vro745c18rpv5" -> null
        }

      - placement_policy {}

      - resources {
          - core_fraction = 100 -> null
          - cores         = 4 -> null
          - gpus          = 0 -> null
          - memory        = 8 -> null
        }

      - scheduling_policy {
          - preemptible = false -> null
        }
    }

  # yandex_compute_instance.node03 will be destroyed
  - resource "yandex_compute_instance" "node03" {
      - allow_stopping_for_update = true -> null
      - created_at                = "2022-02-19T03:10:29Z" -> null
      - folder_id                 = "b1gd3hm4niaifoa8dahm" -> null
      - fqdn                      = "node03.netology.yc" -> null
      - hostname                  = "node03" -> null
      - id                        = "fhml856pv1qm486p5bek" -> null
      - labels                    = {} -> null
      - metadata                  = {
          - "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        } -> null
      - name                      = "node03" -> null
      - network_acceleration_type = "standard" -> null
      - platform_id               = "standard-v1" -> null
      - status                    = "running" -> null
      - zone                      = "ru-central1-a" -> null

      - boot_disk {
          - auto_delete = true -> null
          - device_name = "fhmfnl0t4uqo00iuv1u7" -> null
          - disk_id     = "fhmfnl0t4uqo00iuv1u7" -> null
          - mode        = "READ_WRITE" -> null

          - initialize_params {
              - block_size = 4096 -> null
              - image_id   = "fd87ftkus6nii1k3epnu" -> null
              - name       = "root-node03" -> null
              - size       = 10 -> null
              - type       = "network-ssd" -> null
            }
        }

      - network_interface {
          - index              = 0 -> null
          - ip_address         = "192.168.101.13" -> null
          - ipv4               = true -> null
          - ipv6               = false -> null
          - mac_address        = "d0:0d:15:41:4d:9f" -> null
          - nat                = true -> null
          - nat_ip_address     = "62.84.115.182" -> null
          - nat_ip_version     = "IPV4" -> null
          - security_group_ids = [] -> null
          - subnet_id          = "e9bupc4vro745c18rpv5" -> null
        }

      - placement_policy {}

      - resources {
          - core_fraction = 100 -> null
          - cores         = 4 -> null
          - gpus          = 0 -> null
          - memory        = 8 -> null
        }

      - scheduling_policy {
          - preemptible = false -> null
        }
    }

  # yandex_compute_instance.node04 will be destroyed
  - resource "yandex_compute_instance" "node04" {
      - allow_stopping_for_update = true -> null
      - created_at                = "2022-02-19T03:10:29Z" -> null
      - folder_id                 = "b1gd3hm4niaifoa8dahm" -> null
      - fqdn                      = "node04.netology.yc" -> null
      - hostname                  = "node04" -> null
      - id                        = "fhm9aggjbst462eioh76" -> null
      - labels                    = {} -> null
      - metadata                  = {
          - "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        } -> null
      - name                      = "node04" -> null
      - network_acceleration_type = "standard" -> null
      - platform_id               = "standard-v1" -> null
      - status                    = "running" -> null
      - zone                      = "ru-central1-a" -> null

      - boot_disk {
          - auto_delete = true -> null
          - device_name = "fhm9btlbh3u8g3vbkssu" -> null
          - disk_id     = "fhm9btlbh3u8g3vbkssu" -> null
          - mode        = "READ_WRITE" -> null

          - initialize_params {
              - block_size = 4096 -> null
              - image_id   = "fd87ftkus6nii1k3epnu" -> null
              - name       = "root-node04" -> null
              - size       = 40 -> null
              - type       = "network-ssd" -> null
            }
        }

      - network_interface {
          - index              = 0 -> null
          - ip_address         = "192.168.101.14" -> null
          - ipv4               = true -> null
          - ipv6               = false -> null
          - mac_address        = "d0:0d:95:42:13:5f" -> null
          - nat                = true -> null
          - nat_ip_address     = "62.84.113.181" -> null
          - nat_ip_version     = "IPV4" -> null
          - security_group_ids = [] -> null
          - subnet_id          = "e9bupc4vro745c18rpv5" -> null
        }

      - placement_policy {}

      - resources {
          - core_fraction = 100 -> null
          - cores         = 4 -> null
          - gpus          = 0 -> null
          - memory        = 8 -> null
        }

      - scheduling_policy {
          - preemptible = false -> null
        }
    }

  # yandex_compute_instance.node05 will be destroyed
  - resource "yandex_compute_instance" "node05" {
      - allow_stopping_for_update = true -> null
      - created_at                = "2022-02-19T03:10:29Z" -> null
      - folder_id                 = "b1gd3hm4niaifoa8dahm" -> null
      - fqdn                      = "node05.netology.yc" -> null
      - hostname                  = "node05" -> null
      - id                        = "fhm6s5fqek8iatm0u434" -> null
      - labels                    = {} -> null
      - metadata                  = {
          - "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        } -> null
      - name                      = "node05" -> null
      - network_acceleration_type = "standard" -> null
      - platform_id               = "standard-v1" -> null
      - status                    = "running" -> null
      - zone                      = "ru-central1-a" -> null

      - boot_disk {
          - auto_delete = true -> null
          - device_name = "fhmmr0eru2egmmj8bhc2" -> null
          - disk_id     = "fhmmr0eru2egmmj8bhc2" -> null
          - mode        = "READ_WRITE" -> null

          - initialize_params {
              - block_size = 4096 -> null
              - image_id   = "fd87ftkus6nii1k3epnu" -> null
              - name       = "root-node05" -> null
              - size       = 40 -> null
              - type       = "network-ssd" -> null
            }
        }

      - network_interface {
          - index              = 0 -> null
          - ip_address         = "192.168.101.15" -> null
          - ipv4               = true -> null
          - ipv6               = false -> null
          - mac_address        = "d0:0d:6e:15:fa:75" -> null
          - nat                = true -> null
          - nat_ip_address     = "62.84.115.248" -> null
          - nat_ip_version     = "IPV4" -> null
          - security_group_ids = [] -> null
          - subnet_id          = "e9bupc4vro745c18rpv5" -> null
        }

      - placement_policy {}

      - resources {
          - core_fraction = 100 -> null
          - cores         = 4 -> null
          - gpus          = 0 -> null
          - memory        = 8 -> null
        }

      - scheduling_policy {
          - preemptible = false -> null
        }
    }

  # yandex_compute_instance.node06 will be destroyed
  - resource "yandex_compute_instance" "node06" {
      - allow_stopping_for_update = true -> null
      - created_at                = "2022-02-19T03:10:29Z" -> null
      - folder_id                 = "b1gd3hm4niaifoa8dahm" -> null
      - fqdn                      = "node06.netology.yc" -> null
      - hostname                  = "node06" -> null
      - id                        = "fhm1ehru75ok277nveh7" -> null
      - labels                    = {} -> null
      - metadata                  = {
          - "ssh-keys" = <<-EOT
                centos:ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+9Ei9PdBgvkzoZaKFwoy9mDeug4UUkdibC3r9CRxn2ml0qka0W3JrldqzFj2sZ3N9g3W5LRcVFN0aw42hMxgTvN5OJrP46AnOtuF7JXp3rndq1zsKf1C6fxfV94erFBaJHxtYqRIgfcMxNrqCFs3t6aoc6Rvo6s80Pq+mxwbHUV3z/Rih4xUycnjzmwJOE28NTtRsysdRZoV7KaOTZ3nVgnrjlf/oQRgsyZXQYA6sW4rYMd6UjSXd3dB1N3kOZeyE8zaTjqKQwuwwL1d1JuKrefxrigt+DxAMwq6mIe7eu0SYBcjFAkhglTjuIblo0xrgxbL389MOW/fe2CLqygAb66QZlc85sj1SMuVASlwOliLKU8W7uEJT/1U4zQkAwuEPKZexSNGu0XMOKpByW2A9bPTcKJGRoOUZcRwTp9bVPxHTlfRRtheKVHm3eSzLEt0AN2hbTQmPapaKorcME8FWFr0PLG4Ic3VLwSOX/lWB1Gq5Va+ozsnbZBYfJE7+FMs= root@PC-Ubuntu
            EOT
        } -> null
      - name                      = "node06" -> null
      - network_acceleration_type = "standard" -> null
      - platform_id               = "standard-v1" -> null
      - status                    = "running" -> null
      - zone                      = "ru-central1-a" -> null

      - boot_disk {
          - auto_delete = true -> null
          - device_name = "fhm9jqpad8heq29piih0" -> null
          - disk_id     = "fhm9jqpad8heq29piih0" -> null
          - mode        = "READ_WRITE" -> null

          - initialize_params {
              - block_size = 4096 -> null
              - image_id   = "fd87ftkus6nii1k3epnu" -> null
              - name       = "root-node06" -> null
              - size       = 40 -> null
              - type       = "network-ssd" -> null
            }
        }

      - network_interface {
          - index              = 0 -> null
          - ip_address         = "192.168.101.16" -> null
          - ipv4               = true -> null
          - ipv6               = false -> null
          - mac_address        = "d0:0d:17:47:7e:39" -> null
          - nat                = true -> null
          - nat_ip_address     = "51.250.5.234" -> null
          - nat_ip_version     = "IPV4" -> null
          - security_group_ids = [] -> null
          - subnet_id          = "e9bupc4vro745c18rpv5" -> null
        }

      - placement_policy {}

      - resources {
          - core_fraction = 100 -> null
          - cores         = 4 -> null
          - gpus          = 0 -> null
          - memory        = 8 -> null
        }

      - scheduling_policy {
          - preemptible = false -> null
        }
    }

  # yandex_vpc_network.default will be destroyed
  - resource "yandex_vpc_network" "default" {
      - created_at = "2022-02-19T03:10:28Z" -> null
      - folder_id  = "b1gd3hm4niaifoa8dahm" -> null
      - id         = "enpu3e8fj4cco6abg7o8" -> null
      - labels     = {} -> null
      - name       = "net" -> null
      - subnet_ids = [
          - "e9bupc4vro745c18rpv5",
        ] -> null
    }

  # yandex_vpc_subnet.default will be destroyed
  - resource "yandex_vpc_subnet" "default" {
      - created_at     = "2022-02-19T03:10:28Z" -> null
      - folder_id      = "b1gd3hm4niaifoa8dahm" -> null
      - id             = "e9bupc4vro745c18rpv5" -> null
      - labels         = {} -> null
      - name           = "subnet" -> null
      - network_id     = "enpu3e8fj4cco6abg7o8" -> null
      - v4_cidr_blocks = [
          - "192.168.101.0/24",
        ] -> null
      - v6_cidr_blocks = [] -> null
      - zone           = "ru-central1-a" -> null
    }

Plan: 0 to add, 0 to change, 9 to destroy.

Changes to Outputs:
  - external_ip_address_node01 = "51.250.7.171" -> null
  - external_ip_address_node02 = "51.250.15.231" -> null
  - external_ip_address_node03 = "62.84.115.182" -> null
  - external_ip_address_node04 = "62.84.113.181" -> null
  - external_ip_address_node05 = "62.84.115.248" -> null
  - external_ip_address_node06 = "51.250.5.234" -> null
  - internal_ip_address_node01 = "192.168.101.11" -> null
  - internal_ip_address_node02 = "192.168.101.12" -> null
  - internal_ip_address_node03 = "192.168.101.13" -> null
  - internal_ip_address_node04 = "192.168.101.14" -> null
  - internal_ip_address_node05 = "192.168.101.15" -> null
  - internal_ip_address_node06 = "192.168.101.16" -> null
local_file.inventory: Destroying... [id=72bd628647f2fd67dc7675f3cf29f9d1d286d501]
local_file.inventory: Destruction complete after 0s
yandex_compute_instance.node06: Destroying... [id=fhm1ehru75ok277nveh7]
yandex_compute_instance.node05: Destroying... [id=fhm6s5fqek8iatm0u434]
yandex_compute_instance.node02: Destroying... [id=fhmsv7079ef9kd9q6gv1]
yandex_compute_instance.node04: Destroying... [id=fhm9aggjbst462eioh76]
yandex_compute_instance.node01: Destroying... [id=fhmgnj3ff59ndbov8jl4]
yandex_compute_instance.node03: Destroying... [id=fhml856pv1qm486p5bek]
yandex_compute_instance.node06: Still destroying... [id=fhm1ehru75ok277nveh7, 10s elapsed]
yandex_compute_instance.node04: Still destroying... [id=fhm9aggjbst462eioh76, 10s elapsed]
yandex_compute_instance.node02: Still destroying... [id=fhmsv7079ef9kd9q6gv1, 10s elapsed]
yandex_compute_instance.node05: Still destroying... [id=fhm6s5fqek8iatm0u434, 10s elapsed]
yandex_compute_instance.node03: Still destroying... [id=fhml856pv1qm486p5bek, 10s elapsed]
yandex_compute_instance.node01: Still destroying... [id=fhmgnj3ff59ndbov8jl4, 10s elapsed]
yandex_compute_instance.node04: Destruction complete after 11s
yandex_compute_instance.node02: Destruction complete after 12s
yandex_compute_instance.node01: Destruction complete after 12s
yandex_compute_instance.node05: Destruction complete after 13s
yandex_compute_instance.node03: Destruction complete after 13s
yandex_compute_instance.node06: Destruction complete after 16s
yandex_vpc_subnet.default: Destroying... [id=e9bupc4vro745c18rpv5]
yandex_vpc_subnet.default: Destruction complete after 3s
yandex_vpc_network.default: Destroying... [id=enpu3e8fj4cco6abg7o8]
yandex_vpc_network.default: Destruction complete after 0s

Destroy complete! Resources: 9 destroyed.

```
