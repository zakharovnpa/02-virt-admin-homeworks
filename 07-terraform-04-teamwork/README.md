# "7.4. Средства командной работы над инфраструктурой." - Захаров Сергей Николаевич

## Задача 1. Настроить terraform cloud (необязательно, но крайне желательно).

В это задании предлагается познакомиться со средством командой работы над инфраструктурой предоставляемым
разработчиками терраформа. 

1. Зарегистрируйтесь на [https://app.terraform.io/](https://app.terraform.io/).
(регистрация бесплатная и не требует использования платежных инструментов).
1. Создайте в своем github аккаунте (или другом хранилище репозиториев) отдельный репозиторий с
 конфигурационными файлами прошлых занятий (или воспользуйтесь любым простым конфигом).
1. Зарегистрируйте этот репозиторий в [https://app.terraform.io/](https://app.terraform.io/).
1. Выполните plan и apply. 

В качестве результата задания приложите снимок экрана с успешным применением конфигурации.

**Ответ:**

Задание выполнено частично:
1. Создана УЗ на [https://app.terraform.io/](https://app.terraform.io/).
2. Создан отдельный репозиторий в моем github
3. Создана организация
4. На фазе подключения организации к SVC github столкнулся с ошибкой подключения.

## Задача 2. Написать серверный конфиг для атлантиса. 

Смысл задания – познакомиться с документацией 
о [серверной](https://www.runatlantis.io/docs/server-side-repo-config.html) конфигурации и конфигурации уровня 
 [репозитория](https://www.runatlantis.io/docs/repo-level-atlantis-yaml.html).

Создай `server.yaml` который скажет атлантису:
1. Укажите, что атлантис должен работать только для репозиториев в вашем github (или любом другом) аккаунте.
1. На стороне клиентского конфига разрешите изменять `workflow`, то есть для каждого репозитория можно 
будет указать свои дополнительные команды. 
1. В `workflow` используемом по-умолчанию сделайте так, что бы во время планирования не происходил `lock` состояния.

Создай `atlantis.yaml` который, если поместить в корень terraform проекта, скажет атлантису:
1. Надо запускать планирование и аплай для двух воркспейсов `stage` и `prod`.
1. Необходимо включить автопланирование при изменении любых файлов `*.tf`.

В качестве результата приложите ссылку на файлы `server.yaml` и `atlantis.yaml`.

**Ответ:**

Создан `server.yaml` который говорит Атлантису:
1. Должен работать только для репозиториев в моем github аккаунте.
2. На стороне клиентского конфига разрешено изменять `workflow`, то есть для каждого репозитория можно будет указать свои дополнительные команды. 
3. В `workflow`, используемом по-умолчанию, во время планирования не происходил `lock` состояния.

```yml

repos:
 - id: github.com/zakharovnpa/experiments-netology   # 1. Должен работать только для репозиториев в моем github аккаунте.
 branch: /.*/
 apply_requirements: [approved, mergeable]

 workflow: custom
 allowed_overrides: [apply_requirements, workflow, delete_source_branch_on_merge]
 allowed_workflows: [custom]
 allow_custom_workflows: true
  
      
workflows:  # 2. На стороне клиентского конфига разрешено изменять `workflow`, то есть для каждого репозитория можно будет указать свои дополнительные команды. 
 custom-stage:
    plan:
      steps:
      - run: my-custom-command arg1 arg2
      - init
      - plan:
          extra_args: ["-lock", "false"]  # 3. В `workflow`, используемом по-умолчанию, во время планирования не происходил `lock` состояния.
      - run: my-custom-command arg1 arg2
    apply:
      steps:
      - run: echo Hi! This is a Stage workspace
      - apply
      
 custom-prod:
   plan:
      steps:
      - run: my-custom-command arg1 arg2
      - init
      - plan:
          extra_args: ["-lock", "false"]
      - run: my-custom-command arg1 arg2
   apply:
      steps:
      - run: echo Hi! This is a Prod workspace
      - apply
      
      
```
Создан `atlantis.yaml` который скажет Атлантису:
1. Надо запускать планирование и ` apply ` для двух воркспейсов `stage` и `prod`.
2. Необходимо включить автопланирование при изменении любых файлов `*.tf`.

```yml

version: 0.1
automerge: true
delete_source_branch_on_merge: true

projects:
- dir: ../project/Alfa        # Директория, в которой выполняется команда  ` run appply `
  workspace: stage
  terraform_version: v1.1.2
  delete_source_branch_on_merge: true
  autoplan:
    when_modified: ["*.tf", "../modules/**.tf"]   # При условии, когда модифицируются файлы с указнным расширением
    enabled: true
  apply_requirements: [mergeable, approved]      # Включение автопланирования при изменении файлов "*.tf"
  workflow: myworkflow
    
- dir: ../project/Alfa        # Директория, в которой выполняется команда  ` run appply `
  workspace: prod
  terraform_version: v1.1.2
  delete_source_branch_on_merge: true
  autoplan:
    when_modified: ["*.tf", "../modules/**.tf"]   # При условии, когда модифицируются файлы с указнным расширением
    enabled: true
  apply_requirements: [mergeable, approved]      # Включение автопланирования при изменении файлов "*.tf"
  workflow: myworkflow
      
allowed_regexp_prefixes:
- dev/
- staging/
```



## Задача 3. Знакомство с каталогом модулей. 

1. В [каталоге модулей](https://registry.terraform.io/browse/modules) найдите официальный модуль от aws для создания
`ec2` инстансов. 
2. Изучите как устроен модуль. Задумайтесь, будете ли в своем проекте использовать этот модуль или непосредственно 
ресурс `aws_instance` без помощи модуля?
3. В рамках предпоследнего задания был создан ec2 при помощи ресурса `aws_instance`. 
Создайте аналогичный инстанс при помощи найденного модуля.   

В качестве результата задания приложите ссылку на созданный блок конфигураций. 

**Ответ:**

1. [AWS EC2 Instance Terraform module](https://registry.terraform.io/modules/terraform-aws-modules/ec2-instance/aws/latest)

Terraform module which creates an EC2 instance on AWS.
```tf
module "ec2-instance" {
  source  = "terraform-aws-modules/ec2-instance/aws"
  version = "3.3.0"
  # insert the 34 required variables here
}

```
2.  Изучено стрение модуля. Вопрос: буду ли я в своем проекте использовать этот модуль или непосредственно ресурс `aws_instance` без помощи модуля?

Для создания виртуальных машин ` ec2_instance ` можно и нужно будет использовать модули при развертывании однотипных экзепляров с минимальными отличиями в конфигурации виртуального оборудования.
Гораздо удобнее использовать часто повторяемую часть кода в виде отдельного файла (файлов) и в дальнейшем только делать ссылку на него в других частях кода инфраструктуры.

```tf
module "ec2_instance" {
  source  = "terraform-aws-modules/ec2-instance/aws"
  version = "~> 3.0"

  for_each = toset(["one", "two", "three"])

  name = "instance-${each.key}"

  ami                    = "ami-ebd02392"
  instance_type          = "t2.micro"
  key_name               = "user1"
  monitoring             = true
  vpc_security_group_ids = ["sg-12345678"]
  subnet_id              = "subnet-eddcdzz4"

  tags = {
    Terraform   = "true"
    Environment = "dev"
  }
}
```


---


