### 1 часть

1. Создать локальную директорию для сохранения файлов и выполнения команд:
``ps
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

### 2 часть
```ps

root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# ls -l
итого 0
-rw-r--r-- 1 root root 0 янв  4 13:08 main.tf
-rw-r--r-- 1 root root 0 янв  4 13:08 outputs.tf
-rw-r--r-- 1 root root 0 янв  4 13:08 variables.tf
-rw-r--r-- 1 root root 0 янв  4 13:08 version.tf
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# 
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git remote -v
experiments-netology	git@github.com:zakharovnpa/experiments-netology.git (fetch)
experiments-netology	git@github.com:zakharovnpa/experiments-netology.git (push)
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git fetch
Warning: Permanently added the ECDSA host key for IP address '140.82.121.3' to the list of known hosts.
remote: Enumerating objects: 10, done.
remote: Counting objects: 100% (10/10), done.
remote: Compressing objects: 100% (7/7), done.
remote: Total 9 (delta 1), reused 0 (delta 0), pack-reused 0
Распаковка объектов: 100% (9/9), 1.97 КиБ | 671.00 КиБ/с, готово.
Из github.com:zakharovnpa/experiments-netology
   da3eef8..4350b38  master     -> experiments-netology/master
 * [новая ветка]     main       -> experiments-netology/main
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# ls -la
итого 16
drwxr-xr-x 3 root root 4096 янв  4 13:28 .
drwxr-xr-x 4 root root 4096 янв  4 13:07 ..
drwxr-xr-x 8 root root 4096 янв  4 14:20 .git
-rw-r--r-- 1 root root  862 янв  4 13:28 .gitignore
-rw-r--r-- 1 root root    0 янв  4 13:08 main.tf
-rw-r--r-- 1 root root    0 янв  4 13:08 outputs.tf
-rw-r--r-- 1 root root    0 янв  4 13:08 variables.tf
-rw-r--r-- 1 root root    0 янв  4 13:08 version.tf
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git log
commit da3eef8583426e064e5fc2965a233871bb29b8f9 (HEAD -> master)
Author: Sergey Zakharov <zakharovnpa@gmail.com>
Date:   Tue Jan 4 13:41:26 2022 +0400

    First commit
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git checkout main
Ветка «main» отслеживает внешнюю ветку «main» из «experiments-netology».
Переключено на новую ветку «main»
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# ls -la
итого 20
drwxr-xr-x 4 root root 4096 янв  4 14:24 .
drwxr-xr-x 4 root root 4096 янв  4 13:07 ..
drwxr-xr-x 2 root root 4096 янв  4 14:24 Alfa
drwxr-xr-x 8 root root 4096 янв  4 14:24 .git
-rw-r--r-- 1 root root   65 янв  4 14:24 README.md
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# cd Alfa/
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# ls -la
итого 12
drwxr-xr-x 2 root root 4096 янв  4 14:24 .
drwxr-xr-x 4 root root 4096 янв  4 14:24 ..
-rw-r--r-- 1 root root   63 янв  4 14:24 README.md
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# touch main.tf outputs.tf version.tf variables.tf 
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# git checkout master
Переключено на ветку «master»
Ваша ветка отстает от «experiments-netology/master» на 1 коммит и может быть перемотана вперед.
  (используйте «git pull», чтобы обновить вашу локальную ветку)
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# ls -la
итого 8
drwxr-xr-x 2 root root 4096 янв  4 14:33 .
drwxr-xr-x 4 root root 4096 янв  4 14:33 ..
-rw-r--r-- 1 root root    0 янв  4 14:32 main.tf
-rw-r--r-- 1 root root    0 янв  4 14:32 outputs.tf
-rw-r--r-- 1 root root    0 янв  4 14:32 variables.tf
-rw-r--r-- 1 root root    0 янв  4 14:32 version.tf
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# ls -la
итого 12
drwxr-xr-x 2 root root 4096 янв  4 14:33 .
drwxr-xr-x 4 root root 4096 янв  4 14:33 ..
-rw-r--r-- 1 root root  862 янв  4 14:33 .gitignore
-rw-r--r-- 1 root root    0 янв  4 14:32 main.tf
-rw-r--r-- 1 root root    0 янв  4 14:32 outputs.tf
-rw-r--r-- 1 root root    0 янв  4 14:32 variables.tf
-rw-r--r-- 1 root root    0 янв  4 14:32 version.tf
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# git status
На ветке master
Ваша ветка отстает от «experiments-netology/master» на 1 коммит и может быть перемотана вперед.
  (используйте «git pull», чтобы обновить вашу локальную ветку)

Неотслеживаемые файлы:
  (используйте «git add <файл>…», чтобы добавить в то, что будет включено в коммит)
	./

ничего не добавлено в коммит, но есть неотслеживаемые файлы (используйте «git add», чтобы отслеживать их)
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# cd ..
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git status
На ветке master
Ваша ветка отстает от «experiments-netology/master» на 1 коммит и может быть перемотана вперед.
  (используйте «git pull», чтобы обновить вашу локальную ветку)

Неотслеживаемые файлы:
  (используйте «git add <файл>…», чтобы добавить в то, что будет включено в коммит)
	Alfa/

ничего не добавлено в коммит, но есть неотслеживаемые файлы (используйте «git add», чтобы отслеживать их)
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git add Alfa/
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git status
На ветке master
Ваша ветка отстает от «experiments-netology/master» на 1 коммит и может быть перемотана вперед.
  (используйте «git pull», чтобы обновить вашу локальную ветку)

Изменения, которые будут включены в коммит:
  (используйте «git restore --staged <файл>…», чтобы убрать из индекса)
	новый файл:    Alfa/.gitignore
	новый файл:    Alfa/main.tf
	новый файл:    Alfa/outputs.tf
	новый файл:    Alfa/variables.tf
	новый файл:    Alfa/version.tf

```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git commit -m "Add files in folder Alfa"
[master f858633] Add files in folder Alfa
 5 files changed, 36 insertions(+)
 create mode 100644 Alfa/.gitignore
 create mode 100644 Alfa/main.tf
 create mode 100644 Alfa/outputs.tf
 create mode 100644 Alfa/variables.tf
 create mode 100644 Alfa/version.tf
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git status
На ветке master
Ваша ветка и «experiments-netology/master» разделились
и теперь имеют 1 и 1 разных коммита в каждой соответственно.
  (используйте «git pull», чтобы слить внешнюю ветку в вашу)

нечего коммитить, нет изменений в рабочем каталоге
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git push experiments-netology master
To github.com:zakharovnpa/experiments-netology.git
 ! [rejected]        master -> master (non-fast-forward)
error: не удалось отправить некоторые ссылки в «git@github.com:zakharovnpa/experiments-netology.git»
подсказка: Обновления были отклонены, так как верхушка вашей текущей ветки
подсказка: позади ее внешней части. Заберите и слейте внешние изменения 
подсказка: (например, с помощью «git pull …») перед повторной попыткой отправки
подсказка: изменений.
подсказка: Для дополнительной информации, смотрите «Note about fast-forwards»
подсказка: в «git push --help».
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git diff
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git pull
Merge made by the 'recursive' strategy.
 README.md | 2 ++
 1 file changed, 2 insertions(+)
 create mode 100644 README.md
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git log
commit d95764e9962443e4c3e5bcf4d9842f1eb2c27202 (HEAD -> master)
Merge: f858633 4350b38
Author: Sergey Zakharov <zakharovnpa@gmail.com>
Date:   Tue Jan 4 14:38:57 2022 +0400

    Merge branch 'master' of github.com:zakharovnpa/experiments-netology

commit f858633b608a55426b0c7bd13a1b04cf1da38092
Author: Sergey Zakharov <zakharovnpa@gmail.com>
Date:   Tue Jan 4 14:36:11 2022 +0400

    Add files in folder Alfa

commit 4350b384d0404cb021d867ddd4c1861ffe454635 (experiments-netology/master)
Author: zakharovnpa <89311498+zakharovnpa@users.noreply.github.com>
Date:   Tue Jan 4 14:19:58 2022 +0400

    Create README.md

commit da3eef8583426e064e5fc2965a233871bb29b8f9
Author: Sergey Zakharov <zakharovnpa@gmail.com>
Date:   Tue Jan 4 13:41:26 2022 +0400

    First commit
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git show da3eef8583426e064e5fc2965a233871bb29b8f9
commit da3eef8583426e064e5fc2965a233871bb29b8f9
Author: Sergey Zakharov <zakharovnpa@gmail.com>
Date:   Tue Jan 4 13:41:26 2022 +0400

    First commit

