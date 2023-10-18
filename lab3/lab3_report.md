University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)  
Year: 2023/2024  
Group: K4112c  
Author: Klemesheva Anastasia Sergeevna  
Lab: Lab3  
Date of create: 11.10.2023  
Date of finished: xx.xx.xxxx

---

## Лабораторная работа №3 "Сертификаты и "секреты" в Minikube, безопасное хранение данных."
### Описание
В данной лабораторной работе вы познакомитесь с сертификатами и "секретами" в Minikube, правилами безопасного хранения данных в Minikube. 

### Цель работы
Познакомиться с сертификатами и "секретами" в Minikube, правилами безопасного хранения данных в Minikube.

### Выполнение лабораторной работы
В начале работы был создан файл конфигурации `secret-frontend.yaml`, с помощью которого были развёрнуты пространство имён, ConfigMap, ReplicaSet с двумя репликами контейнера [ifilyaninitmo/itdt-contained-frontend:master](https://hub.docker.com/repository/docker/ifilyaninitmo/itdt-contained-frontend) и сервис для доступа к ним:

![1 secret-frontend](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/48e7f762-f157-42dc-b328-f013ed393206)

В configMap заданы значения переменных `REACT_APP_USERNAME` и `REACT_APP_COMPANY_NAME`, которые передаются в ReplicaSet:

![configmap](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/41c8ab06-63ea-4a6b-92a8-c4b210539151)

![replicaset](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/79b1096a-f0ba-49cb-befe-dae4765200f9)

Затем был включен Ingress и сгенерирован сертификат tls. Полученные публичный и приватный ключи были прописаны в конфигурационном файле секрета, таким образом сертификат был добавлен в пространство имён, где разворачивается наше веб-приложение.

![включаение ингресс](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/7fa558e6-10cc-4424-bdda-e0a1114d4181)

![создание секрета](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/f5c7c53d-2ab4-4396-b7df-767593ab0ec0)

Секрет, FQDN и сервис были прописаны в ingress:

![ingress](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/0de368ee-dacd-4c19-84a3-c305d9a31150)

![сощздание ингресс](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/399f966f-2cf6-47f6-b489-fe2102d63232)

Затем был запущен `minikube tunnel`:
 
![minikube tunnel](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/5225ad9c-5b8c-4f46-ad74-2214543b3fa5)

В `hosts` были прописаны FQDN и IP-адрес Minikube: 

![hosts](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/17a4ec25-4519-4408-8cf4-533e1fa78c82)

Теперь можно зайти в веб-приложение через браузер:

![Приложение работает](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/5888c770-4116-47de-892f-1b99706194e0)

Просмотр сертификата:

![скрин сертификата1](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/266719cf-9553-4686-b8d4-4018c4f477b3)
  
![скрин сертификата2](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/bf1f7122-c345-41c1-a748-e543aa1fe673)

Схема организации контейеров и сервисов:

![Схема_лаб3 drawio](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/ae641da3-1702-48d5-b43e-d14cb04d7472)



