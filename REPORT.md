## Laboratory work IV

Данная лабораторная работа посвещена изучению систем непрерывной интеграции на примере сервиса **Travis CI**

```sh
$ open https://travis-ci.org
```

## Tasks

- [x] 1. Авторизоваться на сервисе **Travis CI** с использованием **GitHub** аккаунта
- [x] 2. Создать публичный репозиторий с названием **lab04** на сервисе **GitHub**
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Включить интеграцию сервиса **Travis CI** с созданным репозиторием
- [x] 5. Получить токен для **Travis CLI** с правами **repo** и **user**
- [x] 6. Получить фрагмент вставки значка сервиса **Travis CI** в формате **Markdown**
- [x] 7. Выполнить инструкцию учебного материала
- [x] 8. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
# Создаем перменную с именем пользователя на GitHub
$ export GITHUB_USERNAME=tishchka
# Создаем переменную с токеном
$ export GITHUB_TOKEN=****************************************
```

```sh
# Переходим в директорию workspace
$ cd ${GITHUB_USERNAME}/workspace
# Запоминаем текущий каталог в виртуальном стеке каталогов
$ pushd .
# Исполняем команду из файла scripts/activate
$ source scripts/activate
```

```sh
# Переходим по данной ссылке и читаем команды, игнорируя точечные файлы
$ \curl -sSL https://get.rvm.io | bash -s -- --ignore-dotfiles
Installing RVM to /home/tishchka/.rvm/
Installation of RVM in /home/tishchka/.rvm/ is almost complete:

  * To start using RVM you need to run `source /home/tishchka/.rvm/scripts/rvm`
    in all your open shell windows, in rare cases you need to reopen all shell windows.
Thanks for installing RVM 🙏
Please consider donating to our open collective to help us maintain RVM.

👉  Donate: https://opencollective.com/rvm/donate

# Записываем новую команду в scripts/activate
$ echo "source $HOME/.rvm/scripts/rvm" >> scripts/activate

# Исполняем команды в из этого файла
$ . scripts/activate

# Отключаем автоматическое управление зависимостями
$ rvm autolibs disable

# Устанавливаем ruby
$ rvm install ruby-2.4.2
Searching for binary rubies, this might take some time.
Found remote file https://rvm_io.global.ssl.fastly.net/binaries/ubuntu/20.04/x86_64/ruby-2.4.2.tar.bz2
ruby-2.4.2 - #configure
ruby-2.4.2 - #download
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 18.7M  100 18.7M    0     0   187k      0  0:01:42  0:01:42 --:--:-- 2351k
ruby-2.4.2 - #validate archive
ruby-2.4.2 - #extract
ruby-2.4.2 - #validate binary
ruby-2.4.2 - #setup
ruby-2.4.2 - #gemset created /home/gndavydov/.rvm/gems/ruby-2.4.2@global
ruby-2.4.2 - #importing gemset /home/gndavydov/.rvm/gemsets/global.gems..................................
ruby-2.4.2 - #generating global wrappers........
ruby-2.4.2 - #gemset created /home/gndavydov/.rvm/gems/ruby-2.4.2
ruby-2.4.2 - #importing gemsetfile /home/gndavydov/.rvm/gemsets/default.gems evaluated to empty gem list
ruby-2.4.2 - #generating default wrappers........

# Устанавливаем версию по умолчанию
$ rvm use 2.4.2 --default
Using /home/gndavydov/.rvm/gems/ruby-2.4.2

