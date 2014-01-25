Виртуальная машина для веб-разработки
----------

Виртуальная машина основата на утилите Vagrant, для работы нужно следующее:
 - [Vagrant](http://www.vagrantup.com/downloads.html)
 - [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

После развертывания, запускается из консоли командой `vagrant up` либо командным файлом `bin\up.bat`. 
После этого начинается процесс инициализации, который длится достаточно долго, инициализация производится только при первом запуске.

Во время инициализации из интернета скачивается некоторое количество мегабайт, так что нужен неплохой интернет.
Подробнее о работе с утилитой можно почитать [здесь](http://habrahabr.ru/post/113354/). Описание установки и настройки можно пропустить.

После окончания работы машину нужно корректно выключить командой `vagrant halt`, доступ к виртуальному серверу можно получить с помощью `vagrant ssh` или напрямую - адрес машины `192.168.2.10`.

Сервер предоставляет следующие сервисы:
 - Веб-сервер (Apache 2 + PHP 5.4),
 - MySQL
 - PostgreSQL
 - Redis
 - Memcached
 - DNS
 
Так же внутри настроены SQLite, Vim, Python PIP, PHP Pear и другие приятные вещи.

Для пользователя `root` в MySQL и пользователя `postgres` в PostgreSQL установлен пароль `password`.


Параметры, утилиты и командные файлы
-----------
Параметры хранятся в файле `params.ini`, эти параметры распространяются как на виртуальную машину, так и на утилиты.

В каталоге `bin` находятся утилиты и командные файлы.

Виртуальный сервер автоматически определяет DocumentRoot по заголовку Host, используется принцип `(?P<document_root>.+?)\.loc`.
По умолчанию он ищет сайты в каталоге `D:\htdocs` для Windows и `/var/www` для Unix-like систем, это можно изменить в файле `params.ini`.
IP-адрес виртуальной машины в закрытой виртуальной сети по умолчанию `192.168.2.10`, его можно изменить в файле `params.ini`, после его изменения требуется повторить `vagrant provision`.

Чтобы браузер в Windows корректно открывал сайты в зоне .loc, можно указать в качестве DNS-сервера `192.168.2.10`, но это может (и скорее всего так и будет) привести к замедлению работы интернета.

Альтернативой этому является использование утилиты PatchHosts, которая просматривает папку `D:\htdocs` и дописывает все нужные домены в файл `hosts`.

В случае, если утилита не сможет записать файл самостоятельно (в Windows 8.1 это всегда так, даже с правами администратора), 
она покажет нужный контент в блокноте, в этом случае нужно скопировать нужные значения вручную в файл `hosts`.
