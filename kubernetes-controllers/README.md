# Второе домашнее задание(ДЗ).
## Запуск и проверка
Проверялось на версии minikube 1.35, kubectl 1.32 на VM с Ubuntu 24.04
1. Клонируем ветку kubernetes-controllers туда, где есть настроенный minikube и kubectl.
2. Создаем новый namespace
```
kubectl apply -f kubernetes-controllers/namespace.yaml
```
3. Проверяем, что namecpace создался
```
kubectl get ns
```
4. Создаем деплоймент
```
kubectl apply -f kubernetes-controllers/deployment.yaml
```
5. Проверяем, что деплоймент создался
```
kubectl get deployment -n homework
```
6. Проверяем pod-ы в deployment. Поскольку в nemespace только один deployment - просто смотрим pod в namespace
```
kubectl get pod -n homework
```
![Видим, что все поды в статусе Pending](screenshots/otus_2nd_hw_01.jpg)

7. Добавляем метку на хост minikube
```
kubectl label node minikube homework='true'
```
8. Выполняем пункт 6. Для проверки подов. ЗАДАНИЕ СО * ВЫПОЛНЕНО.
![Видим, чтоб поды в статусе Running и после проверки Rediness Probe, поды станут Ready](screenshots/otus_2nd_hw_02.jpg)

9. Проверка доступности вебсервера. Включаем порт форвард
```
kubectl port-forward deployment/depl-wserver -n homework --address 0.0.0.0 8000:8000
```
10.  Переходим по адресу http://IP_minikube_host:8000
![Страница доступна](screenshots/otus_2nd_hw_04.jpg)
11.  Проверка Rolling Update. В манифесте kubernetes-controllers/deployment.yaml поменять что-нить в генерации index.html
12. Обновить deployment, используя команду из пункта 4.
13. Проверить поды в namespace.


![](screenshots/otus_2nd_hw_03.jpg)

В стратегии RollingUpdate стоит недоступность максимум одного контейнера, но можно при апдейте поднимать два дополнительных.

