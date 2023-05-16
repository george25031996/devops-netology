# Домашнее задание №5.2
## Задача №1
Опишите своими словами основные преимущества применения на практике IaaC паттернов
Паттерны — это способ построения (структуризации) программного кода специальным образом. На практике паттерны используются программистами для того, чтобы решить какую-нибудь проблему, устранить "неудобства" разработчика. Предполагается, что существует некоторый перечень общих формализованных проблем, причем данные проблемы встречаются относительно часто. Выходом из ситуации являются паттерны, которые как раз таки и предоставляют способы решения этих проблем.

Преимущество применения паттернов IaaС на практике это возможность единожды описав инфраструктуру многократно её воспроизводить, производить развёртывние идентичных сервера/сред для тестирования/разработки, масштабирование при необходимости. Следующим преимуществом является автоматизация рутинных действий что приводит к снижению трудозатрат на их выполнение - как следствие повышается скорость разработки, выявления и устранения дефектов за счёт более раннего их обнаружения и тестирования на этапе сборки. Автоматизация поставки - позволяет сократить время от этапа разработки до внедрения. Паттерны IaaC позволяют стандартизировать развёртывание инфраструктуры, что снижает вероятность появления ошибок или отклонений связанных с человеческим фактором.

Применение на практике IaaC паттернов позволяет ускорить процесс разработки, снизить трудозатраты на поиск и устранение дефектов, организовать непрерывную поставку продукта

Какой из принципов IaaC является основополагающим?
Идемпотентность операций - свойство сценария/операции позволяющее многократно получать/воспроизводить одно и то же состояние объекта (среды) что и при первом применении, т.е. не зависимо от того сколько раз будет проигран сценарий, результат всегда будет идентичен результату полученному в первый раз.

## Задача №2
Чем Ansible выгодно отличается от других систем управление конфигурациями?
Не требует установки агентов на клиентах, использует SSH или WinRM соединение. Низкий порог входа, поддержка декларативного и императивного подхода, описание конфигурации - «плейбуки» вформате YAML Поддерживает широкий набор модулей позволяющих управлять конфигурацией как ОС, так и различным ПО и сетевым оборудованием. Ansible Galaxy - публичный репозиторий, в котором размещается огромное количество готовых ролей Ansible.

Какой, на ваш взгляд, метод работы систем конфигурации более надёжный push или pull?
Я думаю, что более надёжный push, так как он позволяет определить когда, куда и какую конфигурацию отправить, так же позволяет проконтролировать результат применения.

## Задача №3
Установить на личный компьютер:
1. VirtualBox

```sh
(base) glisikh@glisikh-OptiPlex-3020:~/devops-netology/docker/5.2$ virtualbox --help
Oracle VM VirtualBox VM Selector v6.1.38_Ubuntu
(C) 2005-2022 Oracle Corporation
All rights reserved.

No special options.

If you are looking for --startvm and related options, you need to use VirtualBoxVM.
```
2. Vagrant
```sh
(base) glisikh@glisikh-OptiPlex-3020:~/devops-netology/docker/5.2$ vagrant --version
Vagrant 2.2.19
```
3. Ansible
```sh
(base) glisikh@glisikh-OptiPlex-3020:~/devops-netology/docker/5.2$ ansible --version
ansible 2.10.8
  config file = None
  configured module search path = ['/home/glisikh/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 3.10.6 (main, Mar 10 2023, 10:55:28) [GCC 11.3.0]
```

## Задача №4
1. Создайте виртуальную машину
```sh
(base) glisikh@glisikh-OptiPlex-3020:~/devops-netology/docker/5.2/vagrant$ vagrant up
Bringing machine 'server1.netology' up with 'virtualbox' provider...
==> server1.netology: Clearing any previously set forwarded ports...
==> server1.netology: Clearing any previously set network interfaces...
==> server1.netology: Preparing network interfaces based on configuration...
    server1.netology: Adapter 1: nat
    server1.netology: Adapter 2: bridged
==> server1.netology: Forwarding ports...
    server1.netology: 22 (guest) => 20011 (host) (adapter 1)
    server1.netology: 22 (guest) => 2222 (host) (adapter 1)
==> server1.netology: Running 'pre-boot' VM customizations...
==> server1.netology: Booting VM...
==> server1.netology: Waiting for machine to boot. This may take a few minutes...
    server1.netology: SSH address: 127.0.0.1:2222
    server1.netology: SSH username: vagrant
    server1.netology: SSH auth method: private key
==> server1.netology: Machine booted and ready!
==> server1.netology: Checking for guest additions in VM...
    server1.netology: The guest additions on this VM do not match the installed version of
    server1.netology: VirtualBox! In most cases this is fine, but in rare cases it can
    server1.netology: prevent things such as shared folders from working properly. If you see
    server1.netology: shared folder errors, please make sure the guest additions within the
    server1.netology: virtual machine match the version of VirtualBox you have installed on
    server1.netology: your host and reload your VM.
    server1.netology: 
    server1.netology: Guest Additions Version: 7.0.6 r155176
    server1.netology: VirtualBox Version: 6.1
==> server1.netology: Setting hostname...
==> server1.netology: Configuring and enabling network interfaces...
==> server1.netology: Mounting shared folders...
    server1.netology: /vagrant => /home/glisikh/devops-netology/docker/5.2/vagrant
==> server1.netology: Machine already provisioned. Run `vagrant provision` or use the `--provision`
==> server1.netology: flag to force provisioning. Provisioners marked to run always will still run.
(base) glisikh@glisikh-OptiPlex-3020:~/devops-netology/docker/5.2/vagrant$ vagrant provision
==> server1.netology: Running provisioner: ansible...
    server1.netology: Running ansible-playbook...

PLAY [nodes] *******************************************************************

TASK [Gathering Facts] *********************************************************
ok: [server1.netology]

TASK [Create directory for ssh-keys] *******************************************
ok: [server1.netology]

TASK [Adding rsa-key in /root/.ssh/authorized_keys] ****************************
An exception occurred during task execution. To see the full traceback, use -vvv. The error was: If you are using a module and expect the file to exist on the remote, see the remote_src option
fatal: [server1.netology]: FAILED! => {"changed": false, "msg": "Could not find or access '~/.ssh/id_rsa.pub' on the Ansible Controller.\nIf you are using a module and expect the file to exist on the remote, see the remote_src option"}
...ignoring

TASK [Checking DNS] ************************************************************
changed: [server1.netology]

TASK [Installing tools] ********************************************************
ok: [server1.netology] => (item=git)
ok: [server1.netology] => (item=curl)

TASK [Installing docker] *******************************************************

changed: [server1.netology]

TASK [Add the current user to docker group] ************************************
changed: [server1.netology]

PLAY RECAP *********************************************************************
server1.netology           : ok=7    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=1
```
2. Зайти внутрь ВМ, убедиться, что Docker установлен с помощью команды
```sh
(base) glisikh@glisikh-OptiPlex-3020:~/devops-netology/docker/5.2/vagrant$ vagrant ssh
Welcome to Ubuntu 20.04.6 LTS (GNU/Linux 5.4.0-144-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

 System information disabled due to load higher than 1.0

 * Introducing Expanded Security Maintenance for Applications.
   Receive updates to over 25,000 software packages with your
   Ubuntu Pro subscription. Free for personal use.

     https://ubuntu.com/pro


This system is built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento
Last login: Tue May 16 05:37:10 2023 from 10.0.2.2
vagrant@server1:~$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
