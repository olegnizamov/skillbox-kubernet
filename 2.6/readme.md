## 2.6 Практическая работа

[](https://go.skillbox.ru/education/course/devops-kubernetes/a5ac13fe-5051-4023-a14b-c26c752e77ab)

## Цель домашнего задания

Pods — основные строительные элементы Kubernetes, и большая часть работы DevOps-инженера связана с их запуском, апдейтом и устранением неисправностей. Поэтому цель этой домашней работы — закрепить знания о pods и отработать основные операции с ними: создание, обновление и траблшутинг. Это заложит фундамент для дальнейшего обучения, так как практически все остальные объекты Kubernetes связаны с pods.

### Что нужно сделать

NB: Все задания выполняются в minikube кластере версии не ниже 1.0.0.

### Задание 1

создайте файл pod.yaml и скопируйте в него следующий манифест:

```
apiVersion: v1
kind: Pod
metadata:
 name: my-nginx
spec:
 containers:
   name: nginx-container
   image: nginx:1.10
```

* попробуйте создать из этого манифеста pod с помощью команды kubectl create -f pod.yaml
* kubectl не может применить yaml-файл, в чём ошибка?

Ответ:
![1.png](1.png)
некорректный синтаксис файла. Перед  name: nginx-container должен быть знак "-".

как исправить - добавить знак, перезапустить создание через kubectl create -f pod.yaml

![2.png](2.png)


### Задание 2

* запустите pod redis в кластере с помощью команды: kubectl run redis --image=redis:5.0 -n default
* проверьте, что redis запустился и находится в статусе Running, с помощью команды: kubectl get pods -n default
* удостоверьтесь, что версия docker image — redis:5.0, с помощью команды: kubectl get pod redis -n default -o jsonpath=”{..image}”
* отредактируйте pod redis с помощью команды kubectl edit pod redis -n default так, чтобы версия docker image стала redis:6.0
  Примечание: вы можете изменять текстовый редактор, используемый командой kubectl edit по умолчанию, с помощью переменной окружения KUBE_EDITOR — например, export KUBE_EDITOR=nano или export KUBE_EDITOR=vim.
* сохраните изменения и проверьте логи контейнера с помощью команды: kubectl logs redis -n default

Изменилась ли версия контейнера?

Ответ:
![3.png](3.png)
