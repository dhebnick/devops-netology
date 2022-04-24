
# Домашнее задание к занятию "5.2. Применение принципов IaaC в работе с виртуальными машинами"

## Задача 1

1.1 Опишите своими словами основные преимущества применения на практике IaaC паттернов.
1.2 Какой из принципов IaaC является основополагающим?

Ответ:
1.1 Оптимитизация рабочих процессов, лучше создать скрипт выполнения действий и править его при необходимости, нежели делать одну и туже работу руками.
Не знаю кто это сказал, но враза запомнилась: "Тяжелые времена порождают сильных программистов. Сильные программисты создают фреймворки. Фреймворки порождают слабых программистов." Это я к тому, что лучше создавать каркасы и тратить время на изучение чего то нового. Руками мы пытаемся сделать всё и сразу и быстрее, а спешка ни к чему хорошему как правило не приводит, а последовательное и закономерное выполнение действий убирает много огрехов. Люди не машины и могут что то забыть, а инфраструктура в виде когда поможет всё упорядочить.

1.2 Идемпоте́нтность (лат.idem — тот же самый + potens — способный) — свойство объекта или операции, при повторном выполнении которого получать результат идентичный предыдущему и всем последующим выполнениям.


## Задача 2

- Чем Ansible выгодно отличается от других систем управление конфигурациями?

- Какой, на ваш взгляд, метод работы систем конфигурации более надёжный push или pull?

Ответ:

Ansible отличается простотой использования за счет формата YAML для playbooks, имеет безагентную среду и за счет того, что написан на Python легко расширяемый. Метод push является более надежным за счет того, что не надо на хосте устанавливать лишнее, то есть более надежно.


## Задача 3

Установить на личный компьютер:

- VirtualBox
- Vagrant
- Ansible

*Приложить вывод команд установленных версий каждой из программ, оформленный в markdown.*

```
nick@ban42ru:~$ VBoxManage --version
6.1.32_Ubuntur149290
nick@ban42ru:~$ ansible --version
ansible 2.9.6
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/home/nick/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 3.8.10 (default, Mar 15 2022, 12:22:08) [GCC 9.4.0]
nick@ban42ru:~$ vagrant -v
Vagrant 2.2.6
```

## Задача 4 (*)

Воспроизвести практическую часть лекции самостоятельно.

- Создать виртуальную машину.
- Зайти внутрь ВМ, убедиться, что Docker установлен с помощью команды
```
nick@ban42ru:~/src/vagrant$ vagrant up
Bringing machine 'server1.netology' up with 'virtualbox' provider...
==> server1.netology: Box 'bento/ubuntu-20.04' could not be found. Attempting to find and install...
    server1.netology: Box Provider: virtualbox
    server1.netology: Box Version: >= 0
The box 'bento/ubuntu-20.04' could not be found or
could not be accessed in the remote catalog. If this is a private
box on HashiCorp's Vagrant Cloud, please verify you're logged in via
vagrant login. Also, please double-check the name. The expanded
URL and error message are shown below:

URL: ["https://vagrantcloud.com/bento/ubuntu-20.04"]
Error: The requested URL returned error: 404 Not Found
```
К сожалению уже закрыли нам доступ к vagrant.
На ноуте две ОС: Ubuntu 20.04 (Пришлось слегка повозиться с VirtualBox из-за UEFI) и Windows 11
