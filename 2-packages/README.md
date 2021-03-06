##Управление пакетами	

####Yum/Apt, установка, удаление, пересборка пакетов. Определение файлов в пакетах и зависимостей. Описание spec-файлов. Прочие пакетные менеджеры, pip, npm и т.п.	

Система управления пакетами(СУП) или Пакетный менеджер(ПМ) - Специальное ПО для расширения возможностей 
ОС посредством установки подолнительного ПО и зависимостей.

Наиболее популярный менеджер пакетов Linux, использующий систему управления RPM - YUM и
APT в основе которого используется DPKG работающий в Debian. Кроме того, 
вокруг популярных языков программирования созданы собственные менеджеры пакетов, 
обеспечивающие установку приложений на этих языках и необходимых библиотек, 
среди популярных: 
- Composer (PHP)
- NPM (JavaScript, менеджер пакетов в составе Node.js)
- Pip (Python)
- Gem (Ruby)

При наличии установленного языка в системе, с помощью его менеджера, можно установить 
любой софт написанный на этом языке. Как правило, система управления пакетами работает со 
множеством пакетов, хранящихся в репозитории — хранилище, которое может располагаться на запоминающих устройствах, 
флешке или жёстком диске или на удалённой машине в интернете. Каждый пакет имеет в своем составе, 
исходный код программы или скомпилированный файл совместимый с ядром где работает ПМ.
Помимо этого пакет содержит набор определённых метаданных(spec), которые могут включать в себя полное имя пакета, 
описание пакета, имя разработчика, контрольную сумму, отношения с другими пакетами. 
Метаданные сохраняются в системной базе данных пакетов называемых "cache".

Как правило к любому пакету, в том числе ПМ предоставляется справка по использованию. 
Вызвать справку можно передав в качестве аргумента "help" или "--help"
или "-h"
Например:
~~~shell script
apt help
apt --help
apt -h
~~~
Выведет информацию с помощью о использовании программы.

В этой директории вы найдете файлы для управления пакетами в дистрибутивах на базе Debian и Redhat.

###Обработка ошибок
Бывает, что возникают ошибки на ровном месте. К примеру сразу после установки чистой системы отказывается работать yum или apt
Первым делом проверяется сеть, если доступ к зеркалам есть, то идем дальше.
Большинство остальных ошибок лечатся банальным удалением кэша.
```shell script
rpm -rf /etc/yum.repos.d/*
rm -rf /var/cache/*
```

Команда удаления, поддерживает опцию --test. Если от пакета зависит большое число установленного ПО, можно проверить, 
какие приложения и библиотеки утратят свою работоспособность ```rpm e --test syslinux```

Некоторые пакеты могут предоставлять возможности, которые пересекаются с похожими от других пакетов. Такая ситуация называется 
конфликтом и обрабатывается форсированным методом. Попытка установки конфликтующего пакета приведет к ошибке. 
Например, пакет httpd, содержащий веб-сервер Apache, конфликтует с пакетом thttpd. Оба этих пакета предоставляют 
системе предпочитаемый веб-сервер. Конфликт можно обойти с помощью опций форсирования установки, но с точки зрения 
функционала это как правило приводит к ошибкам стадии выполнения. Передайте менеджеру пакетов флаг -f для принудительной
установки.
[Go back](https://github.com/AlexCollin/linux-short-lesson)