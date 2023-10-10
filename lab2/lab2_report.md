University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)  
Year: 2023/2024  
Group: K4112c  
Author: Klemesheva Anastasia Sergeevna  
Lab: Lab2  
Date of create: 06.10.2023  
Date of finished: xx.xx.xxxx 

---

## Лабораторная работа №2 "Развертывание веб сервиса в Minikube, доступ к веб интерфейсу сервиса. Мониторинг сервиса."
### Описание

В данной лабораторной работе предполагается знакомство с развертыванием полноценного веб сервиса с несколькими репликами. 

### Цель работы

Ознакомиться с типами "контроллеров" развертывания контейнеров, ознакомиться с сетевыми сервисами и развернуть свое веб приложение. 

### Ход работы

- Создать `deployment` с 2 репликами контейнера [ifilyaninitmo/itdt-contained-frontend:master](https://hub.docker.com/repository/docker/ifilyaninitmo/itdt-contained-frontend) и передать переменные в эти реплики: `REACT_APP_USERNAME`, `REACT_APP_COMPANY_NAME`.

- Создать сервис, через который у вас будет доступ на эти "поды". Выбор типа сервиса остается на ваше усмотрение. 

- Запустить в `minikube` режим проброса портов и подключиться к вашим контейнерам через веб браузер.

- Проверить на странице в веб браузере переменные `REACT_APP_USERNAME`, `REACT_APP_COMPANY_NAME` и `Container name`. Изменяются ли они? Если да то почему?

- Проверить логи контейнеров, приложить логи в отчёт.

### Выполнение лабораторной работы

Был проведен запуск minikube:  

![1 запуск миникуба](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/3edb380b-15ea-4e59-a5ff-e8f8b86179ed)  

Создан манифест deployment с 2 репликами контейнера [ifilyaninitmo/itdt-contained-frontend:master](https://hub.docker.com/repository/docker/ifilyaninitmo/itdt-contained-frontend), переменным `REACT_APP_USERNAME` и `REACT_APP_COMPANY_NAME` были присвоены значения `primellin` и `ITMO` соотвественно:  

![2 файл деплоймента](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/1cd4b322-f4f1-4bac-8343-dd165cd5af6d)

Далее был создан манифест сервиса:  

![3 файл сервиса](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/a33675c2-6f79-4f46-9414-c3fff0219e68)

После этого было создано пространство имен:  

![3 5 пространство имен](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/01fc6c65-55c2-4bdf-ab8b-822935017e47)  

![4 развертывание пространства имен](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/df17278c-fdbf-457d-8d5b-734844370496)

Создан деплоймент и сервис типа `NodePort` для доступа к его контейнерам:  

![5 развертывание деплоймента](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/7073c168-ac30-45e7-96ca-64dba5ee4241)  

![6 создание сервиса](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/1d1b62f6-6b7f-4658-abd3-4c5dfa15b6cf)  

Прокидывание порта:  

![7 прокидывание порта](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/c2737196-d20e-488c-ae30-29ef6abcb09a)  

Теперь приложение можно открыть с помощью веб-браузера. На странице отображаются заданные в манифесте деплоймента значения переменных `REACT_APP_USERNAME` и `REACT_APP_COMPANY_NAME`, IP и название контейнера, на который идет запрос:

![8 приложение работает](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/b7af2b6e-8565-4b82-ab9e-2a099c71b644)  

Список контейнеров:  

![9 1 перечень подов](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/d676455c-24d8-419f-8387-bcf372d66e82)

Логи у них одинаковые:

![логи первого](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/0e8b768a-00cc-4df9-ae6f-b678ac5abb37)  

![10 логи второго контейнера](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/082a28d0-b606-4fbf-b30c-32c2151a4da4)

Схема организации контейеров и сервисов:  

![Схема_2лаб](https://github.com/primellin/2023_2024-introduction_to_distributed_technologies-K4112c-klemesheva_a_s/assets/88944945/68847729-251d-4201-ae3d-cd4df764dedc)
