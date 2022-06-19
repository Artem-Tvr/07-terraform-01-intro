# Домашнее задание к занятию "7.1. Инфраструктура как код"

## Задача 1. Выбор инструментов.

### Легенда

Через час совещание на котором менеджер расскажет о новом проекте. Начать работу над которым надо будет уже сегодня. На данный момент известно, что это будет сервис, который ваша компания будет предоставлять внешним заказчикам. Первое время, скорее всего, будет один внешний клиент, со временем внешних клиентов станет больше.

Так же по разговорам в компании есть вероятность, что техническое задание еще не четкое, что приведет к большому количеству небольших релизов, тестирований интеграций, откатов, доработок, то есть скучно не будет.

Вам, как девопс инженеру, будет необходимо принять решение об инструментах для организации инфраструктуры. На данный момент в вашей компании уже используются следующие инструменты:

* остатки СloudFormation,
* некоторые образы сделаны при помощи Packer,
* год назад начали активно использовать Terraform,
* разработчики привыкли использовать Docker,
* уже есть большая база Kubernetes конфигураций,
* для автоматизации процессов используется Teamcity,
* также есть совсем немного Ansible скриптов,
* и ряд bash скриптов для упрощения рутинных задач.

Для этого в рамках совещания надо будет выяснить подробности о проекте, что бы в итоге определиться с инструментами:

1. Какой тип инфраструктуры будем использовать для этого проекта: изменяемый или не изменяемый?
2. Будет ли центральный сервер для управления инфраструктурой?
3. Будут ли агенты на серверах?
4. Будут ли использованы средства для управления конфигурацией или инициализации ресурсов?

В связи с тем, что проект стартует уже сегодня, в рамках совещания надо будет определиться со всеми этими вопросами.

### В результате задачи необходимо

1. Ответить на четыре вопроса представленных в разделе "Легенда".
2. Какие инструменты из уже используемых вы хотели бы использовать для нового проекта?
3. Хотите ли рассмотреть возможность внедрения новых инструментов для этого проекта?

Если для ответа на эти вопросы недостаточно информации, то напишите какие моменты уточните на совещании.

*Ответ:*

1.

1.1 не изменеямый

1.2 не будет центрального сервера

1.3 агентов не будет

1.4 да, будут использоваться средства для управления конфигурацией

2. Будем тспользовать - Packer, Terraform, Docker, Teamcity, Ansible, bash скрипты.
3. Так как работы над проектом надо начинать уже сегодня, новые инструменты не стал бы на нем применять, потому что ожидаемо это привело бы к багам на первывх порах.

   Я бы задал дополнительные вопросы, чтобы выяснить какие данные и в каком количестве будут поступать с этого проекта, чтобы определиться с типом базы данных, а так же вопросы, чтобы выяснить тип веб сервера.


## Задача 2. Установка терраформ.

