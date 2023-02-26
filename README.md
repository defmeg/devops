Установка Kubernetes кластера с помощью Kubespray и Terraform в Yandex Cloud

Для запуска установки трребуется vm с установленной ubuntu 20.04 \
1) Подготовка к установке: \
  Устанавливаем binenv - https://github.com/devops-works/binenv \
  Устанавливаем Terraform - ```$ binenv install terraform``` \
  Устанавливаем kubectl - ```$ binenv install kubectl``` \
  Устанавливаем helm - ```$ binenv install helm``` \
  Устанавливаем jq - ```$ sudo apt install jq``` \
  Устанавливаем pip3 и git - ```$ sudo apt install python3-pip git``` \
  Устанавливаем yandex-cli - https://cloud.yandex.ru/docs/cli/operations/install-cli

2) Скачиваем Kubespray версии 2.17.1 и установим зависимости для Kubespray
```
$ wget https://github.com/kubernetes-sigs/kubespray/archive/refs/tags/v2.17.1.tar.gz
$ tar -xvzf v2.17.1.tar.gz
$ mv kubespray-2.17.1 kubespray
$ sudo pip3 install -r kubespray/requirements.txt
```

3) Настраиваем Terraform переменные для доступа к Yandex Cloud
```
$ cp terraform/private.auto.tfvars.example terraform/private.auto.tfvars
$ yc config list
$ vim terraform/private.auto.tfvars
```

3) Сгенерим ssh ключи 
```
$ ssh-keygen -t rsa
```

4) Запкускаем установку Kubernetes кластера
```
$ bash cluster_install.sh
```

5) После установки копируем конфиг kubernetes
```
$ mkdir -p ~/.kube && cp kubespray/inventory/mycluster/artifacts/admin.conf ~/.kube/config
```

6) Удаление кластера kubernetes и ресурсов в Yandex Cloud
```
$ bash cluster_destroy.sh
```
