## Автоматизация установки антивируса Касперского на серверы с CentOS 7. 

### Окружение
    Сервер №1: OS - Centos 7 x64. IP - 10.10.10.10
    Роль: Хранилище.
    Описание: Настроен Nginx который отдает файлы по http по порту 8099 с авторизацией
    Сервер №2: OS - Centos 7 x64. IP - 10.10.10.20
    Роль: Исполнитель.
    Описание: Сервер, на котором установлен ansible
    Сервер №3: OS - Centos 7 x64. IP - 10.10.10.30
    Роль: Целевой.
    Описание: на данный сервер необходимо установить klnagent>

## Kaspersky агент администрирования
### Варианты запуска
В предложенной реализации, возможно два варианта запуска playbook. Для всех хостов, описанных в файле hosts:

    ansible-playbook service_install_klnagent_all_servers.yml --vault-password-file=/u01/ansible/secret --diff -vv 
Точечно выбирать хосты, на которые необходимо запустить роль. Если необходимо, чтобы установка запустилась на нескольких хостах, указываем их через запятую. Не забываем, что указанные хосты должны соответствовать именам в файле hosts и host_vars:

    ansible-playbook service_install_klnagent_select_servers.yml -e "host=test01" --vault-password-file=/u01/ansible/secret --diff -vv

### Переменные
    metod_klnagent_param: "custom_install" # autonomous_package или custom_install

    # -----используется в случае metod_klnagent_param: "autonomous_package"--------
    klnagent_autonomous_package_name: "klnagent64-11.0.0-38.x86_64.sh" 
    # -----------------------------------------------------------------------------------------------

    # -----используется в случае metod_klnagent_param: "custom_install"------------
    klnagent_url: URL для получения пакета klnagent
    KLNAGENT_SERVER: IP адрес или имя сервера администрирования
    KLNAGENT_PORT: "14000"
    KLNAGENT_SSLPORT: "13000"
    KLNAGENT_USESSL: "1"
    KLNAGENT_GW_MODE: "1" 
Более подробную инстукцию можно найти по адресу https://ittx.ru/note/2021/03/18/ansible-klnagent/

## Kaspersky Endpoint Security
### Варианты запуска
В предложенной реализации, возможно два варианта запуска playbook. Для всех хостов, описанных в файле hosts:

    ansible-playbook service_install_kesl_all_servers.yml --vault-password-file=/u01/ansible/secret --diff -vv 
Точечно выбирать хосты, на которые необходимо запустить роль. Если необходимо, чтобы установка запустилась на нескольких хостах, указываем их через запятую. Не забываем, что указанные хосты должны соответствовать именам в файле hosts и host_vars:

    ansible-playbook service_install_kesl_select_servers.yml -e "host=test01" --vault-password-file=/u01/ansible/secret --diff -vv

### Переменные
    kesl_file_name: "kesl-11.1.0-3013.x86_64.rpm"
    EULA_AGREED: "yes"
    PRIVACY_POLICY_AGREED: "yes"
    SERVICE_LOCALE: "en_US.UTF-8"
    USE_KSN: "yes"
    USE_GUI: "no"
    INSTALL_LICENSE: ""
    ScanMemoryLimit: "2048"
Более подробную инстукцию можно найти по адресу https://ittx.ru/note/2021/03/15/ansible-kesl/

https://ittx.ru
