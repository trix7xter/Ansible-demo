## Описание

Проект, разворачивающий на локальной машине Grafana, Cadvisor, Victoria-metrics в docker-контейнерах.
Кроме того, в рамках установки проекта происходит установка (обновление) зависимостей и создание пользователя.

Сборка предназначена для виртуальной машины на базе Debian 11 (bullseye)

Для запуска необходим ansible-core версии 2.11 и старше, установленные коллекции docker и general

Для установки коллекций нужно выполнить команды:
`ansible-galaxy collection install community.docker`
`ansible-galaxy collection install community.general`

## Данные и переменные

Дефолтные данные создаваемого аккаунта:
login: `login`, password: `password`

Дефолтные данные для сервисов:
login: `admin`, password: `password1`

- [ ] В рамках учебного приложения используется универсальный логин и пароль для cAdvisor, grafana и victoriametrics (universe_login и universe_password)
- [ ] Для создания пользователя используются переменные user_login, user_password
- [ ] Для редактирования переменных необходимо расшифровать файл vars с помощью ansible vault

Пароль для декрипта `cloudpassword123`
```
ansible-vault decrypt vars.yaml          # для декрипта vars.yaml
ansible-vault encrypt vars.yaml          # для шифрования vars.yaml
```

## Установка 

- Для установки требуется выполнить команду `ansible-playbook playbook.yaml --ask-become-pass --ask-become-pass`
- Введите пароль пользователя и пароль для декрипта (`cloudpassword123`)

## Следующие приложения будут установлены и развернуты: 

* Docker  
* cAdvisor (порт 8080)
* victoriaMetrics (порт 8428)
* grafana (порт 3000)
* alertmanager (порт 9093)
* vmalert (порт 8880)

## Проверка работы

1. Выполнить установку приложения
2. Авторизоваться под созданным пользователем (по умолчанию данные login/password)
3. Перейти на localhost:3000/
4. Авторизоваться под универсальным логином и паролем для приложений (по умолчанию данные admin/password1)
5. Проверить отображение добавленного дашборда