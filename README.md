## Задание D2.4.1
<details>
  <summary><strong>Поднимите у себя локальный K8S-кластер с помощью Minikube.</strong></summary>

        curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
        chmod +x minikube
        sudo mv minikube /usr/local/bin/  
</details>
<details>
  <summary><strong>В кластере должно быть всего пять нод, одна из них должна быть Сontrol Plane-нода</strong></summary>

        minikube start --nodes=5 --driver=docker

</details>
<details>
  <summary><strong>После того как ноды поднимутся, получите список всех нод в вашем локальном кластере</strong></summary>

        kubectl get nodes

</details>
<details>
  <summary><strong>Все команды и вывод результатов выполнения этих команд отправьте ментору на проверку</strong></summary>

![Альтернативный текст](./img/img_1.png)

![Альтернативный текст](./img/img_2.png)

![Альтернативный текст](./img/img_3.png)
</details>


## Установка Minikube
<details>
  <summary><strong>Скачиваем</strong></summary>

    curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    curl -Lo minikube https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64 
</details>
<details>
  <summary><strong>Делаем исполняемым</strong></summary>

    chmod +x minikube
</details>
<details>
  <summary><strong>Перемещаем файл</strong></summary>

    sudo mv minikube /usr/local/bin/
</details>
<details>
  <summary><strong>После установки проверь</strong></summary>

    which minikube
    Должно вернуть: /usr/local/bin/minikube
    minikube version
</details>
<details>
  <summary><strong>сброс пароля</strong></summary>

    passwd
</details>

## Запустите Minikube 
<details>
  <summary><strong>Используя Docker-драйвер (рекомендуется) </strong></summary>

    minikube start --driver=docker
    minikube start --nodes=5 --driver=docker
    💡 Предупреждение:
    ❗ /usr/local/bin/kubectl is version 1.29.2, which may have incompatibilities with Kubernetes 1.33.1.
    ▪ Want kubectl v1.33.1? Try 'minikube kubectl -- get pods -A'

    Это важное замечание:
    Версия установленного у тебя kubectl (v1.29 ) немного младше версии Kubernetes в кластере (v1.33 ).
    В большинстве случаев это не критично, но если ты хочешь использовать совместимую версию kubectl , 
    используй команду:
        minikube kubectl -- get pods -A
    Либо установи более свежий kubectl отдельно, чтобы он соответствовал версии кластера. 

</details>

<details>
  <summary><strong>Проверка состояния кластера</strong></summary>

    kubectl get nodes
    Ожидаемый вывод:
        NAME       STATUS   ROLES           AGE   VERSION
        minikube   Ready    control-plane   XXs   v1.33.1

    И проверь системные поды:
    kubectl get pods -A

    Должны быть такие компоненты:
    kube-system → coredns, etcd, kube-apiserver, kube-controller-manager, kube-proxy, kube-scheduler
    kube-node-lease → информация о доступности нод
    default → storage-provisioner
     
</details>

## Как дальше использовать Minikube
<details>
  <summary><strong>Запуск собственных приложений</strong></summary>

  - **Например, запусти простое демо-приложение:**

        kubectl create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.4

  - **И открой его во внешнем доступе:**

        kubectl expose deployment hello-minikube --type=NodePort --port=8080


  - **Посмотри URL:**

        minikube service hello-minikube --url

  - **Или просто открой в браузере:**

        minikube service hello-minikube

</details>
<details>
  <summary><strong>Остановка и удаление кластера</strong></summary>

  - **Если нужно остановить кластер:**

        minikube stop

  - **Если нужно полностью удалить кластер:**

        minikube delete
        minikube delete --all

</details>

<details>
  <summary><strong>Полезные команды</strong></summary>

  - **Показывает текущее состояние кластера**

        minikube status
	
  - **Информация о кластере**

        kubectl cluster-info
	
  - **Показать все ресурсы**

        kubectl get all --all-namespaces
	
  - **Открыть веб-интерфейс Kubernetes**

        minikube dashboard
	
  - **Показать IP-адрес Minikube**

        minikube ip

</details>

<details>
  <summary><strong>Полезные команды для проверки </strong></summary>

  - **Посмотреть все namespaces**

        kubectl get namespaces

  - **Посмотреть все ресурсы во всех namespaces**

        kubectl get all --all-namespaces

  - **Посмотреть объекты Lease в kube-node-lease**
  - 
        kubectl get leases -n kube-node-lease

  - **Посмотреть поды в default (если есть)**

        kubectl get pods -n default
</details>

## Дополнительно

<details>
  <summary><strong>Dashboard Kubernetes</strong></summary>

 - **Запустите панель управления**   

        minikube dashboard
        Она автоматически откроет браузер с веб-интерфейсом
        http://127.0.0.1:37913/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/
 - **получить URL**    

        minikube dashboard --url

</details>


<details>
  <summary><strong></strong></summary>
</details>



 
 
 