Официальный сайт: [https://www.terraform.io/](https://www.terraform.io/)

Установите терраформ при помощи менеджера пакетов используемого в вашей операционной системе. В виде результата этой задачи приложите вывод команды `terraform --version`.

*Ответ:*

```
root@cadcixztkv:~# terraform --version
Terraform v1.1.9
on linux_amd64

Your version of Terraform is out of date! The latest version
is 1.2.3. You can update by downloading from https://www.terraform.io/downloads.html

```

## Задача 3. Поддержка легаси кода.

В какой-то момент вы обновили терраформ до новой версии, например с 0.12 до 0.13. А код одного из проектов настолько устарел, что не может работать с версией 0.13. В связи с этим необходимо сделать так, чтобы вы могли одновременно использовать последнюю версию терраформа установленную при помощи штатного менеджера пакетов и устаревшую версию 0.12.

В виде результата этой задачи приложите вывод `--version` двух версий терраформа доступных на вашем компьютере или виртуальной машине.

*Ответ:*

```
root@cadcixztkv:~# mkdir -p /usr/local/tf
root@cadcixztkv:~# mkdir -p /usr/local/tf/12
root@cadcixztkv:~# mkdir -p /usr/local/tf/12
root@cadcixztkv:~# cd /usr/local/tf/12/
root@cadcixztkv:/usr/local/tf/12# wget https://hashicorp-releases.website.yandexcloud.net/terraform/0.12.0/terraform_0.12.0_linux_amd64.zip
--2022-06-17 12:10:29--  https://hashicorp-releases.website.yandexcloud.net/terraform/0.12.0/terraform_0.12.0_linux_amd64.zip
Resolving hashicorp-releases.website.yandexcloud.net (hashicorp-releases.website.yandexcloud.net)... 213.180.193.247, 2a02:6b8::1da
Connecting to hashicorp-releases.website.yandexcloud.net (hashicorp-releases.website.yandexcloud.net)|213.180.193.247|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 14907580 (14M) [application/zip]
Saving to: ‘terraform_0.12.0_linux_amd64.zip’

terraform_0.12.0_linux_amd64. 100%[===============================================>]  14.22M  35.6MB/s    in 0.4s

Last-modified header invalid -- time-stamp ignored.
2022-06-17 12:10:30 (35.6 MB/s) - ‘terraform_0.12.0_linux_amd64.zip’ saved [14907580/14907580]

root@cadcixztkv:/usr/local/tf/12# cd /usr/local/tf/13/
root@cadcixztkv:/usr/local/tf/13# wget https://hashicorp-releases.website.yandexcloud.net/terraform/0.13.0/terraform_0.13.0_linux_amd64.zip
--2022-06-17 12:12:07--  https://hashicorp-releases.website.yandexcloud.net/terraform/0.13.0/terraform_0.13.0_linux_amd64.zip
Resolving hashicorp-releases.website.yandexcloud.net (hashicorp-releases.website.yandexcloud.net)... 213.180.193.247, 2a02:6b8::1da
Connecting to hashicorp-releases.website.yandexcloud.net (hashicorp-releases.website.yandexcloud.net)|213.180.193.247|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 34851622 (33M) [application/zip]
Saving to: ‘terraform_0.13.0_linux_amd64.zip’

terraform_0.13.0_linux_amd64. 100%[===============================================>]  33.24M  39.5MB/s    in 0.8s

Last-modified header invalid -- time-stamp ignored.
2022-06-17 12:12:08 (39.5 MB/s) - ‘terraform_0.13.0_linux_amd64.zip’ saved [34851622/34851622]

root@cadcixztkv:/usr/local/tf/13# unzip terraform_0.13.0_linux_amd64.zip
Archive:  terraform_0.13.0_linux_amd64.zip
  inflating: terraform
root@cadcixztkv:/usr/local/tf/13# cd /usr/local/tf/12/
root@cadcixztkv:/usr/local/tf/12# unzip terraform_0.12.0_linux_amd64.zip
Archive:  terraform_0.12.0_linux_amd64.zip
  inflating: terraform
root@cadcixztkv:/usr/local/tf/12# cd
root@cadcixztkv:~# ln -s /usr/local/tf/12/terraform /usr/bin/terraform12
root@cadcixztkv:~# ln -s /usr/local/tf/13/terraform /usr/bin/terraform13
root@cadcixztkv:~# chmod ugo+x /usr/bin/terraform*
root@cadcixztkv:~# terraform12
Usage: terraform [-version] [-help] <command> [args]

The available commands for execution are listed below.
The most common, useful commands are shown first, followed by
less common or more advanced commands. If you're just getting
started with Terraform, stick with the common commands. For the
other commands, please read the help and docs before usage.

Common commands:
    apply              Builds or changes infrastructure
    console            Interactive console for Terraform interpolations
    destroy            Destroy Terraform-managed infrastructure
    env                Workspace management
    fmt                Rewrites config files to canonical format
    get                Download and install modules for the configuration
    graph              Create a visual graph of Terraform resources
    import             Import existing infrastructure into Terraform
    init               Initialize a Terraform working directory
    output             Read an output from a state file
    plan               Generate and show an execution plan
    providers          Prints a tree of the providers used in the configuration
    refresh            Update local state file against real resources
    show               Inspect Terraform state or plan
    taint              Manually mark a resource for recreation
    untaint            Manually unmark a resource as tainted
    validate           Validates the Terraform files
    version            Prints the Terraform version
    workspace          Workspace management

All other commands:
    0.12upgrade        Rewrites pre-0.12 module source code for v0.12
    debug              Debug output management (experimental)
    force-unlock       Manually unlock the terraform state
    push               Obsolete command for Terraform Enterprise legacy (v1)
    state              Advanced state management

root@cadcixztkv:~# terraform12 --version
Terraform v0.12.0

Your version of Terraform is out of date! The latest version
is 1.2.3. You can update by downloading from www.terraform.io/downloads.html
root@cadcixztkv:~# terraform13
Usage: terraform [-version] [-help] <command> [args]

The available commands for execution are listed below.
The most common, useful commands are shown first, followed by
less common or more advanced commands. If you're just getting
started with Terraform, stick with the common commands. For the
other commands, please read the help and docs before usage.

Common commands:
    apply              Builds or changes infrastructure
    console            Interactive console for Terraform interpolations
    destroy            Destroy Terraform-managed infrastructure
    env                Workspace management
    fmt                Rewrites config files to canonical format
    get                Download and install modules for the configuration
    graph              Create a visual graph of Terraform resources
    import             Import existing infrastructure into Terraform
    init               Initialize a Terraform working directory
    login              Obtain and save credentials for a remote host
    logout             Remove locally-stored credentials for a remote host
    output             Read an output from a state file
    plan               Generate and show an execution plan
    providers          Prints a tree of the providers used in the configuration
    refresh            Update local state file against real resources
    show               Inspect Terraform state or plan
    taint              Manually mark a resource for recreation
    untaint            Manually unmark a resource as tainted
    validate           Validates the Terraform files
    version            Prints the Terraform version
    workspace          Workspace management

All other commands:
    0.12upgrade        Rewrites pre-0.12 module source code for v0.12
    0.13upgrade        Rewrites pre-0.13 module source code for v0.13
    debug              Debug output management (experimental)
    force-unlock       Manually unlock the terraform state
    push               Obsolete command for Terraform Enterprise legacy (v1)
    state              Advanced state management
root@cadcixztkv:~# terraform13 --version

Your version of Terraform is out of date! The latest version
is 1.2.3. You can update by downloading from https://www.terraform.io/downloads.html
Terraform v0.13.0

```