diff --git a/.gitignore b/.gitignore
new file mode 100644
index 0000000..41574c7
--- /dev/null
+++ b/.gitignore
@@ -0,0 +1,36 @@
+# Local .terraform directories
+**/.terraform/*
+
+# .tfstate files
+*.tfstate
+*.tfstate.*
+
+# Crash log files
+crash.log
+
+# Exclude all .tfvars files, which are likely to contain sentitive data, such as
+# password, private keys, and other secrets. These should not be part of version
+# control as they are data points which are potentially sensitive and subject
+# to change depending on the environment.
+#
+*.tfvars
+
+# Ignore override files as they are usually used to override resources locally and so
+# are not checked in
+override.tf
+override.tf.json
+*_override.tf
+*_override.tf.json
+
+# Include override files you do wish to add to version control using negated pattern
+#
+# !example_override.tf
+
+# Include tfplan files to ignore the plan output of command: terraform plan -out=tfplan
+# example: *tfplan*
+
+# Ignore CLI configuration files
+.terraformrc
+terraform.rc
+
+
diff --git a/main.tf b/main.tf
new file mode 100644
index 0000000..e69de29
diff --git a/outputs.tf b/outputs.tf
new file mode 100644
index 0000000..e69de29
diff --git a/variables.tf b/variables.tf
new file mode 100644
index 0000000..e69de29
diff --git a/version.tf b/version.tf
new file mode 100644
index 0000000..e69de29
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git log --graph --oneline
*   d95764e (HEAD -> master) Merge branch 'master' of github.com:zakharovnpa/experiments-netology
|\  
| * 4350b38 (experiments-netology/master) Create README.md
* | f858633 Add files in folder Alfa
|/  
* da3eef8 First commit
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git status
На ветке master
Ваша ветка опережает «experiments-netology/master» на 2 коммита.
  (используйте «git push», чтобы опубликовать ваши локальные коммиты)

нечего коммитить, нет изменений в рабочем каталоге
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git remote -v
experiments-netology	git@github.com:zakharovnpa/experiments-netology.git (fetch)
experiments-netology	git@github.com:zakharovnpa/experiments-netology.git (push)
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# ls -lha
итого 24K
drwxr-xr-x 4 root root 4,0K янв  4 14:38 .
drwxr-xr-x 4 root root 4,0K янв  4 13:07 ..
drwxr-xr-x 2 root root 4,0K янв  4 14:33 Alfa
drwxr-xr-x 8 root root 4,0K янв  4 15:48 .git
-rw-r--r-- 1 root root  862 янв  4 14:33 .gitignore
-rw-r--r-- 1 root root    0 янв  4 14:33 main.tf
-rw-r--r-- 1 root root    0 янв  4 14:33 outputs.tf
-rw-r--r-- 1 root root   65 янв  4 14:38 README.md
-rw-r--r-- 1 root root    0 янв  4 14:33 variables.tf
-rw-r--r-- 1 root root    0 янв  4 14:33 version.tf
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git checkout main
Переключено на ветку «main»
Ваша ветка обновлена в соответствии с «experiments-netology/main».
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# ls -lha
итого 20K
drwxr-xr-x 4 root root 4,0K янв  4 15:50 .
drwxr-xr-x 4 root root 4,0K янв  4 13:07 ..
drwxr-xr-x 2 root root 4,0K янв  4 15:50 Alfa
drwxr-xr-x 8 root root 4,0K янв  4 15:50 .git
-rw-r--r-- 1 root root   65 янв  4 14:38 README.md
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git status
На ветке main
Ваша ветка обновлена в соответствии с «experiments-netology/main».

нечего коммитить, нет изменений в рабочем каталоге
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git checkout master
Переключено на ветку «master»
Ваша ветка опережает «experiments-netology/master» на 2 коммита.
  (используйте «git push», чтобы опубликовать ваши локальные коммиты)
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git status
На ветке master
Ваша ветка опережает «experiments-netology/master» на 2 коммита.
  (используйте «git push», чтобы опубликовать ваши локальные коммиты)

нечего коммитить, нет изменений в рабочем каталоге
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# ls -lha
итого 24K
drwxr-xr-x 4 root root 4,0K янв  4 15:50 .
drwxr-xr-x 4 root root 4,0K янв  4 13:07 ..
drwxr-xr-x 2 root root 4,0K янв  4 15:50 Alfa
drwxr-xr-x 8 root root 4,0K янв  4 15:50 .git
-rw-r--r-- 1 root root  862 янв  4 15:50 .gitignore
-rw-r--r-- 1 root root    0 янв  4 15:50 main.tf
-rw-r--r-- 1 root root    0 янв  4 15:50 outputs.tf
-rw-r--r-- 1 root root   65 янв  4 14:38 README.md
-rw-r--r-- 1 root root    0 янв  4 15:50 variables.tf
-rw-r--r-- 1 root root    0 янв  4 15:50 version.tf
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# cd Alfa/
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# ls -lha
итого 12K
drwxr-xr-x 2 root root 4,0K янв  4 15:50 .
drwxr-xr-x 4 root root 4,0K янв  4 15:50 ..
-rw-r--r-- 1 root root  862 янв  4 15:50 .gitignore
-rw-r--r-- 1 root root    0 янв  4 15:50 main.tf
-rw-r--r-- 1 root root    0 янв  4 15:50 outputs.tf
-rw-r--r-- 1 root root    0 янв  4 15:50 variables.tf
-rw-r--r-- 1 root root    0 янв  4 15:50 version.tf
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# git push experiments-netology master
Перечисление объектов: 6, готово.
Подсчет объектов: 100% (6/6), готово.
При сжатии изменений используется до 6 потоков
Сжатие объектов: 100% (4/4), готово.
Запись объектов: 100% (4/4), 518 байтов | 518.00 КиБ/с, готово.
Всего 4 (изменения 2), повторно использовано 0 (изменения 0)
remote: Resolving deltas: 100% (2/2), completed with 1 local object.
To github.com:zakharovnpa/experiments-netology.git
   4350b38..d95764e  master -> master
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# ls -lha
итого 12K
drwxr-xr-x 2 root root 4,0K янв  4 15:50 .
drwxr-xr-x 4 root root 4,0K янв  4 15:50 ..
-rw-r--r-- 1 root root  862 янв  4 15:50 .gitignore
-rw-r--r-- 1 root root    0 янв  4 15:50 main.tf
-rw-r--r-- 1 root root    0 янв  4 15:50 outputs.tf
-rw-r--r-- 1 root root    0 янв  4 15:50 variables.tf
-rw-r--r-- 1 root root    0 янв  4 15:50 version.tf
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# vim README.md
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# git status
На ветке master
Ваша ветка обновлена в соответствии с «experiments-netology/master».

Неотслеживаемые файлы:
  (используйте «git add <файл>…», чтобы добавить в то, что будет включено в коммит)
	README.md

ничего не добавлено в коммит, но есть неотслеживаемые файлы (используйте «git add», чтобы отслеживать их)
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# git add README.md 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# git status
На ветке master
Ваша ветка обновлена в соответствии с «experiments-netology/master».

Изменения, которые будут включены в коммит:
  (используйте «git restore --staged <файл>…», чтобы убрать из индекса)
	новый файл:    README.md

```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# git commit -m "Adding_README.md"
[master e93e03e] Adding_README.md
 1 file changed, 3 insertions(+)
 create mode 100644 Alfa/README.md
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# ls -lha
итого 16K
drwxr-xr-x 2 root root 4,0K янв  4 15:54 .
drwxr-xr-x 4 root root 4,0K янв  4 15:50 ..
-rw-r--r-- 1 root root  862 янв  4 15:50 .gitignore
-rw-r--r-- 1 root root    0 янв  4 15:50 main.tf
-rw-r--r-- 1 root root    0 янв  4 15:50 outputs.tf
-rw-r--r-- 1 root root  257 янв  4 15:54 README.md
-rw-r--r-- 1 root root    0 янв  4 15:50 variables.tf
-rw-r--r-- 1 root root    0 янв  4 15:50 version.tf
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# mkdir -p modules
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# cd modules/
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa/modules# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa/modules# ls -lha
итого 8,0K
drwxr-xr-x 2 root root 4,0K янв  4 15:57 .
drwxr-xr-x 3 root root 4,0K янв  4 15:57 ..
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa/modules# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa/modules# touch main.tf outputs.tf variables.tf version.tf
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa/modules# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa/modules# cd ..
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# cd ..
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git status
На ветке master
Ваша ветка опережает «experiments-netology/master» на 1 коммит.
  (используйте «git push», чтобы опубликовать ваши локальные коммиты)

Неотслеживаемые файлы:
  (используйте «git add <файл>…», чтобы добавить в то, что будет включено в коммит)
	Alfa/modules/

ничего не добавлено в коммит, но есть неотслеживаемые файлы (используйте «git add», чтобы отслеживать их)
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git add Alfa/modules/
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# git status
На ветке master
Ваша ветка опережает «experiments-netology/master» на 1 коммит.
  (используйте «git push», чтобы опубликовать ваши локальные коммиты)

Изменения, которые будут включены в коммит:
  (используйте «git restore --staged <файл>…», чтобы убрать из индекса)
	новый файл:    Alfa/modules/main.tf
	новый файл:    Alfa/modules/outputs.tf
	новый файл:    Alfa/modules/variables.tf
	новый файл:    Alfa/modules/version.tf

```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project# cd Alfa
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# vim main.tf 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# vim version.tf 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# vim main.tf 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# vim main.tf 
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform -v
Terraform v1.1.2
on linux_amd64
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform init

Initializing the backend...

Initializing provider plugins...
- Finding hashicorp/aws versions matching "~> 2.0"...
- Installing hashicorp/aws v2.70.1...
- Installed hashicorp/aws v2.70.1 (signed by HashiCorp)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

╷
│ Warning: Version constraints inside provider configuration blocks are deprecated
│ 
│   on main.tf line 9, in provider "aws":
│    9:   version = "~> 2.0"
│ 
│ Terraform 0.13 and earlier allowed provider version constraints inside the provider configuration block, but that is now deprecated and will be removed in a future version of Terraform. To silence this
│ warning, move the provider version constraint into the required_providers block.
╵

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

```tf
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # aws_instance.example will be created
  + resource "aws_instance" "example" {
      + ami                          = "ami-0c55b159cbfafe1f0"
      + arn                          = (known after apply)
      + associate_public_ip_address  = (known after apply)
      + availability_zone            = (known after apply)
      + cpu_core_count               = (known after apply)
      + cpu_threads_per_core         = (known after apply)
      + get_password_data            = false
      + host_id                      = (known after apply)
      + id                           = (known after apply)
      + instance_state               = (known after apply)
      + instance_type                = "t2.micro"
      + ipv6_address_count           = (known after apply)
      + ipv6_addresses               = (known after apply)
      + key_name                     = (known after apply)
      + network_interface_id         = (known after apply)
      + outpost_arn                  = (known after apply)
      + password_data                = (known after apply)
      + placement_group              = (known after apply)
      + primary_network_interface_id = (known after apply)
      + private_dns                  = (known after apply)
      + private_ip                   = (known after apply)
      + public_dns                   = (known after apply)
      + public_ip                    = (known after apply)
      + security_groups              = (known after apply)
      + source_dest_check            = true
      + subnet_id                    = (known after apply)
      + tags                         = {
          + "Name" = "terraform-example"
        }
      + tenancy                      = (known after apply)
      + volume_tags                  = (known after apply)
      + vpc_security_group_ids       = (known after apply)

      + ebs_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + snapshot_id           = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }

      + ephemeral_block_device {
          + device_name  = (known after apply)
          + no_device    = (known after apply)
          + virtual_name = (known after apply)
        }

      + metadata_options {
          + http_endpoint               = (known after apply)
          + http_put_response_hop_limit = (known after apply)
          + http_tokens                 = (known after apply)
        }

      + network_interface {
          + delete_on_termination = (known after apply)
          + device_index          = (known after apply)
          + network_interface_id  = (known after apply)
        }

      + root_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }
    }

Plan: 1 to add, 0 to change, 0 to destroy.
╷
│ Warning: Version constraints inside provider configuration blocks are deprecated
│ 
│   on main.tf line 9, in provider "aws":
│    9:   version = "~> 2.0"
│ 
│ Terraform 0.13 and earlier allowed provider version constraints inside the provider configuration block, but that is now deprecated and will be removed in a future version of Terraform. To silence this
│ warning, move the provider version constraint into the required_providers block.
╵

─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# vim main.tf 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform init

Initializing the backend...

Initializing provider plugins...
- Reusing previous version of hashicorp/aws from the dependency lock file
- Using previously-installed hashicorp/aws v2.70.1

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # aws_instance.example will be created
  + resource "aws_instance" "example" {
      + ami                          = "ami-0c55b159cbfafe1f0"
      + arn                          = (known after apply)
      + associate_public_ip_address  = (known after apply)
      + availability_zone            = (known after apply)
      + cpu_core_count               = (known after apply)
      + cpu_threads_per_core         = (known after apply)
      + get_password_data            = false
      + host_id                      = (known after apply)
      + id                           = (known after apply)
      + instance_state               = (known after apply)
      + instance_type                = "t2.micro"
      + ipv6_address_count           = (known after apply)
      + ipv6_addresses               = (known after apply)
      + key_name                     = (known after apply)
      + network_interface_id         = (known after apply)
      + outpost_arn                  = (known after apply)
      + password_data                = (known after apply)
      + placement_group              = (known after apply)
      + primary_network_interface_id = (known after apply)
      + private_dns                  = (known after apply)
      + private_ip                   = (known after apply)
      + public_dns                   = (known after apply)
      + public_ip                    = (known after apply)
      + security_groups              = (known after apply)
      + source_dest_check            = true
      + subnet_id                    = (known after apply)
      + tags                         = {
          + "Name" = "terraform-example"
        }
      + tenancy                      = (known after apply)
      + volume_tags                  = (known after apply)
      + vpc_security_group_ids       = (known after apply)

      + ebs_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + snapshot_id           = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }

      + ephemeral_block_device {
          + device_name  = (known after apply)
          + no_device    = (known after apply)
          + virtual_name = (known after apply)
        }

      + metadata_options {
          + http_endpoint               = (known after apply)
          + http_put_response_hop_limit = (known after apply)
          + http_tokens                 = (known after apply)
        }

      + network_interface {
          + delete_on_termination = (known after apply)
          + device_index          = (known after apply)
          + network_interface_id  = (known after apply)
        }

      + root_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }
    }

Plan: 1 to add, 0 to change, 0 to destroy.

─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform apply --help
Usage: terraform [global options] apply [options] [PLAN]

  Creates or updates infrastructure according to Terraform configuration
  files in the current directory.

  By default, Terraform will generate a new plan and present it for your
  approval before taking any action. You can optionally provide a plan
  file created by a previous call to "terraform plan", in which case
  Terraform will take the actions described in that plan without any
  confirmation prompt.

Options:

  -auto-approve          Skip interactive approval of plan before applying.

  -backup=path           Path to backup the existing state file before
                         modifying. Defaults to the "-state-out" path with
                         ".backup" extension. Set to "-" to disable backup.

  -compact-warnings      If Terraform produces any warnings that are not
                         accompanied by errors, show them in a more compact
                         form that includes only the summary messages.

  -lock=false            Don't hold a state lock during the operation. This is
                         dangerous if others might concurrently run commands
                         against the same workspace.

  -lock-timeout=0s       Duration to retry a state lock.

  -input=true            Ask for input for variables if not directly set.

  -no-color              If specified, output won't contain any color.

  -parallelism=n         Limit the number of parallel resource operations.
                         Defaults to 10.

  -state=path            Path to read and save state (unless state-out
                         is specified). Defaults to "terraform.tfstate".

  -state-out=path        Path to write state to that is different than
                         "-state". This can be used to preserve the old
                         state.

  If you don't provide a saved plan file then this command will also accept
  all of the plan-customization options accepted by the terraform plan command.
  For more information on those options, run:
      terraform plan -help
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform apply -auto-approve

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # aws_instance.example will be created
  + resource "aws_instance" "example" {
      + ami                          = "ami-0c55b159cbfafe1f0"
      + arn                          = (known after apply)
      + associate_public_ip_address  = (known after apply)
      + availability_zone            = (known after apply)
      + cpu_core_count               = (known after apply)
      + cpu_threads_per_core         = (known after apply)
      + get_password_data            = false
      + host_id                      = (known after apply)
      + id                           = (known after apply)
      + instance_state               = (known after apply)
      + instance_type                = "t2.micro"
      + ipv6_address_count           = (known after apply)
      + ipv6_addresses               = (known after apply)
      + key_name                     = (known after apply)
      + network_interface_id         = (known after apply)
      + outpost_arn                  = (known after apply)
      + password_data                = (known after apply)
      + placement_group              = (known after apply)
      + primary_network_interface_id = (known after apply)
      + private_dns                  = (known after apply)
      + private_ip                   = (known after apply)
      + public_dns                   = (known after apply)
      + public_ip                    = (known after apply)
      + security_groups              = (known after apply)
      + source_dest_check            = true
      + subnet_id                    = (known after apply)
      + tags                         = {
          + "Name" = "terraform-example"
        }
      + tenancy                      = (known after apply)
      + volume_tags                  = (known after apply)
      + vpc_security_group_ids       = (known after apply)

      + ebs_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + snapshot_id           = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }

      + ephemeral_block_device {
          + device_name  = (known after apply)
          + no_device    = (known after apply)
          + virtual_name = (known after apply)
        }

      + metadata_options {
          + http_endpoint               = (known after apply)
          + http_put_response_hop_limit = (known after apply)
          + http_tokens                 = (known after apply)
        }

      + network_interface {
          + delete_on_termination = (known after apply)
          + device_index          = (known after apply)
          + network_interface_id  = (known after apply)
        }

      + root_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }
    }

Plan: 1 to add, 0 to change, 0 to destroy.
aws_instance.example: Creating...
╷
│ Error: Error launching source instance: InvalidAMIID.NotFound: The image id '[ami-0c55b159cbfafe1f0]' does not exist
│ 	status code: 400, request id: 2b84c247-32f1-4bb5-ba16-fb67733351da
│ 
│   with aws_instance.example,
│   on main.tf line 12, in resource "aws_instance" "example":
│   12: resource "aws_instance" "example" {
│ 
╵
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# vim main.tf 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
```

```tf
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform init

Initializing the backend...

Initializing provider plugins...
- Reusing previous version of hashicorp/aws from the dependency lock file
- Using previously-installed hashicorp/aws v2.70.1

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
```

```tf
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform validate
Success! The configuration is valid.
```

```tf
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # aws_instance.example will be created
  + resource "aws_instance" "example" {
      + ami                          = "ami-0892d3c7ee96c0bf7"
      + arn                          = (known after apply)
      + associate_public_ip_address  = (known after apply)
      + availability_zone            = (known after apply)
      + cpu_core_count               = (known after apply)
      + cpu_threads_per_core         = (known after apply)
      + get_password_data            = false
      + host_id                      = (known after apply)
      + id                           = (known after apply)
      + instance_state               = (known after apply)
      + instance_type                = "t2.micro"
      + ipv6_address_count           = (known after apply)
      + ipv6_addresses               = (known after apply)
      + key_name                     = (known after apply)
      + network_interface_id         = (known after apply)
      + outpost_arn                  = (known after apply)
      + password_data                = (known after apply)
      + placement_group              = (known after apply)
      + primary_network_interface_id = (known after apply)
      + private_dns                  = (known after apply)
      + private_ip                   = (known after apply)
      + public_dns                   = (known after apply)
      + public_ip                    = (known after apply)
      + security_groups              = (known after apply)
      + source_dest_check            = true
      + subnet_id                    = (known after apply)
      + tags                         = {
          + "Name" = "terraform-example"
        }
      + tenancy                      = (known after apply)
      + volume_tags                  = (known after apply)
      + vpc_security_group_ids       = (known after apply)

      + ebs_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + snapshot_id           = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }

      + ephemeral_block_device {
          + device_name  = (known after apply)
          + no_device    = (known after apply)
          + virtual_name = (known after apply)
        }

      + metadata_options {
          + http_endpoint               = (known after apply)
          + http_put_response_hop_limit = (known after apply)
          + http_tokens                 = (known after apply)
        }

      + network_interface {
          + delete_on_termination = (known after apply)
          + device_index          = (known after apply)
          + network_interface_id  = (known after apply)
        }

      + root_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }
    }

Plan: 1 to add, 0 to change, 0 to destroy.

─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
```

```tf
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform apply -auto-approve

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # aws_instance.example will be created
  + resource "aws_instance" "example" {
      + ami                          = "ami-0892d3c7ee96c0bf7"
      + arn                          = (known after apply)
      + associate_public_ip_address  = (known after apply)
      + availability_zone            = (known after apply)
      + cpu_core_count               = (known after apply)
      + cpu_threads_per_core         = (known after apply)
      + get_password_data            = false
      + host_id                      = (known after apply)
      + id                           = (known after apply)
      + instance_state               = (known after apply)
      + instance_type                = "t2.micro"
      + ipv6_address_count           = (known after apply)
      + ipv6_addresses               = (known after apply)
      + key_name                     = (known after apply)
      + network_interface_id         = (known after apply)
      + outpost_arn                  = (known after apply)
      + password_data                = (known after apply)
      + placement_group              = (known after apply)
      + primary_network_interface_id = (known after apply)
      + private_dns                  = (known after apply)
      + private_ip                   = (known after apply)
      + public_dns                   = (known after apply)
      + public_ip                    = (known after apply)
      + security_groups              = (known after apply)
      + source_dest_check            = true
      + subnet_id                    = (known after apply)
      + tags                         = {
          + "Name" = "terraform-example"
        }
      + tenancy                      = (known after apply)
      + volume_tags                  = (known after apply)
      + vpc_security_group_ids       = (known after apply)

      + ebs_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + snapshot_id           = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }

      + ephemeral_block_device {
          + device_name  = (known after apply)
          + no_device    = (known after apply)
          + virtual_name = (known after apply)
        }

      + metadata_options {
          + http_endpoint               = (known after apply)
          + http_put_response_hop_limit = (known after apply)
          + http_tokens                 = (known after apply)
        }

      + network_interface {
          + delete_on_termination = (known after apply)
          + device_index          = (known after apply)
          + network_interface_id  = (known after apply)
        }

      + root_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }
    }

Plan: 1 to add, 0 to change, 0 to destroy.
aws_instance.example: Creating...
╷
│ Error: Error launching source instance: UnauthorizedOperation: You are not authorized to perform this operation. Encoded authorization failure message: a0d8wzwN9f8EdEjszDrVmCQSToWLWQvUl0n70tweYlGcRgLnMv0n2Ja7a7W1M58E7uiW7ofavbIUEFzHg1Aqvr5XPtT6oCQBJ4Jipa8cc2zNo1oe-yrw7OwIu3biHOdznxi7B5Nl2o_T9zl554FjHjEN-2G4apegl5bL_Vcp4bNjP3p-aEh106sDCoBinTvXPsQKvEHLiU4GZVarLcKfgh23QkSm_4t9-SJmtGIH51i2etNhjfNrsXkwNhr4QJiXs--Vx18y_BIEjF_YBirdrzKlaAHz_BeuN9vtysnCphX60VL4JeIgdHN97xBpVorWPG6RWvAoaz2fwk-lhQmoKPuGHdYyhXU-TzTZkeB77YlHbnLnE2zq99ekGS8f3DviOlpzlj-nyQlV2iD_QV-3072_69_U50A8yzfSQB_r67BkS1PDxGVok-dOkEgRyM0C4xizQ289hPS9mE4jn6F8Gp9zZ7ylBkWpV0Ipb-K5pGK-HONfJ08ym-Mxn_xxKtVCWjJ0GKs1DrIpvAfKrdXGCl-mC2rJ1HoouXC3IDsSXiZNfcp262qNOIucg2BxWteS5HmpzPnBeQjVhHNQQhZ-oNRAqMnIhtb24iwQsUqoyj40MDZY-8yH3MWbu-KELJque90O-gljEyJsmKH3XpLzagYPNpsUW1TiQqgA3HuAmJDwycauoUtV-pAz8cFrvdYQ2NHGHPJLCal7tulwXha7XGuERN0UaGF0qdwjlvNFcmlEDMBN1fgOEBcwPIID9ku6rPSlQrUL7oIUv0OeOBrUtoua9SnDhmTXROoYZhIBCxQHBJKPOsDzF5mTCurqtWpF86qoBdydVwZCelMzeRRSavbzmLpuk67jEsLFRFztHa_ieZlILaIcUMkMYwYeQnX_206Tr4sdsJW02C3sfKNNMB9oXkmS7MK2jaT7S2fRx_CHH-A5xPSvnOFv900XZOzgMM2YaIwCv0Hptcia5kClmK3BlsWYfBJZYzWDriqBYGQRvdA5NS2jiYMmarFmDODmChRkR4tMcw8TRbXQlz8df9cAs51hHQg3bbC49yUgsMoYMJX7h7f56St80b3DKvU0fU8hxJz4GsgenxgUC4_hkw2nMpgQbVz0XhlW7EAYoZpNf-WjTVjgwWSWfNVXLjfbtYFUhvlY6d_cN5E_ZRVvZDxDUnlK-M1IelmAiI-XnbvGH3dFv4TMD51-B4k0zf8gzv4Urqf9GEZXPZqHYO1c8HuRMCKrxCaV3bMvdVJQmV6NOEDLcuFq2s3F9l8yaWzmgtAGe9GUPDRvR2_6cW5nqxRgPrzrOLyuLnh1trll6Ml5lWRKOrEXyzB6fVvfwk0o_VDD3A
│ 	status code: 403, request id: f9e1af94-f155-49cb-a546-9134859d2746
│ 
│   with aws_instance.example,
│   on main.tf line 12, in resource "aws_instance" "example":
│   12: resource "aws_instance" "example" {
│ 
╵
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# vim main.tf 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform init
There are some problems with the configuration, described below.

The Terraform configuration must be valid before initialization so that
Terraform can determine which modules and providers need to be installed.
╷
│ Error: Unsupported argument
│ 
│   on main.tf line 3, in terraform:
│    3:   key    = "/root/.aws/credentials"	
│ 
│ An argument named "key" is not expected here.
╵
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# vim main.tf 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform state list
```
Выполнение добавления переменных и запуск terraform по рекомендации из [Authenticating to AWS with Environment Variables](https://blog.gruntwork.io/authenticating-to-aws-with-environment-variables-e793d6f6d02e)
результат не дало. аутентификация терраформа не проходит
```tf
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# export AWS_ACCESS_KEY_ID=AKIAWVMKWHEXCVVYEBFX
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# export AWS_SECRET_ACCESS_KEY=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
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform apply

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # aws_instance.example will be created
  + resource "aws_instance" "example" {
      + ami                          = "ami-0892d3c7ee96c0bf7"
      + arn                          = (known after apply)
      + associate_public_ip_address  = (known after apply)
      + availability_zone            = (known after apply)
      + cpu_core_count               = (known after apply)
      + cpu_threads_per_core         = (known after apply)
      + get_password_data            = false
      + host_id                      = (known after apply)
      + id                           = (known after apply)
      + instance_state               = (known after apply)
      + instance_type                = "t2.micro"
      + ipv6_address_count           = (known after apply)
      + ipv6_addresses               = (known after apply)
      + key_name                     = (known after apply)
      + network_interface_id         = (known after apply)
      + outpost_arn                  = (known after apply)
      + password_data                = (known after apply)
      + placement_group              = (known after apply)
      + primary_network_interface_id = (known after apply)
      + private_dns                  = (known after apply)
      + private_ip                   = (known after apply)
      + public_dns                   = (known after apply)
      + public_ip                    = (known after apply)
      + security_groups              = (known after apply)
      + source_dest_check            = true
      + subnet_id                    = (known after apply)
      + tags                         = {
          + "Name" = "terraform-example"
        }
      + tenancy                      = (known after apply)
      + volume_tags                  = (known after apply)
      + vpc_security_group_ids       = (known after apply)

      + ebs_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + snapshot_id           = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }

      + ephemeral_block_device {
          + device_name  = (known after apply)
          + no_device    = (known after apply)
          + virtual_name = (known after apply)
        }

      + metadata_options {
          + http_endpoint               = (known after apply)
          + http_put_response_hop_limit = (known after apply)
          + http_tokens                 = (known after apply)
        }

      + network_interface {
          + delete_on_termination = (known after apply)
          + device_index          = (known after apply)
          + network_interface_id  = (known after apply)
        }

      + root_block_device {
          + delete_on_termination = (known after apply)
          + device_name           = (known after apply)
          + encrypted             = (known after apply)
          + iops                  = (known after apply)
          + kms_key_id            = (known after apply)
          + volume_id             = (known after apply)
          + volume_size           = (known after apply)
          + volume_type           = (known after apply)
        }
    }

Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

aws_instance.example: Creating...
╷
│ Error: Error launching source instance: UnauthorizedOperation: You are not authorized to perform this operation. Encoded authorization failure message: skY8pWON6taZ9L3uFxAnOfDSxcdE-0S7QAYBlkX7m4TFUYel7ZVPYs8MSF7OECdkJSfaH2GkGfcmAoe6f-fWzMF-mXAzBhDAFQB4j-nKvWCmlUd5351jMo82022tM5fTKlLWoffZ6_D0p6mZd5abGDFWq3O4DSGCgrl2napQyV1pSiILOXbhZNszOEJRQtHAyf7M_WuZ4z2KrmgHosIC5B18bPvQ_iKZFJdiR_FDSkG136udrm2G_WWH7moj7u97oYbXi2aAL4zEfUvLU-qhNpDWihoHmm60GYr3Wx3q4O230AgNiIlueJeL_shAmOAwZgPiQj8BKZThTRJAbqE42Sx9YcxA32IWx7zPOL7w37UCPk048GNzbkUZRMImIHP8AJiIH4umGgcYbnGCXNAv984z7zwVU01hI58PUg8WwzZj7FuG_HjhgPG-uRCdfHhZsXKoMsVjSIc25kpc2KRY9O1X_4aBCEX7fm-6wccM4SZpfWi5OWIvy3D1gjKiLOxiSdRXoFLyMJ2ZntSdCXQ2Mf2wEAXok_E-7dB17jRfr51DCRU8p0Ny7FdPUglrYADFaboctm4XSfYAfeAM1kNdGiuqzcmj3UzLOkomzOYdH1rVR5MdyYslnnoeQ46_o0aJJSfhp45bC4RWhZRQd027Phv3Y2GZhPAGnT4K9Kz1t4G-F9EgPUaIYzugD55Y3xBooto-aRfGr1x_FRuTWL5f8Yd97X4wqBzbkz1S89sVSVkRQx7MgwkXENO7KA6RwN2MyHcoU21vIFmT9HIPc-bxb6xue_qZ6_Uc63gbAfcM55iloRTebzu2WQJuIsMBWcjhS1noXqTklmfGraBh2mi5yUVzAQqtmqqYs8t72IYxzv6LHd5FRC6-4UOxBHLe_YjtbUjt_ewf6YsG6jt4BE8BEX3dgruYaxdfbeFBxGSS1dD112tec5jxkxe3zWXe4nFswNVDO8MQ-sdl3aV119-RRY3A66n3bre08AF0uYgikrNAEpZ-d8YooQVBtKjCs0a2Bd-lKiPkJISWa9Vhej7mbUzk5AZOCJxMZq5o_G9djv-N2DjR5GTDWDX1m-tqt1F-a1nMFDSG_D8jK4KfUeh9nI46vavKfgLU56udqt-j4bIwqXeezxgF1QILKbqh9PmIyqxv2QQ2U5M3AyhLWxye8Ipde-K0mDgjxA7CYgyyIJvBGBhMMMQN4fq1trdLvdruBRRByRNJPEObseQh4Art7eHsPbL974jJhNOObr8PLqo1FWtbWWNOZwWurL7LsYbYDs2j6RqQ5Rz9uVBi4zH6ye-VYHqBlncOiA9jldUJF61AbunAdOQR2m4GaYNm1XmGpvpsDA
│ 	status code: 403, request id: 71f2aeb6-b6b9-48cc-8777-da3aee5fe681
│ 
│   with aws_instance.example,
│   on main.tf line 13, in resource "aws_instance" "example":
│   13: resource "aws_instance" "example" {
│ 
╵
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# aws configure list
      Name                    Value             Type    Location
      ----                    -----             ----    --------
   profile                <not set>             None    None
access_key     ****************EBFX              env    
secret_key     ****************HNCZ              env    
    region                us-west-2      config-file    ~/.aws/config
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# aws sts decode-authorization-message --encoded-message (Error launching source instance: UnauthorizedOperation: You are not authorized to perform this operation. Encoded authorization failure message: skY8pWON6taZ9L3uFxAnOfDSxcdE-0S7QAYBlkX7m4TFUYel7ZVPYs8MSF7OECdkJSfaH2GkGfcmAoe6f-fWzMF-mXAzBhDAFQB4j-nKvWCmlUd5351jMo82022tM5fTKlLWoffZ6_D0p6mZd5abGDFWq3O4DSGCgrl2napQyV1pSiILOXbhZNszOEJRQtHAyf7M_WuZ4z2KrmgHosIC5B18bPvQ_iKZFJdiR_FDSkG136udrm2G_WWH7moj7u97oYbXi2aAL4zEfUvLU-qhNpDWihoHmm60GYr3Wx3q4O230AgNiIlueJeL_shAmOAwZgPiQj8BKZThTRJAbqE42Sx9YcxA32IWx7zPOL7w37UCPk048GNzbkUZRMImIHP8AJiIH4umGgcYbnGCXNAv984z7zwVU01hI58PUg8WwzZj7FuG_HjhgPG-uRCdfHhZsXKoMsVjSIc25kpc2KRY9O1X_4aBCEX7fm-6wccM4SZpfWi5OWIvy3D1gjKiLOxiSdRXoFLyMJ2ZntSdCXQ2Mf2wEAXok_E-7dB17jRfr51DCRU8p0Ny7FdPUglrYADFaboctm4XSfYAfeAM1kNdGiuqzcmj3UzLOkomzOYdH1rVR5MdyYslnnoeQ46_o0aJJSfhp45bC4RWhZRQd027Phv3Y2GZhPAGnT4K9Kz1t4G-F9EgPUaIYzugD55Y3xBooto-aRfGr1x_FRuTWL5f8Yd97X4wqBzbkz1S89sVSVkRQx7MgwkXENO7KA6RwN2MyHcoU21vIFmT9HIPc-bxb6xue_qZ6_Uc63gbAfcM55iloRTebzu2WQJuIsMBWcjhS1noXqTklmfGraBh2mi5yUVzAQqtmqqYs8t72IYxzv6LHd5FRC6-4UOxBHLe_YjtbUjt_ewf6YsG6jt4BE8BEX3dgruYaxdfbeFBxGSS1dD112tec5jxkxe3zWXe4nFswNVDO8MQ-sdl3aV119-RRY3A66n3bre08AF0uYgikrNAEpZ-d8YooQVBtKjCs0a2Bd-lKiPkJISWa9Vhej7mbUzk5AZOCJxMZq5o_G9djv-N2DjR5GTDWDX1m-tqt1F-a1nMFDSG_D8jK4KfUeh9nI46vavKfgLU56udqt-j4bIwqXeezxgF1QILKbqh9PmIyqxv2QQ2U5M3AyhLWxye8Ipde-K0mDgjxA7CYgyyIJvBGBhMMMQN4fq1trdLvdruBRRByRNJPEObseQh4Art7eHsPbL974jJhNOObr8PLqo1FWtbWWNOZwWurL7LsYbYDs2j6RqQ5Rz9uVBi4zH6ye-VYHqBlncOiA9jldUJF61AbunAdOQR2m4GaYNm1XmGpvpsDA) --query DecodedMessage --output text | jq '.'
-bash: синтаксическая ошибка рядом с неожиданным маркером «(»
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# aws sts decode-authorization-message --encoded-message (skY8pWON6taZ9L3uFxAnOfDSxcdE-0S7QAYBlkX7m4TFUYel7ZVPYs8MSF7OECdkJSfaH2GkGfcmAoe6f-fWzMF-mXAzBhDAFQB4j-nKvWCmlUd5351jMo82022tM5fTKlLWoffZ6_D0p6mZd5abGDFWq3O4DSGCgrl2napQyV1pSiILOXbhZNszOEJRQtHAyf7M_WuZ4z2KrmgHosIC5B18bPvQ_iKZFJdiR_FDSkG136udrm2G_WWH7moj7u97oYbXi2aAL4zEfUvLU-qhNpDWihoHmm60GYr3Wx3q4O230AgNiIlueJeL_shAmOAwZgPiQj8BKZThTRJAbqE42Sx9YcxA32IWx7zPOL7w37UCPk048GNzbkUZRMImIHP8AJiIH4umGgcYbnGCXNAv984z7zwVU01hI58PUg8WwzZj7FuG_HjhgPG-uRCdfHhZsXKoMsVjSIc25kpc2KRY9O1X_4aBCEX7fm-6wccM4SZpfWi5OWIvy3D1gjKiLOxiSdRXoFLyMJ2ZntSdCXQ2Mf2wEAXok_E-7dB17jRfr51DCRU8p0Ny7FdPUglrYADFaboctm4XSfYAfeAM1kNdGiuqzcmj3UzLOkomzOYdH1rVR5MdyYslnnoeQ46_o0aJJSfhp45bC4RWhZRQd027Phv3Y2GZhPAGnT4K9Kz1t4G-F9EgPUaIYzugD55Y3xBooto-aRfGr1x_FRuTWL5f8Yd97X4wqBzbkz1S89sVSVkRQx7MgwkXENO7KA6RwN2MyHcoU21vIFmT9HIPc-bxb6xue_qZ6_Uc63gbAfcM55iloRTebzu2WQJuIsMBWcjhS1noXqTklmfGraBh2mi5yUVzAQqtmqqYs8t72IYxzv6LHd5FRC6-4UOxBHLe_YjtbUjt_ewf6YsG6jt4BE8BEX3dgruYaxdfbeFBxGSS1dD112tec5jxkxe3zWXe4nFswNVDO8MQ-sdl3aV119-RRY3A66n3bre08AF0uYgikrNAEpZ-d8YooQVBtKjCs0a2Bd-lKiPkJISWa9Vhej7mbUzk5AZOCJxMZq5o_G9djv-N2DjR5GTDWDX1m-tqt1F-a1nMFDSG_D8jK4KfUeh9nI46vavKfgLU56udqt-j4bIwqXeezxgF1QILKbqh9PmIyqxv2QQ2U5M3AyhLWxye8Ipde-K0mDgjxA7CYgyyIJvBGBhMMMQN4fq1trdLvdruBRRByRNJPEObseQh4Art7eHsPbL974jJhNOObr8PLqo1FWtbWWNOZwWurL7LsYbYDs2j6RqQ5Rz9uVBi4zH6ye-VYHqBlncOiA9jldUJF61AbunAdOQR2m4GaYNm1XmGpvpsDA)
-bash: синтаксическая ошибка рядом с неожиданным маркером «(»
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# aws sts decode-authorization-message --encoded-message (skY8pWON6taZ9L3uFxAnOfDSxcdE-0S7QAYBlkX7m4TFUYel7ZVPYs8MSF7OECdkJSfaH2GkGfcmAoe6f-fWzMF-mXAzBhDAFQB4j-nKvWCmlUd5351jMo82022tM5fTKlLWoffZ6_D0p6mZd5abGDFWq3O4DSGCgrl2napQyV1pSiILOXbhZNszOEJRQtHAyf7M_WuZ4z2KrmgHosIC5B18bPvQ_iKZFJdiR_FDSkG136udrm2G_WWH7moj7u97oYbXi2aAL4zEfUvLU-qhNpDWihoHmm60GYr3Wx3q4O230AgNiIlueJeL_shAmOAwZgPiQj8BKZThTRJAbqE42Sx9YcxA32IWx7zPOL7w37UCPk048GNzbkUZRMImIHP8AJiIH4umGgcYbnGCXNAv984z7zwVU01hI58PUg8WwzZj7FuG_HjhgPG-uRCdfHhZsXKoMsVjSIc25kpc2KRY9O1X_4aBCEX7fm-6wccM4SZpfWi5OWIvy3D1gjKiLOxiSdRXoFLyMJ2ZntSdCXQ2Mf2wEAXok_E-7dB17jRfr51DCRU8p0Ny7FdPUglrYADFaboctm4XSfYAfeAM1kNdGiuqzcmj3UzLOkomzOYdH1rVR5MdyYslnnoeQ46_o0aJJSfhp45bC4RWhZRQd027Phv3Y2GZhPAGnT4K9Kz1t4G-F9EgPUaIYzugD55Y3xBooto-aRfGr1x_FRuTWL5f8Yd97X4wqBzbkz1S89sVSVkRQx7MgwkXENO7KA6RwN2MyHcoU21vIFmT9HIPc-bxb6xue_qZ6_Uc63gbAfcM55iloRTebzu2WQJuIsMBWcjhS1noXqTklmfGraBh2mi5yUVzAQqtmqqYs8t72IYxzv6LHd5FRC6-4UOxBHLe_YjtbUjt_ewf6YsG6jt4BE8BEX3dgruYaxdfbeFBxGSS1dD112tec5jxkxe3zWXe4nFswNVDO8MQ-sdl3aV119-RRY3A66n3bre08AF0uYgikrNAEpZ-d8YooQVBtKjCs0a2Bd-lKiPkJISWa9Vhej7mbUzk5AZOCJxMZq5o_G9djv-N2DjR5GTDWDX1m-tqt1F-a1nMFDSG_D8jK4KfUeh9nI46vavKfgLU56udqt-j4bIwqXeezxgF1QILKbqh9PmIyqxv2QQ2U5M3AyhLWxye8Ipde-K0mDgjxA7CYgyyIJvBGBhMMMQN4fq1trdLvdruBRRByRNJPEObseQh4Art7eHsPbL974jJhNOObr8PLqo1FWtbWWNOZwWurL7LsYbYDs2j6RqQ5Rz9uVBi4zH6ye-VYHqBlncOiA9jldUJF61AbunAdOQR2m4GaYNm1XmGpvpsDA
-bash: синтаксическая ошибка рядом с неожиданным маркером «(»
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# aws sts decode-authorization-message --encoded-message skY8pWON6taZ9L3uFxAnOfDSxcdE-0S7QAYBlkX7m4TFUYel7ZVPYs8MSF7OECdkJSfaH2GkGfcmAoe6f-fWzMF-mXAzBhDAFQB4j-nKvWCmlUd5351jMo82022tM5fTKlLWoffZ6_D0p6mZd5abGDFWq3O4DSGCgrl2napQyV1pSiILOXbhZNszOEJRQtHAyf7M_WuZ4z2KrmgHosIC5B18bPvQ_iKZFJdiR_FDSkG136udrm2G_WWH7moj7u97oYbXi2aAL4zEfUvLU-qhNpDWihoHmm60GYr3Wx3q4O230AgNiIlueJeL_shAmOAwZgPiQj8BKZThTRJAbqE42Sx9YcxA32IWx7zPOL7w37UCPk048GNzbkUZRMImIHP8AJiIH4umGgcYbnGCXNAv984z7zwVU01hI58PUg8WwzZj7FuG_HjhgPG-uRCdfHhZsXKoMsVjSIc25kpc2KRY9O1X_4aBCEX7fm-6wccM4SZpfWi5OWIvy3D1gjKiLOxiSdRXoFLyMJ2ZntSdCXQ2Mf2wEAXok_E-7dB17jRfr51DCRU8p0Ny7FdPUglrYADFaboctm4XSfYAfeAM1kNdGiuqzcmj3UzLOkomzOYdH1rVR5MdyYslnnoeQ46_o0aJJSfhp45bC4RWhZRQd027Phv3Y2GZhPAGnT4K9Kz1t4G-F9EgPUaIYzugD55Y3xBooto-aRfGr1x_FRuTWL5f8Yd97X4wqBzbkz1S89sVSVkRQx7MgwkXENO7KA6RwN2MyHcoU21vIFmT9HIPc-bxb6xue_qZ6_Uc63gbAfcM55iloRTebzu2WQJuIsMBWcjhS1noXqTklmfGraBh2mi5yUVzAQqtmqqYs8t72IYxzv6LHd5FRC6-4UOxBHLe_YjtbUjt_ewf6YsG6jt4BE8BEX3dgruYaxdfbeFBxGSS1dD112tec5jxkxe3zWXe4nFswNVDO8MQ-sdl3aV119-RRY3A66n3bre08AF0uYgikrNAEpZ-d8YooQVBtKjCs0a2Bd-lKiPkJISWa9Vhej7mbUzk5AZOCJxMZq5o_G9djv-N2DjR5GTDWDX1m-tqt1F-a1nMFDSG_D8jK4KfUeh9nI46vavKfgLU56udqt-j4bIwqXeezxgF1QILKbqh9PmIyqxv2QQ2U5M3AyhLWxye8Ipde-K0mDgjxA7CYgyyIJvBGBhMMMQN4fq1trdLvdruBRRByRNJPEObseQh4Art7eHsPbL974jJhNOObr8PLqo1FWtbWWNOZwWurL7LsYbYDs2j6RqQ5Rz9uVBi4zH6ye-VYHqBlncOiA9jldUJF61AbunAdOQR2m4GaYNm1XmGpvpsDA

An error occurred (AccessDenied) when calling the DecodeAuthorizationMessage operation: User: arn:aws:iam::458241751342:user/sergey.zakharov is not authorized to perform: sts:DecodeAuthorizationMessage because no identity-based policy allows the sts:DecodeAuthorizationMessage action
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# ls -l
итого 16
-rw-r--r-- 1 root root  384 янв  4 17:07 main.tf
drwxr-xr-x 2 root root 4096 янв  4 15:58 modules
-rw-r--r-- 1 root root    0 янв  4 15:50 outputs.tf
-rw-r--r-- 1 root root  257 янв  4 15:54 README.md
-rw-r--r-- 1 root root  155 янв  4 17:17 terraform.tfstate
-rw-r--r-- 1 root root    0 янв  4 15:50 variables.tf
-rw-r--r-- 1 root root    0 янв  4 15:50 version.tf
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# vim main.tf 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 


```
### 3 часть

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# aws sts decode-authorization-message --encoded-message skY8pWON6taZ9L3uFxAnOfDSxcdE-0S7QAYBlkX7m4TFUYel7ZVPYs8MSF7OECdkJSfaH2GkGfcmAoe6f-fWzMF-mXAzBhDAFQB4j-nKvWCmlUd5351jMo82022tM5fTKlLWoffZ6_D0p6mZd5abGDFWq3O4DSGCgrl2napQyV1pSiILOXbhZNszOEJRQtHAyf7M_WuZ4z2KrmgHosIC5B18bPvQ_iKZFJdiR_FDSkG136udrm2G_WWH7moj7u97oYbXi2aAL4zEfUvLU-qhNpDWihoHmm60GYr3Wx3q4O230AgNiIlueJeL_shAmOAwZgPiQj8BKZThTRJAbqE42Sx9YcxA32IWx7zPOL7w37UCPk048GNzbkUZRMImIHP8AJiIH4umGgcYbnGCXNAv984z7zwVU01hI58PUg8WwzZj7FuG_HjhgPG-uRCdfHhZsXKoMsVjSIc25kpc2KRY9O1X_4aBCEX7fm-6wccM4SZpfWi5OWIvy3D1gjKiLOxiSdRXoFLyMJ2ZntSdCXQ2Mf2wEAXok_E-7dB17jRfr51DCRU8p0Ny7FdPUglrYADFaboctm4XSfYAfeAM1kNdGiuqzcmj3UzLOkomzOYdH1rVR5MdyYslnnoeQ46_o0aJJSfhp45bC4RWhZRQd027Phv3Y2GZhPAGnT4K9Kz1t4G-F9EgPUaIYzugD55Y3xBooto-aRfGr1x_FRuTWL5f8Yd97X4wqBzbkz1S89sVSVkRQx7MgwkXENO7KA6RwN2MyHcoU21vIFmT9HIPc-bxb6xue_qZ6_Uc63gbAfcM55iloRTebzu2WQJuIsMBWcjhS1noXqTklmfGraBh2mi5yUVzAQqtmqqYs8t72IYxzv6LHd5FRC6-4UOxBHLe_YjtbUjt_ewf6YsG6jt4BE8BEX3dgruYaxdfbeFBxGSS1dD112tec5jxkxe3zWXe4nFswNVDO8MQ-sdl3aV119-RRY3A66n3bre08AF0uYgikrNAEpZ-d8YooQVBtKjCs0a2Bd-lKiPkJISWa9Vhej7mbUzk5AZOCJxMZq5o_G9djv-N2DjR5GTDWDX1m-tqt1F-a1nMFDSG_D8jK4KfUeh9nI46vavKfgLU56udqt-j4bIwqXeezxgF1QILKbqh9PmIyqxv2QQ2U5M3AyhLWxye8Ipde-K0mDgjxA7CYgyyIJvBGBhMMMQN4fq1trdLvdruBRRByRNJPEObseQh4Art7eHsPbL974jJhNOObr8PLqo1FWtbWWNOZwWurL7LsYbYDs2j6RqQ5Rz9uVBi4zH6ye-VYHqBlncOiA9jldUJF61AbunAdOQR2m4GaYNm1XmGpvpsDA

An error occurred (AccessDenied) when calling the DecodeAuthorizationMessage operation: User: arn:aws:iam::458241751342:user/sergey.zakharov is not authorized to perform: sts:DecodeAuthorizationMessage because no identity-based policy allows the sts:DecodeAuthorizationMessage action
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# aws sts decode-authorization-message --encoded-message skY8pWON6taZ9L3uFxAnOfDSxcdE-0S7QAYBlkX7m4TFUYel7ZVPYs8MSF7OECdkJSfaH2GkGfcmAoe6f-fWzMF-mXAzBhDAFQB4j-nKvWCmlUd5351jMo82022tM5fTKlLWoffZ6_D0p6mZd5abGDFWq3O4DSGCgrl2napQyV1pSiILOXbhZNszOEJRQtHAyf7M_WuZ4z2KrmgHosIC5B18bPvQ_iKZFJdiR_FDSkG136udrm2G_WWH7moj7u97oYbXi2aAL4zEfUvLU-qhNpDWihoHmm60GYr3Wx3q4O230AgNiIlueJeL_shAmOAwZgPiQj8BKZThTRJAbqE42Sx9YcxA32IWx7zPOL7w37UCPk048GNzbkUZRMImIHP8AJiIH4umGgcYbnGCXNAv984z7zwVU01hI58PUg8WwzZj7FuG_HjhgPG-uRCdfHhZsXKoMsVjSIc25kpc2KRY9O1X_4aBCEX7fm-6wccM4SZpfWi5OWIvy3D1gjKiLOxiSdRXoFLyMJ2ZntSdCXQ2Mf2wEAXok_E-7dB17jRfr51DCRU8p0Ny7FdPUglrYADFaboctm4XSfYAfeAM1kNdGiuqzcmj3UzLOkomzOYdH1rVR5MdyYslnnoeQ46_o0aJJSfhp45bC4RWhZRQd027Phv3Y2GZhPAGnT4K9Kz1t4G-F9EgPUaIYzugD55Y3xBooto-aRfGr1x_FRuTWL5f8Yd97X4wqBzbkz1S89sVSVkRQx7MgwkXENO7KA6RwN2MyHcoU21vIFmT9HIPc-bxb6xue_qZ6_Uc63gbAfcM55iloRTebzu2WQJuIsMBWcjhS1noXqTklmfGraBh2mi5yUVzAQqtmqqYs8t72IYxzv6LHd5FRC6-4UOxBHLe_YjtbUjt_ewf6YsG6jt4BE8BEX3dgruYaxdfbeFBxGSS1dD112tec5jxkxe3zWXe4nFswNVDO8MQ-sdl3aV119-RRY3A66n3bre08AF0uYgikrNAEpZ-d8YooQVBtKjCs0a2Bd-lKiPkJISWa9Vhej7mbUzk5AZOCJxMZq5o_G9djv-N2DjR5GTDWDX1m-tqt1F-a1nMFDSG_D8jK4KfUeh9nI46vavKfgLU56udqt-j4bIwqXeezxgF1QILKbqh9PmIyqxv2QQ2U5M3AyhLWxye8Ipde-K0mDgjxA7CYgyyIJvBGBhMMMQN4fq1trdLvdruBRRByRNJPEObseQh4Art7eHsPbL974jJhNOObr8PLqo1FWtbWWNOZwWurL7LsYbYDs2j6RqQ5Rz9uVBi4zH6ye-VYHqBlncOiA9jldUJF61AbunAdOQR2m4GaYNm1XmGpvpsDA --query DecodedMessage --output text | jq '.'

Команда «jq» не найдена, но может быть установлена с помощью:

snap install jq  # version 1.5+dfsg-1, or
apt  install jq  # version 1.6-1ubuntu0.20.04.1

See 'snap info jq' for additional versions.


An error occurred (AccessDenied) when calling the DecodeAuthorizationMessage operation: User: arn:aws:iam::458241751342:user/sergey.zakharov is not authorized to perform: sts:DecodeAuthorizationMessage because no identity-based policy allows the sts:DecodeAuthorizationMessage action
```
Установка утилиты jq - Command-line JSON processor
```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# apt  install jq
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
Будут установлены следующие дополнительные пакеты:
  libjq1 libonig5
Следующие НОВЫЕ пакеты будут установлены:
  jq libjq1 libonig5
Обновлено 0 пакетов, установлено 3 новых пакетов, для удаления отмечено 0 пакетов, и 0 пакетов не обновлено.
Необходимо скачать 313 kB архивов.
После данной операции объём занятого дискового пространства возрастёт на 1 062 kB.
Хотите продолжить? [Д/н] y
Пол:1 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 libonig5 amd64 6.9.4-1 [142 kB]
Пол:2 http://ru.archive.ubuntu.com/ubuntu focal-updates/universe amd64 libjq1 amd64 1.6-1ubuntu0.20.04.1 [121 kB]
Пол:3 http://ru.archive.ubuntu.com/ubuntu focal-updates/universe amd64 jq amd64 1.6-1ubuntu0.20.04.1 [50,2 kB]
Получено 313 kB за 0с (717 kB/s)
Выбор ранее не выбранного пакета libonig5:amd64.
(Чтение базы данных … на данный момент установлено 231827 файлов и каталогов.)
Подготовка к распаковке …/libonig5_6.9.4-1_amd64.deb …
Распаковывается libonig5:amd64 (6.9.4-1) …
Выбор ранее не выбранного пакета libjq1:amd64.
Подготовка к распаковке …/libjq1_1.6-1ubuntu0.20.04.1_amd64.deb …
Распаковывается libjq1:amd64 (1.6-1ubuntu0.20.04.1) …
Выбор ранее не выбранного пакета jq.
Подготовка к распаковке …/jq_1.6-1ubuntu0.20.04.1_amd64.deb …
Распаковывается jq (1.6-1ubuntu0.20.04.1) …
Настраивается пакет libonig5:amd64 (6.9.4-1) …
Настраивается пакет libjq1:amd64 (1.6-1ubuntu0.20.04.1) …
Настраивается пакет jq (1.6-1ubuntu0.20.04.1) …
Обрабатываются триггеры для man-db (2.9.1-1) …
Обрабатываются триггеры для libc-bin (2.31-0ubuntu9.2) …
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# aws sts decode-authorization-message --encoded-message skY8pWON6taZ9L3uFxAnOfDSxcdE-0S7QAYBlkX7m4TFUYel7ZVPYs8MSF7OECdkJSfaH2GkGfcmAoe6f-fWzMF-mXAzBhDAFQB4j-nKvWCmlUd5351jMo82022tM5fTKlLWoffZ6_D0p6mZd5abGDFWq3O4DSGCgrl2napQyV1pSiILOXbhZNszOEJRQtHAyf7M_WuZ4z2KrmgHosIC5B18bPvQ_iKZFJdiR_FDSkG136udrm2G_WWH7moj7u97oYbXi2aAL4zEfUvLU-qhNpDWihoHmm60GYr3Wx3q4O230AgNiIlueJeL_shAmOAwZgPiQj8BKZThTRJAbqE42Sx9YcxA32IWx7zPOL7w37UCPk048GNzbkUZRMImIHP8AJiIH4umGgcYbnGCXNAv984z7zwVU01hI58PUg8WwzZj7FuG_HjhgPG-uRCdfHhZsXKoMsVjSIc25kpc2KRY9O1X_4aBCEX7fm-6wccM4SZpfWi5OWIvy3D1gjKiLOxiSdRXoFLyMJ2ZntSdCXQ2Mf2wEAXok_E-7dB17jRfr51DCRU8p0Ny7FdPUglrYADFaboctm4XSfYAfeAM1kNdGiuqzcmj3UzLOkomzOYdH1rVR5MdyYslnnoeQ46_o0aJJSfhp45bC4RWhZRQd027Phv3Y2GZhPAGnT4K9Kz1t4G-F9EgPUaIYzugD55Y3xBooto-aRfGr1x_FRuTWL5f8Yd97X4wqBzbkz1S89sVSVkRQx7MgwkXENO7KA6RwN2MyHcoU21vIFmT9HIPc-bxb6xue_qZ6_Uc63gbAfcM55iloRTebzu2WQJuIsMBWcjhS1noXqTklmfGraBh2mi5yUVzAQqtmqqYs8t72IYxzv6LHd5FRC6-4UOxBHLe_YjtbUjt_ewf6YsG6jt4BE8BEX3dgruYaxdfbeFBxGSS1dD112tec5jxkxe3zWXe4nFswNVDO8MQ-sdl3aV119-RRY3A66n3bre08AF0uYgikrNAEpZ-d8YooQVBtKjCs0a2Bd-lKiPkJISWa9Vhej7mbUzk5AZOCJxMZq5o_G9djv-N2DjR5GTDWDX1m-tqt1F-a1nMFDSG_D8jK4KfUeh9nI46vavKfgLU56udqt-j4bIwqXeezxgF1QILKbqh9PmIyqxv2QQ2U5M3AyhLWxye8Ipde-K0mDgjxA7CYgyyIJvBGBhMMMQN4fq1trdLvdruBRRByRNJPEObseQh4Art7eHsPbL974jJhNOObr8PLqo1FWtbWWNOZwWurL7LsYbYDs2j6RqQ5Rz9uVBi4zH6ye-VYHqBlncOiA9jldUJF61AbunAdOQR2m4GaYNm1XmGpvpsDA --query DecodedMessage --output text | jq '.'

An error occurred (AccessDenied) when calling the DecodeAuthorizationMessage operation: User: arn:aws:iam::458241751342:user/sergey.zakharov is not authorized to perform: sts:DecodeAuthorizationMessage because no identity-based policy allows the sts:DecodeAuthorizationMessage action
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform help
Terraform has no command named "help".

To see all of Terraform's top-level commands, run:
  terraform -help
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform -help
Usage: terraform [global options] <subcommand> [args]

The available commands for execution are listed below.
The primary workflow commands are given first, followed by
less common or more advanced commands.

Main commands:
  init          Prepare your working directory for other commands
  validate      Check whether the configuration is valid
  plan          Show changes required by the current configuration
  apply         Create or update infrastructure
  destroy       Destroy previously-created infrastructure

All other commands:
  console       Try Terraform expressions at an interactive command prompt
  fmt           Reformat your configuration in the standard style
  force-unlock  Release a stuck lock on the current workspace
  get           Install or upgrade remote Terraform modules
  graph         Generate a Graphviz graph of the steps in an operation
  import        Associate existing infrastructure with a Terraform resource
  login         Obtain and save credentials for a remote host
  logout        Remove locally-stored credentials for a remote host
  output        Show output values from your root module
  providers     Show the providers required for this configuration
  refresh       Update the state to match remote systems
  show          Show the current state or a saved plan
  state         Advanced state management
  taint         Mark a resource instance as not fully functional
  test          Experimental support for module integration testing
  untaint       Remove the 'tainted' state from a resource instance
  version       Show the current Terraform version
  workspace     Workspace management

Global options (use these before the subcommand, if any):
  -chdir=DIR    Switch to a different working directory before executing the
                given subcommand.
  -help         Show this help output, or the help for a specified subcommand.
  -version      An alias for the "version" subcommand.
  ```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform output
╷
│ Error: Unsupported block type
│ 
│   on main.tf line 4, in terraform:
│    4:   data "aws_caller_identity" "current" {
│ 
│ Blocks of type "data" are not expected here.
╵
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform show
╷
│ Error: Unsupported block type
│ 
│   on main.tf line 4, in terraform:
│    4:   data "aws_caller_identity" "current" {
│ 
│ Blocks of type "data" are not expected here.
╵

root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# vim main.tf 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform show
╷
│ Error: Argument or block definition required
│ 
│   on main.tf line 16:
│   16: }
│ 
│ An argument or block definition is required here.
╵

root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# vim main.tf 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform show

root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# terraform output
╷
│ Warning: No outputs found
│ 
│ The state file either has no outputs defined, or all the defined outputs are empty. Please define an output in your configuration with the `output` keyword and run `terraform refresh` for it to become
│ available. If you are using interpolation, please verify the interpolated value is not empty. You can use the `terraform console` command to assist.
╵
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
```

```ps
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# echo $$
165474
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# type mc
для mc вычислен хэш (/usr/bin/mc)
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# echo $$
165474
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# echo $
$
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# echo $PATH
/root/yandex-cloud/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# echo $AWS_ACCESS_KEY_ID
AKIAWVMKWHEXCVVYEBFX
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# echo $AWS_SECRET_ACCESS_KEY
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
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 
root@PC-Ubuntu:~/netology-project/learning-terraform/aws-cloud-learning/my-project/Alfa# 


```