# Устанавливаем travis
$ gem install travis
Fetching faraday-1.3.0.gem
Fetching highline-2.0.3.gem
Fetching i18n-1.8.9.gem
Fetching multipart-post-2.1.1.gem
Fetching ruby2_keywords-0.0.4.gem
Fetching faraday_middleware-1.0.0.gem
Fetching addressable-2.7.0.gem
Fetching faraday-net_http-1.0.1.gem
Fetching concurrent-ruby-1.1.8.gem
Fetching net-http-persistent-2.9.4.gem
Fetching net-http-pipeline-1.0.1.gem
Fetching multi_json-1.15.0.gem
Fetching public_suffix-4.0.6.gem
Fetching thread_safe-0.3.6.gem
Fetching json_pure-2.5.1.gem
Fetching pusher-client-0.6.2.gem
Fetching tzinfo-1.2.9.gem
Fetching gh-0.18.0.gem
Fetching activesupport-5.2.5.gem
Fetching launchy-2.4.3.gem
Fetching travis-1.10.0.gem
Fetching websocket-1.2.9.gem
Successfully installed faraday-net_http-1.0.1
Successfully installed multipart-post-2.1.1
Successfully installed ruby2_keywords-0.0.4
Successfully installed faraday-1.3.0
Successfully installed faraday_middleware-1.0.0
Successfully installed highline-2.0.3
Successfully installed concurrent-ruby-1.1.8
Successfully installed i18n-1.8.9
Successfully installed thread_safe-0.3.6
Successfully installed tzinfo-1.2.9
Successfully installed activesupport-5.2.5
Successfully installed multi_json-1.15.0
Successfully installed public_suffix-4.0.6
Successfully installed addressable-2.7.0
Successfully installed net-http-persistent-2.9.4
Successfully installed net-http-pipeline-1.0.1
Successfully installed gh-0.18.0
Successfully installed launchy-2.4.3
Successfully installed json_pure-2.5.1
Successfully installed websocket-1.2.9
Successfully installed pusher-client-0.6.2
Successfully installed travis-1.10.0
Parsing documentation for faraday-net_http-1.0.1
Installing ri documentation for faraday-net_http-1.0.1
Parsing documentation for multipart-post-2.1.1
Installing ri documentation for multipart-post-2.1.1
Parsing documentation for ruby2_keywords-0.0.4
Installing ri documentation for ruby2_keywords-0.0.4
Parsing documentation for faraday-1.3.0
Installing ri documentation for faraday-1.3.0
Parsing documentation for faraday_middleware-1.0.0
Installing ri documentation for faraday_middleware-1.0.0
Parsing documentation for highline-2.0.3
Installing ri documentation for highline-2.0.3
Parsing documentation for concurrent-ruby-1.1.8
Installing ri documentation for concurrent-ruby-1.1.8
Parsing documentation for i18n-1.8.9
Installing ri documentation for i18n-1.8.9
Parsing documentation for thread_safe-0.3.6
Installing ri documentation for thread_safe-0.3.6
Parsing documentation for tzinfo-1.2.9
Installing ri documentation for tzinfo-1.2.9
Parsing documentation for activesupport-5.2.5
Installing ri documentation for activesupport-5.2.5
Parsing documentation for multi_json-1.15.0
Installing ri documentation for multi_json-1.15.0
Parsing documentation for public_suffix-4.0.6
Installing ri documentation for public_suffix-4.0.6
Parsing documentation for addressable-2.7.0
Installing ri documentation for addressable-2.7.0
Parsing documentation for net-http-persistent-2.9.4
Installing ri documentation for net-http-persistent-2.9.4
Parsing documentation for net-http-pipeline-1.0.1
Installing ri documentation for net-http-pipeline-1.0.1
Parsing documentation for gh-0.18.0
Installing ri documentation for gh-0.18.0
Parsing documentation for launchy-2.4.3
Installing ri documentation for launchy-2.4.3
Parsing documentation for json_pure-2.5.1
Installing ri documentation for json_pure-2.5.1
Parsing documentation for websocket-1.2.9
Installing ri documentation for websocket-1.2.9
Parsing documentation for pusher-client-0.6.2
Installing ri documentation for pusher-client-0.6.2
Parsing documentation for travis-1.10.0
Installing ri documentation for travis-1.10.0
Done installing documentation for faraday-net_http, multipart-post, ruby2_keywords, faraday, faraday_middleware, highline, concurrent-ruby, i18n, thread_safe, tzinfo, activesupport, multi_json, public_suffix, addressable, net-http-persistent, net-http-pipeline, gh, launchy, json_pure, websocket, pusher-client, travis after 16 seconds
22 gems installed
```

```sh
# Клонируем репозиторий, созданный во 3-ей лабораторной
# в папку с лабораторной №4
$ git clone https://github.com/${GITHUB_USERNAME}/lab03 projects/lab04
loning into 'projects/lab04'...
remote: Enumerating objects: 22, done.
remote: Counting objects: 100% (22/22), done.
remote: Compressing objects: 100% (14/14), done.
remote: Total 22 (delta 2), reused 22 (delta 2), pack-reused 0
Unpacking objects: 100% (22/22), 3.69 KiB | 943.00 KiB/s, done.

