Role Name
=========

Автоматическая установка ELKF стака по заданию.

Задание
-------

1. Подготовить Docker-образы ElasticSearch, Kibana, Logstash, Filebeat 6.7.2 и 7.7.0 версий
2. С помощью ansible уметь моментально разворачивать стек ELKF обоих версий
3. Filebeat:
   1. собрать логи из файла test.log
   2. из контейнера filebeat с помощью module:docker
   3. написать 2 конфига для output: в файл и в logstash
4. Lostash:
   1. настроить input на прием через порт
   2. в filter:
      1. обработать логи из test.log (разделить строку на следующие поля: Time, Priority, Logger, RandomNumber, RandomSymbol Message)
      2. из логов контейнера filebeat: убрать лишние поля (log.file.path, prospector.type, docker.container.id, docker.container.image); переименовать: host.name => host, message => Message; добавить в tags значение из docker.container.name (убрать соответвенно docker.container.name)
   3. в output логи из test.log отправить в ElasticSearch в индекс test-%Y.%m.%d, а логи файлбита записать в файл logstash-output.log
5. **TODO** В ElasticSearch подготоваить template для индекса test-* для 6.7.2 и 7.7.0 версий
6. В Kibana:
   1. сохранить поисковый запрос по индексу test-* за последние 12 часов, где выведены все поля, обработанные в Logstash
   2. создать визуализацию, в которой указывается кол-во документов для каждого значения поля Priority
   3. такую же визуализацию, но уже для поля Logger
   4. создать dashboard, в котором будут отображаться все выше перечисленные запросы и визуализации

Requirements
------------

Предполагается, что на хосте уже установлен docker.

У пользователя от имени которого подключаемся есть права sudo `%sudo   ALL=(ALL:ALL) NOPASSWD:ALL`. Подключение по ключам ssh.

Тестировалось на хосте с Debian 12.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
