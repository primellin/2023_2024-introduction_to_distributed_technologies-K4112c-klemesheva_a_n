University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)  
Year: 2023/2024  
Group: K4112c  
Author: Klemesheva Anastasia Sergeevna  
Lab: Lab4  
Date of create: 28.10.2023  
Date of finished: xx.xx.xxxx

---

## Лабораторная работа №4 "Сети связи в Minikube, CNI и CoreDNS"
### Цель работы

Познакомиться с CNI Calico и функцией `IPAM Plugin`, изучить особенности работы CNI и CoreDNS.

### Ход работы

Запускаем кластер с двумя нодами и установливаем плагин `CNI Calico`:

![1](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/0f2138bf-3e9f-4875-9b7a-2cba4a8600fb)

Проверим наличие двух подов Calico и двух нод:

![2](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/701fa13f-4117-40d5-97ba-5634d1375bf9)

Притворимся, что у нас есть две стойки, и назначим нодам соответствующие их номерам метки:

![3](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/55b37e2b-6b56-4b39-a284-9b0c5dcf0d87)

С помощью команды `kubectl describe nodes` проверим, что наши метки успешно назначены, и действительно, они находятся в конце списка всех меток нод:

![5](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/e538d577-c29a-4119-a603-e772b224b069)

![4](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/7511bdb8-bc5d-4304-8a62-721b03c475b4)

По умолчанию Calico создает свой IPPool, удалим его и проверим, что он действительно удален:

![6](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/8eb4375d-d02a-4283-86ea-7378d85990b1)

![7](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/81d451d4-b169-4ac2-ae91-ecfdbf465366)

Затем создадим свои, по одному для каждой ноды, указав ранее заданные метки нод в качестве селектора.

![ippool](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/4a7b18d3-0f80-4763-8c59-25f0e69ee898)

![8](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/c2d289fb-59e6-4682-aa97-53bc8187e316)

Проверяем, что они и правда созданы:

![9](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/11ad409e-d4a1-404b-af0a-78ab2b2a2430)

Разворачиваем `Namespace`, `Deployment` с двумя репликами контейнера и `Service` для доступа к ним. Манифест находится в файле frontend.yaml.

![10](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/cb436b14-55ac-4c59-a953-58f3908453ee)

Поды развернулись на двух нодах, этим подам были назначены IP-адреса, соответствующие диапазонам, которые мы указали в IPPool.

![11](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/3c268c8d-3066-4cc5-9fda-a743017924d5)

Прокидываем порт, благодаря этому получаем доступ к приложению через браузер.

![12](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/3288f88c-d9a0-4fa5-8aa2-17ac8cc26545)

На странице приложения видим имя и IP-адрес пода. По ним понимаем, что приложение сейчас работает в поде `frontend-7cc6876ffb-d5dms` с IP-адресом `192.168.0.65` на ноде `minikube`. Значения имени и IP-адреса поменялись бы, если бы приложение работало на другой ноде, `minikube-m02`, в поде `frontend-7cc6876ffb-tg4fl` с IP-адресом `192.168.1.0`.

![13](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/b92c0fbf-e46c-46f9-94fc-8ee09338b696)

![11](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/c4c73c1d-6ae7-4574-8fa0-778076ef7ab2)

Заходим в один из подов, узнаем FQDN второго пода и по нему пингуем его:

![14](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/e04ac73f-99c6-459a-9c08-158659bb5495)

Схема организации контейеров и сервисов:

![Scheme](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/f94c9a9f-4fb6-4d6d-88e8-26bd89caed69)