# Переходим в созданную директорию
$ cd projects/lab04
# Удаляем ссылку на репозиторий 3-ей лабораторной
$ git remote remove origin
# Добывляем ссылку с именем origin на созданный репозиторий 4-ей лабораторной
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab04
```

```sh
# Устанавливаем настройки сборки для travis
$ cat > .travis.yml <<EOF
language: cpp
EOF
```

```sh
$ cat >> .travis.yml <<EOF

script:
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build
- cmake --build _build --target install
EOF
```

```sh
$ cat >> .travis.yml <<EOF

addons:
  apt:
    sources:
      - george-edison55-precise-backports
    packages:
      - cmake
      - cmake-data
EOF
```

```sh
# Логинемся на Travis
$ travis login --github-token ${GITHUB_TOKEN}
Shell completion not installed. Would you like to install it now? |y| y
Successfully logged in as GNDavydov!
```

```sh
# Проверяем на отсутствие предупрежденй для .travis.yml
$ travis lint
Hooray, .travis.yml looks valid :)
```

```sh
# Вставляем в README.md иконку Travis
$ ex -sc '1i|[![Build Status](https://travis-ci.org/GNDavydov/lab04.svg?branch=main)](https://travis-ci.org/GNDavydov/lab04)' -cx README.md
```

```sh
# Добавляем файлы для отслеживания
$ git add .travis.yml
$ git add README.md

# Делаем коммит
$ git commit -m"added CI"
[main 81f084f] added CI
 2 files changed, 16 insertions(+), 1 deletion(-)
 create mode 100644 .travis.yml

# Отправляем изменения на удаленный репозиторий
$ git push origin main
Username for 'https://github.com': tishchka
Password for 'https://tishchka@github.com': 
Enumerating objects: 26, done.
Counting objects: 100% (26/26), done.
Delta compression using up to 2 threads
Compressing objects: 100% (20/20), done.
Writing objects: 100% (26/26), 4.23 KiB | 1.06 MiB/s, done.
Total 26 (delta 3), reused 0 (delta 0)
remote: Resolving deltas: 100% (3/3), done.
To https://github.com/GNDavydov/lab04
 + 729a08a...81f084f main -> main (forced update)

```

```sh
$ travis lint
Hooray, .travis.yml looks valid :)

# Показывает аккаунты и кол-во репозиториев в них
$ travis accounts
tishchka (tishchka): subscribed, 3 repositories

# Синхронизируем с GitHub
$ travis sync
synchronizing: . done

# Выводим доступные репозитории
$ travis repos
tishchka/lab02 (active: no, admin: yes, push: yes, pull: yes)
Description: TIMP Lab02

tishchka/lab03 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

tishchka/lab04 (active: yes, admin: yes, push: yes, pull: yes)
Description: ???

# Делаем проект доступным
$ travis enable
Detected repository as tishchka/lab04, is this correct? |yes| yes
tishchka/lab04: enabled :)

# Перечисляем последние сборки
$ travis whatsup
tishchka/lab04 passed: #1

# Выводим последние сборки для каждой ветки
$ travis branches
main:  #1    passed     added CI

# Выводим историю сборок
$ travis history
#1 passed:       main added CI

# Отображаем информацию о сборке
$ travis show
Job #1.1:  added CI
State:         passed
Type:          push
Branch:        main
Commit:        81f084f
Compare URL:   https://github.com/GNDavydov/lab04/compare/729a08aa6d40...81f084f56c4c
Duration:      38 sec
Started:       2021-03-28 03:40:40
Finished:      2021-03-28 03:41:18
Allow Failure: false
Config:        os: linux

```

## Report

```sh
$ popd
$ export LAB_NUMBER=04
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Homework

Вы продолжаете проходить стажировку в "Formatter Inc." (см [подробности](https://github.com/tp-labs/lab03#Homework)).

В прошлый раз ваше задание заключалось в настройке автоматизированной системы **CMake**.

Сейчас вам требуется настроить систему непрерывной интеграции для библиотек и приложений, с которыми вы работали в [прошлый раз](https://github.com/tp-labs/lab03#Homework). Настройте сборочные процедуры на различных платформах:
* используйте [TravisCI](https://travis-ci.com/) для сборки на операционной системе **Linux** с использованием компиляторов **gcc** и **clang**;
* используйте [AppVeyor](https://www.appveyor.com/) для сборки на операционной системе **Windows**.

## Links

- [Travis Client](https://github.com/travis-ci/travis.rb)
- [AppVeyour](https://www.appveyor.com/)
- [GitLab CI](https://about.gitlab.com/gitlab-ci/)

```
Copyright (c) 2015-2021 The ISC Authors
```
