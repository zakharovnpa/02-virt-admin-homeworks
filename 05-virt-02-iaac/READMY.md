
# Домашнее задание к занятию "5.2. Применение принципов IaaC в работе с виртуальными машинами"

## Как сдавать задания

Обязательными к выполнению являются задачи без указания звездочки. Их выполнение необходимо для получения зачета и диплома о профессиональной переподготовке.

Задачи со звездочкой (*) являются дополнительными задачами и/или задачами повышенной сложности. Они не являются обязательными к выполнению, но помогут вам глубже понять тему.

Домашнее задание выполните в файле readme.md в github репозитории. В личном кабинете отправьте на проверку ссылку на .md-файл в вашем репозитории.

Любые вопросы по решению задач задавайте в чате учебной группы.

---

## Задача 1

- Опишите своими словами основные преимущества применения на практике IaaC паттернов.
- Какой из принципов IaaC является основополагающим?

## Задача 2

- Чем Ansible выгодно отличается от других систем управление конфигурациями?
- Какой, на ваш взгляд, метод работы систем конфигурации более надёжный push или pull?

## Задача 3

Установить на личный компьютер:

- VirtualBox
- Vagrant
- Ansible

*Приложить вывод команд установленных версий каждой из программ, оформленный в markdown.*

Установка на Windows 10 Домашняя WSL 2: 
Из [статьи](https://www.thomasmaurer.ch/2019/06/install-wsl-2-on-windows-10/) команды выполненные в PowerShell под администратором:

```bash
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
ПК перезагрузиться.

Затем выполнить:
```bash
Включить - WindowsOptionalFeature - Online - FeatureName VirtualMachinePlatform
```
ПК перезагрузиться.

Затем из [статьи](https://www.thomasmaurer.ch/2018/04/windows-subsystem-for-linux-on-windows-server/)
выполнить команды на  скачивание и установку дистрибутивов Linux

```bash
# For Ubuntu 16.04
 
Invoke-WebRequest -Uri https://aka.ms/wsl-ubuntu-1604 -OutFile ~/Ubuntu.zip -UseBasicParsing
 
# For Ubuntu 18.04
 
Invoke-WebRequest -Uri https://aka.ms/wsl-ubuntu-1804 -OutFile ~/Ubuntu1804.zip -UseBasicParsing
 
# For OpenSUSE 42
 
Invoke-WebRequest -Uri https://aka.ms/wsl-opensuse-42 -OutFile ~/OpenSUSE.zip -UseBasicParsing
 
# For SLES 12
 
Invoke-WebRequest -Uri https://aka.ms/wsl-sles-12 -OutFile ~/SLES.zip -UseBasicParsing
```
Затем распаковать архив с дистрибутивом

```bash
Expand-Archive ~/Ubuntu.zip C:\Distros\Ubuntu
```
Затем запустить файл .exe. Установиться ВМ.

## Задача 4 (*)

Воспроизвести практическую часть лекции самостоятельно.

- Создать виртуальную машину.
- Зайти внутрь ВМ, убедиться, что Docker установлен с помощью команды
```
docker ps
```
