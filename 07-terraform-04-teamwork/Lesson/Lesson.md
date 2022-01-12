### Выполнение ДЗ по теме "7.4. Средства командной работы над инфраструктурой."

Ссылки из лекции

https://github.com/hamnsk/go_psql_redis_example

https://github.com/vectordotdev/vector


##### Создайте `server.yaml` который скажет атлантису:
1. Укажите, что атлантис должен работать только для репозиториев в вашем github (или любом другом) аккаунте.
2. На стороне клиентского конфига разрешите изменять `workflow`, то есть для каждого репозитория можно будет указать свои дополнительные команды. 
3. В `workflow` используемом по-умолчанию сделайте так, что бы во время планирования не происходил `lock` состояния.

```yml

repos:
 - id: github.com/zakharovnpa/experiments-netology   # My repo
 branch: /.*/
 apply_requirements: [approved, mergeable]

 workflow: custom
 allowed_overrides: [apply_requirements, workflow, delete_source_branch_on_merge]
 allowed_workflows: [custom]
 allow_custom_workflows: true
  
      
workflows:
 custom-stage:
    plan:
      steps:
      - run: my-custom-command arg1 arg2
      - init
      - plan:
          extra_args: ["-lock", "false"]
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
##### Создать `atlantis.yaml` который, если поместить егов корень terraform проекта, скажет атлантису:
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
  
  
  
workflows:
  myworkflow-stage:
    plan:
      steps:
      - run: my-custom-command arg1 arg2
      - init
      - plan:
          extra_args: ["-lock", "false"]
      - run: my-custom-command arg1 arg2
    apply:
      steps:
      - run: echo Hi! This is a Stage workspace
      - apply
      
     myworkflow-prod:
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
      
      
allowed_regexp_prefixes:
- dev/
- staging/
```
