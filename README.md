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

## Задание D2.4.2
<details>
  <summary><strong>Описание:</strong></summary>

    Сообщество Kubernetes объявило, что в конце 2021 года Docker в качестве среды выполнения контейнеров 
    будет объявлен как устаревший и не будет использоваться в K8S-кластере. 
    Но Kind, который поднимает K8S-кластер на Docker, говорит о том, 
    что в отношении поддержки работы кластера K8S беспокоиться не стоит.

</details>
<details>
  <summary><strong>Задание:</strong></summary>

    Почему Kind говорит, что это изменение его не затронет?

</details>
<details>
  <summary><strong>Ответ:</strong></summary>

    Сообщество Kubernetes действительно объявило, что Docker в качестве среды выполнения контейнеров 
    будет объявлен устаревшим к концу 2021 года 

    Это связано с тем, что Docker не является CRI-совместимым (Container Runtime Interface), 
    и для его использования внутри K8s-кластера требуется специальный шим — Dockershim. 
    Удаление Dockershim из Kubelet означает, что Docker больше не может быть использован 
    как runtime в K8s без дополнительных инструментов. 

    Однако kind  (Kubernetes IN Docker) говорит, что это изменение его не затронет, 
    потому что он использует Docker не как контейнерный runtime для узлов кластера , 
    а как средство для запуска контейнеров, представляющих узлы самого кластера . То есть: 

    kind создает локальный K8s-кластер, где каждый узел — это отдельный контейнер Docker ;
    внутри этих контейнеров kind использует уже CRI-совместимые runtimes , 
    такие как containerd или CRI-O, которые и управляют контейнерами приложений 

    Таким образом, даже после удаления поддержки Docker как контейнерного рантайма в K8s, 
    kind продолжает использовать Docker только на уровне хоста для создания и управления узлами-контейнерами , 
    но не для запуска контейнеров внутри кластера. Это делает изменения в K8s невлияющими на работоспособность kind. 

    Кроме того, kind официально заявляет, что поддерживает сборку и запуск кластеров из исходников Kubernetes, 
    а также совместим с Linux, macOS и Windows, что усиливает его гибкость и надежность 
    вне зависимости от изменений в основной кодовой базе Kubernetes

    Поэтому в отношении поддержки работы кластера K8S с помощью kind беспокоиться не стоит : 
    он не зависит от внутренней политики K8s по отношению к Docker как рантайму, 
    так как использует Docker лишь как платформу для запуска системных контейнеров, 
    а не как исполнительную среду для рабочих нагрузок кластера. 

</details>


<details>
  <summary><strong>Runtime (среда выполнения )</strong></summary>

    Runtime  (или среда выполнения ) — это вычислительное окружение, 
    необходимое для запуска компьютерной программы и доступное во время её выполнения. 
    Оно обеспечивает выполнение кода, управляет ресурсами, предоставляет библиотеки и 
    инструменты для работы приложения 

    Например, runtime может включать в себя:
        Менеджер памяти;
        Средства управления типами данных;
        Библиотеки, реализующие системные вызовы и стандартные функции;
        Поддержку многопоточности и обработки исключений.

    Также runtime можно рассматривать как слой абстракции между операционной системью и приложением, 
    который позволяет программе работать на виртуальной или вымышленной машине 

    Часто термин используется в контексте фреймворков и платформ, 
    например, .NET Runtime — это среда, которая выполняет код и 
    управляет классами приложений, созданных на основе .NET 

    В программировании также упоминаются runtime-компоненты  — это элементы, 
    которые обеспечивают выполнение программы непосредственно во время её запуска 

    Таким образом, runtime — это совокупность механизмов и компонентов, 
    без которых невозможно запустить и выполнить программу. 
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



 
 
 

