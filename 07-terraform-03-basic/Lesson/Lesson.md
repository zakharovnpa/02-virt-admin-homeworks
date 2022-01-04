## Выполнение ДЗ "7.3. Основы и принцип работы Терраформ"

### Задача 1. Создадим бэкэнд в S3 (необязательно, но крайне желательно).

Если в рамках предыдущего задания у вас уже есть аккаунт AWS, то давайте продолжим знакомство со взаимодействием
терраформа и aws. 

1. Создайте s3 бакет, iam роль и пользователя от которого будет работать терраформ. Можно создать отдельного пользователя,
а можно использовать созданного в рамках предыдущего задания, просто добавьте ему необходимы права, как описано 
[здесь](https://www.terraform.io/docs/backends/types/s3.html).
1. Зарегистрируйте бэкэнд в терраформ проекте как описано по ссылке выше. 

**Ход выполнения:**
1. Создать локальную директорию для сохранения файлов и выполнения команд:

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning# mkdir -p my-project
```
```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning# cd my-project/
```
```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# touch main.tf outputs.tf version.tf variables.tf
```
```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# ls -l
итого 0
-rw-r--r-- 1 root root 0 янв  4 13:08 main.tf
-rw-r--r-- 1 root root 0 янв  4 13:08 outputs.tf
-rw-r--r-- 1 root root 0 янв  4 13:08 variables.tf
-rw-r--r-- 1 root root 0 янв  4 13:08 version.tf

```
1. Инициализировать Git, подключить удаленный репозиторий, добавить файл ` .gitignore `
```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git init
Инициализирован пустой репозиторий Git в /root/netology-project/learning-terraform/aws-cloud-learning/my-project/.git/
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# ls -l
итого 0
-rw-r--r-- 1 root root 0 янв  4 13:08 main.tf
-rw-r--r-- 1 root root 0 янв  4 13:08 outputs.tf
-rw-r--r-- 1 root root 0 янв  4 13:08 variables.tf
-rw-r--r-- 1 root root 0 янв  4 13:08 version.tf
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# ls -la
итого 12
drwxr-xr-x 3 root root 4096 янв  4 13:21 .
drwxr-xr-x 4 root root 4096 янв  4 13:07 ..
drwxr-xr-x 7 root root 4096 янв  4 13:21 .git
-rw-r--r-- 1 root root    0 янв  4 13:08 main.tf
-rw-r--r-- 1 root root    0 янв  4 13:08 outputs.tf
-rw-r--r-- 1 root root    0 янв  4 13:08 variables.tf
-rw-r--r-- 1 root root    0 янв  4 13:08 version.tf
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# 
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git status
На ветке master

Еще нет коммитов

Неотслеживаемые файлы:
  (используйте «git add <файл>…», чтобы добавить в то, что будет включено в коммит)
	main.tf
	outputs.tf
	variables.tf
	version.tf

ничего не добавлено в коммит, но есть неотслеживаемые файлы (используйте «git add», чтобы отслеживать их)
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# vim .gitignore
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git status
На ветке master

Еще нет коммитов

Неотслеживаемые файлы:
  (используйте «git add <файл>…», чтобы добавить в то, что будет включено в коммит)
	.gitignore
	main.tf
	outputs.tf
	variables.tf
	version.tf

ничего не добавлено в коммит, но есть неотслеживаемые файлы (используйте «git add», чтобы отслеживать их)
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git add .gitignore main.tf outputs.tf variables.tf version.tf 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git status
На ветке master

Еще нет коммитов

Изменения, которые будут включены в коммит:
  (используйте «git rm --cached <файл>…», чтобы убрать из индекса)
	новый файл:    .gitignore
	новый файл:    main.tf
	новый файл:    outputs.tf
	новый файл:    variables.tf
	новый файл:    version.tf
  ```
  Добавление удаленного репозитория ` experiments-netology `:
  ```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git remote add experiments-netology git@github.com:zakharovnpa/experiments-netology.git
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git remote -v
experiments-netology	git@github.com:zakharovnpa/experiments-netology.git (fetch)
experiments-netology	git@github.com:zakharovnpa/experiments-netology.git (push)
```
Отправка изменений из локальной директории в удаленный репозиторий:
```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git push
fatal: Не настроена точка назначения для отправки.
Либо укажите URL с помощью командной строки, либо настройте внешний репозиторий с помощью

    git remote add <имя> <адрес>

а затем отправьте изменения с помощью имени внешнего репозитория

    git push <имя>
```
Смотрим состояние Git
```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git status
На ветке master

Еще нет коммитов

Изменения, которые будут включены в коммит:
  (используйте «git rm --cached <файл>…», чтобы убрать из индекса)
	новый файл:    .gitignore
	новый файл:    main.tf
	новый файл:    outputs.tf
	новый файл:    variables.tf
	новый файл:    version.tf
```
Выполняем первый коммит
```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git commit -m "First commit"
[master (корневой коммит) da3eef8] First commit
 5 files changed, 36 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 main.tf
 create mode 100644 outputs.tf
 create mode 100644 variables.tf
 create mode 100644 version.tf
 ```
 
 ```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git status
На ветке master
нечего коммитить, нет изменений в рабочем каталоге
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git push
fatal: Не настроена точка назначения для отправки.
Либо укажите URL с помощью командной строки, либо настройте внешний репозиторий с помощью

    git remote add <имя> <адрес>

а затем отправьте изменения с помощью имени внешнего репозитория

    git push <имя>

```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git push experiments-netology git@github.com:zakharovnpa/experiments-netology.git
error: src refspec git@github.com does not match any
error: не удалось отправить некоторые ссылки в «git@github.com:zakharovnpa/experiments-netology.git»
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git status
На ветке master
нечего коммитить, нет изменений в рабочем каталоге
```
Выполняем отправку изменений в удаленный репозиторий ` git push experiments-netology master `
```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git push experiments-netology master
The authenticity of host 'github.com (140.82.121.4)' can't be established.
ECDSA key fingerprint is SHA256:p2QAMXNIC1TJYWeIOttrVc98/R1BUFWu3/LiyKgUfQM.
Are you sure you want to continue connecting (yes/no/[fingerprint])? 
Host key verification failed.
fatal: Не удалось прочитать из внешнего репозитория.

Удостоверьтесь, что у вас есть необходимые права доступа
и репозиторий существует.
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git remote -v
experiments-netology	git@github.com:zakharovnpa/experiments-netology.git (fetch)
experiments-netology	git@github.com:zakharovnpa/experiments-netology.git (push)
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git push master
fatal: Текущая ветка master не имеет вышестоящей ветки.
Чтобы отправить текущую ветку и установить внешнюю ветку как вышестоящую для этой ветки, используйте

    git push --set-upstream master master

```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git push origiin
fatal: Текущая ветка master не имеет вышестоящей ветки.
Чтобы отправить текущую ветку и установить внешнюю ветку как вышестоящую для этой ветки, используйте

    git push --set-upstream origiin master
```

```ps

root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git push --set-upstream origiin master
fatal: 'origiin' does not appear to be a git repository
fatal: Не удалось прочитать из внешнего репозитория.

Удостоверьтесь, что у вас есть необходимые права доступа
и репозиторий существует.
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# ls -l
итого 0
-rw-r--r-- 1 root root 0 янв  4 13:08 main.tf
-rw-r--r-- 1 root root 0 янв  4 13:08 outputs.tf
-rw-r--r-- 1 root root 0 янв  4 13:08 variables.tf
-rw-r--r-- 1 root root 0 янв  4 13:08 version.tf
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git log
commit da3eef8583426e064e5fc2965a233871bb29b8f9 (HEAD -> master)
Author: Sergey Zakharov <zakharovnpa@gmail.com>
Date:   Tue Jan 4 13:41:26 2022 +0400

    First commit
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# ls -la
итого 16
drwxr-xr-x 3 root root 4096 янв  4 13:28 .
drwxr-xr-x 4 root root 4096 янв  4 13:07 ..
drwxr-xr-x 8 root root 4096 янв  4 13:43 .git
-rw-r--r-- 1 root root  862 янв  4 13:28 .gitignore
-rw-r--r-- 1 root root    0 янв  4 13:08 main.tf
-rw-r--r-- 1 root root    0 янв  4 13:08 outputs.tf
-rw-r--r-- 1 root root    0 янв  4 13:08 variables.tf
-rw-r--r-- 1 root root    0 янв  4 13:08 version.tf
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git remote -v
experiments-netology	git@github.com:zakharovnpa/experiments-netology.git (fetch)
experiments-netology	git@github.com:zakharovnpa/experiments-netology.git (push)
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git push --repo=experiments-netology master
fatal: Текущая ветка master не имеет вышестоящей ветки.
Чтобы отправить текущую ветку и установить внешнюю ветку как вышестоящую для этой ветки, используйте

    git push --set-upstream master master
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git push
fatal: Не настроена точка назначения для отправки.
Либо укажите URL с помощью командной строки, либо настройте внешний репозиторий с помощью

    git remote add <имя> <адрес>

а затем отправьте изменения с помощью имени внешнего репозитория

    git push <имя>
    
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git push experiments-netology
fatal: Текущая ветка master не имеет вышестоящей ветки.
Чтобы отправить текущую ветку и установить внешнюю ветку как вышестоящую для этой ветки, используйте

    git push --set-upstream experiments-netology master
```
Удачная передача файлов в удаленный репозиторий ` git push --set-upstream experiments-netology master `
```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git push --set-upstream experiments-netology master
The authenticity of host 'github.com (140.82.121.4)' can't be established.
ECDSA key fingerprint is SHA256:p2QAMXNIC1TJYWeIOttrVc98/R1BUFWu3/LiyKgUfQM.
Are you sure you want to continue connecting (yes/no/[fingerprint])? y
Please type 'yes', 'no' or the fingerprint: yes
Warning: Permanently added 'github.com,140.82.121.4' (ECDSA) to the list of known hosts.
Перечисление объектов: 4, готово.
Подсчет объектов: 100% (4/4), готово.
При сжатии изменений используется до 6 потоков
Сжатие объектов: 100% (3/3), готово.
Запись объектов: 100% (4/4), 726 байтов | 363.00 КиБ/с, готово.
Всего 4 (изменения 0), повторно использовано 0 (изменения 0)
remote: 
remote: Create a pull request for 'master' on GitHub by visiting:
remote:      https://github.com/zakharovnpa/experiments-netology/pull/new/master
remote: 
To github.com:zakharovnpa/experiments-netology.git
 * [new branch]      master -> master
Ветка «master» отслеживает внешнюю ветку «master» из «experiments-netology».
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# 

```



**Ответ:**

### Задача 2. Инициализируем проект и создаем воркспейсы. 

1. Выполните `terraform init`:
    * если был создан бэкэнд в S3, то терраформ создат файл стейтов в S3 и запись в таблице 
dynamodb.
    * иначе будет создан локальный файл со стейтами.  
1. Создайте два воркспейса `stage` и `prod`.
1. В уже созданный `aws_instance` добавьте зависимость типа инстанса от вокспейса, что бы в разных ворскспейсах 
использовались разные `instance_type`.
1. Добавим `count`. Для `stage` должен создаться один экземпляр `ec2`, а для `prod` два. 
1. Создайте рядом еще один `aws_instance`, но теперь определите их количество при помощи `for_each`, а не `count`.
1. Что бы при изменении типа инстанса не возникло ситуации, когда не будет ни одного инстанса добавьте параметр
жизненного цикла `create_before_destroy = true` в один из рессурсов `aws_instance`.
1. При желании поэкспериментируйте с другими параметрами и рессурсами.

В виде результата работы пришлите:
* Вывод команды `terraform workspace list`.
* Вывод команды `terraform plan` для воркспейса `prod`.  

**Ответ:**
